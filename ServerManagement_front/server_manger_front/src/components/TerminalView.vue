<template>
  <div ref="terminalContainer" class="w-full h-full bg-black"></div>
</template>

<script setup lang="ts">
import { onMounted, ref, onBeforeUnmount } from "vue";
import { Terminal } from "xterm";
import "xterm/css/xterm.css";

interface Server {
  id: number;
  name: string;
  ip: string;
  user: string;
  port: number;
}

const props = defineProps<{
  server: Server;
}>();

const terminalContainer = ref<HTMLDivElement | null>(null);
let terminal: Terminal | null = null;
let socket: WebSocket | null = null;

onMounted(() => {
  terminal = new Terminal({
    cursorBlink: true,
    fontSize: 14,
    theme: { background: "#000000" },
  });
  if (terminalContainer.value) {
    terminal.open(terminalContainer.value);
  }

  // WebSocket 连接 (需后端支持)
  socket = new WebSocket(`ws://localhost:3000/ssh?id=${props.server.id}`);

  socket.onmessage = (e: MessageEvent) => {
    terminal?.write(e.data);
  };

  terminal.onData((data) => {
    socket?.send(data);
  });
});

onBeforeUnmount(() => {
  socket?.close();
  terminal?.dispose();
});
</script>

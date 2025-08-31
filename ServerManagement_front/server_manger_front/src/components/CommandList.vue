<template>
  <div>
    <h2 class="text-lg font-bold mb-2">常用指令</h2>
    <ul>
      <li
        v-for="(cmd, index) in commands"
        :key="index"
        class="p-1 border-b"
      >
        {{ cmd }}
      </li>
    </ul>

    <div class="mt-4 flex gap-2">
      <input v-model="newCommand" placeholder="输入新指令" class="border px-2 py-1 rounded" />
      <button @click="addCommand" class="bg-blue-500 text-white px-3 py-1 rounded">
        添加
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface Server {
  id: number;
  name: string;
  ip: string;
  user: string;
  port: number;
}

defineProps<{
  server: Server;
}>();

const commands = ref<string[]>(["ls -al", "df -h", "top"]);
const newCommand = ref("");

function addCommand() {
  if (newCommand.value.trim()) {
    commands.value.push(newCommand.value);
    newCommand.value = "";
  }
}
</script>

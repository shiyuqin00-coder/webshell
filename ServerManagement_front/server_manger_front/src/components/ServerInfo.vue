<template>
  <div>
    <h2 class="text-lg font-bold mb-2">SSH 配置信息</h2>
    <p><b>名称：</b>{{ server.name }}</p>
    <p><b>IP：</b>{{ server.ip }}</p>
    <p><b>用户：</b>{{ server.user }}</p>
    <p><b>端口：</b>{{ server.port }}</p>
  </div>
</template>

<script setup lang="ts">
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
</script>

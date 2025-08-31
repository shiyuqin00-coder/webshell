<template>
  <div class="h-full bg-gray-100">
    <h2 class="p-2 font-bold border-b">服务器列表</h2>
    <ul>
      <li
        v-for="s in servers"
        :key="s.id"
        class="p-2 hover:bg-blue-100 cursor-pointer"
        @click="$emit('select', s)"
      >
        {{ s.name }}
      </li>
    </ul>
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
  servers: Server[];
}>();

defineEmits<{
  (e: "select", server: Server): void;
}>();
</script>

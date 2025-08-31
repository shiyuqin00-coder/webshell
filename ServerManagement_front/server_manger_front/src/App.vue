<template>
  <div class="flex h-screen">
    <!-- 左侧服务器列表 -->
    <Sidebar :servers="servers" @select="selectServer" class="w-60 border-r" />

    <!-- 主内容区 -->
    <div class="flex-1 flex flex-col">
      <!-- 顶部 Tabs -->
      <div class="border-b flex">
        <button
          v-for="tab in tabs"
          :key="tab"
          :class="['px-4 py-2', activeTab === tab ? 'border-b-2 border-blue-500 font-bold' : '']"
          @click="activeTab = tab"
        >
          {{ tab }}
        </button>
      </div>

      <!-- 内容切换 -->
      <div class="flex-1 overflow-auto p-4">
        <TerminalView v-if="activeTab === '终端'" :server="currentServer" />
        <ServerInfo v-else-if="activeTab === 'SSH配置信息'" :server="currentServer" />
        <CommandList v-else-if="activeTab === '指令添加'" :server="currentServer" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Sidebar from "./components/Sidebar.vue";
import TerminalView from "./components/TerminalView.vue";
import ServerInfo from "./components/ServerInfo.vue";
import CommandList from "./components/CommandList.vue";

interface Server {
  id: number;
  name: string;
  ip: string;
  user: string;
  port: number;
}

const tabs = ["终端", "SSH配置信息", "指令添加"];
const activeTab = ref("终端");

const servers = ref<Server[]>([
  { id: 1, name: "服务器 A", ip: "192.168.1.10", user: "root", port: 22 },
  { id: 2, name: "服务器 B", ip: "192.168.1.11", user: "ubuntu", port: 22 },
]);

const currentServer = ref<Server>(servers.value[0]);

function selectServer(server: Server) {
  currentServer.value = server;
}
</script>

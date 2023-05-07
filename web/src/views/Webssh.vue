<template>
  <div v-if="conn" id="xterm" :style="xtermStyle"></div>
</template>

<script setup lang="ts">
import 'xterm/css/xterm.css'
import { Terminal } from 'xterm'
import { AttachAddon } from 'xterm-addon-attach'
import { FitAddon } from 'xterm-addon-fit'
import { reactive, onMounted, onBeforeUnmount, ref } from 'vue'

let conn = ref(true)
const xtermStyle = reactive({
  width: '1200px',
  height: '500px'
})
const socket = new WebSocket(import.meta.env.VITE_WS_SERVER)
const term = new Terminal({
  theme: {
    foreground: '#0FF'
  }
})

onMounted(() => {
  initTerm()
})
const initTerm = () => {
  const attachAddon = new AttachAddon(socket)
  const fitAddon = new FitAddon()
  term.loadAddon(attachAddon)
  term.loadAddon(fitAddon)

  term.open(document.getElementById('xterm') as HTMLElement)
  fitAddon.fit()
  term.focus()
}
onBeforeUnmount(() => {
  socket.close()
  term.dispose()
})
</script>

<template>
    <div id="xterm"></div>
</template>

<script>
import { Terminal } from 'xterm'
import { FitAddon } from 'xterm-addon-fit'
import { AttachAddon } from 'xterm-addon-attach'
import 'xterm/css/xterm.css'


export default {
  name: 'XTerm',
  props: {
    socketURI: {
        type: String,
        default: ''
    }
  },
  data(){
    return {
        socket: null,
        term: null
    }
  },
  mounted(){
    this.initSocket()
  },
  beforeDestroy(){

  },
  methods: {
    initTerm() {
        const term = new Terminal()
        const attachADdon = new AttachAddon(this.socket)
        const fitAddon = new FitAddon()
        term.loadAddon(attachADdon)
        term.loadAddon(fitAddon)
        term.open(document.getElementById('xterm'))
        fitAddon.fit()
        term.focus()
        this.term = term
    },
    initSocket() {
        this.socket = new WebSocket(this.socketURI);
        this.socketOnOpen();
        this.socketOnClose();
        this.socketOnError();
    },
    socketOnOpen() {
        this.socket.onopen = () => {
            this.initTerm()
        }
    },
    socketOnClose() {
      this.socket.onclose = () => {
        // console.log('close socket')
      }
    },
    socketOnError() {
      this.socket.onerror = () => {
        // console.log('socket 链接失败')
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#xterm {
    height: 100%;
}
</style>

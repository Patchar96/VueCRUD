<template>
  <div>
    {{text}}
  </div>
</template>

<script>
import { EventBus } from '@/EventBus.js'
export default {
  data () {
    return {
      text: ''
    }
  },
  mounted () {
    EventBus.$on('showText', this.initial)
  },
  methods: {
    initial (sendText) {
      this.text = sendText
    }
  }
}
</script>

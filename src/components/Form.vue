<template>
  <div>
    <v-text-field
      name="name"
      label="label"
      v-model="name"
    ></v-text-field>
    <v-btn color="success" @click="submit">submit</v-btn>
  </div>
</template>

<script>
import { EventBus } from '@/EventBus.js'
export default {
  data () {
    return {
      name: ''
    }
  },
  methods: {
    submit () {
      EventBus.$emit('showText', this.name)
    }
  }
}
</script>

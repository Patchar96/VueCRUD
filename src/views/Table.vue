<template>
  <div>
    <v-data-table
    :headers="headers"
    :items="students"
    sort-by="calories"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-toolbar-title>My Student</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-btn color="success" @click="openNewStudent">New Student</v-btn>
      </v-toolbar>
    </template>
    <template v-slot:item.action="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pen
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item._id)"
      >
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>
  <Dialog/>
  </div>
</template>

<script>
import { EventBus } from '@/EventBus'
import Dialog from '@/components/Dialog.vue'
export default {
  components: {
    Dialog
  },
  data: () => ({
    headers: [
      { text: 'Firstname', value: 'firstname' },
      { text: 'Lastname', value: 'lastname' },
      { text: 'Lineid', value: 'lineid' },
      { text: 'Tel', value: 'tel' },
      { text: 'Actions', value: 'action', sortable: false }
    ],
    students: []
  }),
  created () {
    this.initialize()
  },
  mounted () {
    EventBus.$on('getdata', this.initialize)
  },
  methods: {
    async initialize () {
      try {
        var { data } = await this.axios.get('http://labkk.ga:3000/persons')
        console.log(data)
        this.students = data
      } catch (error) {
        console.log(error.message)
      }
    },
    openNewStudent () {
      EventBus.$emit('openNewStudent')
    },
    editItem (item) {
      EventBus.$emit('editStudent', item)
    },
    async deleteItem (item) {
      console.log('item ', item)
      if (confirm('Are you sure you want to delete this item?')) {
        try {
          var { data } = await this.axios.delete('http://labkk.ga:3000/person/' + item)
          console.log(data)
          if (data.message === 'removesuccess') {
            this.initialize()
          }
        } catch (error) {
          console.log(error.message)
        }
      }
    }
  }
}
</script>

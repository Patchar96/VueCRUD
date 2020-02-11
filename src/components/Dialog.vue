<template>
      <v-dialog v-model="dialog" max-width="500px">
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6">
                    <v-text-field v-model="editedItem.firstname" label="Firstname"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field v-model="editedItem.lastname" label="Lastname"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field v-model="editedItem.lineid" label="Lineid"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field v-model="editedItem.tel" label="Tel"></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="save">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
</template>

<script>
import { EventBus } from '@/EventBus'
export default {
  data () {
    return {
      dialog: false,
      formTitle: '',
      editedItem: {}
    }
  },
  mounted () {
    EventBus.$on('openNewStudent', this.openDialog)
    EventBus.$on('editStudent', this.openEditDialog)
  },
  methods: {
    openDialog () {
      this.editedItem = {}
      this.dialog = true
      this.formTitle = 'New student'
    },
    openEditDialog (student) {
      this.dialog = true
      this.formTitle = 'Edit student'
      console.log(student)
      this.editedItem = student
    },
    async save () {
      if (this.formTitle === 'New student') {
        try {
          var { data } = await this.axios.post('http://labkk.ga:3000/person', this.editedItem)
          console.log(data)
          if (data.message === 'insertsuccess') {
            this.dialog = false
            EventBus.$emit('getdata')
          }
        } catch (error) {
          console.log(error.message)
        }
      } else if (this.formTitle === 'Edit student') {
        try {
          var { data1 } = await this.axios.put('http://labkk.ga:3000/person/' + this.editedItem._id, this.editedItem)
          console.log(data1)
          if (data.message === 'updatesuccess') {
            this.dialog = false
            EventBus.$emit('getdata')
          }
        } catch (error) {
          console.log(error.message)
        }
      }
    },
    close () {
      this.dialog = false
    }
  }
}
</script>

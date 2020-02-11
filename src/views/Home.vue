<template>
  <v-card class="d-flex flex-row">
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant.sync="mini"
      permanent
    >
      <v-list-item>
        <v-list-item-avatar>
          <v-img src="../assets/iconfinder_38_Target_Audience_1688838.png"></v-img>
        </v-list-item-avatar>
        <v-list-item-title>Username</v-list-item-title>
        <v-btn
          icon
          @click.stop="mini = !mini"
        >
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
      </v-list-item>
      <v-divider></v-divider>
      <v-list nav dense>
        <v-list-item-group v-model="item" color="primary">
        <v-list-item
          v-for="( item, i ) in items"
          :key="i"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <div style="width: 100%">
      <v-card class="d-flex flex-column ma-2 ml-4">
        <v-card class="d-flex flex-row" outlined>
           <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
            class="ml-4 mr-4"
            >
        </v-text-field>
        <v-btn rounded color="primary" dark class="mt-2 mr-4">Add</v-btn>
        </v-card>
        <v-data-table
          :headers="headers"
          :items="desserts"
          :search="search"
        ></v-data-table>
      </v-card>
    </div>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      drawer: true,
      search: '',
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'left',
          filterable: false,
          value: 'name'
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Iron (%)', value: 'iron' }
      ],
      desserts: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%'
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%'
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%'
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: '8%'
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: '16%'
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: '0%'
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: '2%'
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: '45%'
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: '22%'
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: '6%'
        }
      ],
      items: [
        { title: 'Properties', icon: 'mdi-home-outline' },
        { title: 'Location', icon: 'mdi-city-variant-outline' },
        { title: 'Sales', icon: 'mdi-shield-outline' },
        { title: 'Clients', icon: 'mdi-account-outline' },
        { title: 'Calendar', icon: 'mdi-calendar-blank-outline' },
        { title: 'Inbox', icon: 'mdi-comment-outline' },
        { title: 'Statistic', icon: 'mdi-signal-cellular-outline' }
      ],
      mini: true
    }
  }
}
</script>

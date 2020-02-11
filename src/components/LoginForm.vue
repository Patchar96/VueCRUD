<template>
  <v-container fluid fill-height class="orange">
    <v-row justify="center">
      <v-col
        md="6"
        sm="12"
      >
        <v-card>
          <v-card-text>
            <v-text-field
              label="username"
              prepend-icon="mdi-account"
            >
            </v-text-field>
            <v-text-field
              label="password"
              prepend-icon="mdi-lock"
              type="password"
            >
            </v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-row justify="center">
              <v-btn class="success">Submit</v-btn>
            </v-row>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

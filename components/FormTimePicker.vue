<template>
  <v-menu
    ref="menu"
    v-model="menu"
    :close-on-content-click="false"
    :return-value.sync="time"
    lazy
    transition="scale-transition"
    offset-y
    full-width
    max-width="290px"
    min-width="290px"
  >
    <template v-slot:activator="{ on }">
      <v-text-field
        v-editable="blok"
        v-model="time"
        :label="blok.label"
        prepend-icon="mdi-calendar-clock"
        readonly
        v-on="on"
        :rules="blok.required ? [v => !!v || blok.label + ' is required'] : []"
        :name="blok.label"
      ></v-text-field>
    </template>
    <v-time-picker v-if="menu" v-model="time" full-width color="primary">
      <v-btn color="primary" rounded @click="$refs.menu.save(time)">OK</v-btn>
      <v-spacer></v-spacer>
      <v-btn text color="red" rounded @click="menu = false">Cancel</v-btn>
    </v-time-picker>
  </v-menu>
</template>

<script>
export default {
  props: ["blok"],
  data: () => ({
    time: null,
    menu: false
  })
};
</script>

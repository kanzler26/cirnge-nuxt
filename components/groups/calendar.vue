<template>
  <v-menu
    ref="menu"
    v-model="menu"
    :close-on-content-click="false"
    transition="scale-transition"
    offset-y
    min-width="auto"
  >
    <template #activator="{ on, attrs }">
      <v-text-field
        v-model="date"
        label="Начало/конец"
        prepend-icon="mdi-calendar"
        readonly
        v-bind="attrs"
        v-on="on"
      ></v-text-field>
    </template>
    <v-date-picker v-model="date" range></v-date-picker>
  </v-menu>
</template>
<script>
import Vue from "vue"

export default Vue.extend( {
  name: "GroupCalendar",
  props: {
    dateGr: {
      type: Array,
      default: () => [],
    },
  },
  data: () => ( {
    activePicker: null,
    date: [],
    menu: false,
    dateArr: [],
    dateStart: "",
    dateEnd: "",
  } ),
  watch: {
    menu ( val ) {
      val && setTimeout( () => ( this.activePicker = "YEAR" ) )
    },
  },
  mounted () {
    this.date.push( this.dateGr[ 0 ], this.dateGr[ 1 ] )
    console.log( "that mounted", this.dateArr )
  },
  // TODO: че за хуйня
  methods: {
    save ( date ) {
      this.$refs.menu.save( date )
    },
  },
} )
</script>

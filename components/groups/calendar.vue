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
        hint="год/месяц/день"
        persistent-hint
        label="Начало/конец"
        prepend-icon="mdi-calendar"
        readonly
        v-bind="attrs"
        v-on="on"
      ></v-text-field>
    </template>
    <v-date-picker
     v-model="date" range
     @change="sendToEdit"> </v-date-picker>
  </v-menu>
</template>
<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'GroupCalendar',
  props: {
    dateGr: {
      type: Array,
      default: () => [],
    },
    saved: {
      type: Boolean,
      default: () => false,
    },
    closed: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ({
    activePicker: null,
    date: [],
    menu: false,
    dateArr: [],
    dateStart: '',
    dateEnd: '',
    closeDialog: false,
    groupIndex: null,
  }),
  watch: {
    menu(val) {
      val && setTimeout(() => (this.activePicker = 'YEAR'))
    },
    // если меняется свойство, то передаём родителю данные
    // saveChanges() {
    //   this.$emit('saveChanges', this.closeDialog)
    //   this.$emit('saveChanges', this.date)
    //   this.$emit('saveChanges', this.groupIndex)
    // },
    closeDialog() {
      this.$emit('closeEdit', this.closeDialog)
    },
  },
  mounted() {
    // при загрузке записали данные из пропсы
    this.date.push(this.dateGr[0], this.dateGr[1])
    this.saveChanges = this.saved
    this.closeDialog = this.closed
    this.groupIndex = this.dateGr[2]
    // eslint-disable-next-line no-console
    console.log('mount ind:', this.dateGr)
  },
  // TODO: че за хуйня
  methods: {
    // save ( date ) {
    //   this.$refs.menu.save( date )
    //   console.log(date)
    // },
    sendToEdit() {
      this.$emit('sendToEdit', this.date)
      // this.menu = true
      // eslint-disable-next-line no-console
      console.log('change in calendar', this.date)
    },
  },
})
</script>

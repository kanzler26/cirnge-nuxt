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
    <v-date-picker v-model="date" range @change="sendToEdit"> </v-date-picker>
  </v-menu>
</template>
<script>
import Vue from 'vue'

// const dateNow = new Date().toISOString().split('T')[0]
// const day =  dateNow.getDay()
// const month = dateNow.getMonth()
// const year = dateNow.getFullYear()
// const formatDate = year + '-' + month + '-' + day
// const dateNowAddWeek = new Date(dateNow.setDate(dateNow.getDate() + 7))

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
    closeDialog() {
      this.$emit('closeEdit', this.closeDialog)
    },
  },
  mounted() {
    // при загрузке записали данные из пропсы
    // если есть данные из пропсы из компонента edit,
    // тогда передаём в инпут, если нет то по умолчанию
    if (this.dateGr.length > 0) {
      this.date.push(this.dateGr[0], this.dateGr[1])
      this.groupIndex = this.dateGr[2]
    } else {
      const dateObj = new Date()
      const dateNow = new Date().toISOString().split('T')[0]
      const dateNowAddWeek = new Date(dateObj.setDate(dateObj.getDate() + 7))
        .toISOString()
        .split('T')[0]
      this.date.push(dateNow, dateNowAddWeek)
    }
    this.saveChanges = this.saved
    this.closeDialog = this.closed
  },
  methods: {
    sendToEdit() {
      this.$emit('sendToEdit', this.date)
      // this.menu = true
      // eslint-disable-next-line no-console
      console.log('change in calendar', this.date)
    },
  },
})
</script>

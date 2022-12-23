<template>
  <v-dialog v-model="dialog" @click:outside="initClose">
    <v-card>
      <v-card-title>
        <span class="text-h5">Редактирование группы</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="form.name"
                prepend-icon=""
                label="Название"
              >
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <!-- <v-text-field v-model="form.type" label="Форма обучения">
              </v-text-field> -->
            <types-group :type-val="form.type" /> 
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <group-calendar
                :date-gr="[form.start, form.end, groupIndex]"
                :saved="saved"
                :closed="closed"
                @sendToEdit="saveChanges"
                @closeEdit="closeEdit"
              ></group-calendar>
            </v-col>
          </v-row>
          <v-btn @click="initSave"> сохранить </v-btn>
          <v-btn @click="initClose"> закрыть </v-btn>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>
<script lang="ts">
import Vue from 'vue'
import types from '@/components/groups/types.vue'
import calendar from '@/components/groups/calendar.vue'
export interface Form {
  name: string
  type: string
  start: string
  end: string
}
// добавить поле для выбора курсов чтобы при нажатии появился функционал Марка

export default Vue.extend({
  name: 'EditGroupModal',
  components: {
    'group-calendar': calendar,
    'types-group':types
  },
  layout: 'admin',
  props: {
    group: {
      type: Object,
      default: () => {},
    },
    open: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ({
    menu: null,
    dialog: false,
    form: {} as Form,

    date: '',
    saved: false,
    closed: false,
    calcDate: [],
    groupIndex: null,
  }),
  watch: {
    open(val) {
      this.dialog = val
    },
    group: {
      handler() {
        this.groupIndex = this.group.index
        Object.assign(this.form, this.group.item)
      },
    },
  },
  methods: {
    // сохранить кнопка
    initSave() {
      this.initClose()
      this.$emit('changeGroup', {
        index: this.groupIndex,
        form: this.form,
      })
    },

    // закрыть кнопка
    initClose() {
      this.closeEdit()
      this.$emit('closeEdit')
    },
    // событие календаря, при изменении поля с датой
    saveChanges(date: any) {
      this.dialog = true
      this.form.start = date[0]
      this.form.end = date[1]
    },
    closeEdit() {
      this.dialog = false
    },
  },
})
</script>

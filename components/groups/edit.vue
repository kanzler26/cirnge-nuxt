<template>
  <v-dialog v-model="dialog">
    <v-card>
      <v-card-title>
        <span class="text-h5">Редактирование группы</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="groupName"
                prepend-icon=""
                label="Название"
              >
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="groupType" label="Форма обучения">
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <group-calendar
                :date-gr="[groupStart, groupEnd, groupIndex]"
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
import calendar from '@/components/groups/calendar.vue'
export default Vue.extend({
  name: 'EditGroupModal',
  components: {
    'group-calendar': calendar,
  },
  layout: 'admin',
  props: {
    groupItem: {
      type: Object,
      default: () => null,
    },
    open: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ({
    menu: null,
    dialog: false,
    // editItem:{},
    groupName: '',
    groupType: '',
    groupStart: '',
    groupEnd: '',
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
    groupItem: {
      handler(val) {
        this.groupName = val.item.name
        this.groupType = val.item.type
        this.groupStart = val.item.start
        this.groupEnd = val.item.end
        this.groupIndex = val.index
      },
    },
  },
  methods: {
    initSave() {
      this.saved = true
      if (this.calcDate) {
        this.groupStart = this.calcDate[0]
        this.groupEnd = this.calcDate[1]
        // eslint-disable-next-line no-console
        console.log('wtf', this.groupEnd)
      }
      this.closeEdit()
    },
    initClose() {
      this.closed = true
    },
    saveChanges(date: any) {
      this.dialog = true
      this.calcDate = date
      this.$emit("changeGroup",)
      console.log("groupIndex:", this.groupIndex)
      console.log("groupIndex from calc:", date)
    },
    closeEdit() {
      this.dialog = false
    },
  },
})
</script>

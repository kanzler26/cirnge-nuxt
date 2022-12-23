<template>
  <v-dialog v-model="openModal" @click:outside="btnClose">
    <v-card>
      <v-card-title>
        <span class="text-h5">Создание группы</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="group.name"
                prepend-icon=""
                label="Название*"
                :rules="[rules.required]"
              >
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <types-group> </types-group>
              <!-- <v-text-field v-model="group.type" label="Форма обучения">
              </v-text-field> -->
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <group-calendar
                :saved="saved"
                :closed="closed"
                @sendToEdit="saveChanges"
                @closeEdit="closeEdit"
              ></group-calendar>
            </v-col>
          </v-row>
          <v-btn @click="btnSave"> сохранить </v-btn>
          <v-btn @click="btnClose"> закрыть </v-btn>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>
<script lang="ts">
import Vue from 'vue'
import calendar from '@/components/groups/calendar.vue'
import types from '@/components/groups/types.vue'

interface Group {
  name: string
  type: string
  start: string
  end: string
}
export default Vue.extend({
  name: 'CreateGroup',
  components: {
    'group-calendar': calendar,
    'types-group': types,
  },
  props: {
    openModalProp: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ({
    openModal: false,
    saved: false,
    closed: false,
    group: {} as Group,
    types: ['очная', 'заочная', 'заочно-очная'],
    rules: {
      required: (value: any) => !!value || 'введите название.',
      email: (value: any) => {
        const pattern =
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        return pattern.test(value) || 'Invalid e-mail.'
      },
    },
  }),
  watch: {
    openModalProp: {
      handler() {
        this.openModal = this.openModalProp
      },
    },
  },
  methods: {
    saveChanges(date: any) {
      this.group.start = date[0]
      this.group.end = date[1]
    },
    btnSave() {
      if (this.group.name?.length > 0) {
        this.openModal = false
        this.$emit('saveChanges', { item: this.group, close: false })
      }
    },

    btnClose() {
      this.openModal = false
      this.$emit('closeGroupModal')
    },
    closeEdit() {},
  },
})
</script>

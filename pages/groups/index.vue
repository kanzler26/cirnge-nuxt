<template>
  <div>
    <v-btn @click="openModalCreate">
      <v-icon> mdi-account-multiple-plus-outline </v-icon>
      <create-group-modal
        :open-modal-prop="openModal"
        @saveChanges="saveCreateGroup"
        @closeGroupModal="closeCreateModal"
      >
      </create-group-modal>
    </v-btn>
    <v-data-table
      :headers="datatables.groups.headers"
      :items="datatables.groups.items"
      @update:options="getGroups"
      @click:row="openEditor"
    >
      <template #item.start="{ item }">
        {{ item.start }}/{{ item.end }}
      </template>
    </v-data-table>
    <edit-group-modal
      :group="group"
      :open="dialog"
      @changeGroup="changeGroup"
      @closeEdit="closeEdit"
    ></edit-group-modal>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
// import { GroupsApiPayload } from "~/plugins/api/groups/groups.type"
// import { DataModalStructure } from "~/types/components/modal"
import edit from '~/components/groups/edit.vue'
import create from '~/components/groups/create.vue'
export default Vue.extend({
  name: 'GroupIndexPage',
  components: {
    'edit-group-modal': edit,
    'create-group-modal': create,
  },
  layout: 'admin',
  data: () => ({
    dialog: false,
    openModal: false,
    group: {},
    datatables: {
      groups: {
        loading: false,
        search: null,
        selected: [],
        headers: [
          {
            text: 'Название',
            value: 'name',
            cellClass: 'primary--text font-weight-medium cursor-pointer',
          },
          { text: 'Форма', value: 'type', cellClass: 'font-weight-medium' },
          { text: 'Начало/Конец', value: 'start' },
        ],
        // items: [] as GroupsApiPayload[],
        items: [
          {
            name: 'group1',
            type: 'заочная',
            start: '2022-01-02',
            end: '2022-01-13',
          },
          {
            name: 'group2',
            type: 'очная',
            start: '2022-02-10',
            end: '2022-03-09',
          },
          {
            name: 'group3',
            type: 'заочная',
            start: '2022-01-11',
            end: '2022-02-10',
          },
          {
            name: 'group4',
            type: 'очная',
            start: '2022-03-12',
            end: '2022-04-01',
          },
          {
            name: 'group5',
            type: 'заочная',
            start: '2022-03-12',
            end: '2022-03-17',
          },
        ],
        total: 0,
        page: 1,
        itemsPerPage: 20,
      },
    },
  }),
  head: () => ({
    title: 'Группы',
  }),
  computed: {},
  methods: {
    async getGroups() {
      // const { data, valid } = await this.$api.groups.find()
      // if ( valid && data ) {
      //   this.datatables.groups.items = data
      // }
    },
    changeGroup(item: any) {
      // TODO: переделать на норм инициализацию
      this.datatables.groups.items[item.index].start = item.form.start
      this.datatables.groups.items[item.index].end = item.form.end
      this.datatables.groups.items[item.index].type = item.form.type
      this.datatables.groups.items[item.index].name = item.form.name
      //  this.dialog = item.dialog
    },

    openEditor(item: any) {
      this.dialog = !this.dialog
      this.group = {
        index: this.datatables.groups.items.indexOf(item),
        item,
      }
    },

    closeEdit() {
      this.dialog = false
    },

    openModalCreate() {
      this.openModal = true
    },

    closeCreateModal() {
      this.openModal = false
    },
    saveCreateGroup(group: any) {
      this.openModal = group.close
      this.datatables.groups.items.push(group.item)
    },
  },
})
</script>

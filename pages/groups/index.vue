<template>
  <div>
    <v-data-table
      :headers="datatables.groups.headers"
      :items="datatables.groups.items"
      @update:options="getGroups"
      @click:row="open"
    >
      <template #item.start="{ item }">
        {{ item.start }}/{{ item.end }}
      </template>
    </v-data-table>
    <edit-group-modal
      :group-item="groupItem"
      :open="dialog"
      :change-group="changeGroup"
    ></edit-group-modal>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
// import { GroupsApiPayload } from "~/plugins/api/groups/groups.type"
// import { DataModalStructure } from "~/types/components/modal"
import edit from '~/components/groups/edit.vue'

// interface ModalGroupsProps {
//   groupId: number
// }
export default Vue.extend({
  name: 'GroupIndexPage',
  components: {
    'edit-group-modal': edit,
  },
  layout: 'admin',
  data: () => ({
    dialog: false,
    groupItem: {},
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
    // modals: {
    //   counterpartiesCreate: {
    //     display: false,
    //     props: {},
    //   } as DataModalStructure<ModalGroupsProps>,
    // },
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
      // eslint-disable-next-line no-console
      console.log('item:', item)
    },
    open(item: any) {
      this.dialog = !this.dialog
      this.groupItem = {
        item,
        index: this.datatables.groups.items.indexOf(item),
      }
      // eslint-disable-next-line no-console
      console.log('in open method:', this.groupItem)
    },
  },
})
</script>

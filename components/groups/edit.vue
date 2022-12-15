<template>
  <v-dialog v-model="open">
    <v-card>
      <v-card-title>
        <span class="text-h5">Редактирование группы</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="groupName" prepend-icon="" label="Название">
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="groupType" label="Форма обучения">
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <group-calendar :date-gr="[groupStart, groupEnd]"></group-calendar>
            </v-col>            
          </v-row>
          <v-btn @click="save"> сохранить </v-btn>
          <v-btn @click="close"> закрыть </v-btn>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>
<script lang="ts">
import Vue from "vue"
import calendar from "@/components/groups/calendar.vue"
export default Vue.extend( {
  name: "EditGroupModal",
  components: {
    "group-calendar": calendar,
  },
  layout: "admin",
  props: {
    groupItem: {
      type: Object,
      default: () => null,
    },
    dialog: {
      type: Boolean,
      default: () => false,
    },
  },
  data: () => ( {
    menu: null,
    open: false,
    groupName: "",
    groupType: "",
    groupStart: "",
    groupEnd: "",
    date:""
  } ),
  watch: {
    dialog ( val ) {
      this.open = val
    },
    groupItem: {
      // immediate: true,
      handler ( val ) {
        this.groupName = val.name
        this.groupType = val.type
        this.groupStart = val.start
        this.groupEnd = val.end
      },
    },
  },
  methods: {
    save () {},
    close () {},
  },
} )
</script>

<template>
  <v-select
    v-model="activType"
    :items="types"
    label="Тип обучения*"
    required
  ></v-select>
</template>
// TODO:почему при вызове edit не появляется в селекте переданная пропса type
group
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'GroupTypes',
  props: {
    typeVal: {
      type: String,
      default: () => '',
    },
  },
  data: () => ({
    types: ['очная', 'заочная', 'заочно-очная'],
    activType: '',
  }),
  // watch: {
  //   typeVal: {
  //     handler() {
  //       this.activType = this.typeVal
  //       console.log('typeVal: ', this.activType)
  //     },
  //   },
  // },
  mounted() {
    this.activType = this.typeVal
    console.log('typeVal: ', this.typeVal)
  },
})
</script>

<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
      <tr>
        <th class="text-left" v-for="(item,index) in fields" :key="index">
          {{item}}
        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(key,index) in viewData"
          :key="index"
      >
        <td v-for="(item,index) in fields" :key="index">{{ key[item] }}</td>
      </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
  name: "TableList",
  props:['viewData','fields'],
  data () {
    return {
    }
  },
  methods:{

  },
  filters:{
    viewTab(data){
      console.log(data)
      return ''
    }
  }
}
</script>

<style scoped>

</style>
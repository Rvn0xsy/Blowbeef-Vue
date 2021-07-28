<template>
<v-app>
  <TableList :view-data="dnsData" :fields="dnsData.fields"></TableList>
  <v-simple-table>
    <template v-slot:default>
      <thead>
      <tr>
        <th class="text-left" v-for="(item,index) in dnsData.fields" :key="index">
          {{item}}
        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(key,index) in dnsData.data"
          :key="index"
      >
        <td v-for="(item,index) in dnsData.fields" :key="index">{{ key[item] }}</td>
      </tr>
      </tbody>
    </template>
  </v-simple-table>
</v-app>
</template>

<script>
import handler from "../handler";
import TableList from "../TableList";
export default {
  name: "DnsCache",
  data(){
    return{
      dnsData:null
    }
  },
  mounted() {
    handler.$on('pushDnsCacheData', (dnsData) => {
      console.log('-----On pushDnsCacheData-----')
      this.dnsData = dnsData
      console.log(dnsData)
    });
  },
  components:{
    TableList,
  }
}
</script>

<style scoped>

</style>
<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card>
          <v-toolbar
              flat
              color="success"
              dark
          >
            <v-toolbar-title>Analyze Data</v-toolbar-title>
          </v-toolbar>
          <v-tabs vertical>
            <v-tab v-for="(name,key) in menuList" :key="key">
              {{ name }}
            </v-tab>
            <v-tab-item>
              <v-card flat>
                <v-card-text v-if="checkData('Process')">
                  <Process></Process>
                </v-card-text>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text v-if="checkData('DNSCache')">
                  <DnsCache></DnsCache>
                </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import handler from "./handler";
import Process from "./modules/Process";
import DnsCache from "./modules/DnsCache";
export default {
  name: "Analyze",
  data(){
   return{
     jsonData : null,
     menuList : [],
   }
},
  methods:{
    getData(obj,name){
      let result = null
      for (let o in obj){
        if (obj[o].name === name){
          result = obj[o]
        }
      }
      return result
    },
    checkData(name){
      for (let n in this.menuList){
        // console.log(this.menuList)
        if (this.menuList[n] === name){
          return true
        }
      }

    }
  },
  components:{
    Process,
    DnsCache
  },
  mounted() {
    handler.$on('getUploadJson', (jsonData) => {
      this.jsonData = jsonData
      for (let o in this.jsonData){
        console.log(this.jsonData[o].name)
        this.menuList.push(this.jsonData[o].name)
      }
    });
  },
  updated(){
    handler.$emit('pushProcessData',this.getData(this.jsonData,'Process'))
    handler.$emit('pushDnsCacheData',this.getData(this.jsonData,'DNSCache'))
  },
  filters:{

  }

}
</script>

<style scoped>

</style>
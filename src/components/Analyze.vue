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
            <v-tab>
              Process
            </v-tab>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <Process :process-data="jsonData | filterData('Process')"></Process>
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
export default {
  name: "Analyze",
  data(){
   return{
     jsonData : null
   }
},
  methods:{

  },
  components:{
    Process
  },
  mounted() {
    handler.$on('getUploadJson', (jsonData) => {
      this.jsonData = jsonData
      console.log("Analyze Module....")
      console.log(this.jsonData)
    });
  },
  filters:{
    filterData(sourceData,name){
      console.log(sourceData,name)
      if (sourceData == null){
        return sourceData
      }

      for (let obj in sourceData){
        if(sourceData[obj].name === name){
          console.log(sourceData[obj])
          return sourceData[obj]
        }
        return null
      }
    }
  }

}
</script>

<style scoped>

</style>
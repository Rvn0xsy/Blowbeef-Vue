<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card>
          <v-toolbar
              flat
              color="primary"
              dark
          >
            <v-toolbar-title>Blowbeef</v-toolbar-title>
          </v-toolbar>
          <v-tabs vertical>
            <v-tab v-for="(item,i) in jsonData" :key="i">
              {{ item.name }}
            </v-tab>
            <v-tab-item v-for="(item,i) in jsonData" :key="i">
              <v-card flat>
                <v-card-text>
                  <TableList :fields="item.fields" :view-data="item.data"></TableList>
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
import TableList from "./TableList";
import handler from "./handler";
export default {
  name: "ShowData",
  data(){
    return{
      jsonData:null,
    }
  },
  components:{
    TableList,
  },
  mounted() {
    handler.$on('getUploadJson', (jsonData) => {
      this.jsonData = jsonData
      console.log("ShowData Module....")
      console.log(this.jsonData)
    });
  }
}
</script>

<style scoped>

</style>
<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="" cols="12">
        <v-card
            elevation="2"
            shaped
            tile
        >
          <v-toolbar
              flat
              color="primary"
              dark
          >
            <v-toolbar-title>上传分析数据</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-col class="mb-4">
              <v-file-input
                  show-size
                  truncate-length="15"
                  placeholder="请选择Json文件"
                  @change="readJson"
                  chips
                  accept=".json"
                  v-model="upLoadJSON"
              ></v-file-input>
            </v-col>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import handler from "./handler";
export default {
  name: "Upload",
  data: () => ({
    upLoadJSON:null,
    jsonData:'',
  }),
  methods:{
    readJson(){
      if (this.upLoadJSON !== null) {
        let reader = new FileReader();
        reader.readAsText(this.upLoadJSON);
        let _this = this
        reader.onload = () => {
          if (reader.result !== "") {
            // console.log(reader.result)
            _this.jsonData = JSON.parse(reader.result)
            if(_this.jsonData == null){
              alert("Json Parse Error.")
            }
            // console.log(_this.jsonData)
            handler.$emit('getUploadJson',_this.jsonData)
          }
        };
      }
    }
  },
  components: {

  }
}
</script>

<style scoped>

</style>
<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        BlowBeef
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Upload></Upload>
      <Analyze></Analyze>
      <ShowData></ShowData>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import handler from "./components/handler";
import ShowData from "./components/ShowData";
import Analyze from "./components/Analyze";
import Upload from "./components/Upload";

export default {
  name: 'App',

  components: {
    Upload,
    Analyze,
    ShowData,
    // HelloWorld,
  },
  data: () => ({
    //
    jsonData:null
  }),
  mounted() {
    handler.$on('getUploadJson', (jsonData) => {
      this.jsonData = jsonData
    });
  }
};
</script>

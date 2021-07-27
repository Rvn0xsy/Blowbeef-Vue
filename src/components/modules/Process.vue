<template>
  <v-app>
    <h1>Process 攻击方案 </h1>
    <v-expansion-panels>
      <v-expansion-panel
          v-for="(info,key) in rules" :key="key"
      >
        <v-expansion-panel-header>
         <h3> {{info.info}}</h3>
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          {{info.refUrl}}
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </v-app>
</template>

<script>
export default {
  name: "Process",
  props:['processData'],
  data(){
    return{
      infoList:[],
      rules:[
        {
          name: 'lsass.exe',info: '可以进行转储内存..',refUrl: 'https://baidu.com',type:'info',
        },
        {
          name: 'lsass.exe',info: '可以进行转储内存..',refUrl: '',type:'info',
        }
      ]
    }
  },
  mounted() {
    console.log('...........Process ......',this.processData)
    for (let process in this.processData){
      console.log(process)
    }
  },
  methods:{

  }
}
</script>

<style scoped>

</style>
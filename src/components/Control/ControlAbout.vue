<template>
  <el-dialog width="85%" center top="10vh">
    
    <img v-if="darkMode" src="../../assets/Logo_Dark.png" alt="Logo" />
    <img v-else src="../../assets/Logo_Standard.png" alt="Logo" />

    <el-row style="padding-bottom: 20px;">
      <el-col :span="24">
        <h2>Better test cards for the AV Professional.</h2>
        Custom version for Televic by Pepijn Callaerts<br />
        <br />
        This is a custom version of Kards, tailored for Televic's needs.<br />
        Please contact <a href="mailto:p.callaerts@televic.com">Pepijn Callaerts</a> for any questions or support<br />
        regarding this version, or if any additional features are required. 
        <br />
      </el-col>
    </el-row>

    <el-row>
      <el-form-item label="Version">{{info.version}}</el-form-item>
    </el-row>

    <el-row style="padding-top: 20px;">
      <el-col :span="8">
        <el-button size="small" round @click="openSite"><i class="fa-solid fa-globe green"></i> Website</el-button>
      </el-col>
      <el-col :span="8">
        <el-button size="small" round @click="openAPI"><i class="fa-solid fa-circle-question green"></i> API</el-button>
      </el-col>
      <el-col :span="8">
        <el-button size="small" round @click="openGitHub"><i class="fa-brands fa-github green"></i> GitHub</el-button>
      </el-col>
    </el-row>

  </el-dialog>
</template>

<script>

  export default {
    props: {
      darkMode: Boolean
    },
    data: function() {
      return {
        info: {}
      }
    },
    mounted: function() {
      let vm = this
      window.ipcRenderer.receive('aboutDialogInfo', function(i) {
        vm.info = i
      })
      window.ipcRenderer.send('aboutDialogInfo')
    },
    methods: {
      openSite: function() {
        window.ipcRenderer.send('openUrl', 'https://alteka.solutions/kards/')
      },
      openAPI: function() {
        window.ipcRenderer.send('openUrl', 'https://github.com/Alteka/Kards/wiki/REST-API')
      },
      openGitHub: function() {
        window.ipcRenderer.send('openUrl', 'https://github.com/morlockdarc/Kards')
      },
      openDonate: function() {
        window.ipcRenderer.send('openUrl', 'https://alteka.solutions/donateKards')
      }
    }
  }
</script>

<style scoped>
.el-row {
  text-align: center;
  top: -25px;
}
img {
  height: 75px;
  margin: auto;
  width: 100%;
  object-fit: contain;
  position: relative;
  top: -15px;
}

.version {
  width: 75%;
  left: 6.66%;
  height: 25px;
}
</style>

<template>
  <div id="app">
    <grid-component ref="gridCom" style="padding:50px"></grid-component>
    <div style="padding:20px">
        <button @click="onAddBtnClicked" class="circular ui icon button circular-btn">
          <i class="plus icon btn-icon"></i>
        </button>
    </div>
  </div>
</template>

<script>
import gridComponent from  './components/gridComponent'

export default {
  name: 'app',
  components: {
    gridComponent,
  },
  methods: {
      onAddBtnClicked(){
          this.$refs.gridCom.addGridElement();
      }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.circular-btn{
    position: fixed;
    bottom: 40px;
    right: 40px;
    width: 70px;
    height: 70px;
    color: #FFFFFF !important;
    background-color: rgba(99, 213, 255, 1.0) !important;
    box-shadow: 0px 6px 20px rgba(0, 0, 0, 0.4) !important;
    float: right;
}

.circular-btn:hover{
    background-color: rgba(36, 197, 255, 0.5) !important;
}

.circular-btn:active{
    background-color: rgba(36, 197, 255, 1) !important;
}

.btn-icon{
    font-size: 20px !important;
    color: #FFFFFF !important;
}
</style>

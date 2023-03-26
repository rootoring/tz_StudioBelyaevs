<template>
  <div class="home">
    <div class="container">
      <transition-group name="list" tag="div" class="stopwatch-cards">
        <timeBlock
          v-for="stopwatch of stopwatchs"
          :key="stopwatch.key"
          v-model="stopwatch.attributes"
        />
        <div 
        @click="addStopwatch"
        class="addBlock"
        key="223232"><i class="fas fa-plus"></i></div>
      </transition-group>

        
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  data() {
    return {
      stopwatchs: [
        { 
          attributes:{
            active: false,
            sec: 22222
          },
          key:1
        },
      ],
    }
  },
  methods:{
    addStopwatch(){
      this.stopwatchs.push({
         attributes:{
          active: false,
          sec: 0
        },
        key:Math.random()})
    }
  },
  components: {
    timeBlock: () => import("@/components/timeBlock.vue"),
  },
}
</script>
<style lang="scss">
.container{
  padding: 40px 70px;
  .stopwatch-cards{
    display: flex;
    gap:50px;
    flex-wrap: wrap;
  }
}
.addBlock{
  width: 225px;
  height: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #9E9E9E;
  background: #696969;
  font-size: 17px;
  cursor: pointer;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter,.list-leave-to {
 opacity: 0;
  transform: translateX(-50px);
}        
</style>
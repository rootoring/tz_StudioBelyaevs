<template>
  <div class="home">
    <div class="container">
      <TransitionGroup  name="list" tag="div" class="stopwatch-cards">
        <timeBlock
          v-for="stopwatch of stopwatchs"
          :key="stopwatch.key"
          v-model="stopwatch.attributes"
        />
        <div 
        @click="addStopwatch"
        class="addBlock"
        key="223232"><i class="fas fa-plus"></i></div>
      </TransitionGroup>

        
    </div>
  </div>
</template>

<script>
import timeBlock from "@/components/timeBlock.vue"

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
    timeBlock,
  },
}
</script>
<style lang="scss">
.container{
  padding: 72px;
  .stopwatch-cards{
    display: flex;
    gap:50px;
    flex-wrap: wrap;
    max-width: 775px;
    margin: 0 auto;
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
@media(max-width:1024px){
  .container{
    padding: 72px 135px;
  }
  .stopwatch-cards{
    width: 500px;
  }
}
@media(max-width:768px){
  .container{
    padding: 72px 46px;
  }
  .stopwatch-cards{
    width: 100%;
    flex-direction: column;
    align-items: center;
  }
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}     
</style>
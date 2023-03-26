<template>
  <article 
  class="stopwatch">
    <div 
    :class="data.active ? 'active' : ''"
    class="stopwatch__time">{{ changedTime }}</div>

    <div class="stopwatch__btns">
      <button 
        :class="data.active ? 'active' : ''"
        v-if="!data.active" @click="start"><i class="fas fa-play"></i>
      </button>

      <button
      :class="data.active ? 'active' : ''"
      v-else @click.prevent="pause"><i class="fas fa-pause"></i>
      </button>
      <button 
      :class="data.active ? 'active' : ''"
      @click.prevent="reset"><i class="fas fa-stop"></i>
      </button>
    </div>
  </article>
</template>
<script>


export default {
  data(){
   return {
    data:{},
    timer: null
   } 
  },
  props: {
    value: { type: Object },
  },
  computed: {
    changedTime() {
      if (this.data.sec > 59) {
        let m = this.data.sec / 60;
        let s = this.data.sec % 60;
        if (this.data.sec >= 3600) {
          let h = this.data.sec / 3600;
          m = (this.data.sec - (Math.floor(h) )* 3600) / 60;
          return `${Math.floor(h)} : ${Math.floor(m)} : ${s}`;
        }
        return `${Math.floor(m)} : ${s}`;
      }
      return this.data.sec;
    },
  },
  methods:{
    start(){
      this.data.active = true;
        this.timer = setTimeout(() => {
        this.data.sec++
        this.start()
      }, 1000)
    }, 
    pause(){
      this.data.active = false;
      clearInterval(this.timer);
    },
    reset(){
      this.pause()
      this.data.sec = 0
    }
  },
  watch:{
    data(){
      this.$emit('input', this.data)
    }
  },
  mounted(){
    this.data =  JSON.parse(JSON.stringify(this.value))
  }
}
</script>
<style lang="scss" scoped>

.stopwatch{
  width: 225px;
  height: 120px;
  background: #696969;
  padding: 22px 0;
  color: #9E9E9E;

  .stopwatch__time{
    font-family: 'Gotham Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 22px;
    text-align: center;
    padding-bottom: 20px;
    border-bottom: 1px solid #9E9E9E;
    transition: all .3s;
  }
  .stopwatch__btns{
    display: flex;
    align-items: center;
    justify-content: center;
    padding-top: 20px;
    gap: 48px;

    button{
      transition: all .3s;
      background: transparent;
      color: #9E9E9E;
      font-size: 17px;
    }
  }
}
.active {
  color:#fff !important;
  border-color:  #fff !important;
}
</style>
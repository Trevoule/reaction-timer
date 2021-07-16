<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      click me
      <div>{{reactionTime}}</div>
  </div>
</template>

<script>
export default {
    props:['delay'],
    data(){
        return{
            showBlock:false,
            timer:null,
            reactionTime:0
        }
    },

    /*
     *  when the component firstly mounts 
     * - we wait for this.delay time before block appears
     * - then this.startTimer starts
     * - this.startTimer counts before we @click and will implement stopTimer()  
     */
    mounted(){
        console.log('component mounted')
        setTimeout(()=>{
            this.showBlock = true
            this.startTimer()
            console.log(this.delay);
        }, this.delay)
    },
    methods:{
        startTimer(){
            /*setInterval for counting after func start */
            this.timer =setInterval(()=> {
                this.reactionTime+=10
            },10)
            
        },
        stopTimer(){
            clearInterval(this.timer)
            this.$emit('end' ,this.reactionTime)
        }
    }
}
</script>

<style>
.block{
    width: 400px;
    border-radius: 20px;
    background: darkcyan;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}
</style>
<template>
  <div>
      <button v-if="!isPassed" :class="choose" @click="handlePassing" >Choose me to get passed!</button>
      
      <div v-if="buttonMessage=='second'">
          <Passing  />
          <button v-if="isPassed" :class="unChoose" @click="handleUnPassing">Choose me to reject you!</button>
      </div>
      
      
  </div>
</template>

<script>
import Passing from './Passing'
export default {
    
    
    props: {
        isPassed: Boolean(false)
    },
    components: {Passing},
    
    data: ()=>({
        buttonMessage: 'first'
    }),
    computed:  {
        choose(){ 
            if( this.buttonMessage=='first')
            return 'unselected';
              else 
              return '';
            },
        unChoose(){
            if(this.buttonMessage=='second')
              return 'selected';
              else
                return '';
        }
    },
    methods: {
        handlePassing(){
            this.buttonMessage='second';
            this.$emit('pass');
        },
        handleUnPassing(){
            this.buttonMessage='first';
            this.$emit('reject');
        }
    }

}
</script>

<style scoped >
.selected {
    background-color: red;
}
.unselected {
    background-color:green;
    
}

</style>
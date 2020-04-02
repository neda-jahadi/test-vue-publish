<template>
 <div class='component'>
     <div>
         {{countMessage}}
     </div>
     <button @click="count+=1">Add the count direct</button>
     <button @click="addCount">add the count with function</button>

 </div>

  
</template>

<script>
export default {

  props: {
    msg: String
  },
  data: () =>({
     count: 1

  }),
  computed: {
     /*function->*/ countMessage(){ return `the count is ${this.count}.`;}
  },
  methods: {
      addCount(){this.count+=1;}

      }
}
</script>

<style>

</style>
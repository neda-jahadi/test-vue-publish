<template>
  <header>
     <div>
         [logo] This is header
     </div>
     <div>
         {{authMessage}}
         <button v-show="isAuthenticated" @click="handleSignOut">Sign out</button>
     </div>
  </header>
</template>

<script>
export default {
    
    props: {
        isAuthenticated: Boolean(false)
    },
    data: ()=>({}),
computed: {
    authMessage(){
        if (this.isAuthenticated){
             return 'welcome Neda';
        }else{
           return 'sign in';
        }
           
    }
},
methods:{
    handleSignOut(){this.$emit('signOut');}
}

}
</script>

<style>
header {
    display: block;
    background-color: #A4A4A4;
    color: #1C1C1C;
    padding: 1em;
    display: flex;
    justify-content: space-between;
}

</style>
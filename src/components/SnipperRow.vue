<template>
  <div class="snipper">
           
      <div><span style="font-size:1.2em;"> Title:</span> {{snipper.title}}</div>
       <div><span style="font-size:1.2em;">Content:</span>{{snipper.content}}</div>
      <div class="ranking"> 
            <div><span style="font-size:1.2em;">Score:</span>{{snipper.score}}</div>
            <input type="range" min="1" max="16" v-model="snipper.score" />
      </div>
      <div><button class="report" @click="reportSnipper(snipper.id)">Report!</button></div>
    
  </div>
</template>

<script>
export default {
    props: {
		snipper: Object(null)
    },
    data:()=>({
        url: 'https://www.forverkliga.se/JavaScript/api/api-snippets.php?'
    }),
    methods: {
        async reportSnipper(x) {
            try {
				let response = await this.$http.post(this.url+'report', {
					params: { id: x}
				});
				console.log('sendRequestForReal', response);
				
			} catch(error) {
				console.log('Something went wrong', error);
				
			} 
        }
    }

}
</script>

<style>
.snipper {
    display: grid;
	grid-template-columns: repeat(4, 1fr);
    
}
.snipper > div {
	display: inline-block;
}


  .snipper:nth-child(even){
       background-color: whitesmoke;
  }


</style>
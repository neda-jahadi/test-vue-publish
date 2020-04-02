<template>
  <div> 
      <h1>Start the project</h1>
      
          <div>
              <button  @click="fetchSlowData" :disabled="waitingForData">Latest Snippers!</button>
              <div v-if="errorHappened">
                An error occured, Plese try again!
              </div>
              <div v-else-if="dataFromApi">
                 <div class="snipper-box">
                   <SnipperRow v-for="snipper in dataFromApi" :key="snipper.id" :snipper="snipper" />
                   
                 </div><!--snipper-box -->
              </div>
          
        </div>
        <div>
              <button @click="fetchReports">Get all the reports</button>
              <ReportedRow v-for="reported in reportedFromApi" :key="reported.id" :reported="reported" />
              <RegisterSnipp />
        </div>
  </div>
</template>

<script>
import ReportedRow from './ReportedRow.vue'
import SnipperRow from './SnipperRow.vue'
import RegisterSnipp from './RegisterSnipp.vue';

export default {

    
    data: ()=>({
        dataFromApi: null,
        reportedFromApi: null,
        url: 'https://www.forverkliga.se/JavaScript/api/api-snippets.php?',
        selectStatus: 'selected',
        delay:10,
        waitingForData: false,
        errorHappened: false
    }),
    computed: {
  latestButton(){ if(this.selectStatus=='latest') return 'selected'; else return '';} 
    
  },
  components: {
      RegisterSnipp, 
      SnipperRow,
      ReportedRow
      },

  methods: {
      fetchSlowData(){
          this.waitingForData=true;
          this.errorHappened=false;
          setTimeout(this.fetchDataForReal, this.delay);
      },
	async fetchDataForReal() {
        
		try {
            this.selectStatus='latest';
			let response = await this.$http.get(this.url+'latest');
            this.dataFromApi = response.data;
            
		} catch(error) { 
            console.log('something went wrong', error); 
            
            }finally {
				this.waitingForData = false;
            }
    },
    async fetchReports(){
        try {
			let response = await this.$http.get(this.url+'reported');
            this.reportedFromApi = response.data;
            
		} catch(error) { 
            console.log('something went wrong', error); 
            
            }
    }
}


}
</script>

<style scoped>
.showApiResult {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 0.2em;
}
.showApiResult > div {
    margin: 0.5em;
}
  .selected {
  background: green;
  color: whitesmoke;
}
.snipper-box {
  border: 1px solid gray;
  border-radius: 5px;
  background-color: lightgray;
  
  margin: 0.2em;
}
</style>


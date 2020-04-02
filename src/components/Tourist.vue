<template>
  
      <div>
          <h1>Tourist List</h1>
          <input type="text" placeholder="Skriv vad du vill" />
          <div>
          <button @click="sorteringsNyckel='namn'">Namn</button>
          <button @click="sorteringsNyckel='aktivitet'">Aktivitet</button>
          <button @click="sorteringsNyckel='restaurang'">Restaurang</button>
          <button @click="sorteringsNyckel='sightseeing'">Sightseeing</button>
          </div>
          <div class="List">
              <div class="place-item" v-for="place in sorteradePlatser" :key="place.id">
                 {{place.namn}}
                 {{place.adress}}
                 {{place.aktivitetet}}
                 {{place.restaurang}}
                 {{place.sightseeing}}
               </div>
          </div>
      </div>
      
    
         
  
  
</template>

<script>
export default {
    
  data:()=>({
      places: [
            { id: 1, namn: 'Nordic wellness', adress: 'Såggatan 6', aktivitet: 4, restaurang: 1, sightseeing: 1 },
			{ id: 2, namn: 'Sjömagasinet', adress: 'Adolf Edelsvärds gata 5', aktivitet: 1, restaurang: 4, sightseeing: 1 },
			{ id: 3, namn: 'Älvsborgs fästning', adress: 'Nya Älvsborgs Fästning', aktivitet: 1, restaurang: 1, sightseeing: 5 },
			{ id: 5, namn: 'Miami Design District', adress: '110 NE 40th St, Miami, FL 33137, United States', aktivitet: 3, restaurang: 4, sightseeing: 4 },
			{ id: 6, namn: 'Liseberg', adress: 'Örgrytevägen 5, 402 22 Göteborg', aktivitet: 4, restaurang: 1, sightseeing: 1 },
			{ id: 7, namn: 'Villa Belparc', adress: 'A O Elliots Väg 10', aktivitet: 1, restaurang: 3, sightseeing: 2 },
			{ id: 8, namn: 'Donald Trump', adress: '1600 Pennsylvania Avenue, Washington DC', aktivitet: 4, sightseeing: 1, restaurang: 3 }
      ],
      sorteringsNyckel: 'namn',
      filter: ''
  }),
  computed: {
      sorteradePlatser() {
          let copy=[...this.places];
          if( this.sorteringsNyckel == 'namn' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.namn.toLowerCase() < b.namn.toLowerCase() ) return -1;
					else if( a.namn.toLowerCase() > b.namn.toLowerCase() ) return 1;
					else return 0;
				} )
				return sorterad;
			} 
          else {
               let sorterad = copy.sort((a,b) =>{
                  if(a.aktivitet>b.aktivitet) return -1;
               else if(a.aktivitet<b.aktivitet) return 1;
                else return 0;
            })
            return sorterad;
          }
          
      }//sorterade platser()
  }//methods
}//export default
</script>

<style>
.List {
    text-align: left;
}

</style>
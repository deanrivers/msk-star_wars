<template>
  <div id="api-container">
    <div id="main-container">
      <div id="sw-logo-container">
        <img v-bind:src="'http://loodibee.com/wp-content/uploads/Star-Wars-transparent-logo.png'" alt="sw-logo" class="logo">
      </div>

      <p>What Star Wars category would you like to search?</p>
      <div id="search-container">
        <span>category -></span>
        <select v-model="searchHeader" @change="get(searchHeader)">
          <option>people</option>
          <option>starships</option>
          <option>vehicles</option>
          <option>species</option>
          <option>planets</option>
        </select>
        <span>page -></span>
        <select v-model="page" @change="get(searchHeader)">
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
        </select>

        <button id="searchButton" v-on:click="get(searchHeader)" v-if="!firstSearchDone">Search</button>
      
      </div>
      <div id="loading-container" v-if="info===null && firstSearchDone">
        <img v-bind:src="'https://media2.giphy.com/media/PUYgk3wpNk0WA/giphy.gif?cid=790b761107d64830af64458f375a1b97726c8ad2e59f358e&rid=giphy.gif'" alt="loader-gif" class="loader">
        
      </div>
      <h1 v-if="info !==null"><u>List <span class="lower">of</span> {{searchHeader}}</u></h1>
      <div class="test-container" v-if="info !== null">

        <!-- info card -->
        <div class="info-container" v-for="(item,index) in info.data.results" v-bind:key="index">
          <!-- people -->
          <h3>{{item.name}}</h3>
          <p v-if="searchHeader==='people'">Birth Year: {{item.birth_year}}.</p>
          <p v-if="searchHeader==='people'">Height: {{item.height}} cm.</p>
          <p v-if="searchHeader==='people'">Gender: {{item.gender}}.</p>
          <p v-if="searchHeader==='people'">Hair color: {{item.hair_color}}.</p>
          
          <!-- starship --> 
          <p v-if="searchHeader==='starships'">Model: {{item.model}}.</p>
          <p v-if="searchHeader==='starships'">Manufacturer: {{item.manufacturer}}.</p>
          <p v-if="searchHeader==='starships'">Cost: {{item.cost_in_credits}} credits</p>
          <p v-if="searchHeader==='starships'">Crew size: {{item.crew}}.</p>
          <p v-if="searchHeader==='starships'">Cargo capacity: {{item.cargo_capacity}}.</p>

          <!-- vehicles -->
          <p v-if="searchHeader==='vehicles'">Model: {{item.model}}.</p>
          <p v-if="searchHeader==='vehicles'">Max speed: {{item.max_atmosphering_speed}}.</p>
          <p v-if="searchHeader==='vehicles'">Max Passengers: {{item.passengers}}.</p>
          <p v-if="searchHeader==='vehicles'">Crew size: {{item.crew}}.</p>

          <!-- species -->
          <p v-if="searchHeader==='species'">Classification: {{item.classification}}.</p>
          <p v-if="searchHeader==='species'">Designation: {{item.designation}}.</p>
          <p v-if="searchHeader==='species'">Average Height: {{item.average_height}} cm.</p>
          <p v-if="searchHeader==='species'">Average lifespan: {{item.average_lifespan}} years.</p>
          
          <!-- planets -->
          <p v-if="searchHeader==='planets'">Terrain: {{item.terrain}}.</p>
          <p v-if="searchHeader==='planets'">Population: {{item.population}}.</p>
          <p v-if="searchHeader==='planets'">Gravity: {{item.gravity}}.</p>

        </div>
      </div>
    </div>
  </div>
</template>

<script defer>

import axios from 'axios'

export default {
    name: 'api',
    data(){
      return {
        title: 'test',
        info: null,
        index: 9,
        firstSearchDone: false,
        isLoading: false,
        page:1,

        starwarsCriteria: [
          {people:['item.name','item.birth_year','item.height','item.gender','item.hair_color']},
        ],
        searchHeader: 'people',
        images:{
          credit: 'https://images.pexels.com/photos/414612/pexels-photo-414612.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500'
        }
        
      }
    },
    mounted(){
      //this.get()
    },

    methods:{
      get(searchHeader){
        this.info = null
        axios
        .get('https://swapi.co/api/'+searchHeader+'/?page='+this.page)
        .then(response => (this.info = response))
        this.firstSearchDone = true
        
      },

      

      
    }

    //create array of objects
}

</script>

<style>
html,body{
  width: 100%;
  box-sizing: border-box;
  background: #f4f4f3;
  margin: 0 auto;

}


h1{
  text-transform: capitalize;
  }

span{
  text-transform: lowercase;
  }

#search-container{
  display: flex;
  justify-content: center;
  align-items: center; 
  flex-direction: row; 
  margin-top: 0%;
  margin-bottom: 5%;
}

#search-container select, button{
  margin: 1%;
  }

#sw-logo-container{
  width: 100%;
  margin: 0 auto;

}

.logo{
  max-width: 200px;
  width: 50%
}

/* .info-container{
  border: 1px solid black;
  margin: 5%;
  padding: 5%;

} */

.test-container{
  display: flex;
  justify-content: center;
  flex-direction: row;
  width: 100%;
  align-items: center;
  margin: 0 auto;
  flex-wrap: wrap;
}

.info-container {
  background: white;
  /* border: 1px solid #ddd; */
  /* border-top: 1px solid #ddd; */
  border-bottom: 1px solid #ddd;
  border-radius: 5px;

  width: 500px;
  
  /* width: 350px;
  height: 470px; */

  /* box-shadow: 0 1px 0px rgba(0, 0, 0, 0.07), 0px -1px 4px rgba(1,0,0,0.05); */
  /* box-shadow: 0 1px 0px rgba(15, 15, 27, 0.7), 0px -1px 4px rgba(15,15,27,0.05); */
  /* 0F0F1B */
  /* margin: 10px 5px 15px 5px; */
  bottom: 0px;
  position: relative;
  box-shadow: 0 1px 0px rgba(0,0,0,0.07), 0px -1px 4px rgba(1,0,0,0.05);
  transition: all 250ms cubic-bezier(0.02, 0.01, 0.47, 1);
  overflow: hidden;
  position: relative;
  margin-bottom: 2%;
  
  margin: 1%;
  padding: 1%;
  border: 0px solid #ffc106;


}

.info-container:hover{
  box-shadow: 0 10px 20px rgba(0,0,0,0.15);
  position: relative;
  bottom: 5px;
  border: none;
  background: #ffc1066b;
  /* border: 2px solid #ffc106; */
  /* border: 1px solid #84DBFD; */
} 

select{
  background-color: #ffc1066b;
  color: black;
  border: none;
  width: 80px;
  height: 40px;
}

button#searchButton{
  width: 140px;
  height: 40px;
  
  background-color: #ffc1066b;
  color: black;
  border: none;
  border-radius: 5px;
  border: 0px solid #ffc106;
  transition: 0.2s ease-in-out;
  cursor: pointer;
  background: black;
  color: white;
  outline: none;
}

button#searchButton:hover{
  border: 5px solid #ffc106;

}

.loader{
  max-width: 100px;
}

@media only screen and (max-width: 600px) {
  .info-container{
    margin: 3%;
  }

}


</style>

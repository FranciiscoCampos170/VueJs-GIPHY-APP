<template>
  <div id="app">
    <div id="myDIV" class="header">
          <input type="text" id="myInput" placeholder="Search all the GIFs" v-model="name">
          <span class="addBtn" v-on:click="search">Search</span>
       </div>

  <div class="gallery"> 
    
      <div v-for="data in datas" :key="data.id" class="gallery-panel"> 
        <img alt="" :src="data['images']['fixed_width']['url']">
        </div>
  </div>
       
      
      
  
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      datas: [],
      name: null
      }
  },
  methods: {
    search() {
      console.log(this.name);
      
      fetch('https://api.giphy.com/v1/gifs/search?api_key=s6avXyU73aCpWPNajq2vkLpiJpMHnb53&q='+this.name+"&limit=25&offset=0&rating=G&lang=en", {
      method: 'get',
      headers: {
        'Content-Type': 'application/json'
      },
    }).then((response) => response.json())
        .then((res) => {this.datas = res.data}).catch((error) =>{ console.log(error)
        }); 
  }
   
  },
}
</script>

<style>
 .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
    grid-gap: 1rem;
    max-width: 80rem;
    margin: 5rem auto;
    padding: 0 5rem;
  }
  .gallery-panel img {
    width: 100%;
    height: 22vw;
    object-fit: cover;
    border-radius: 0.75rem;
  }

  #app{
    background-color: #1A202C;
  }
  .notescss{
    width: 200px;
  }

  .time{
    font-size: 0.8em;
  }
* {
  box-sizing: border-box;
}


/* Style the header */
.header {
  background-color: #f44336;
  padding: 30px 40px;
  color: white;
  text-align: center;
}

/* Clear floats after the header */
.header:after {
  content: "";
  display: table;
  clear: both;
}

/* Style the input */
input {
  margin: 0;
  border: none;
  border-radius: 0;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
}

/* Style the "Add" button */
.addBtn {
  padding: 10px;
  width: 25%;
  background: #d9d9d9;
  color: #555;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}

.addBtn:hover {
  background-color: #bbb;
}
</style>

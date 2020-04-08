<template>
  <div id="app">
    <div v-for="data in datas" :key="data.id"> 
      <div>
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
      ex: "ex"
      }
  },
  mounted() {
    fetch('https://api.giphy.com/v1/gifs/search?api_key=s6avXyU73aCpWPNajq2vkLpiJpMHnb53&q='+"mrrobot", {
      method: 'get',
      headers: {
        'Content-Type': 'application/json'
      },
    }).then((response) => response.json())
        .then((res) => {this.datas = res.data}).catch((error) =>{ console.log(error)
        }); 
  }
  
}
</script>

<style>

</style>

<template>
  <div id="main-view">
  

    <div class="fetch">
      <h3><span>News</span> categories</h3>
     <section class="select-box">
        <select v-model="selected" class="select-box">
        <option v-for="value in categories" :key= 'value'> 
          {{value}}
        </option>
      </select>
      <button v-on:click="newsFetch" class="fetch-btn">Fetch article</button>
     </section>
    </div>

    <div v-if="stillFetching" class="loading-msg">
      <h4>Please a wait moment, your news feed is loading ...... </h4>
      <p>grab a coffee</p>
    </div>

    <div v-if="notFetching" class="static-content">
      <h1>Welcome to the world of <span>top stories</span>...</h1>
      <h4> Please select a category above</h4>
    </div>

    <div v-bind="newsFeed" class="news-area">
        <div class="box"  v-for="news in newsFeed" :key= news>
            <p class="title">{{news.title}}</p>
            <small class="author"> Author: {{news.byline}}</small>
            <p class="news-abstract">{{news.abstract}}</p>
            <p class="link"><a v-bind:href="news.short_url" target="_blank">View full article</a></p>
        </div>
    </div>

  </div>
  
    
</template>

<script>
import axios from 'axios'

export default {
  props:["categories"],

  data () {
    return {
     newsFeed:[],
     selected:"",
     stillFetching : false,
     notFetching:true
    }
  },
  methods:{

      newsFetch(){

        this.stillFetching = true
        this.newsFeed = ""
        this.notFetching= false 
         
          const apiKey ='ogAMAnUI0b592Gxiu44pO9EqHTXnGh2Q'
          const appId = '648de852-3a0c-4e24-b167-c57b3b9336d8'

          const base =`https://api.nytimes.com/svc/topstories/v2/${this.selected}.json`

          const query =`?api-key=${apiKey}`

          axios.get(base+""+query)
            .then(res =>{
                console.log("response:", res)
                this.stillFetching = false
                this.newsFeed = res.data.results
                this.newsFeed = this.newsFeed.slice(0,10)
                
                console.log("NewsFeed: ", this.newsFeed)
            }).catch(err =>{
                console.log("Error:", err)
            })

       
      },
  },
  

}


</script>

<style scoped>

.main-view{
  max-width: 80%;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.news-area{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1em;
  max-width: 80%;
  margin: 10px auto;
}

.box{
    /* background: #d3d3d3; */
    width: 300px;
    height: auto;
    border: 0;
    border-radius:5px ;
    color:#42b983;
    margin: 20px;
    padding: 20px;
    box-shadow: 1px 3px 3px 3px #eee;
    margin: 20px ;
}
.fetch{
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content:center;
  padding: 2em;
  margin: 10px auto;
}

.fetch h3{
  color:#42b983;
  padding: 20px;
}

.fetch span{
  text-decoration: underline;
}

.fetch-btn{
  padding: 10px;
  font-weight: bold;
  color: #fff;
  background: #42b983;
  border: 0;
  border-radius: 10px;
  outline: 0;
  margin: 0 10px;
  cursor: pointer;
}
.select-box{
  padding: 10px;
  font-size: 16px;
  color: #42b983;
  outline: 2px #42b983;
}

.loading-msg{
  color: #42b983;
  padding: 10px;
  font-family: "Open sans";
  display: flex;
  align-items: center;
  text-align: left;
  justify-content: center;
  margin: auto;
  flex-direction: column;
}

.static-content{
  color: #42b983;
  padding: 10px;
  font-family: 'poppins';
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.static-content h1{
  font-size: 1.6em;
  font-weight: 700;
}
.static-content h4{
  text-align: left;
}


.static-content span{
  text-decoration: underline;
  font-size: 1.1em;
  font-weight: 600;
}

.title{
  font-family: 'poppins';
  font-size: 1.3em;
  font-weight: 700;
}

.author, .news-abstract, .link{
  font-family: 'Open sans';
}
.author{
  color:#333 ;
  font-size: 15px;
  font-weight: 400;
}
.news-abstract{
  color: #d3d3d3;
  margin:20px 0;
}
.link a{
  text-decoration: none;
  color: #42b983;
  margin: 10px 0;
}

.link a:hover{
  text-decoration: underline;
}
</style>

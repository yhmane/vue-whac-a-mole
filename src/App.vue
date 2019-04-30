<template>
  <div id="app">
    <Title msg="Whac a mole!!"></Title>
    <div class="content">
      <div class="game-panel">
        <hole 
          v-for="molehole in holeList"
          :key="molehole.id"
          @caps="capture(molehole.id)"
        >
        </hole>
      </div>
    </div>
    <button @click="start()">Start</button>
    <button @click="retry()">Retry</button>
  </div>
  
</template>

<script>
import Title from './components/Title.vue'
import Hole from './components/Hole.vue'

export default {
  name: 'app',
  components: {
    Title,
    Hole
  }, 
  data() {
    return {
      count: 13,
      holeList: [
        {id: 1,  type: Number},
        {id: 2,  type: Number},
        {id: 3,  type: Number},
        {id: 4,  type: Number},
        {id: 5,  type: Number},
        {id: 6,  type: Number},
        {id: 7,  type: Number},
        {id: 8,  type: Number},
        {id: 9,  type: Number},
        {id: 10, type: Number},
        {id: 11, type: Number},
        {id: 12, type: Number},
        {id: 13, type: Number},
        {id: 14, type: Number},
        {id: 15, type: Number},
        {id: 16, type: Number}
      ],
      assignHole: [],
      catch:0
    }
  },
  methods: {
    start() {
      alert("Start Whac a mole!!");
      this.assignHole = [];
      const arr = this.assignHole;
      for(var cnt=0; cnt<5; ) {

        const holeNum = Math.floor(Math.random() * 16) + 1;
        const holeFlag = true;
        arr.map(function(value){

          if(value == holeNum) {
            holeFlag = false;
          }
        });

        if(holeFlag == true) {
          arr.push(holeNum);
          holeFlag = false;
          cnt++;
        }
      }
    },
    capture(data) {
      if(this.assignHole.length == 0) {
        alert("Click start button!")
        return;
      }

      if(this.catch == 5) {
        alert("You win!!");
        return;
      }

      this.count = this.count - 1; 
      if(this.count<0) {
        alert("over!");
        return;
      }

      var moleFlag = false;
      for(var cnt=0; cnt<5; cnt++) {
        if(this.assignHole[cnt] == data) {
          moleFlag = true;
          this.catch++;
        }
      }

      if(moleFlag == true) {
        this.$children[data].mole = true;  
      } else {
        this.$children[data].land = true;
      }
    },
    retry() {
      window.location.reload();
    }
  },
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  margin: 0;
  padding: 0;
}
.game-panel {
  background: green;
  width:808px;
  height:808px;
  margin:0 auto;
  border:1px solid grey;
  border-collapse:collapse;
}
button {
  width: 405px;
  border: 1px solid gray;
  height: 50px;
  border-radius: 5px;
  background-color: black;
  color: white;
  font-size: 30px;
  font-style: italic;
}
</style>

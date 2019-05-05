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
      restCount: 13,
      holeList: [
        {id: 1,  check: false},
        {id: 2,  check: false},
        {id: 3,  check: false},
        {id: 4,  check: false},
        {id: 5,  check: false},
        {id: 6,  check: false},
        {id: 7,  check: false},
        {id: 8,  check: false},
        {id: 9,  check: false},
        {id: 10, check: false},
        {id: 11, check: false},
        {id: 12, check: false},
        {id: 13, check: false},
        {id: 14, check: false},
        {id: 15, check: false},
        {id: 16, check: false}
      ],
      assignHole: [],
      moleCatch:0,
    }
  },
  methods: {
    start() {
      this.assignMoleHole();
      alert("Start Whac a mole!!");
    },
    capture(idx) {
      if(this.defineAlertMsg(idx).length>0) return;

      let moleFlag = this.checkMoleFlag(idx);
      if(moleFlag == true)  this.$children[idx].mole = true;
      else                  this.$children[idx].land = true;

      this.count(idx);
    },
    count(data) {
      this.restCount--; 
      this.holeList[data-1].check = true;
    },
    assignMoleHole(data) {
      for(let cnt=0; cnt<5; ) {

        const holeNum = Math.floor(Math.random() * 16) + 1;
        const holeFlag = true;
        this.assignHole.map(value => {
          if(value == holeNum) holeFlag = false;
        });

        if(holeFlag == true) {
          this.assignHole.push(holeNum);
          holeFlag = false;
          cnt++;
        }
      }
    },
    checkMoleFlag(data) {
      let flag = false
      this.assignHole.map( value => {
        if(value == data) {
          flag = true;
          this.moleCatch++;
        }
      });
      return flag;
    },
    defineAlertMsg(data) {
      let msg = "";
      if(this.moleCatch == 5)                  msg = "You Win!!";
      if(this.restCount<0)                     msg = "Over!!";
      if(this.holeList[data-1].check ==  true) msg = "this hole is already opened";
      if(msg.length>0)                         alert(msg);
      return msg;
    },
    retry() {
      window.location.reload();
    }
  },
  mounted() {
    this.start();
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
  width: 810px;
  border: 1px solid gray;
  height: 50px;
  border-radius: 5px;
  background-color: black;
  color: white;
  font-size: 30px;
  font-style: italic;
}
</style>

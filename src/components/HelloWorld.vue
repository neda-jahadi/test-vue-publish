<template>
  <div class="hello">
    <h1>Welcome to vue intro</h1>
    <div v-bind:class="myClass" v-bind:style="{'background-color':myStyle}">
      The value is : {{count}}
    </div>
    <div class='buttons'>
      <input type="text"  @keyup="handleKeyUp" />
      <button @click="handleClickSetColor">Set color?</button>
      <!--{{inputColor}}-->

      <br/>
    <button @click= "myClass='unicorn'">Set color to blue</button>
    <button @click= "myClass='racoon'">Set color to tomato</button>
    <button @click= "myClass='basilisk'">Set color to gray</button>
    <br/>
    {{myClass}}  <!-- felsöknings metod -->
    </div>

    <div v-if="myClass=='racoon'">
       Visible only we have a racoon(tomato)
    </div>
    <div v-else-if="myClass=='unicorn'">
       Visible only we have a unicorn(blue)
    </div>
    <div v-else>
       Somethig else?
    </div>
    <div v-show="myClass=='racoon'">
        Also Visible only we have a racoon(tomato)
    </div>

    <div v-bind:class="neda" v-bind:style="{'color':myColor}" >
        This is neda
    </div>
    <div>
      
       <input type="text" @keyup="handlePenKeyUp"  />
      <button @click="handleClickPen">Set the color</button>
      <br/>
      
   
    <button @click="makeYellow">Set to yellow</button>
    <button @click="neda='green'">Set to green</button>
    <button @click="neda='pink'">Set to pink</button>
    </div>
    <br/>
    
    <div v-if="neda=='myNeda'">Visible when it is blueGreen</div>
    <div v-else-if="neda=='yellow'">Visible when it is yellow</div>
    <div v-else-if="neda=='green'">Visible when it is green</div>
    <div v-else>Visible when it is pink</div>
    <div v-show="neda=='myNeda'">
      Visible when it is blueGreen
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () =>({
  count: 1,
  myClass:'unicorn',
  myStyle: '',
  myColor: '',
  neda: 'myNeda',
  inputColor: '',
  inputPenColor: ''
  

  }),
  methods : {
    handleKeyUp(event){
      console.log('handleKeyUp event=', event);
       this.inputColor=event.target.value;
      },
      handleClickSetColor() {
        this.myStyle=this.inputColor;
      },
      handlePenKeyUp(event){ console.log(event); this.inputPenColor=event.target.value;},
      handleClickPen(){this.myColor=this.inputPenColor;},
      makeYellow(){console.log('yellow button clicked'); this.neda='yellow';}

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.buttons {
  margin-top: 2rem;
}
.myNeda {
  font-size: bold;
  border: 1px solid tomato;
  background-color: aqua;
}
.yellow {
  background-color: yellow;
}
.green {
  background-color: green;
}
.pink {
  background-color: pink;
}
.unicorn {
background-color: lightblue;
}
.racoon {
background-color: tomato;
}
.basilisk {
background-color: gray;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

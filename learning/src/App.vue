<template>
  <title>Udemy Vue Learning</title>
  <h1 id="nav">Udemy Vue Learning</h1>
  <div id="box1">
  <section>
    <h1><u>Exercise 1: Interpolation, Binding and Simple Rendering</u></h1>
  <!-- 1) Output your name -->
  <p>Name: {{ name }}</p>
  <!-- 2) Output your age -->
  <p>Age: {{ age }}</p>
  <!-- 3) Output your age + 5 -->
  <p>Age in 5 years: {{ calculateAge() }}</p>
  <!-- 4) Output a random number (0 to 1) -->
  <p>Favorite Number: {{ calculateRandom() }}</p>
  <div>
    <!-- 5) Display some image you found via Google -->
    <img id="image" v-bind:src="ImageUrl" />
  </div>
  <!-- 6) Prepopulate the input field with your name via the "value" attribute -->
  <input id="input" type="text" v-bind:value="name" /><br>
    <br>
    <hr>
    <br>
  </section>

  <section>
    <div id="box2">
    <h1><u>Exercise 2: Event Listener Bindings</u></h1>
    <!-- 1) Button to increase and decrease -->
    <button id="button" @click="increase">Increase + 1</button>
    <button id="button2" @click="decrease">Decrease - 1</button>
    <p id="result">Counter: {{ counter }}</p>
  </div>
    <br>
    <hr>
    <br>
  </section>
  </div>

  <div id="box3">
  <section>
    <h1><u>Exercise 3: Passing Parameters too the Event Listeners</u></h1>
    <!-- 1) We can add a value num as a parameter to our methods for the buttons -->
    <button id="button" @click="add(10)">Increase + 10</button>
    <button id="button2" @click="subtract(5)">Decrease - 5</button>
    <p id="result">Counter: {{ counter }}</p>
    <br>
    <hr>
    <br>
  </section>

  <section>
    <h1><u>Exercise 4: Input field Email!</u></h1>
    <input id="input" placeholder="Type your email here" type="text" @input="setEmail">
    <p id="result">Your Email: {{ email }}</p>
    <br>
    <hr>
    <br>
  </section>
  </div>

  <div id="box1">
  <section>
    <h1><u>Exercise 5: Practicing Events!</u></h1>
    <!-- 1) Show an alert(any text of your choice) when the button is pressed -->
    <button id="button" @click="showAlert()">SHOW ALERT WHEN BUTTON PRESSED</button><br><br>
    <!-- 2) Register the user input on "keydown" and output it -->
    <input id="input" placeholder="Type text here" type="text" v-model="text">
    <p id="result">Output: {{ text }}</p>
    <button id="button" @click="clearInput()">RESET OUTPUT</button>
    <br>
    <hr>
    <br>
  </section>

    <section>
      <h1><u>Exercise 6: Reactivity in Action!</u></h1>
      <button @click="addNumber(5)">Add 5</button>
      <button @click="addNumber(1)">Add 1</button>
      <!-- 1) Connect the button and calculate a value (a number) -->
      <!-- 2) Show a value of "Not There Yet" until you reach a result of exactly 37 -->
      <!-- 3) Show a value of "Too much!" if the result is greater than 37-->
      <p>Counter: {{ number }}</p>
      <p>Result: {{ result }}</p>
      <p>If Result is smaller than 37 "Not There Yet"</p>
      <p>If Result is equal too 37 = 37</p>
      <p>If Result is bigger than 37 = "Too Much"</p>
      <!-- 4) Watch for changes in "result" and reset the value to 0 after 5 seconds-->
      <br>
      <hr>
      <br>
    </section>
  </div>

  <div id="box3">
  <section>
    <h1><u>Exercise 7: Dynamic Styling!</u></h1>
    <!-- 1) Fetch the user input and use it as a CSS class-->
    <!-- 2) The entered class should be added to the below paragraph-->
    <input type="text" v-model="inputClass">
    <!-- (Available classes: "user1", "user2")-->
    <p :class="inputClass"
    >

    </p>
    <button>Toggle Paragraph</button>
    <br>
    <hr>
    <br>
  </section>
  </div> 

  <h1 id="nav">Monster Slayer Game</h1>
  <section>
    
  </section>

</template>


<script>
export default {
  name: 'App',
  data() {
    return {
      name: 'Michael',
      age: 37,
      ImageUrl: 'https://images.unsplash.com/photo-1453928582365-b6ad33cbcf64?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1773&q=80',
      counter: 0,
      num: 0,
      email: '',
      text: '',
      number: 0,
      inputClass:'',
    };
  },

  //@ We only work with computed values that only need to be rendered alone
  computed: {
    result() {
      if(this.number < 37){
        return 'Not there yet';
      }else if (this.number === 37) {
        return this.number;
      }else {
        return 'Too Much!';
      }
    }
  },

  watch: {
    result() {
      setTimeout(function(){
        this.number = 0;
      }, 5000);
    }
  },

  methods: {
    //@ Exercise 1
    calculateAge() {
      return this.age + 5;
    },
    calculateRandom(){
      return Math.random();
    },

    //@ Exercise 2
    increase(){
      return this.counter++;
    },
    decrease(){
      return this.counter--;
    },

    //@ parameters inside the method
    add(num){
      return this.counter = this.counter + num;
    },
    subtract(num) {
      return this.counter = this.counter - num;
    },

    setEmail(event){
      this.email = event.target.value;
    },

    showAlert(){
      alert ('Button is pressed');
    },

    clearInput(){
      this.text = '';
    },

    addNumber(num){
      this.number = this.number + num;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  background-color: antiquewhite;
}

#box1{
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  background: antiquewhite;
}

#box2{
margin-top: 250px;
}

#box3{
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  background: #ceffea;
}

#input{
  height: 25px;
  width: 250px;
}

#image {
  height: 200px;
  width: 300px;
}

#button {
 margin-right: 30px;
  background: azure;
}

#button2 {
  background: azure;
}

#result {
  font-size: 35px;
  font-family: "Droid Sans Mono",cursive;
  color: darkolivegreen;
}

h1 {
  font-size: 25px;
  color: dimgrey;
}
</style>

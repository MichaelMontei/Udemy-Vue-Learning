# Udemy-Vue-Learning
![Vue](/learning/images/images.png)

Source: https://www.udemy.com/course/vuejs-2-the-complete-guide/

### Learning the Basics of VUE
<br>

# Chapter 1

### 1. Example of Vue Lay-out

```html
<template>
    Here we can render props, methods with interpolation {{}} used in the app.
    <p>{{ methodsName }} </p>
</template>

<script>
    Reserved names (DATA, METHODS, COMPUTED, WATCH)
    Data itself is seen as a function.
    While Methods and Computed take objects or functions.
    Watch looks for changes, like calculations, etc..
</script>

<styling>
    CSS . SASS
</styling>
```
<hr>

### 2. Directive Bindings Examples
<br>

- V-HTML -> will output the render in html style and not just the content of the interpolation! 
- V-BIND -> Will bind for instance an href to output a working url link
- V-ON or @ -> Symbol are event listeners binding we can use in Vue <br>
example of this: @click="methodsName"
- V-MODEL -> This is a special 2-way Binding in Vue that listens for user input and updates it in the Vue model, meaning we can use it later on if needed. It actually is a shortcut for V-BIND and V-INPUT together.

<hr>

### 3. Value Presets in VUE
<br>

In VUE we have 4 VALUE PRESETS that we can use in our "script".
- DATA: to store data deeuh.
- METHOD: Here we can write methods.
- WATCH: is to watch a value changing throughout a method for instance.
- COMPUTED: also a method, but the big difference is that this will render solo.

<hr>

#### 4. First Page of what I Learned and what I created so far
![Vue](/learning/images/page1.JPG)

<hr>
<br>

# Chapter 2

### 1. Creating a Monster Game Slayer

- First we would need to set our data properties:

```js
 data(){
    return {
        playerHealth: 100,
        monsterHealth: 100,
        currentRound: 0,
        winner: null,
        logMessages: []
    };
  },
```
<hr>
<br>

- We then need to set our methods so that we can: 
  - start a new game
  - attack monster
  - attack the player
  - Special attack
  - Heal our player whilst attack from a monster
  - Surrender (resetting the game)
  - add Logs to our combat system

```js
methods: {
    // ~~~~ START NEW GAME ~~~~
    startGame(){
      this.playerHealth = 100;
      this.monsterHealth = 100;
      this.winner = null;
      this.currentRound = 0;
      this.logMessages = [];
    },

    // ~~~~ ATTACK BUTTON ~~~~
    attackMonster(){
      this.currentRound++;
      const attackValue = getRandomValue(5, 12);
      this.monsterHealth = this.monsterHealth - attackValue;
      //@ Whenever we attack the monster it should hit the player back, therefor we call this function here.
      this.addLogMessage('player', 'attack', attackValue);
      this.attackPlayer();
    },
    attackPlayer(){
      const attackValue = getRandomValue(8, 15);
      this.playerHealth = this.playerHealth - attackValue;
      this.addLogMessage('monster', 'attack', attackValue);
    },
    // ~~~~ SPECIAL ATTACK ~~~~
    specialAttackMonster(){
      this.currentRound++;
      const attackValue = getRandomValue(10, 25);
      this.monsterHealth -= attackValue;
      this.addLogMessage('player', 'special-attack', attackValue);
      this.attackPlayer();
    },

    // ~~~~ MEeeDic! ~~~~
    healPLayer(){
      this.currentRound++;
      const healValue = getRandomValue(8, 15);
      if (this.playerHealth + healValue > 100){
        this.playerHealth = 100;
      }else {
      this.playerHealth += healValue;
      }
      this.addLogMessage('player', 'heals', healValue);
      this.attackPlayer();
    },

    surrender(){
      this.winner = 'monster';
    },

    addLogMessage(who, what, value){
      //@ unshift adds something to the beginning of the array
      this.logMessages.unshift({
        actionBy: who,
        actionType: what,
        actionValue: value
      });
    }
  }
```
<hr>
<br>

- Afterwards we can add Computed Methods to calculate healthbars and watchers to see changes in the playerHealth and MonsterHealth.
<br>
<br>
    Computed Section:
  - We check if the playerHealth || MonsterHealth goes below 0 then show a width of 0%
  - We also speficy here that the special attack can only be used every three rounds with a modulus.
<br>
<br>
    Watch Section:
  - Here we watch the PlayerHealth and MonsterHealth and check if certain conditions are met to win, lose or draw the game.

```js
  computed: {
    monsterBarStyles(){
      if(this.monsterHealth < 0) {
        return { width: '0%'};
      }
      return {width: this.monsterHealth + '%'}
    },
    playerBarStyles(){
      if(this.playerHealth < 0) {
        return { width: '0%'};
      }
      return {width: this.playerHealth + '%'}
    },
    mayUseSpecialAttack(){
      return this.currentRound % 3 !== 0
    }
  },
  watch: {
    playerHealth(value){
      if (value <= 0 && this.monsterHealth <= 0) {
        // a draw
        this.winner = 'draw';
      } else if (value <= 0) {
        // Player lost
        this.winner = 'monster';
      }
    },
    monsterHealth(value) {
      if (value <= 0 && this.playerHealth <= 0) {
        // a draw
        this.winner = 'draw';
      } else if (value <= 0) {
        // Monster lost
        this.winner = 'player';
      }
    }
  },
```
<hr>

- As a last step we need to set every binding in our template ofcourse

```js
<section class="container" v-if="winner">
        <h2>Game Over!</h2>
          <h3 v-if="winner === 'monster'">You Lost!</h3>
          <h3 v-else-if="winner === 'player'">You Won!</h3>
          <h3 v-else>It's A Draw!</h3>
          <button @click="startGame">Start A New Game?</button>
      </section>
      <section id="controls" v-else>
        <button @click="attackMonster">ATTACK</button>
        <button :disabled="mayUseSpecialAttack" @click="specialAttackMonster">SPECIAL ATTACK</button>
        <button @click="healPLayer">HEAL</button>
        <button @click="surrender">SURRENDER</button>
      </section>
      <section id="log" class="container">
        <h2>Battle Log</h2>
        <ul>
          <li v-for="logMessage in logMessages" v-bind:key="logMessage.id">
            <span
              :class="{'log--player': logMessage.actionBy === 'player', 'log--monster': logMessage.actionBy === 'monster'}"
              >{{ logMessage.actionBy === 'player' ? 'Player' : 'Monster'
              }}</span
            >
            <span v-if="logMessage.actionType === 'heal'">
              heals himself for
              <span class="log--heal">{{ logMessage.actionValue }}</span></span
            >
            <span v-else>
              attacks and deals
              <span class="log--damage">{{ logMessage.actionValue }}</span>
            </span>
          </li>
        </ul>
      </section>
```
<hr>

- Below we have the example of how the game looks and works. 

![Vue](/monstergame/images/monster.JPG)

<hr>
<br>

# Chapter 3

### 1. What is Reactivity in VUE and what does it do?

- In VUE, your data object is set to a reactive data object behind the scenes. This essentially wraps your data properties into a Javascript features proxy. This way we can use the "this" keyword inside our methods referring to this data properties and much more.

<hr>

### 2. Proxy's in JS u mentioned?

- Lets make an example to explain how VUE handles this: 
```js
const data = {
  message: 'Hello!'
}

const handler = {
  set(target, key, value) {
    console.log(target);
    console.log(key);
    console.log(value);
  }
}

const proxy = new Proxy(data, handler);
proxy.message = 'Hello!!!!'
```

- In our first console.log(target) -> Vue just takes the data object and shows it. ("Hello!")
- In the second console.log(key) -> its show the property "value" in this key message. (message)
- In the third console.log(value) -> it actually updates the target value into our new value ("Hello!!!!")

<hr>
<br>

# Chapter 4

### 1. Introduction too Props
- In our components folder we made a new VUE Project and here we made a new component FriendContact.vue 
- We specified the props: name, phoneNumber and emailAddress (This should always be in camelcase! otherwise it would be an invalid JS property name!)
- We can now use these props inside our template just calling the 'string' name.

```js
<template>
<FriendContact 
  name="Michael Monteiro"
  phone-number="12345 5678 899"
  email-address="michael@localhost.com"
></FriendContact>
</template>

export default {
    name: 'App',
    props: ['name', 'phoneNumber', 'emailAddress'],
}
```
<hr>

### 2. Props behavior and changing
- Data changed in APP.vue should only change in the app itself as a prop. This is called mutation, Vue will not allow this. 
- We can change the data in 2 ways: 
   - we can let the parent know that we want to change the data and pass the updated data.
   - We can also change the data in the child, but then we need to be aware that the data in the parent would not change with it.
<hr>

### 3. Validation of props
- Instead of giving props in an array, we can do a better practice for props to be more strict. For instance, instead of using this props inside an array, we can use an object and give a type to our props.

```js
export default {
    name: 'App',
    //props: ['name', 'phoneNumber', 'emailAddress'],
    //@ lets make the props an object and define type and required for each prop
    props: {
      name: {
        type: String,
        required: true
      },
      phoneNumber: {
        type: String,
        required: true
      },
       emailAddress: {
        type: String,
        required: true
      },
        isFavorite: {
        type: String,
        required: false,
        default: '0'
      },
    }
```

- Supported Types:
  - String / Number / Boolean / Array / Object / Date / Function / Symbol
<hr>
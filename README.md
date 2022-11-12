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
    Reserved names (DATA, METHODS, COMPUTED)
    Data itself is seen as a function.
    While Methods and Computed take objects or functions.
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

- Below we have the example of how the game looks and works. 

![Vue](/monstergame/images/monster.JPG)


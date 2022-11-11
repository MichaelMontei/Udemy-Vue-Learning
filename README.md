# Udemy-Vue-Learning
![Vue](/learning/images/images.png)

Source: https://www.udemy.com/course/vuejs-2-the-complete-guide/

### Learning the Basics of VUE
<br>

#### 1. Example of Vue Lay-out

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
<br>

#### 2. Directive Bindings Examples
<br>

- V-HTML -> will output the render in html style and not just the content of the interpolation! 
- V-BIND -> Will bind for instance an href to output a working url link
- V-ON or @ -> Symbol are event listeners binding we can use in Vue <br>
example of this: @click="methodsName"
- V-MODEL -> This is a special 2-way Binding in Vue that listens for user input and updates it in the Vue model, meaning we can use it later on if needed. It actually is a shortcut for V-BIND and V-INPUT together.

<br>

#### 3. Value Presets in VUE
<br>

In VUE we have 4 VALUE PRESETS that we can use in our "script".
- DATA: to store data deeuh.
- METHOD: Here we can write methods.
- WATCH: is to watch a value changing throughout a method for instance.
- COMPUTED: also a method, but the big difference is that this will render solo.

<br>

#### 4. First Page of what I Learned and what I created so far
![Vue](/learning/images/page1.JPG)
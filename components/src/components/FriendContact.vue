<template>
    <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Vue Basics</title>
      <link
        href="https://fonts.googleapis.com/css2?family=Jost:wght@400;700&display=swap"
        rel="stylesheet"
      />
      <link rel="stylesheet" href="styles.css" />
  
    </head>
    <body>
      <header>
        <h1>FriendList</h1>
      </header>
      <section id="app">
        <ul>
          <li>
            <h2>{{ name }}</h2>
            <button @click="toggleDetails">Show Details</button>
            <ul v-if="showDetails">
              <li><strong>Phone:</strong> {{ phoneNumber }}</li>
              <li><strong>Email:</strong> {{ emailAddress }}</li>
            </ul>
          </li>
        </ul>
      </section>
    </body>
  </html>
  
  </template>
  
  <script>
  
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
      }
    },
   
    data(){
      return {
        showDetails: false,
      }
    },
    methods: {
      toggleDetails(){
        this.showDetails = !this.showDetails;
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
    margin-top: 60px;
  }
  
  * {
    box-sizing: border-box;
  }
  
  html {
    font-family: 'Jost', sans-serif;
  }
  
  body {
    margin: 0;
  }
  
  header {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 3rem auto;
    border-radius: 10px;
    padding: 1rem;
    background-color: #58004d;
    color: white;
    text-align: center;
    width: 90%;
    max-width: 40rem;
  }
  
  #app ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  
  #app li {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 1rem auto;
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    width: 90%;
    max-width: 40rem;
  }
  
  #app h2 {
    font-size: 2rem;
    border-bottom: 4px solid #ccc;
    color: #58004d;
    margin: 0 0 1rem 0;
  }
  
  #app button {
    font: inherit;
    cursor: pointer;
    border: 1px solid #ff0077;
    background-color: #ff0077;
    color: white;
    padding: 0.05rem 1rem;
    box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
  }
  
  #app button:hover,
  #app button:active {
    background-color: #ec3169;
    border-color: #ec3169;
    box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
  }
  
  </style>
  
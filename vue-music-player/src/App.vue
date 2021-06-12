<template>
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>

    <main>
      <section class="player">
        //The double curly braces are called template strings! Didn't know that
        <h2 class="song-title">{{ current.title }}</h2>
      </section>
    </main>

  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    //Controls the state
    return {
      current: {
        titile: 'SONG TITLE'
      },
      songs: [
      {
        titile: 'Always with me always with you',
        artist: 'Joe Satriani',
        image: '',
        src: require('./assets/songs/AlwaysWithMeAlwaysWithYou.mp3')
      },
      {
        titile: 'Another one bites the Dust',
        artist: 'Queen',
        image: '',
        src: require('./assets/songs/AnotherOneBitesTheDust.mp3')
      },
      {
        titile: 'Fool in the rain',
        artist: 'Pink Floyd',
        image: '',
        src: require('./assets/songs/FoolInTheRain.mp3')
      },
      {
        titile: 'Policy of truth',
        artist: 'Depeche Mode',
        image: '',
        src: require('./assets/songs/PolicyOfTruth.mp3')
      },
      {
        titile: 'Where the eagles learn to fly',
        artist: 'Pink Cream',
        image: '',
        src: require('./assets/songs/WhereTheEaglesLearnToFly.mp3')
      }
      ]
    }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    font-family: sans-serif;
  }
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #fff;
  }
</style>

<template>
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>

    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - {{ current.artist }}</h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <button v-for="song in songs" :key="song.src" @click="play(song)" 
        :class="(song.src == current.src) ? 'song playing' : 'song'">
        {{ song.title }} - {{ song.artist }}
        </button>
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
      index: 0,
      isPlaying: false,
      current: {

      },
      songs: [
      {
        title: 'Always with me always with you',
        artist: 'Joe Satriani',
        image: '',
        src: require('./assets/songs/AlwaysWithMeAlwaysWithYou.mp3')
      },
      {
        title: 'Another one bites the Dust',
        artist: 'Queen',
        image: '',
        src: require('./assets/songs/AnotherOneBitesTheDust.mp3')
      },
      {
        title: 'Fool in the rain',
        artist: 'Pink Floyd',
        image: '',
        src: require('./assets/songs/FoolInTheRain.mp3')
      },
      {
        title: 'Policy of truth',
        artist: 'Depeche Mode',
        image: '',
        src: require('./assets/songs/PolicyOfTruth.mp3')
      },
      {
        title: 'Where the eagles learn to fly',
        artist: 'Pink Cream',
        image: '',
        src: require('./assets/songs/WhereTheEaglesLearnToFly.mp3')
      }
      ],
      player: new Audio()
    }
  },
  //the object of methods
  methods: {
    play(song) {
      if(typeof song.src !== "undefined") {
        this.current = song;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    prev() {
      this.index--;
      if(this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next() {
      this.index++;
      if(this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  //lifecycle method
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
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

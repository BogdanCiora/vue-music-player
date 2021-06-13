<template>
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>

    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <br>
        <div style="padding-left: 200px">
          <img v-bind:src="`${ current.image }`">
        </div>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
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
        image: require('./assets/images/JoeSatriani.jpg'),
        src: require('./assets/songs/AlwaysWithMeAlwaysWithYou.mp3')
      },
      {
        title: 'Another one bites the Dust',
        artist: 'Queen',
        image: require('./assets/images/Queen.jpg'),
        src: require('./assets/songs/AnotherOneBitesTheDust.mp3')
      },
      {
        title: 'Fool in the rain',
        artist: 'Pink Floyd',
        image: require('./assets/images/PinkFloyd.jpg'),
        src: require('./assets/songs/FoolInTheRain.mp3')
      },
      {
        title: 'Policy of truth',
        artist: 'Depeche Mode',
        image: require('./assets/images/DepecheMode.png'),
        src: require('./assets/songs/PolicyOfTruth.mp3')
      },
      {
        title: 'Where the eagles learn to fly',
        artist: 'Pink Cream',
        image: require('./assets/images/PinkCream.jpg'),
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
      this.player.addEventListener('ended', function () {
        this.next();
      }.bind(this));
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if(this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if(this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    }
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
  main {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    padding: 25px;
  }
  .song-title {
    color: #212121;
    font-size: 32px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
  }
  .song-title span {
    font-weight: 400;
    font-style: italic;
  }
  .controls {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 30px 15px;
  }
  button {
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
  }
  .play, .pause {
    font-size: 20px;
    font-weight: 700;
    padding: 15px 25px;
    margin: 0px 15px;
    border-radius: 6px;
    color: #fff;
    background-color: #cc2e5d;
  }
  .next, .prev {
    font-size: 16px;
    font-weight: 700;
    padding: 10px 20px;
    margin: 0px 15px;
    border-radius: 6px;
    color: #fff;
    background-color: #ff5858;
  }
  .playlist {
    padding: 0px 30px;
  }
  .playlist h3 {
    color: #212121;
    font-size: 28px;
    font-weight: 400;
    margin-bottom: 30px;
    text-align: center;
  }
  .playlist .song {
    display: block;
    width: 100%;
    padding: 15px;
    font-size: 20px;
    font-weight: 700;
    cursor: pointer;
  }
  .playlist .song:hover {
    color: #ff5858;
  }
  .playlist .song.playing {
    color: #fff;
    background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  }
  img {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 300px;
    border-radius: 30%;
    box-shadow: 0 0 3px 8px black;
  }

</style>

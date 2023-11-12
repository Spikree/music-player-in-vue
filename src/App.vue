<template>
  <header>
    <h1>My music</h1>
  </header>
  <main>
    <section class="player">
      <h2 class="song-title">
        {{ current.title }} -
        <span>{{ current.aritst }}</span>
      </h2>
      <div class="controls">
        <button class="previous" @click="previous">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
      </div>
    </section>
    <section class="playlist">
      <h3>The playlist</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing': 'song'">
        {{ song.title }} - {{ song.aritst }}
      </button>
    </section>
  </main>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      current: {

      },
      isPlaying : false,
      index : 0,
      songs: [

      {
        title: 'Love',
        aritst: 'Kendrick lamar',
        src: require('./assets/LOVE ft. Zacari.mp3')
      },
      {
        title: 'FASHION',
        aritst: 'Britney Manson',
        src: require('./assets/fashion.mp3')
      },
      {
        title: 'Tek it',
        aritst: 'Cafuné ',
        src: require('./assets/tekit.mp3')
      },
      {
        title: 'Grateful',
        aritst: 'Neffix',
        src: require('./assets/Grateful.mp3')
      },
    ],
    player: new Audio()
    }
  },
  methods: {
    play (song) {
      if(typeof song.src != 'undefined'){
        this.current = song;
        this.player.addEventListener('ended', function() {
          this.index ++;
          if (this.index > this.songs.length - 1 ) {
      this.index = 0
    }

    this.current = this.songs[this.index];
    this.play(this.current);
        }.bind(this));
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
    this.player.pause();
    this.isPlaying = false;
  },
  next () {
    this.index += 1
    if (this.index > this.songs.length - 1 ) {
      this.index = 0
    }

    this.current = this.songs[this.index];
    this.play(this.current);
  },
  previous () {
    this.index -= 1
    if (this.index < 0 ) {
      this.index = this.songs.length - 1;
    }

    this.current = this.songs[this.index];
    this.play(this.current);
  }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
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

  button{
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
  }

  .play {
    font-size: 20px;
    font-weight: 700;
    padding: 15px 25px;
    margin: 0px 15px;
    border-radius: 8px;
    color: #fff;
    background-color: #cc2e5d;
  }
  
  button:hover {
    opacity: 0.8;
  }

  .pause {
    font-size: 20px;
    font-weight: 700;
    padding: 15px 25px;
    margin: 0px 15px;
    border-radius: 8px;
    color: #fff;
    background-color: #cc2e5d;
  }

  .next , .previous {
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
  .playlist h3{
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
    cursor: pounter;
  }

  .playlist .song:hover {
    color: #ff5858;
  }

  .playlist .song.playing {
    color: white;
    background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  }
</style>

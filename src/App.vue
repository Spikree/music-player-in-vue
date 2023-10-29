<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      current : {
      },
      index : 0,
      songs: [
        {
          title : 'Grateful',
          artist : 'Neffex',
          src: require('./assets/Grateful(PaglaSongs).mp3')
        }
      ],
      player: new Audio()
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: sans-serif;
}

header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
</style>

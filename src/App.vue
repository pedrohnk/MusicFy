<template>
  <div style="display: flex, flex-direction:columm, min-height:100vh">
    <header class="header">
      <h1>MUSICFY</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }}-<span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Voltar</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pausar</button>
          <button class="next" @click="next">Prox</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} -{{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script >
export default {
  name: "app",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "Acontece",
          artist: "Vitor Fernandes",
          src: require("./assets/gabriel-o-principe-misterioso-pf.mp3"),
        },
        {
          title: "Kletka",
          artist: "Molchat doma",
          src: require("./assets/kletka-kletka.mp3"),
        },
        {
          title: "The Weeknd",
          artist: "The Hills",
          src: require("./assets/the-hills-official-video.mp3"),
        },
        {
          title: "Paul Anka",
          artist: "Put Your Head On My Shoulder",
          src: require("./assets/paul-anka-put-your-head-on-my-shoulder-letra-video.mp3"),
        },
        {
          title: "Rita",
          artist: "Tierry",
          src: require("./assets/rita-promocional-atualizadao-junino.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
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
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #212121;
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  color: #fff;
  background-color: #7700ff;
  font-family: Segoe UI;
  text-transform: uppercase;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #fff;
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
button:hover {
  opacity: 0.8;
}
.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #7700ff;
}
.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #3b007e;
}
.playlist {
  background-color: #fff;
  border: none;
  border-radius: 20px;
  padding: 10px 10px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 30px;
  text-align: center;
  font-family: Segoe UI;
  text-transform: uppercase;
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
  color: #7700ff;
}

.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #7700ff, #0051ca);
}
</style>
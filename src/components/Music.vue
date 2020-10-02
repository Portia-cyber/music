<template>
  <div>
    <header>
      <h1>
        My Music
      </h1>
    </header>
    <section class="player">
      <main>
        <h2 class="song-title">
          {{ current.title }}
          - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button v-if="!isPlaying" class="play" @click="play">Play</button>
          <button v-else class="pause" @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
          <button class="stop" @click="pause">Stop</button>
        </div>
      </main>
    </section>
    <section class="playlist">
      <h3>The Playlist</h3>
      <Button v-for="song in songs" :key="song.src" :class="(song.src == current.src) ? 'song playing' :'song' "
              @click="play(song)">
        {{ song.title }} - {{ song.artist }}
      </Button>
    </section>
  </div>
</template>

<script>
export default {
  name: "Music",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Demons',
          artist: 'Olamide',
          src: require('./Olamide-ft-Jackmillz-Demons.mp3')
        },
        {
          title: 'Wonma',
          artist: 'Olamide',
          src: require('./Olamide-Wonma-.mp3')
        },
        {
          title: 'Rich And Famos',
          artist: 'Olamide',
          src: require('./Olamide-Rick-Famous.mp3')
        },
        {
          title: 'Mojo',
          artist: 'Olamide',
          src: require('./Olamide-ft-Jayboi-Mojo.mp3')
        },
        {
          title: 'Milly Talk',
          artist: 'Olamide',
          src: require('./Olamide-ft-Milly-Billion-Talk.mp3')
        },
        {
          title: 'No Time',
          artist: 'Olamide',
          src: require('./Olamide-No-Time.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if (typeof song.src != 'undefined') {
        this.current = song
        this.player.src = this.current.src
      }
      this.player.play()
      this.player.addEventListener('ended', function () {
        this.index++
        if (this.index > this.songs.length - 1) {
          this.index = 0
        }
        this.current = this.songs[this.index]
        this.play(this.current)
      }.bind(this))
      this.isPlaying = true
    },
    pause() {
      this.player.pause()
      this.isPlaying = false
    },
    next() {
      this.index++
      if (this.index > this.songs.length - 1) {
        this.index = 0
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    },
    prev() {
      this.index--
      if (this.index < 0) {
        this.index = this.songs.length - 1
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    }
  },
  created() {
    this.current = this.songs[this.index]
    this.player.src = this.current.src
    //this.player.play()
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Roboto Light", serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: #212121;
  color: #fff;
}
</style>

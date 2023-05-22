<template>
  <div class="home">

    <h2>
      Just say what you want
    </h2>

    <vue-speech
      lang="en-EN"
      @onTranscriptionEnd="onEnd"
    />
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
  },
  methods: {
    /* eslint-disable */
    onEnd ({ lastSentence, transcription }) {
      // `lastSentence` is the last sentence before the pause
      // `transcription` is the full array of sentences

      if (lastSentence.toUpperCase() == 'WHAT YOU WANT') {
        alert('finally')

        this.$router.push('about')
      }
    }
  }
}
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h2>And is about time</h2>

    <vue-speech
      lang="es-AR"
      :continuous="true"
      @onTranscriptionEnd="test"
    />

    lastList: {{ lastList }}

    <div>
      lists:
      <div
        v-if="lists.length"
      >
        <ul
          v-for="(list, index) in lists"
          :key="index"
        >
          {{ list.name }}
          <li
            v-for="(item, itemIndex) in list.content"
            :key="itemIndex"
          >
            {{ item }}
          </li>
        </ul>
      </div>
      <b
        v-else
      >
        no lists!
      </b>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      lists: [],
      lastList: ''
    }
  },
  methods: {
    test ({ lastSentence, transcription }) {
      console.log(transcription)
      if (lastSentence.includes('crear lista')) {
        let listName = lastSentence.split('crear lista')[1]

        if (!this.lists.find(list => list.name == listName)) {
          this.lists.push({
            name: listName,
            content: []
          })
        }
        this.lastList = listName
      }
      if (lastSentence.includes('agregar')) {
        this.lists.find(list => list.name == this.lastList).content.push(lastSentence.split('agregar')[1])
      }
    }
  }
}
</script>

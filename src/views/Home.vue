<template>
  <div class="home">
    <section class='hero is-medium is-dark mb-6'>
      <div class='hero-body has-text-centered'>
        <p class='title mb-6'>
          Welcome to Core
        </p>
        <p>
          The best cores online
        </p>
      </div>
    </section>

    <div class='columns is=multiline'>
      <div class='column is-12'>
        <h2 class='is-size-2 has-text-centered'>Last cores</h2>
      </div>
    </div>

      <div
       class='column is-3'
       v-for='poll in latestPolls'
       v-bind:key='poll.id'
      >
        <h3 class='is-size-4'>{{poll.title}}</h3>
        <router-link :to="src+poll.id" class='navbar-item'><strong>{{poll.title}}</strong></router-link>
      </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data() {
    return {
      latestPolls: [],
      src: '/poll/'
    }
  },
  computed: {
    getPollUrl() {
        return '/poll/' + this.poll.id
    }
  },
  components: {
  },
  mounted() {
    this.getLatestPolls()
  },
  methods: {
    getLatestPolls() {
        axios
          .get('/api/v1/latest-polls/')
          .then(response => {
            this.latestPolls = response.data
          })
          .catch(error => {
            console.log(error)
          })
    }
  }
}
</script>

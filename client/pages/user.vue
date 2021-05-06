<template>
  <card :title="$t('user')">
    <div class="form-group">
      <label class="control-label">Name</label>
      <input v-model="user.name" class="form-control">
    </div>
    <div v-if="isVisibleEmail" class="form-group">
      <label class="control-label">Email</label>
      <input v-model="user.email" class="form-control">
    </div>

    <button class="btn btn-secondary mt-3" @click.prevent="back">
      Back
    </button>
  </card>
</template>

<script>
import axios from 'axios'

export default {
  middleware: 'auth',

  data: () => ({
    user: [],
    isVisibleEmail: false
  }),

  head () {
    return { title: this.$t('user') }
  },

  mounted () {
    axios
      .get('user/' + this.$route.params.id)
      .then((response) => {
        this.user = response.data
        if ((this.user.id % 2) === 0) {
          this.isVisibleEmail = true
        }
      })
      .catch((error) => {
      })
  },

  methods: {
    back () {
      this.$router.back()
    }
  }
}
</script>

<template>
  <div>
    <card :title="$t('home')">
      {{ $t('you_are_logged_in') }}
    </card>
    <Users />
  </div>
</template>

<script>
import Users from './users'

export default {
  components: { Users },

  middleware: 'auth',

  head () {
    return { title: this.$t('home') }
  }
}
</script>

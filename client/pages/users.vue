<template>
  <card :title="$t('users')" class="mt-3">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users">
          <th scope="row">{{ user.id }}</th>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <div class="btn-group btn-group-sm" role="group" aria-label="edit controls">
              <router-link :to="{ path: $route.path + '/' + user.id }" class="btn btn-secondary">
                Edit
              </router-link>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </card>
</template>

<script>
import axios from 'axios'

export default {
  middleware: 'auth',

  data: () => ({
    users: []
  }),

  head () {
    return { title: this.$t('home') }
  },

  mounted () {
    axios
      .get('user/list')
      .then((response) => {
        this.users = response.data
      })
      .catch((error) => {
      })
  }
}
</script>

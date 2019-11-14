<template>
  <div class="user">
    <template v-if="user !== false">
      <article>
        <div>
          <h1>{{ user.name.title}} {{ user.name.first}} {{ user.name.last}}</h1>
          <img :src="user.picture.large" />
          <a :href="'mailto:' + user.email">{{ user.email }}</a>
        </div>
        <button @click="fetchUser">next!</button>
      </article>
    </template>
  </div>
</template>

<script>
export default {
  name: "home",
  data() {
    return {
      url: "https://randomuser.me/api/",
      user: false
    };
  },
  created() {
    this.fetchUser();
  },
  methods: {
    fetchUser() {
      fetch(this.url)
        .then(response => {
          return response.json();
        })
        .then(json => {
          this.user = json.results[0];
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>
<style scoped>
.user a {
  color: gold;
  margin-bottom: 15px;
  display: block;
}
</style>

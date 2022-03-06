<template>
  <div class="home">
    <authenticator>
    <template v-slot="{ user, signOut }">
      <h3>{{ user.attributes.nickname }}</h3>
      <p v-if="user.attributes.nickname == 'dododada'">This is dododada</p>
      <button @click="createAuthor">Create Authors</button>
      {{authors}}
      <button @click="queryAuthors">Query Authors</button>
      <div v-for="author in authors" :key=author.id>
        <h1>
          {{author.last_name}}
        </h1>
        <h5>
          {{author.first_name}}
        </h5>
      </div>
      <button @click="signOut">Sign Out</button>
      </template>
      </authenticator>
  </div>
</template>

<script>
// @ is an alias to /src
import {Authenticator} from "@aws-amplify/ui-vue";
import { DataStore } from '@aws-amplify/datastore'
import { Authors } from '../models';
export default {
  name: 'HomeView',
  components: {
    Authenticator
  },
  data() {
    return {
      authors: []
    }
  },
  methods: {
    async createAuthor() {
      await DataStore.save(
        new Authors({
          "first_name": "Lorem",
          "last_name": "Episum",
          "Posts": []
        })
      );
    },
    async queryAuthors() {
      const models = await DataStore.query(Authors);
      this.authors = models;
      console.log(models);
    }, 
  }
}
</script>

<template>
  <v-container>
    <form @submit.prevent="addSearch">
      <input type="text" v-model="inputVal" placeholder="Search" />
    </form>
    <div v-for="meme in displayedMemes" :key="meme.id" class="py-5">
      <router-link :to="`/meme/${meme.id}`">
        <meme
          class="mx-auto mt-6"
          :top="meme.topText"
          :bottom="meme.bottomText"
          :imageURL="meme.imageURL"
        />
      </router-link>
    </div>
  </v-container>
</template>

<script>
import { db } from "../firebase";
import Meme from "../components/Meme";

export default {
  components: { Meme },
  data() {
    return {
      memes: [],
      inputVal: "",
      searchTerm: ""
    };
  },
  methods: {
    addSearch() {
      this.searchTerm = this.inputVal;
    }
  },
  mounted() {
    db.collection("memes").onSnapshot((snap) => {
      const memes = snap.docs.map((doc) => {
        return {
          ...doc.data(),
          id: doc.id,
        };
      });
      this.memes = memes;
    });
  },
  computed: {
  displayedMemes() {
    if (!this.searchTerm) return this.memes;

    const normalizedSearchTerm = this.searchTerm.toUpperCase();
    return this.memes.filter(m => {
      return m.normalized.includes(normalizedSearchTerm);
    });
  }},
};
</script>

<style></style>
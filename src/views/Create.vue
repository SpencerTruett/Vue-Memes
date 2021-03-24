<template>
  <div>
    <form @submit.prevent="generateMeme">
      <input placeholder="Image URL" type="text" v-model="imageURL" />
      <input placeholder="Top Text" type="text" v-model="topText" />
      <input placeholder="Bottom Text" type="text" v-model="bottomText" />
      <button type="submit">Generate Meme!</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageURL: "",
      topText: "",
      bottomText: "",
    };
  },
  methods: {
    generateMeme() {
      console.log("building a meme....");
    },
  },
};
</script>

<style></style>
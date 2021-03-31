<template>
  <v-container>
    <div class="d-flex justify-center">
      <div class="d-flex flex-column">
        <v-alert v-if="errorMessage" type="error">
          <h5>{{ errorMessage }}</h5>
        </v-alert>
        <h1 class="d-flex justify-center">WELCOME</h1>
        <img :src="require('@/assets/logo.png')" />
        <h1>VUE MEMES ONLY</h1>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      errorMessage: null,
    };
  },
  mounted() {
    const hasAuthErr = this.$route.query.unauthorized === "true";
    if (hasAuthErr) {
      this.errorMessage = "You must be logged in to do that";
    }
  },
};
</script>

<style></style>
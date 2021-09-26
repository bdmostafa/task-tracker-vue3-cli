<template>
  <footer>
    <p>
      Copyright &copy; 2021. Developed by
      <a href="https://mdmostafa.com" target="_blank" class="mostafa">Mostafa</a>
    </p>
    <router-link v-show="!contactPage" to="/contact"> Contact </router-link>
  </footer>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      isContactPage: true,
    };
  },
  computed: {
    contactPage() {
      if (this.$route.path === "/contact") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style scoped>
a {
  color: #333;
}
footer {
  margin-top: 30px;
  text-align: center;
}
.mostafa {
  color: blue;
  text-decoration: none;
}
</style>

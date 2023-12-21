<template>
  <div>
    <Navbar :isIndexPage="isIndexPage" />

    <Nuxt />

    <Footer />
  </div>
</template>

<script>
import Footer from "@/components/Footer.vue";
import Navbar from "@/components/Navbar.vue";

export default {
  components: {
    Navbar,
    Footer,
  },
  computed: {
    isIndexPage() {
      return this.$route.path === "/";
    },
  },
};
</script>

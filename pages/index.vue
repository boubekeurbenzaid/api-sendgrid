<template>
  <div id="app">
    <h1>API send email with SendGrid</h1>
    <ContactFormVue />
  </div>
</template>

<script>
import ContactFormVue from '~/components/ContactForm.vue'

export default {
  name: 'App',
  components: {
    ContactFormVue,
  },
}
</script>

<style scoped>
h1 {
  margin: 2rem 0 4rem;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #f1f1f1;
}
</style>

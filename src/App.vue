<template>

  <Header />
  
  <Form/>
</template>

<script>

import Header from './components/Header.vue'
import Form from './components/form.vue'

export default {
  name: 'App',
  components: {
    Header,
    Form
  }
}
</script>


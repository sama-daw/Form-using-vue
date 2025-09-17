<template>
  <div id="app">
    <FormComponent />
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue';

export default {
  components: {
    FormComponent,
  },
};
</script>
<style>
body {
  margin: 0;
  min-height: 100vh;
  background: linear-gradient(135deg, #181818 0%, #232526 100%);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>

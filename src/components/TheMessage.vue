<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>
<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>
<style scoped>
.message {
  text-align: center;
  padding: 20px 0;
}
p {
  color: #ba3838;
}
</style>

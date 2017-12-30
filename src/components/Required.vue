<template>
  <p class="error-message" v-if="!isRequired">{{name}} must not be empty.</p>
</template>

<script>
export default {
  props: ['isRequired', 'name'],
};
</script>

<style>
.error-message {
  color: red;
}
</style>

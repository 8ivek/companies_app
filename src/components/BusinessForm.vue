<template>
  <div id="business-form">
    <form @submit.prevent="handleSubmit">
      <label>Business name</label>
      <input v-model="business.name"  type="text" />
      <label>Business Email</label>
      <input v-model="business.email" type="text" />
      <button>Add Business</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'business-form',
  data() {
    return {
      business: {
        name: '',
        email: '',
      },
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.business);
      this.$emit('add:employee', this.business);
    },
  },
};
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>

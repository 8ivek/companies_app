<template>
  <div id="business-form">
    <form @submit.prevent="handleSubmit">
      <label>Business name</label>
      <input v-model="business.name"
        type="text"
        ref="first"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Business Email</label>
      <input v-model="business.email" type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">
        ❗ Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">
        ✅ Business successfully added
      </p>
      <button>Add Business</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'business-form',
  data() {
    return {
      submitting: false, // whether or not the form is currently being submitted.
      error: false, // set if something goes wrong.
      success: false, // if everything went well.
      business: {
        name: '',
        email: '',
      },
    };
  },
  methods: {
    handleSubmit() {
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }
      this.$emit('add:business', this.business);
      this.$refs.first.focus();
      this.business = {
        name: '',
        email: '',
      };
      this.setSuccessStatus();
    },
    clearStatus() {
      this.submitting = true;
      this.success = false;
      this.error = false;
    },
    setSuccessStatus() {
      this.error = false;
      this.success = true;
      this.submitting = false;
    },
  },
  computed: {
    invalidName() {
      return this.business.name === '';
    },

    invalidEmail() {
      return this.business.email === '';
    },
  },
};
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>

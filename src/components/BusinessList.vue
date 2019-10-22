<template>
  <div id="business-list">
    <p v-if="businesses.length < 1" class="empty-table">
      No business
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Business Name</th>
          <th>Business Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="business in businesses" :key="business.id">
          <td>{{ business.name }}</td>
          <td>{{ business.email }}</td>
          <td>
            <button>Edit</button>
            <button @click="$emit('delete:business', business.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'business-list',
  props: {
    businesses: Array,
  },
};
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>

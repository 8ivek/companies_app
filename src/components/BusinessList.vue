<template>
  <div id="business-list">
    <table>
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
          <td>&nbsp;</td>
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

<style scoped></style>

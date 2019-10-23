<template>
  <div id="business-list">
    <p v-if="businesses.length < 1" class="empty-table">
      No business
    </p>
    <table width="100%" v-else>
      <thead>
        <tr>
          <th width="30%">Business Name</th>
          <th width="30%">Business Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="business in businesses" :key="business.id">
          <td v-if="editing === business.id">
            <input type="text" v-model="business.name" />
          </td>
          <td v-else>{{ business.name }}</td>
          <td v-if="editing === business.id">
            <input type="text" v-model="business.email" />
          </td>
          <td v-else>{{ business.email }}</td>
          <td v-if="editing === business.id">
            <button @click = "editBusiness(business)">Save</button>
            <button class="muted-button" @click="cancelEdit(business)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(business)">Edit</button>
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
  data() {
    return {
      editing: null,
      cachedBusiness: null,
    };
  },
  methods: {
    editMode(business) {
      this.cachedBusiness = Object.assign({}, business);
      this.editing = business.id;
    },
    cancelEdit(business) {
      Object.assign(business, this.cachedBusiness);
      this.editing = null;
    },
    editBusiness(business) {
      if (business.name === '' || business.email === '') return;
      this.$emit('edit:business', business.id, business);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>

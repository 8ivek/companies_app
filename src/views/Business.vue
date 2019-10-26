<template>
  <div id="business" class="small-container">
    <h1>Business Listings</h1>
    <business-form @add:business="addBusiness" />
    <business-list
      :businesses="businesses"
      @delete:business="deleteBusiness"
      @edit:business='editBusiness'
    />
  </div>
</template>

<script>
import BusinessForm from '@/components/BusinessForm.vue';
import BusinessList from '@/components/BusinessList.vue';

export default {
  name: 'business',
  components: {
    BusinessForm,
    BusinessList,
  },
  data() {
    return {
      apiurl: 'https://api.bivek.ca/api',
      businesses: [],
    };
  },
  mounted() {
    this.getBusinesses();
  },
  methods: {
    async getBusinesses() {
      try {
        const response = await fetch(`${this.apiurl}/companies`);
        const data = await response.json();
        this.businesses = data.data;
      } catch (error) {
        console.error(error);
      }
    },
    async addBusiness(business) {
      try {
        const response = await fetch(`${this.apiurl}/companies`, {
          method: 'POST',
          body: JSON.stringify(business),
          headers: { 'Content-Type': 'application/json;charset=UTF-8' },
        });
        const data = await response.json();
        this.businesses = [...this.businesses, data];
      } catch (error) {
        console.error(error);
      }
    },
    async editBusiness(id, updatedBusiness) {
      try {
        const response = await fetch(`${this.apiurl}/companies/${id}`, {
          method: 'PUT',
          body: JSON.stringify(updatedBusiness),
          headers: { 'Content-Type': 'application/json;charset=UTF-8' },
        });
        const data = await response.json();
        if (data) {
          this.businesses = this.businesses.map(
            business => (business.id === id ? updatedBusiness : business),
          );
        }
      } catch (error) {
        console.error(error);
      }
    },
    async deleteBusiness(id) {
      try {
        const response = await fetch(`${this.apiurl}/companies/${id}`, {
          method: 'DELETE',
          headers: { 'Content-Type': 'application/json;charset=UTF-8' },
        });
        const data = await response.json();
        if (data.data === 'Company delete successful.') {
          this.businesses = this.businesses.filter(
            business => business.id !== id,
          );
        }
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>

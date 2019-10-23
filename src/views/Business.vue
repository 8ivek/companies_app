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
      businesses: [
        {
          id: 1,
          name: 'Samsung Electronics',
          email: 'infosamsung.ca',
        },
        {
          id: 2,
          name: 'Xerox Ltd.',
          email: 'info@xerox.ca',
        },
        {
          id: 3,
          name: 'World Vision',
          email: 'info@worldvision.ca',
        },
      ],
    };
  },
  methods: {
    addBusiness(business) {
      const lastId = this.businesses.length > 0
        ? this.businesses[this.businesses.length - 1].id : 0;
      const id = lastId + 1;
      const newBusiness = { ...business, id };
      this.businesses = [...this.businesses, newBusiness];
    },
    deleteBusiness(id) {
      this.businesses = this.businesses.filter(
        business => business.id !== id,
      );
    },
    editBusiness(id, updatedBusiness) {
      this.businesses = this.businesses.map(
        business => (business.id === id ? updatedBusiness : business),
      );
      console.log(this.businesses);
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

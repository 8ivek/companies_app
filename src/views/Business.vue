<template>
  <div id="business" class="small-container">
    <h1>Business Listings</h1>
    <business-form @add:business="addBusiness" />
    <business-list :businesses="businesses" />
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
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
      ],
    };
  },
  methods: {
    addbusiness(business) {
      const lastId = this.businesses.length > 0
        ? this.businesses[this.businesses.length - 1].id : 0;
      const id = lastId + 1;
      const newBusiness = { ...business, id };
      this.businesses = [...this.businesses, newBusiness];
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

<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      
      <template>
  <v-data-table
    :headers="headers"
    :items="customers"
    :items-per-page="10"
    class="elevation-1"
    :loading="loading"
    loading-text="Please Wait"
  >
<template v-slot:item.profilePicture="{item}">
  <v-badge

          color="red"
          overlap
          content="VIP"
          offset-x="60"
          offset-y="20"
          bordered
          v-if="item.isVip == true"
  >
 <v-avatar siz="60">
  <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="80"
  max-width="80"
  :src="item.profilePicture"
></v-img>
</v-avatar>
</v-badge>
<div v-else>
  <v-avatar siz="60">
  <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="80"
  max-width="80"
  :src="item.profilePicture"
></v-img>
</v-avatar>
</div>

</template>
</v-data-table>
</template>

    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return{
      headers: [
          { text: 'Photo', value: 'profilePicture' },
          { text: 'Name', value: 'name' },
          { text: 'Email', value: 'email' },
          { text: 'Phone', value: 'phone' },
          { text: 'Address', value: 'address' },
          { text: 'Age', value: 'age' },
          { text: 'Status', value: 'status' }
        ],
        customers: [],
        loading:true
      }
    },
    methods: {
      getCustomers() {
        this.$axios.get('/customers')
        .then(response => {
          console.log(response.data)
          this.customers = response.data;
          this.loading = false
        })
        .catch(error => {
          console.log(error)
        })
      }
    },
    
    mounted() {
      this.getCustomers()
    }
  }
      
</script>

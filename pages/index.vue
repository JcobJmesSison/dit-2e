<template>
  <v-row justify="center" align="center">
    <v-col cols="12">

      <template>
        <v-data-table :headers="headers" :items="customers" :items-per-page="10" class="elevation-1" :loading="loading"
          loading-text="Please Wait">
          <template v-slot:item.profilePicture="{ item }">
            <v-badge color="#FB8C00" overlap content="VIP" offset-x="60" offset-y="20" bordered
              v-if="item.isVip == true">
              <v-avatar siz="60">
                <v-img lazy-src="https://picsum.photos/id/11/10/6" max-height="80" max-width="80"
                  :src="item.profilePicture"></v-img>
              </v-avatar>
            </v-badge>
            <div v-else>
              <v-avatar siz="60">
                <v-img lazy-src="https://picsum.photos/id/11/10/6" max-height="80" max-width="80"
                  :src="item.profilePicture"></v-img>
              </v-avatar>
            </div>

          </template>
          <template v-slot:item.actions="{ item }">
            <v-btn color="#26C6DA" @click="getCustomerDetails(item)">View</v-btn>
          </template>
        </v-data-table>

        <v-dialog v-model="customerDialog" width="700" >
          <v-card>
            <v-card-title class="text h-5 cyan accent-4">
              <v-icon>mdi-account</v-icon>
              Customers Information
            </v-card-title>

            <v-row>
              <v-col cols="12" md="4"></v-col>
            <v-card-text class="mt-5">
              <!-- Picture -->
              <v-img 
              max-height="150" 
              max-width="250" 
              src="https://picsum.photos/id/11/500/300"></v-img>
            </v-card-text>

             
              <v-col cols="12" md="8"></v-col>
               <!-- Customer Name -->
               <v-list-item two-line>
                
               </v-list-item>
              </v-row>
            

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn color="#1E88E5" text @click="dialog = false">
               Update
              </v-btn>
              <v-btn color="#D50000" text @click="dialog = false">
                Delete
              </v-btn>

            </v-card-actions>
          </v-card>
        </v-dialog>

      </template>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      headers: [
        { text: 'Photo', value: 'profilePicture' },
        { text: 'Name', value: 'name' },
        { text: 'Email', value: 'email' },
        { text: 'Phone', value: 'phone' },
        { text: 'Address', value: 'address' },
        { text: 'Age', value: 'age' },
        { text: 'Status', value: 'status' },
        { text: '', value: 'actions' }
      ],
      customers: [],
      loading: true,
      customerDialog: false,
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
    },

    getCustomerDetails(item) {
      console.log(item);

      this.customerDialog = item.name
    }
  },

  mounted() {
    this.getCustomers()
  }
}

</script>

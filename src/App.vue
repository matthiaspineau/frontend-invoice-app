<template>
  <div id="app" :class="{ 'moon' : theme == 'moon' }">

    <!-- Navbar -->
     <nav class="nav">
       <div class="navbar">
         <div class="navbar__brand">
          <img :src="require('@/assets/images/logo-app.svg')" alt="logo">  
         </div>
         <div class="navbar__theme">
           <img v-if="theme == 'sun'"
            @click="switchThemes"
           :src="require('@/assets/images/icon-sun.svg')" alt="icon sun">
           <img  v-if="theme == 'moon'"
           @click="switchThemes"
           :src="require('@/assets/images/icon-moon.svg')" alt="icon moon">
         </div>
         <div class="navbar__avatar">
           <img :src="require('@/assets/images/image-avatar.jpg')" alt="avatar">
         </div>
       </div>
     </nav>

    <!-- Components: View-invoice-item -->
    <component :is="componentviewIncoiceItemActive" 
     @close-view-incoice-item="closeViewIncoice"
     :invoice="invoiceEdit"
     ></component>

    <!-- Main -->
     <main class="main container">

        <!-- Header -->
        <header class="header">
          <div class="header__heading">
            <h1>Invoices</h1>
            <span class="text--secondary">There are {{ nbInvoices }} total invoices</span>
          </div>

          <div class="header__filter">
            <label for="" class="header__filter--label text--primary">Filter <span>by status</span></label>
            <select name="" id="" v-model="filterArgInvoices">
              <option value="">All</option>
              <option value="draft">Draft</option>
              <option value="paid">Paid</option>
              <option value="pending">Pending</option>
            </select>
          </div>

          <button class="btn btn__2">New invoices</button>
        </header>

        <!-- Section Central -->
        <section class="central">
          <!-- Empty -->
          <div v-if="db.length < 1" class="empty">
            <div class="empty__media">
              <img :src="require('@/assets/images/illustration-empty.svg')" alt="empty img">
            </div>
            <div class="empty__text">
              <h3>There is nothing here</h3>
              <p class="text--secondary">Create an invoice by clicking the <br><span class="font--bold">New Invoice</span> button and get started</p>
            </div>
          </div>
          <div v-else>
            <!-- Invoice -->
            <div class="wrap__invoices">
              <list-invoice-item v-for="(invoice, index) in getInvoices" :key="index" 
              :theme="theme"
              :data="invoice"
              @show-invoice="editInvoice(invoice)"></list-invoice-item>
            </div>
          </div>
        </section>

     </main>

  </div>
</template>

<script>
import ListInvoiceItem from './components/invoice/ListInvoiceItem.vue';
import ViewInvoiceItem from './components/invoice/ViewInvoiceItem.vue';
// import { mapGetters } from 'vuex';


export default {
  data() {
    return {
      theme: 'sun',
      db: ['1'],
      filterArgInvoices: null,
      componentviewIncoiceItemActive: null,
      invoiceEdit: {}
    }
  },
  methods: {
    switchThemes() {
      this.theme = this.theme == 'sun' ? 'moon' : 'sun';
    },
    editInvoice(item) {
      this.invoiceEdit = item
      this.componentviewIncoiceItemActive = ViewInvoiceItem;
    },
    closeViewIncoice() {
      console.log('close')
      this.componentviewIncoiceItemActive = null;
    }
  },
  computed: {
    getInvoices() {
      return this.$store.getters.getInvoiceByStatus(this.filterArgInvoices);
    },
    nbInvoices() {
      return this.getInvoices.length < 1 ? 'No invoices' : this.getInvoices.length
    } 
  },
  name: 'App',
  components: {
    ListInvoiceItem,
    ViewInvoiceItem
  }
}
</script>

<style src="@/assets/scss/app.scss" lang="scss"></style>

<template>
    <div class="wrapper__view-invoice-item bg--page">
        <div class="container">
            <div class="view-invoice-item">
                <!-- BreadCrumb -->
                <div class="view--invoice--breadcrumb" @click="close">
                    <img :src="require('@/assets/images/icon-arrow-left.svg')" alt="icon arrow">
                    <span class="text--primary">Go back</span>
                </div>                

                <!-- Sidebar -->
                <div class="view--invoice--sidebar bg--block">
                    <div class="view--invoice--sidebar__text">
                        <span class="text--secondary">Status</span>
                        <div class="list--invoice__status" :class="'list--invoice__status--'+invoice.status"><span>{{ invoice.status }}</span></div>
                    </div>
                    <div class="view--invoice--sidebar__action bg--block">
                        <button class="btn btn__3">Edit</button>
                        <button class="btn btn__2">Delete</button>
                        <button class="btn btn__5">Mark a paid</button>
                    </div>
                </div>

                <!-- Invoice information -->
                <section class="view--invoice--main bg--block">
                    <div class="view--invoice--main__ref">
                        <span class="view--invoice--main__ref--d text--block--secondary">#</span>
                        <span class="view--invoice--main__ref--id text--block--primary text--lg">{{ invoice.id }}</span>
                        <span class="text--secondary d-block text--xs">Graphic Design</span>
                    </div>

                    <div class="view--invoice--main__sender">
                        <span v-for="(sender, index) in invoice.senderAddress" :key="index"
                        class="text--block--secondary text--xs">{{ sender }}</span>
                    </div>

                    <div class="view--invoice--main__created">
                        <span class="text--block--secondary text--xs">Invoice Date</span>
                        <span class="text--block--primary d-block text--lg">{{ invoice.createdAt }}</span>
                    </div>

                    <div class="view--invoice--main__payment">
                        <span class="text--block--secondary text--xs">Payment Date</span>
                        <span class="text--block--primary d-block text--lg">{{ invoice.paymentDue }}</span>
                    </div>

                    <div class="view--invoice--main__client">
                        <span class="text--block--secondary text-xs">Bill To</span>
                        <span class="text--block--primary d-block text--lg">{{ invoice.clientName }}</span>
                        <span v-for="(client, index) in invoice.clientAddress" :key="index"
                        class="text--block--secondary d-block text--xs">{{ client }}</span>
                    </div>

                    <div class="view--invoice--main__sent">
                        <span class="text--block--secondary text--xs">Sent To</span>
                        <span class="text--block--primary d-block text--lg">{{ invoice.clientEmail }}</span>
                    </div>

                    <div class="view--invoice--main__table invoice--table">
                        <div v-for="(item, index) in invoice.items" :key="index"
                        class="invoice--table__row">
                            <div class="invoice--table__row--detail">
                                <span class="text--block--primary d-block text--md font--bold">{{ item.name }}</span>
                                <span class="text--block--secondary d-block text--sm">{{ item.quantity }} x $ {{ item.price }}</span>
                            </div>
                            <span class="invoice--table__price text--block--primary">$ {{ item.total }}</span>
                        </div>
                        <div class="invoice--table__total">
                            <span>Grand Total</span>
                            <span class="text--20 text-white">$ {{ invoice.total }}</span>
                        </div>
                    </div>

                </section>

            </div>
        </div>
    </div>  
</template>

<script>
export default {
    props: {
        invoice: {
            type: Object,
            default() {
                return { 
                    id: "RT1111",
                    createdAt: "2021-08-18",
                    paymentDue: "2021-08-19",
                    description: "Re-branding",
                    paymentTerms: 1,
                    clientName: "Jensen Huang",
                    clientEmail: "jensenh@mail.com",
                    status: "paid",
                    senderAddress: {
                        street: "19 Union Terrace",
                        city: "London",
                        postCode: "E1 3EZ",
                        country: "United Kingdom"
                    },
                    clientAddress: {
                        street: "106 Kendell Street",
                        city: "Sharrington",
                        postCode: "NR24 5WQ",
                        country: "United Kingdom"
                    },
                    items: [
                        {
                        name: "Brand Guidelines",
                        quantity: 1,
                        price: 1800.90,
                        total: 1800.90
                        }
                    ],
                    total: 1800.90
        
                }
            }
        }
    },
    methods: {
        close() {
            // console.log('click')
            this.$emit('close-view-incoice-item')
            this.$destroy();
        }
    },
    name: 'ViewIncoiceItem'
}
</script>
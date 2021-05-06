<template>
    <div class="list--invoice" 
    :class="{ 'moon' : theme == 'moon' }"
    :data-id="data.id"
    @click="showInvoice">
        <div class="list--invoice__ref">
            <span class="list--invoice__ref--d">#</span>
            <span class="list--invoice__ref--id">{{ data.id }}</span>
        </div>
        <div class="list--invoice__date">{{ data.createdAt }}</div>
        <div class="list--invoice__name">{{ data.clientName }}</div>
        <div class="list--invoice__amount">${{ data.total }}</div>
        <div class="list--invoice__status" :class="'list--invoice__status--'+data.status"><span>{{ data.status }}</span></div>
        <img class="list--invoice__arrow" :src="require('@/assets/images/icon-arrow-right.svg')" alt="icon arrow">
    </div>
</template>

<script>
export default {
    props: {
        theme: {
            type: String,
            default: ''
        },
        data: {
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
        showInvoice() {
            this.$emit('show-invoice')
        }
    },
    name: 'ListInvoiceItem'
}
</script>
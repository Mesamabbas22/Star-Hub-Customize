<script setup>
import { Mail, Search } from '@lucide/vue';
import AdminShell from './AdminShell.vue';

defineProps({
    customers: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <AdminShell title="Customers" subtitle="Review buyer profiles, order history, and account status.">
        <section class="admin-panel">
            <div class="admin-section-head">
                <label class="admin-search">
                    <Search :size="17" />
                    <input type="search" placeholder="Search customers">
                </label>
                <button class="secondary-button" type="button"><Mail :size="17" /> Message selected</button>
            </div>

            <div class="admin-table">
                <div class="admin-table__row admin-table__head">
                    <span>Customer</span>
                    <span>Email</span>
                    <span>Orders</span>
                    <span>Spent</span>
                    <span>Status</span>
                </div>
                <div v-for="customer in customers" :key="customer.email" class="admin-table__row">
                    <span>{{ customer.name }}</span>
                    <span>{{ customer.email }}</span>
                    <span>{{ customer.orders }}</span>
                    <span>${{ customer.spent }}</span>
                    <span><mark :class="customer.statusTone">{{ customer.status }}</mark></span>
                </div>
            </div>
        </section>
    </AdminShell>
</template>

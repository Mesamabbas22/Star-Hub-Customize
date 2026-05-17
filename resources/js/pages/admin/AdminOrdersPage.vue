<script setup>
import { Search, Truck } from '@lucide/vue';
import AdminShell from './AdminShell.vue';

defineProps({
    orders: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <AdminShell title="Orders" subtitle="Track customer orders from proofing through delivery.">
        <section class="admin-panel">
            <div class="admin-section-head">
                <label class="admin-search">
                    <Search :size="17" />
                    <input type="search" placeholder="Search orders">
                </label>
                <button class="secondary-button" type="button"><Truck :size="17" /> Shipping queue</button>
            </div>

            <div class="admin-table">
                <div class="admin-table__row admin-table__head">
                    <span>Order</span>
                    <span>Customer</span>
                    <span>Items</span>
                    <span>Status</span>
                    <span>Total</span>
                </div>
                <div v-for="order in orders" :key="order.id" class="admin-table__row">
                    <span>{{ order.id }}</span>
                    <span>{{ order.customer }}</span>
                    <span>{{ order.items }}</span>
                    <span><mark :class="order.statusTone">{{ order.status }}</mark></span>
                    <span>${{ order.total }}</span>
                </div>
            </div>
        </section>
    </AdminShell>
</template>

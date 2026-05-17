<script setup>
import { ArrowRight, Boxes, DollarSign, ShoppingBag, UsersRound } from '@lucide/vue';
import AdminShell from './AdminShell.vue';

defineProps({
    stats: {
        type: Array,
        required: true,
    },
    orders: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <AdminShell title="Dashboard" subtitle="Today at a glance across sales, orders, products, and customers.">
        <div class="admin-stats">
            <article v-for="stat in stats" :key="stat.label" class="admin-stat-card">
                <component :is="{ revenue: DollarSign, orders: ShoppingBag, products: Boxes, customers: UsersRound }[stat.icon]" :size="22" />
                <span>{{ stat.label }}</span>
                <strong>{{ stat.value }}</strong>
                <small>{{ stat.note }}</small>
            </article>
        </div>

        <section class="admin-panel">
            <div class="admin-section-head">
                <div>
                    <h2>Recent orders</h2>
                    <p>Orders that need proofing, production, or shipping follow-up.</p>
                </div>
                <a class="secondary-button" href="/admin/orders">View orders <ArrowRight :size="16" /></a>
            </div>

            <div class="admin-table">
                <div class="admin-table__row admin-table__head">
                    <span>Order</span>
                    <span>Customer</span>
                    <span>Status</span>
                    <span>Total</span>
                </div>
                <div v-for="order in orders.slice(0, 4)" :key="order.id" class="admin-table__row">
                    <span>{{ order.id }}</span>
                    <span>{{ order.customer }}</span>
                    <span><mark :class="order.statusTone">{{ order.status }}</mark></span>
                    <span>${{ order.total }}</span>
                </div>
            </div>
        </section>
    </AdminShell>
</template>

<script setup>
import { Heart, ShoppingBag, UserRound } from '@lucide/vue';
import PageTitle from '../components/PageTitle.vue';

defineProps({
    page: {
        type: Object,
        required: true,
    },
});
</script>

<template>
    <section class="page-shell">
        <PageTitle :page="page" />
        <div class="simple-grid">
            <div class="info-card"><UserRound :size="22" /><h3>Customer profile</h3><p>Manage your contact details and preferences.</p></div>
            <div class="info-card"><ShoppingBag :size="22" /><h3>Recent order</h3><p>SHC-1042 is currently in proofing.</p></div>
            <div class="info-card"><Heart :size="22" /><h3>Saved products</h3><p>Keep favorite products ready for your next order.</p></div>
        </div>
    </section>
</template>

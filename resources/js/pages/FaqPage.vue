<script setup>
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
        <div class="panel stack">
            <details open><summary>How long does production take?</summary><p>Most orders are proofed within 48 hours and produced after approval.</p></details>
            <details><summary>Can I order in bulk?</summary><p>Yes, bulk packaging and shipping are available for teams and clients.</p></details>
            <details><summary>Can I use my own logo?</summary><p>Yes, the storefront is ready for custom uploaded branding.</p></details>
        </div>
    </section>
</template>

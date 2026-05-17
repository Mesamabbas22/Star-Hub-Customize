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
        <div class="checkout-layout">
            <form class="panel form-panel">
                <label>Name<input type="text" placeholder="Your name"></label>
                <label>Email<input type="email" placeholder="you@example.com"></label>
                <label>Message<textarea placeholder="How can we help?"></textarea></label>
                <button class="primary-button" type="button">Send message</button>
            </form>
            <div class="panel">
                <h3>Support details</h3>
                <p>Email: support@starhubcustomize.test</p>
                <p>Phone: +1 555 0100</p>
                <p>Hours: Monday to Friday, 9 AM to 6 PM</p>
            </div>
        </div>
    </section>
</template>

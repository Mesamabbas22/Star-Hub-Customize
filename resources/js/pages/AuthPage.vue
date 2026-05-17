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
    <section class="page-shell narrow">
        <PageTitle :page="page" />
        <form class="panel form-panel">
            <label>Email address<input type="email" placeholder="you@example.com"></label>
            <label v-if="page.type !== 'auth-forgot'">Password<input type="password" placeholder="Password"></label>
            <label v-if="page.type === 'auth-register'">Full name<input type="text" placeholder="Your name"></label>
            <button class="primary-button w-full" type="button">{{ page.title }}</button>
        </form>
    </section>
</template>

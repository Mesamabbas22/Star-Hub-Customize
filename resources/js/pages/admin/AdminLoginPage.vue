<script setup>
import { LockKeyhole, ShieldCheck } from '@lucide/vue';
</script>

<template>
    <section class="admin-login">
        <div class="admin-login__brand">
            <ShieldCheck :size="34" />
            <div>
                <p class="eyebrow">Admin Portal</p>
                <h1>Manage Star Hub Customize.</h1>
                <p>Sign in to review orders, update products, and manage customer activity from one focused workspace.</p>
            </div>
        </div>

        <form class="admin-login__panel">
            <div class="admin-badge"><LockKeyhole :size="16" /> Secure staff access</div>
            <label>Email address<input type="email" placeholder="admin@starhubcustomize.test"></label>
            <label>Password<input type="password" placeholder="Password"></label>
            <button class="primary-button w-full" type="button">Login</button>
            <a class="admin-link" href="/admin">Preview dashboard</a>
        </form>
    </section>
</template>

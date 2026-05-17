<script setup>
import { Boxes, LayoutDashboard, LogOut, PackageCheck, ShoppingBag, UsersRound } from '@lucide/vue';

defineProps({
    title: {
        type: String,
        required: true,
    },
    subtitle: {
        type: String,
        required: true,
    },
});

const adminLinks = [
    { href: '/admin', label: 'Dashboard', icon: LayoutDashboard },
    { href: '/admin/products', label: 'Products', icon: Boxes },
    { href: '/admin/orders', label: 'Orders', icon: ShoppingBag },
    { href: '/admin/customers', label: 'Customers', icon: UsersRound },
];
</script>

<template>
    <section class="admin-shell">
        <aside class="admin-sidebar">
            <a class="admin-logo" href="/admin">
                <PackageCheck :size="24" />
                <span>Admin</span>
            </a>
            <nav>
                <a v-for="link in adminLinks" :key="link.href" :href="link.href">
                    <component :is="link.icon" :size="18" />
                    {{ link.label }}
                </a>
            </nav>
            <a class="admin-logout" href="/admin/login"><LogOut :size="17" /> Logout</a>
        </aside>

        <div class="admin-content">
            <header class="admin-topbar">
                <div>
                    <p class="eyebrow">Star Hub Customize</p>
                    <h1>{{ title }}</h1>
                    <p>{{ subtitle }}</p>
                </div>
                <a class="secondary-button" href="/">Storefront</a>
            </header>

            <slot />
        </div>
    </section>
</template>

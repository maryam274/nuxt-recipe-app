<template>
    <nav
        :class="['sticky top-0 w-full flex items-center justify-between px-4 shadow-md transition-all duration-300',
            { 'bg-white text-gray-900': isScrolled || $route.path !== '/', 'bg-gray-800 text-white': !isScrolled && $route.path === '/' }]">
        <div class="flex items-center">
            <NuxtLink to="/">
                <img :src="$route.path === '/' && !isScrolled ? '/images/logo.svg' : '/images/logo2.svg'" alt="Logo"
                    class="w-22 transition-all duration-300">
            </NuxtLink>
        </div>
        <ul class="flex space-x-6">
            <li>
                <NuxtLink to="/" :class="[linkClass, { 'text-orange-600': isActive('/') }]">Home</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/chefs" :class="[linkClass, { 'text-orange-600': isActive('/chefs') }]">Chefs</NuxtLink>
            </li>
            <li>
                <NuxtLink to="/recipes" :class="[linkClass, { 'text-orange-600': isActive('/recipes') }]">Recipes
                </NuxtLink>
            </li>
            <li>
                <NuxtLink to="/categories" :class="[linkClass, { 'text-orange-600': isActive('/categories') }]">
                    Categories</NuxtLink>
            </li>
        </ul>
        <div class="flex items-center space-x-4">
            <NuxtLink to="/cart" :class="[linkClass, { 'text-orange-600': isActive('/cart') }]">
                <i class="fas fa-shopping-cart"></i>
            </NuxtLink>
            <NuxtLink to="/favorites" :class="[linkClass, { 'text-orange-600': isActive('/favorites') }]">
                <i class="fas fa-heart"></i>
            </NuxtLink>
            <NuxtLink to="/auth/login" :class="[linkClass, { 'text-orange-600': isActive('/login') }]">Login</NuxtLink>
            <NuxtLink to="/auth/signup"
                :class="[linkClass, 'bg-orange-500 px-4 py-3 text-white rounded hover:text-orange-600 hover:bg-white', { 'text-orange-600': isActive('/signup') }]">
                Sign Up
            </NuxtLink>
        </div>
    </nav>
</template>

<script>
export default {
    name: 'Navbar',
    data() {
        return {
            isScrolled: false
        };
    },
    computed: {
        linkClass() {
            return this.isScrolled || this.$route.path !== '/' ? 'text-gray-700 hover:text-gray-900' : 'hover:text-orange-200';
        }
    },
    mounted() {
        window.addEventListener('scroll', this.handleScroll);
    },
    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        handleScroll() {
            this.isScrolled = window.scrollY > 0;
        },
        isActive(path) {
            return this.$route.path === path;
        }
    }
}
</script>
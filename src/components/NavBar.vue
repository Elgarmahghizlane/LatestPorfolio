<template>
    <div class="bg-black sticky top-0 z-50">
        <div class="flex justify-between md:items-center items-start p-2 gap-4 max-w-6xl mx-auto">
            <div class="flex items-center mt-0">
                <img :src="logo" alt="logo" class="w-10">
                <h1 class="text-white font-bold text-base md:pt-0 pt-4">Creative Idea</h1>
            </div>
            <div class="hidden md:flex justify-between md:gap-8">
                <h1 class=" text-white hover:text-yellow-300 uppercase font-bold text-sm cursor-pointer" v-for="(m, i) in menu" :key="i"
                    @click="handleMenuItemClick(m.ref)">
                    {{ m.name }}
                </h1>

            </div>
            <div class="md:hidden p-4">
                <button @click="toggleMenu" class="text-white float-right">
                    <font-awesome-icon class="w-8 h-6" :icon="['fas', 'bars']" style="color: #ecd33c;" />
                </button>
                <div v-if="isMenuOpen" class="pt-6">
                    <h1 class="text-white uppercase font-bold py-3 text-sm cursor-pointer" v-for="(m, i) in menu" :key="i" @click="handleMenuItemClick(m.ref)">
                        {{ m.name }}
                    </h1>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import logo from '../assets/logo.png';
export default {
    data() {
        return {
            menu: [
                { name: 'Home', ref: 'headSection' },
                { name: 'About', ref: 'aboutSection' },
                { name: 'Portfolio', ref: 'portfolioSection' },
                { name: 'contact', ref: 'contactSection' },
            ],
            logo: logo,
            isMenuOpen: false,
        };
    },
    methods: {
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
        },
        handleMenuItemClick(sectionRef) {
            this.$emit('menu-item-clicked', sectionRef);
        },
    },
};
</script>

<style>
@media (min-width: 768px) {
    .max-w-6xl {
        max-width: 1440px;
        
    }
}
</style>

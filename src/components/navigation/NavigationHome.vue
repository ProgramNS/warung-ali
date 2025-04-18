<script setup>
import { ref, onMounted, nextTick } from 'vue'
import gsap from 'gsap'

const menuOpen = ref(false)      // untuk kontrol icon
const menuVisible = ref(false)   // untuk close menu
const animationRef = ref(null) // untuk animasi
const toggleMenu = async () => {
    if (!menuOpen.value) {
        // Buka menu
        menuVisible.value = true
        menuOpen.value = true
        await nextTick()

        gsap.fromTo('.mobile-menu',
            { opacity: 0, y: -50 },
            { opacity: 1, y: 0, duration: 0.5, ease: 'power2.out' }
        )

        gsap.from('.mobile-menu li', {
            opacity: 0,
            y: -20,
            duration: 0.3,
            stagger: 0.1,
            delay: 0.2,
            ease: 'power2.out'
        })

    } else {
        // Tutup menu dengan animasi
        menuOpen.value = false // untuk ubah icon
        gsap.to('.mobile-menu', {
            opacity: 0,
            y: -50,
            duration: 0.4,
            ease: 'power2.in',
            onComplete: () => {
                menuVisible.value = false // baru sembunyikan menu
            }
        })
    }
}
const animation = () => {
    gsap.from(animationRef.value, {
        opacity: 0,
        y: -50,
        duration: 0.5,
        ease: 'power2.out'
    })
}
onMounted(() => {
    // Animasi saat komponen dimuat
    animation()
})

</script>
<template>
    <!-- Navigation Bar -->
    <!-- Menggunakan Tailwind CSS untuk styling dan responsif -->
    <nav class="bg-yellow-50 fixed w-full z-20" ref="animationRef">
        <div class="mx-auto px-4 sm:px-5 lg:px-6">
            <div class="relative flex items-center h-16">

                <!-- Logo kiri -->
                <div class="absolute left-0">
                    <h1 class="text-xl font-bold text-yellow-700">ALI CATHERING</h1>
                </div>

                <!-- Menu tengah (Desktop) -->
                <ul class="hidden md:flex absolute left-1/2 -translate-x-1/2 space-x-6 text-gray-600 text-lg">
                    <li><a href="#Home" class="hover:text-yellow-600">Home</a></li>
                    <li><a href="#About" class="hover:text-yellow-600">About</a></li>
                    <li><a href="#ContactUs" class="hover:text-yellow-600">Contact Us</a></li>
                    <li><a href="#Order" class="hover:text-yellow-600">Order</a></li>
                </ul>

                <!-- Icon Burger / X (Mobile) -->
                <div class="md:hidden absolute right-4">
                    <button @click="toggleMenu" class="text-yellow-700 cursor-pointer focus:outline-none">
                        <svg v-if="!menuOpen" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                            stroke="currentColor" class="w-8 h-8">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M4 6h16M4 12h16M4 18h16" />
                        </svg>
                        <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                            stroke="currentColor" class="w-8 h-8">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>

                <!-- Mobile Menu -->
                <div v-show="menuVisible"
                    class="mobile-menu md:hidden absolute left-1/2 -translate-x-1/2 top-16 bg-white w-full py-4 shadow-lg">
                    <ul class="space-y-4 text-gray-600 text-lg text-center">
                        <li><a href="#Home" class="hover:text-yellow-600">Home</a></li>
                        <li><a href="#About" class="hover:text-yellow-600">About</a></li>
                        <li><a href="#ContactUs" class="hover:text-yellow-600">Contact Us</a></li>
                        <li><a href="#Order" class="hover:text-yellow-600">Order</a></li>
                    </ul>
                </div>

            </div>
        </div>
    </nav>
</template>

<script setup>
import NavigationHome from '@/components/navigation/NavigationHome.vue'
import GlobalBtn from '@/components/button/GlobalBtn.vue'
import { ref, onMounted, nextTick } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Autoplay } from 'swiper/modules' // <<< ini sudah benar!
import 'swiper/css'
import 'swiper/css/autoplay'
import 'swiper/css/bundle'
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
import gsap from 'gsap'

const images = ['/menu.png', '/menu2.png']

const showCard = ref(false)
const whatsappNumber = ref('+62 878-8707-3476')

const showWhatsAppCard = () => {
    showCard.value = true

    nextTick(() => {
        gsap.from('.whatsapp-card', {
            opacity: 0,
            y: -20,
            duration: 0.5,
            ease: 'power2.out'
        })
    })
}

onMounted(() => {
    nextTick(() => {
        const map = L.map('map', {
            center: [-6.1822902, 106.9072311],
            zoom: 13,
            dragging: false,
            tap: false,
        })

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(map)

        L.marker([-6.1822902, 106.9072311]).addTo(map)
            .bindPopup('<b>Masakan Warung Ali</b><br>Our location.')
            .openPopup()

        // Tambahkan element notifikasi
        const notif = document.createElement('div')
        notif.innerText = 'Gunakan 2 jari untuk menggeser atau zoom peta'
        notif.style.position = 'absolute'
        notif.style.top = '10px'
        notif.style.left = '50%'
        notif.style.transform = 'translateX(-50%)'
        notif.style.background = 'rgba(0, 0, 0, 0.7)'
        notif.style.color = 'white'
        notif.style.padding = '8px 12px'
        notif.style.borderRadius = '8px'
        notif.style.fontSize = '14px'
        notif.style.zIndex = 1000
        notif.style.display = 'none' // Awalnya disembunyiin
        document.getElementById('map').appendChild(notif)

        // Event listener touch
        map.getContainer().addEventListener('touchstart', (e) => {
            if (e.touches.length >= 2) {
                map.dragging.enable();
                notif.style.display = 'none'; // Sembunyikan notif saat 2 jari
            } else {
                map.dragging.disable();
                notif.style.display = 'block'; // Tampilkan notif saat cuma 1 jari
            }
        })

        map.getContainer().addEventListener('touchend', (e) => {
            map.dragging.disable();
            notif.style.display = 'none'; // Sembunyikan notif setelah touch selesai
        })
    })

    gsap.from('.home-section', { opacity: 0, duration: 1, y: 50 })
    gsap.from('.about-section', { opacity: 0, duration: 1, y: 50, delay: 0.5 })
    gsap.from('.contact-section', { opacity: 0, duration: 1, y: 50, delay: 1 })
    gsap.from('.order-section', { opacity: 0, duration: 1, y: 50, delay: 1.5 })
    gsap.from('.footer', { opacity: 0, duration: 1, y: 50, delay: 2 })
})
</script>


<template>
    <header>
        <NavigationHome /> <!-- Tidak ada animasi di sini -->
    </header>

    <main>
        <!-- Home Section -->
        <section id="Home" class="bg-yellow-50 w-full flex items-center justify-center home-section">
            <swiper :modules="[Autoplay]" :slides-per-view="1" :loop="true"
                :autoplay="{ delay: 1000, disableOnInteraction: false }" :speed="800" class="w-full h-full">
                <swiper-slide v-for="(image, index) in images" :key="index" class="flex items-center justify-center">
                    <div class="text-center">
                        <img :src="image" alt="Slide Image" class="mx-auto mb-6 rounded-lg w-full mt-16" />
                    </div>
                </swiper-slide>
            </swiper>
        </section>

        <!-- About Section -->
        <section id="About" class="bg-white h-auto py-10 about-section">
            <div class="text-center">
                <h2 class="text-4xl font-bold text-yellow-700">About Us</h2>
                <p class="mt-4 text-lg text-gray-600">Masakan Warung Ali telah melayani ribuan pelanggan sejak 2020
                    dengan masakan lezat dan berkualitas.</p>
            </div>

            <div class="mt-10 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 px-6">
                <div class="bg-yellow-100 p-6 rounded-lg shadow-lg">
                    <h3 class="text-2xl font-semibold text-yellow-700">Berdiri Sejak 2020</h3>
                    <p class="mt-4 text-gray-600">
                        Masakan Warung Ali dimulai pada tahun 2020 dengan visi untuk memberikan makanan rumahan yang
                        lezat dan bergizi.
                    </p>
                </div>

                <div class="bg-yellow-100 p-6 rounded-lg shadow-lg">
                    <h3 class="text-2xl font-semibold text-yellow-700">Pelanggan Setia</h3>
                    <p class="mt-4 text-gray-600">
                        Sejak awal berdiri, kami telah melayani banyak pelanggan setia yang terus kembali menikmati
                        masakan kami.
                    </p>
                </div>

                <div class="bg-yellow-100 p-6 rounded-lg shadow-lg">
                    <h3 class="text-2xl font-semibold text-yellow-700">Komitmen Kami</h3>
                    <p class="mt-4 text-gray-600">
                        Kami berkomitmen untuk terus berinovasi dalam memberikan pengalaman kuliner terbaik yang
                        memuaskan pelanggan.
                    </p>
                </div>
            </div>
        </section>

        <!-- Order Section -->
        <section id="Order"
            class="bg-white min-h-screen flex flex-col items-center justify-center py-16 px-6 order-section">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-bold text-yellow-700">Order Now</h2>
                <p class="mt-4 text-lg text-gray-600">Temukan menu favoritmu!</p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8 w-full max-w-7xl">
                <!-- Paket 1 -->
                <div data-aos="fade-right" data-aos-duration="800"
                    class="bg-yellow-50 p-6 rounded-2xl shadow-xl flex flex-col justify-between text-center hover:scale-105 transition-transform">
                    <div>
                        <h3 class="text-2xl font-bold text-yellow-700 mb-4">Paket 1</h3>
                        <img src="/ayambakar.jpg" alt="Paket 1" class="mx-auto mb-4 rounded-full shadow-md" />
                        <ul class="text-gray-600 mb-6 space-y-1 text-sm">
                            <li>Ayam Bumbu Bakar</li>
                            <li>Nasi Putih</li>
                            <li>Tahu</li>
                            <li>Lalapan</li>
                            <li>Sambal</li>
                        </ul>
                    </div>
                    <div>
                        <p class="text-xl font-bold text-yellow-700 mb-2">Rp 22.000</p>
                        <a :href="'https://wa.me/6287887073476?text=Halo%20saya%20mau%20pesan%20Paket%201'"
                            target="_blank">
                            <GlobalBtn label="Pesan Sekarang" />
                        </a>
                    </div>
                </div>

                <!-- Paket 2 -->
                <div data-aos="fade-right" data-aos-duration="900"
                    class="bg-yellow-50 p-6 rounded-2xl shadow-xl flex flex-col justify-between text-center hover:scale-105 transition-transform">
                    <div>
                        <h3 class="text-2xl font-bold text-yellow-700 mb-4">Paket 2</h3>
                        <img src="/ayamgoreng.jpg" alt="Paket 2" class="mx-auto mb-4 rounded-full shadow-md" />
                        <ul class="text-gray-600 mb-6 space-y-1 text-sm">
                            <li>Ayam Goreng</li>
                            <li>Nasi Putih</li>
                            <li>Tahu</li>
                            <li>Lalapan</li>
                            <li>Sambal</li>
                        </ul>
                    </div>
                    <div>
                        <p class="text-xl font-bold text-yellow-700 mb-2">Rp 22.000</p>
                        <a :href="'https://wa.me/6287887073476?text=Halo%20saya%20mau%20pesan%20Paket%202'"
                            target="_blank">
                            <GlobalBtn label="Pesan Sekarang" />
                        </a>
                    </div>
                </div>

                <!-- Paket 3 -->
                <div data-aos="fade-right" data-aos-duration="1000"
                    class="bg-yellow-50 p-6 rounded-2xl shadow-xl flex flex-col justify-between text-center hover:scale-105 transition-transform">
                    <div>
                        <h3 class="text-2xl font-bold text-yellow-700 mb-4">Paket 3</h3>
                        <img src="/ayamkemangi.jpg" alt="Paket 3" class="mx-auto mb-4 rounded-full shadow-md" />
                        <ul class="text-gray-600 mb-6 space-y-1 text-sm">
                            <li>Ayam Kemangi</li>
                            <li>Nasi Putih</li>
                            <li>Tahu</li>
                            <li>Lalapan</li>
                            <li>Sambal</li>
                        </ul>
                    </div>
                    <div>
                        <p class="text-xl font-bold text-yellow-700 mb-2">Rp 24.000</p>
                        <a :href="'https://wa.me/6287887073476?text=Halo%20saya%20mau%20pesan%20Paket%203'"
                            target="_blank">
                            <GlobalBtn label="Pesan Sekarang" />
                        </a>
                    </div>
                </div>

                <!-- Paket 4 -->
                <div data-aos="fade-right" data-aos-duration="1100"
                    class="bg-yellow-50 p-6 rounded-2xl shadow-xl flex flex-col justify-between text-center hover:scale-105 transition-transform">
                    <div>
                        <h3 class="text-2xl font-bold text-yellow-700 mb-4">Paket 4</h3>
                        <img src="/bebek.jpg" alt="Paket 4" class="mx-auto mb-4 rounded-full shadow-md" />
                        <ul class="text-gray-600 mb-6 space-y-1 text-sm">
                            <li>Bebek Goreng</li>
                            <li>Nasi Putih</li>
                            <li>Bumbu Hitam</li>
                            <li>Timun</li>
                            <li>Sambal</li>
                        </ul>
                    </div>
                    <div>
                        <p class="text-xl font-bold text-yellow-700 mb-2">Rp 25.000</p>
                        <a :href="'https://wa.me/6287887073476?text=Halo%20saya%20mau%20pesan%20Paket%204'"
                            target="_blank">
                            <GlobalBtn label="Pesan Sekarang" />
                        </a>
                    </div>
                </div>

            </div>
        </section>
        <!-- Contact Us Section -->
        <section id="ContactUs" class="bg-yellow-50 py-10 contact-section">
            <h2 class="text-4xl font-bold text-yellow-700 text-center mb-5">Hubungi Kami</h2>
            <div class="max-w-7xl w-full flex flex-col lg:flex-row items-center justify-between gap-8 px-6">

                <!-- Left: WA Icon + Card -->
                <div class="flex flex-col items-center w-full lg:w-1/3">
                    <!-- WhatsApp Icon -->
                    <div @click="showWhatsAppCard" class="flex justify-center items-center cursor-pointer mb-4">
                        <i class="fab fa-whatsapp text-5xl text-green-500"></i>
                    </div>

                    <!-- Address Card -->
                    <div class="w-full bg-white shadow-lg rounded-lg p-6 text-center">
                        <h3 class="text-2xl font-bold text-yellow-700">Masakan Warung Ali</h3>
                        <p class="mt-2 text-gray-600"> JL Perintis kemerdekaan RT 07/RW 02,Pulogadung Jakarta Timur, NO
                            100</p>
                        <p class="mt-2 text-gray-600">Buka Senin - Sabtu, 10.00 - 21.00 WIB</p>

                        <!-- WhatsApp Number Card (Hidden Initially) -->
                        <!-- WhatsApp Number Card (Hidden Initially) -->
                        <div v-if="showCard" class="whatsapp-card mt-4 bg-yellow-50 shadow rounded-lg p-4">
                            <a href="https://wa.me/+6287887073476" target="_blank" rel="noopener noreferrer">
                                <p class="text-gray-700">{{ whatsappNumber }}</p>
                            </a>
                        </div>
                    </div>
                </div>

                <!-- Right: Map -->
                <div class="w-full lg:w-2/3">
                    <div id="map" class="rounded-lg h-[500px] w-full"></div>
                </div>
            </div>
        </section>



        <!-- Footer -->
        <footer class="bg-yellow-50 text-white text-center py-4 bottom-0 w-full footer">
            <p class="text-xl font-bold text-yellow-700">&copy; 2025 Masakan Warung Ali</p>
        </footer>
    </main>
</template>


<style scoped>
#map {
    height: 500px;
    /* Set height to 500px or any value you prefer */
    width: 100%;
    /* Full width */
}

a .contact-section {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}
</style>

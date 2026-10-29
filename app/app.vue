<template>
  <div class="h-screen w-screen flex flex-col bg-[#110f0e] text-[#f4efe6] font-sans overflow-hidden select-none">
    
    <!-- FIXED DARK HEADER -->
    <header class="h-20 bg-[#110f0e]/95 backdrop-blur-md border-b border-[#c59a3f]/20 px-8 flex items-center justify-between z-50 shrink-0">
      <div class="flex items-center gap-3 cursor-pointer" @click="scrollToSection('hero')">
        <div class="w-10 h-10 rounded-full border border-[#c59a3f]/60 bg-[#6b2d22] text-[#d4af37] flex items-center justify-center font-cinzel font-bold text-xl shadow-md">
          M
        </div>
        <div>
          <h1 class="font-cinzel text-base font-bold tracking-widest text-[#f4efe6] leading-none">MAISON & HERITAGE</h1>
          <span class="text-[9px] tracking-[0.3em] text-[#c59a3f] font-serif uppercase block mt-1">Estates 1920</span>
        </div>
      </div>

      <!-- Navigation Matching Reference Image -->
      <nav class="hidden md:flex items-center space-x-8">
        <button 
          v-for="item in navItems" 
          :key="item.id"
          @click="scrollToSection(item.id)"
          :class="[
            'text-xs uppercase tracking-[0.2em] font-medium transition-all duration-300 relative py-1 cursor-pointer flex items-center gap-1.5',
            activeSection === item.id ? 'text-[#d4af37] font-bold' : 'text-[#f4efe6]/70 hover:text-[#d4af37]'
          ]"
        >
          <span>{{ item.icon }}</span>
          <span>{{ item.label }}</span>
          <span 
            v-if="activeSection === item.id" 
            class="absolute bottom-0 left-0 w-full h-[2px] bg-[#d4af37]"
          ></span>
        </button>
      </nav>

      <div class="text-xs uppercase tracking-widest text-[#f4efe6]/70 cursor-pointer hover:text-[#d4af37]">
        Saved (0)
      </div>
    </header>

    <!-- SCROLLABLE MAIN CONTENT BODY -->
    <main 
      ref="mainScrollContainer" 
      @scroll="handleScroll"
      class="flex-1 overflow-y-auto scroll-smooth snap-y snap-mandatory"
    >
      <!-- HERO SECTION -->
      <section id="hero" class="min-h-[calc(100vh-10rem)] snap-start relative flex flex-col items-center justify-center px-6 py-12 bg-cover bg-center" style="background-image: linear-gradient(to bottom, rgba(17,15,14,0.85), rgba(17,15,14,0.95)), url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=1920&q=80');">
        
        <div class="max-w-4xl text-center text-[#f4efe6] space-y-4 mb-8">
          <span class="inline-block px-4 py-1 border border-[#c59a3f]/40 bg-[#1c1917]/80 text-[#d4af37] text-[10px] uppercase tracking-[0.35em] rounded-full">
            ✦ Curators of Architectural Provenance ✦
          </span>
          <h2 class="font-serif text-4xl md:text-6xl font-bold tracking-wide text-[#f4efe6]">
            Timeless Estates &<br/>
            <span class="italic font-normal text-[#d4af37]">Historic Manors</span>
          </h2>
          <p class="text-[#eadfcf]/80 text-xs md:text-sm max-w-xl mx-auto font-light leading-relaxed">
            Maison & Heritage represents the world's most distinguished classical residences, Victorian manors, and century-old architectural masterpieces.
          </p>
        </div>

        <!-- SEARCH WIDGET BOX WITH CORRECT SWAPPED COLORS (Cream/Light Container) -->
        <div class="w-full max-w-3xl bg-[#f5efe6] text-[#1c1917] p-6 shadow-2xl border border-[#c59a3f]/50 rounded-sm">
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
            <div>
              <label class="block text-[10px] uppercase tracking-wider font-bold text-[#2c2825] mb-1.5">Property Type</label>
              <select class="w-full bg-[#fdfbf7] border border-[#d2c3aa] px-3 py-2.5 text-xs text-[#2c2825] focus:outline-none focus:border-[#6b2d22]">
                <option>All Architectures</option>
                <option>Victorian Manors</option>
                <option>Tudor Estates</option>
                <option>Tuscan Villas</option>
              </select>
            </div>
            <div>
              <label class="block text-[10px] uppercase tracking-wider font-bold text-[#2c2825] mb-1.5">Region</label>
              <select class="w-full bg-[#fdfbf7] border border-[#d2c3aa] px-3 py-2.5 text-xs text-[#2c2825] focus:outline-none focus:border-[#6b2d22]">
                <option>All Regions</option>
                <option>Europe & Cotswolds</option>
                <option>North America</option>
                <option>Mediterranean</option>
              </select>
            </div>
            <div>
              <label class="block text-[10px] uppercase tracking-wider font-bold text-[#2c2825] mb-1.5">Century Era</label>
              <select class="w-full bg-[#fdfbf7] border border-[#d2c3aa] px-3 py-2.5 text-xs text-[#2c2825] focus:outline-none focus:border-[#6b2d22]">
                <option>All Eras</option>
                <option>19th Century</option>
                <option>Early 20th Century (1900–1930)</option>
                <option>Renaissance</option>
              </select>
            </div>
          </div>
          <button @click="scrollToSection('properties')" class="w-full py-3.5 bg-[#8b3a2b] hover:bg-[#6b2d22] text-[#f4efe6] text-xs font-semibold tracking-[0.2em] uppercase transition-colors shadow-md cursor-pointer flex items-center justify-center gap-2">
            <span>⌕</span> Search Historic Portfolio
          </button>
        </div>
      </section>

      <!-- PROPERTIES SECTION -->
      <section id="properties" class="min-h-[calc(100vh-10rem)] snap-start px-8 py-16 max-w-7xl mx-auto flex flex-col justify-center">
        <div class="text-center mb-12">
          <span class="text-xs uppercase tracking-[0.3em] text-[#d4af37] font-semibold">Featured Collection</span>
          <h2 class="font-serif text-4xl text-[#f4efe6] mt-2">Curated Historic Estates</h2>
          <div class="w-16 h-0.5 bg-[#d4af37] mx-auto mt-4"></div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="estate in properties" :key="estate.title" class="bg-[#1c1917] border border-[#c59a3f]/30 shadow-xl overflow-hidden group hover:border-[#d4af37] transition-all">
            <div class="relative h-64 overflow-hidden">
              <img :src="estate.image" :alt="estate.title" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" />
              <span class="absolute top-4 left-4 bg-[#8b3a2b] text-[#f4efe6] text-[10px] uppercase tracking-widest px-3 py-1 font-semibold">{{ estate.tag }}</span>
            </div>
            <div class="p-6">
              <div class="flex justify-between items-baseline mb-2">
                <h3 class="font-serif text-xl font-bold text-[#f4efe6]">{{ estate.title }}</h3>
                <span class="text-[#d4af37] font-serif font-bold text-lg">{{ estate.price }}</span>
              </div>
              <p class="text-xs text-[#eadfcf]/60 mb-4">{{ estate.location }}</p>
              <div class="pt-4 border-t border-[#f4efe6]/10 flex justify-between text-xs text-[#eadfcf]/80 font-medium">
                <span>{{ estate.beds }} Beds</span>
                <span>•</span>
                <span>{{ estate.baths }} Baths</span>
                <span>•</span>
                <span>{{ estate.sqft }} Sq Ft</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- HERITAGE SECTION -->
      <section id="heritage" class="min-h-[calc(100vh-10rem)] snap-start bg-[#161412] text-[#f4efe6] px-8 py-16 flex items-center">
        <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-12 items-center">
          <div class="space-y-6">
            <span class="text-xs uppercase tracking-[0.3em] text-[#d4af37] font-semibold">A Century of Honor</span>
            <h2 class="font-serif text-4xl font-bold leading-tight">Preserving Architectural Integrity Since 1920</h2>
            <p class="text-sm text-[#eadfcf]/70 leading-relaxed font-light">Founded over a hundred years ago, Maison & Heritage specializes in the restoration and stewardship of properties with rich history and enduring grandeur.</p>
            <div class="grid grid-cols-2 gap-6 pt-4 border-t border-[#c59a3f]/20">
              <div>
                <span class="font-serif text-3xl font-bold text-[#d4af37] block">120+</span>
                <span class="text-xs text-[#eadfcf]/50 uppercase tracking-wider">Restored Mansions</span>
              </div>
              <div>
                <span class="font-serif text-3xl font-bold text-[#d4af37] block">100%</span>
                <span class="text-xs text-[#eadfcf]/50 uppercase tracking-wider">Historical Fidelity</span>
              </div>
            </div>
          </div>
          <div class="relative">
            <img src="https://images.unsplash.com/photo-1513694203232-719a280e022f?auto=format&fit=crop&w=800&q=80" alt="Vintage interior" class="rounded-sm border-4 border-[#c59a3f]/30 shadow-2xl" />
          </div>
        </div>
      </section>

      <!-- BOOK TOUR / CONTACT SECTION -->
      <section id="book-tour" class="min-h-[calc(100vh-10rem)] snap-start px-8 py-16 max-w-4xl mx-auto flex flex-col justify-center">
        <div class="text-center mb-10">
          <span class="text-xs uppercase tracking-[0.3em] text-[#d4af37] font-semibold">Private Consultation</span>
          <h2 class="font-serif text-4xl text-[#f4efe6] mt-2">Schedule a Private Tour</h2>
          <p class="text-xs text-[#eadfcf]/60 mt-2">Our private advisors will arrange a bespoke tour for you.</p>
        </div>

        <form @submit.prevent="handleSubmit" class="bg-[#1c1917] p-8 border border-[#c59a3f]/30 shadow-xl space-y-6">
          <div class="grid md:grid-cols-2 gap-6">
            <div>
              <label class="block text-xs uppercase tracking-wider text-[#f4efe6] font-semibold mb-2">Full Name</label>
              <input type="text" required placeholder="Lord / Lady Sterling" class="w-full bg-[#110f0e] border border-[#c59a3f]/30 px-4 py-3 text-sm text-[#f4efe6] focus:outline-none focus:border-[#d4af37]" />
            </div>
            <div>
              <label class="block text-xs uppercase tracking-wider text-[#f4efe6] font-semibold mb-2">Email Address</label>
              <input type="email" required placeholder="sterling@estate.com" class="w-full bg-[#110f0e] border border-[#c59a3f]/30 px-4 py-3 text-sm text-[#f4efe6] focus:outline-none focus:border-[#d4af37]" />
            </div>
          </div>
          <div>
            <label class="block text-xs uppercase tracking-wider text-[#f4efe6] font-semibold mb-2">Preferred Estate</label>
            <select class="w-full bg-[#110f0e] border border-[#c59a3f]/30 px-4 py-3 text-sm text-[#f4efe6] focus:outline-none focus:border-[#d4af37]">
              <option>The Ashworth Manor (Victorian)</option>
              <option>The Renaissance Villa (Tuscan)</option>
              <option>Oakridge Tudor Estate (Tudor)</option>
            </select>
          </div>
          <div>
            <label class="block text-xs uppercase tracking-wider text-[#f4efe6] font-semibold mb-2">Inquiry / Requirements</label>
            <textarea rows="4" placeholder="Mention any specific historical requirements or desired inspection dates..." class="w-full bg-[#110f0e] border border-[#c59a3f]/30 px-4 py-3 text-sm text-[#f4efe6] focus:outline-none focus:border-[#d4af37]"></textarea>
          </div>
          <button type="submit" class="w-full py-4 bg-[#8b3a2b] hover:bg-[#6b2d22] text-[#f4efe6] text-xs tracking-[0.2em] font-semibold uppercase transition-colors shadow-md cursor-pointer">
            Submit Tour Request
          </button>
        </form>
      </section>
    </main>

    <!-- FIXED FOOTER -->
    <footer class="h-16 bg-[#110f0e] border-t border-[#c59a3f]/20 px-8 flex items-center justify-between text-xs text-[#eadfcf]/50 z-50 shrink-0">
      <div class="flex items-center gap-2">
        <span class="font-cinzel text-[#d4af37] font-bold">MAISON & HERITAGE</span>
        <span>© 1920–2026. All rights reserved.</span>
      </div>
      <div class="flex space-x-6">
        <a href="#" class="hover:text-[#d4af37] transition-colors">Privacy Policy</a>
        <a href="#" class="hover:text-[#d4af37] transition-colors">Terms of Stewardship</a>
        <a href="#" class="hover:text-[#d4af37] transition-colors">Concierge Desk</a>
      </div>
    </footer>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const activeSection = ref('hero')
const mainScrollContainer = ref(null)

const navItems = [
  { id: 'hero', label: 'Home', icon: '🏠' },
  { id: 'properties', label: 'Properties', icon: '🏛️' },
  { id: 'heritage', label: 'Heritage', icon: '📜' },
  { id: 'book-tour', label: 'Book Tour', icon: '📅' }
]

const properties = [
  {
    title: 'The Ashworth Manor',
    price: '$4,850,000',
    location: 'Cotswolds, England',
    beds: 6,
    baths: 5,
    sqft: '7,200',
    tag: 'Victorian',
    image: 'https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800&q=80'
  },
  {
    title: 'The Renaissance Villa',
    price: '$6,200,000',
    location: 'Tuscany, Italy',
    beds: 8,
    baths: 7,
    sqft: '9,500',
    tag: 'Colonial',
    image: 'https://images.unsplash.com/photo-1600596542815-ffad4c1539a9?auto=format&fit=crop&w=800&q=80'
  },
  {
    title: 'Oakridge Tudor Estate',
    price: '$3,900,000',
    location: 'Boston, Massachusetts',
    beds: 5,
    baths: 4,
    sqft: '5,800',
    tag: 'Tudor',
    image: 'https://images.unsplash.com/photo-1600585154526-990dced4db0d?auto=format&fit=crop&w=800&q=80'
  }
]

const scrollToSection = (id) => {
  activeSection.value = id
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleScroll = (e) => {
  const sections = navItems.map(item => document.getElementById(item.id))
  const scrollPosition = e.target.scrollTop + 200

  for (const section of sections) {
    if (section) {
      const top = section.offsetTop
      const height = section.offsetHeight
      if (scrollPosition >= top && scrollPosition < top + height) {
        activeSection.value = section.id
        break
      }
    }
  }
}

const handleSubmit = () => {
  alert('Thank you for your tour request. Our concierge representative will reach out shortly.')
}
</script>
<script setup>
import { ref, computed, onMounted } from 'vue'

const isRtl = ref(true)
const currentLang = ref('ar')
const isMenuOpen = ref(false)
const isScrolled = ref(false)

const toggleLanguage = () => {
  isRtl.value = !isRtl.value
  currentLang.value = isRtl.value ? 'ar' : 'en'
  document.documentElement.dir = isRtl.value ? 'rtl' : 'ltr'
}

const content = computed(() => currentLang.value === 'ar' ? arContent : enContent)

const arContent = {
  nav: {
    home: 'الرئيسية',
    about: 'من نحن',
    products: 'منتجاتنا',
    branches: 'فروعنا',
    contact: 'تواصل معنا'
  },
  hero: {
    title: 'خباز المدينة',
    subtitle: 'طعم الجودة في كل لقمة',
    slogan: 'خبز طازج، مكونات نقية، جودة مضمونة',
    welcome: 'عوافي ومية هلا.. خباز المدينة يقدملكم ريحة وهوا بغداد بأشهى المعجنات والحلويات اللي تنعمل بحب لإرضاء ذوقكم العالي',
    cta1: 'اطلب الآن',
    cta2: 'تصفح منتجاتنا',
    freshBadge: 'طازج يومياً'
  },
  about: {
    title: 'من نحن',
    subtitle: 'ريحة خبزنا.. ترد الروح',
    description: 'شركة متخصصة في إنتاج وتسويق المخبوزات والحلويات، انطلقت عام 2025 لتضع معايير جديدة للجودة والطعم الأصيل في قلب بغداد.',
    vision: 'رؤيتنا',
    visionText: 'أن نكون المخبز المفضل لكل عائلة عراقية، نجمع بين عراقة الطعم وحداثة الإنتاج',
    mission: 'مهمتنا',
    missionText: 'تقديم منتجات طازجة يومياً بأعلى معايير السلامة الغذائية التي تضمن صحة وسعادة عملائنا',
    values: [
      { icon: 'wheat', title: 'مكونات طبيعية', desc: 'نستخدم أجود أنواع الدقيق والمكونات الطبيعية' },
      { icon: 'chef', title: 'خبرة حرفية', desc: 'فريق من أمهر الخبازين والحلوانيين' },
      { icon: 'trophy', title: 'جودة مضمونة', desc: 'معايير صحية وجودة عالمية' },
      { icon: 'truck', title: 'توصيل سريع', desc: 'طازج من الفرن إلى بابك' }
    ]
  },
  products: {
    title: 'منتجاتنا',
    subtitle: 'تشكيلة واسعة من أشهى المخبوزات والحلويات',
    categories: [
      {
        icon: 'bread',
        title: 'الخبز الطازج',
        desc: 'الرغيف العراقي، الخبز الفرنسي، التورتيلا والصمون',
        items: ['رغيف عراقي', 'خبز فرنسي', 'صمون', 'تورتيلا'],
        image: 'https://images.unsplash.com/photo-1549931319-a545dcf3bc73?w=600'
      },
      {
        icon: 'croissant',
        title: 'المعجنات',
        desc: 'كرواسون، باتيه، سمبوسة وفطائر متنوعة',
        items: ['كرواسون', 'باتيه', 'سمبوسة', 'فطائر'],
        image: 'https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=600'
      },
      {
        icon: 'cake',
        title: 'الحلويات الشرقية',
        desc: 'بقلاوة، كنافة، معمول وحلويات المناسبات',
        items: ['بقلاوة', 'كنافة', 'معمول', 'زنود الست'],
        image: 'https://images.unsplash.com/photo-1519915028121-7d3463d5b1ff?w=600'
      },
      {
        icon: 'birthday',
        title: 'الحلويات الغربية',
        desc: 'كيك، تورت، إكلير وحلويات عصرية',
        items: ['كيك', 'تورت', 'إكلير', 'تشيز كيك'],
        image: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?w=600'
      },
      {
        icon: 'cookie',
        title: 'البسكويت والكوكيز',
        desc: 'بسكويت طازج وكوكيز بنكهات متعددة',
        items: ['كوكيز شوكولاتة', 'بسكويت زبدة', 'غريبة'],
        image: 'https://images.unsplash.com/photo-1499636136210-6f4ee915583e?w=600'
      },
      {
        icon: 'sparkles',
        title: 'طلبات المناسبات',
        desc: 'تجهيز حفلات وأعراس ومناسبات خاصة',
        items: ['كيك مناسبات', 'حلويات أعراس', 'بوفيهات'],
        image: 'https://images.unsplash.com/photo-1464349095431-e9a21285b5f3?w=600'
      }
    ]
  },
  branches: {
    title: 'فروعنا',
    subtitle: 'زورونا في أقرب فرع',
    locations: [
      {
        name: 'فرع المنصور',
        address: 'قرب صاج البديع',
        phone: '07863331999',
        image: 'https://images.unsplash.com/photo-1517433670267-08bbd4be890f?w=600'
      },
      {
        name: 'فرع شارع النضال',
        address: 'عمارة ابن سينا',
        phone: '07863331999',
        image: 'https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=600'
      }
    ]
  },
  contact: {
    title: 'تواصل معنا',
    subtitle: 'نسعد بخدمتكم',
    email: 'info@citybaker.iq',
    phone: '07863331999',
    hours: 'يومياً من 7 صباحاً - 11 مساءً',
    form: {
      name: 'الاسم',
      phone: 'رقم الهاتف',
      message: 'رسالتك',
      submit: 'إرسال'
    }
  },
  footer: {
    rights: 'جميع الحقوق محفوظة',
    company: 'خباز المدينة'
  }
}

const enContent = {
  nav: {
    home: 'Home',
    about: 'About',
    products: 'Products',
    branches: 'Branches',
    contact: 'Contact'
  },
  hero: {
    title: 'City Baker',
    subtitle: 'Quality Taste in Every Bite',
    slogan: 'Fresh Bread, Pure Ingredients, Guaranteed Quality',
    welcome: 'Welcome to City Baker.. We bring you the finest pastries and sweets made with love to satisfy your refined taste',
    cta1: 'Order Now',
    cta2: 'Browse Products',
    freshBadge: 'Fresh Daily'
  },
  about: {
    title: 'About Us',
    subtitle: 'The Aroma of Our Bread.. Revives the Soul',
    description: 'A specialized company in producing and marketing baked goods and sweets, launched in 2025 to set new standards for quality and authentic taste in the heart of Baghdad.',
    vision: 'Our Vision',
    visionText: 'To become the preferred bakery for every Iraqi family, combining traditional taste with modern production',
    mission: 'Our Mission',
    missionText: 'Delivering fresh products daily with the highest food safety standards ensuring the health and happiness of our customers',
    values: [
      { icon: 'wheat', title: 'Natural Ingredients', desc: 'We use the finest flour and natural ingredients' },
      { icon: 'chef', title: 'Craftsmanship', desc: 'Team of skilled bakers and pastry chefs' },
      { icon: 'trophy', title: 'Guaranteed Quality', desc: 'Global health and quality standards' },
      { icon: 'truck', title: 'Fast Delivery', desc: 'Fresh from the oven to your door' }
    ]
  },
  products: {
    title: 'Our Products',
    subtitle: 'Wide selection of delicious baked goods and sweets',
    categories: [
      {
        icon: 'bread',
        title: 'Fresh Bread',
        desc: 'Iraqi bread, French bread, Tortilla and Samoon',
        items: ['Iraqi Bread', 'French Bread', 'Samoon', 'Tortilla'],
        image: 'https://images.unsplash.com/photo-1549931319-a545dcf3bc73?w=600'
      },
      {
        icon: 'croissant',
        title: 'Pastries',
        desc: 'Croissants, Pate, Samosa and various pies',
        items: ['Croissant', 'Pate', 'Samosa', 'Pies'],
        image: 'https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=600'
      },
      {
        icon: 'cake',
        title: 'Eastern Sweets',
        desc: 'Baklava, Kunafa, Maamoul and occasion sweets',
        items: ['Baklava', 'Kunafa', 'Maamoul', 'Znoud El-Sit'],
        image: 'https://images.unsplash.com/photo-1519915028121-7d3463d5b1ff?w=600'
      },
      {
        icon: 'birthday',
        title: 'Western Sweets',
        desc: 'Cakes, Tarts, Eclairs and modern desserts',
        items: ['Cake', 'Tart', 'Eclair', 'Cheesecake'],
        image: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?w=600'
      },
      {
        icon: 'cookie',
        title: 'Biscuits & Cookies',
        desc: 'Fresh biscuits and multi-flavored cookies',
        items: ['Chocolate Cookies', 'Butter Biscuits', 'Ghraybeh'],
        image: 'https://images.unsplash.com/photo-1499636136210-6f4ee915583e?w=600'
      },
      {
        icon: 'sparkles',
        title: 'Special Orders',
        desc: 'Catering for parties, weddings and special occasions',
        items: ['Occasion Cakes', 'Wedding Sweets', 'Buffets'],
        image: 'https://images.unsplash.com/photo-1464349095431-e9a21285b5f3?w=600'
      }
    ]
  },
  branches: {
    title: 'Our Branches',
    subtitle: 'Visit us at the nearest branch',
    locations: [
      {
        name: 'Mansour Branch',
        address: 'Near Saj Al-Badi',
        phone: '07863331999',
        image: 'https://images.unsplash.com/photo-1517433670267-08bbd4be890f?w=600'
      },
      {
        name: 'Al-Nidhal Street Branch',
        address: 'Ibn Sina Building',
        phone: '07863331999',
        image: 'https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=600'
      }
    ]
  },
  contact: {
    title: 'Contact Us',
    subtitle: 'We are happy to serve you',
    email: 'info@citybaker.iq',
    phone: '07863331999',
    hours: 'Daily 7 AM - 11 PM',
    form: {
      name: 'Name',
      phone: 'Phone',
      message: 'Message',
      submit: 'Send'
    }
  },
  footer: {
    rights: 'All Rights Reserved',
    company: 'City Baker'
  }
}

if (typeof window !== 'undefined') {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
  })
}

onMounted(() => {
  document.documentElement.dir = 'rtl'
  document.documentElement.lang = 'ar'
})

const submitForm = () => {
  alert(isRtl.value ? 'شكراً لتواصلك! سنرد عليك قريباً' : 'Thank you! We will contact you soon')
}
</script>

<template>
  <div :dir="isRtl ? 'rtl' : 'ltr'" class="min-h-screen bg-[#FEF7ED]">
    <!-- Navbar -->
    <nav :class="['fixed top-0 left-0 right-0 z-50 transition-all duration-500', isScrolled ? 'bg-white/95 backdrop-blur-xl shadow-lg py-3' : 'bg-transparent py-5']">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between">
          <!-- Logo -->
          <div class="flex items-center gap-3">
            <img src="./assets/logo.svg" alt="City Baker Logo" class="h-14 w-auto" />
          </div>

          <!-- Desktop Nav -->
          <div class="hidden lg:flex items-center gap-1">
            <a v-for="(item, key) in content.nav" :key="key" :href="`#${key}`" :class="['px-5 py-2.5 font-medium transition-all rounded-full', isScrolled ? 'text-[#2C1810] hover:bg-[#78BE20]/10 hover:text-[#78BE20]' : 'text-white/90 hover:text-white hover:bg-white/10']">{{ item }}</a>
          </div>

          <!-- Language & CTA -->
          <div class="hidden md:flex items-center gap-4">
            <button @click="toggleLanguage" :class="['px-4 py-2.5 rounded-full font-medium transition-all', isScrolled ? 'bg-[#78BE20]/10 text-[#78BE20]' : 'bg-white/10 text-white']">
              {{ currentLang === 'ar' ? 'EN' : 'عربي' }}
            </button>
            <a href="#contact" class="btn-primary">{{ content.hero.cta1 }}</a>
          </div>

          <!-- Mobile Menu -->
          <button @click="isMenuOpen = !isMenuOpen" :class="['lg:hidden p-2.5 rounded-xl', isScrolled ? 'bg-[#78BE20]/10 text-[#2C1810]' : 'bg-white/10 text-white']">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
        </div>

        <!-- Mobile Menu Panel -->
        <div v-show="isMenuOpen" class="lg:hidden mt-4 pb-4 bg-white rounded-2xl p-6 shadow-xl">
          <div class="flex flex-col gap-2">
            <a v-for="(item, key) in content.nav" :key="key" :href="`#${key}`" @click="isMenuOpen = false" class="font-medium text-[#2C1810] py-3 px-4 hover:bg-[#78BE20]/10 rounded-xl transition-all">{{ item }}</a>
            <hr class="border-gray-200 my-2">
            <button @click="toggleLanguage" class="text-start font-medium text-[#2C1810] py-3 px-4">{{ currentLang === 'ar' ? 'English' : 'عربي' }}</button>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section - Warm Bakery Style -->
    <section id="home" class="relative min-h-screen flex items-center overflow-hidden">
      <!-- Background Image -->
      <div class="absolute inset-0">
        <img src="https://images.unsplash.com/photo-1509440159596-0249088772ff?w=1920" alt="Fresh Bread" class="w-full h-full object-cover" />
        <div class="absolute inset-0 bg-gradient-to-br from-[#2C1810]/90 via-[#2C1810]/80 to-[#78BE20]/40"></div>
      </div>

      <!-- Decorative Elements -->
      <div class="absolute top-1/4 left-10 w-80 h-80 bg-[#78BE20]/30 rounded-full blur-[100px] animate-float"></div>
      <div class="absolute bottom-1/4 right-10 w-96 h-96 bg-yellow-500/20 rounded-full blur-[120px] animate-float" style="animation-delay: 2s;"></div>

      <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-32 pb-20">
        <div class="grid lg:grid-cols-2 gap-16 items-center">
          <div class="text-white animate-fade-in">
            <!-- Fresh Badge -->
            <div class="inline-flex items-center gap-3 bg-[#78BE20]/20 backdrop-blur-sm px-5 py-3 rounded-full mb-8 border border-[#78BE20]/40">
              <svg class="w-6 h-6 text-[#78BE20]" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456Z" />
              </svg>
              <span class="text-[#78BE20] font-bold">{{ content.hero.freshBadge }}</span>
            </div>

            <h1 class="text-5xl md:text-6xl lg:text-7xl font-black mb-6 leading-[1.1]">{{ content.hero.title }}</h1>

            <h2 class="text-2xl md:text-3xl font-bold text-gradient mb-6">{{ content.hero.subtitle }}</h2>

            <div class="bg-white/10 backdrop-blur-sm border border-white/20 rounded-3xl p-6 mb-8">
              <p class="text-yellow-300 font-bold text-lg mb-3">{{ content.hero.slogan }}</p>
              <p class="text-white/80 leading-relaxed">{{ content.hero.welcome }}</p>
            </div>

            <div class="flex flex-wrap gap-4 mb-10">
              <a href="#contact" class="btn-primary group">
                <svg class="w-5 h-5 group-hover:scale-110 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 0 0-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 0 0-16.536-1.84M7.5 14.25 5.106 5.272M6 20.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Zm12.75 0a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Z" /></svg>
                {{ content.hero.cta1 }}
              </a>
              <a href="#products" class="btn-white">{{ content.hero.cta2 }}</a>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-4 gap-4">
              <div class="text-center">
                <div class="text-2xl md:text-3xl font-black text-white mb-1">2</div>
                <div class="text-xs text-white/70 font-medium">{{ isRtl ? 'فروع' : 'Branches' }}</div>
              </div>
              <div class="text-center">
                <div class="text-2xl md:text-3xl font-black text-[#78BE20] mb-1">50+</div>
                <div class="text-xs text-white/70 font-medium">{{ isRtl ? 'منتج' : 'Products' }}</div>
              </div>
              <div class="text-center">
                <div class="text-2xl md:text-3xl font-black text-white mb-1">5.0</div>
                <div class="text-xs text-white/70 font-medium">{{ isRtl ? 'تقييم' : 'Rating' }}</div>
              </div>
              <div class="text-center">
                <div class="text-2xl md:text-3xl font-black text-yellow-400 mb-1">16h</div>
                <div class="text-xs text-white/70 font-medium">{{ isRtl ? 'يومياً' : 'Daily' }}</div>
              </div>
            </div>
          </div>

          <!-- Hero Visual - Bakery Products -->
          <div class="hidden lg:block">
            <div class="relative">
              <!-- Main Product Image -->
              <div class="relative rounded-[40px] overflow-hidden shadow-2xl shadow-black/30 animate-float">
                <img src="https://images.unsplash.com/photo-1608198093002-ad4e005f0f5a?w=700" alt="Fresh Pastries" class="w-full h-[550px] object-cover" />
                <div class="absolute inset-0 bg-gradient-to-t from-[#2C1810] via-transparent to-transparent"></div>

                <!-- Quality Badge -->
                <div class="absolute bottom-6 left-6 right-6 bg-white/95 backdrop-blur-md rounded-2xl p-5 shadow-xl">
                  <div class="flex items-center justify-between">
                    <div>
                      <div class="text-[#2C1810] font-bold text-lg mb-1">{{ isRtl ? 'من الفرن إلى بابك' : 'From Oven to Your Door' }}</div>
                      <div class="text-[#78BE20] font-semibold text-sm">{{ isRtl ? 'طازج ولذيذ' : 'Fresh & Delicious' }}</div>
                    </div>
                    <div class="w-16 h-16 bg-[#78BE20] rounded-2xl flex items-center justify-center text-white">
                      <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 8.25v-1.5m0 1.5c-1.355 0-2.697.056-4.024.166C6.845 8.51 6 9.473 6 10.608v2.513m6-4.871c1.355 0 2.697.056 4.024.166C17.155 8.51 18 9.473 18 10.608v2.513M15 8.25v-1.5m-6 1.5v-1.5m12 9.75-1.5.75a3.354 3.354 0 0 1-3 0 3.354 3.354 0 0 0-3 0 3.354 3.354 0 0 1-3 0 3.354 3.354 0 0 0-3 0 3.354 3.354 0 0 1-3 0L3 16.5m15-3.379a48.474 48.474 0 0 0-6-.371c-2.032 0-4.034.126-6 .371m12 0c.39.049.777.102 1.163.16 1.07.16 1.837 1.094 1.837 2.175v5.169c0 .621-.504 1.125-1.125 1.125H4.125A1.125 1.125 0 0 1 3 20.625v-5.17c0-1.08.768-2.014 1.837-2.174A47.78 47.78 0 0 1 6 13.12" />
                      </svg>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Floating Product Card -->
              <div class="absolute -top-8 -left-8 w-44 h-44 rounded-3xl overflow-hidden shadow-2xl animate-float border-4 border-white" style="animation-delay: 1s;">
                <img src="https://images.unsplash.com/photo-1558961363-fa8fdf82db35?w=300" alt="Croissant" class="w-full h-full object-cover" />
              </div>

              <!-- Floating Badge -->
              <div class="absolute -bottom-4 -right-4 bg-yellow-400 rounded-2xl p-5 shadow-xl animate-float" style="animation-delay: 2s;">
                <div class="flex items-center gap-3">
                  <svg class="w-8 h-8 text-[#2C1810]" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M11.48 3.499a.562.562 0 0 1 1.04 0l2.125 5.111a.563.563 0 0 0 .475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 0 0-.182.557l1.285 5.385a.562.562 0 0 1-.84.61l-4.725-2.885a.562.562 0 0 0-.586 0L6.982 20.54a.562.562 0 0 1-.84-.61l1.285-5.386a.562.562 0 0 0-.182-.557l-4.204-3.602a.562.562 0 0 1 .321-.988l5.518-.442a.563.563 0 0 0 .475-.345L11.48 3.5Z" />
                  </svg>
                  <div class="text-[#2C1810]">
                    <div class="font-black text-xl">5.0</div>
                    <div class="text-xs font-semibold">{{ isRtl ? 'تقييم' : 'Rating' }}</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Wave Divider -->
      <div class="absolute bottom-0 left-0 right-0">
        <svg viewBox="0 0 1440 120" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 120L60 105C120 90 240 60 360 45C480 30 600 30 720 37.5C840 45 960 60 1080 67.5C1200 75 1320 75 1380 75L1440 75V120H1380C1320 120 1200 120 1080 120C960 120 840 120 720 120C600 120 480 120 360 120C240 120 120 120 60 120H0Z" fill="#FEF7ED"/>
        </svg>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-32 bg-[#FEF7ED]">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-20">
          <span class="inline-flex items-center gap-2 px-5 py-2 bg-[#78BE20]/10 text-[#78BE20] rounded-full text-sm font-bold mb-6">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
            {{ isRtl ? 'قصتنا' : 'Our Story' }}
          </span>
          <h2 class="text-4xl md:text-5xl font-black text-[#2C1810] mb-4">{{ content.about.title }}</h2>
          <p class="text-xl text-[#78BE20] font-bold">{{ content.about.subtitle }}</p>
        </div>

        <div class="grid lg:grid-cols-2 gap-16 items-center mb-20">
          <!-- Image Grid -->
          <div class="relative">
            <div class="grid grid-cols-2 gap-4">
              <div class="space-y-4">
                <div class="rounded-3xl overflow-hidden h-56 shadow-xl">
                  <img src="https://images.unsplash.com/photo-1517433670267-08bbd4be890f?w=500" alt="Bakery" class="w-full h-full object-cover hover:scale-110 transition-transform duration-500" />
                </div>
                <div class="rounded-3xl overflow-hidden h-72 shadow-xl">
                  <img src="https://images.unsplash.com/photo-1556217477-d325251ece38?w=500" alt="Fresh Bread" class="w-full h-full object-cover hover:scale-110 transition-transform duration-500" />
                </div>
              </div>
              <div class="space-y-4 pt-8">
                <div class="rounded-3xl overflow-hidden h-72 shadow-xl">
                  <img src="https://images.unsplash.com/photo-1486427944544-d2c6ec376e2d?w=500" alt="Pastries" class="w-full h-full object-cover hover:scale-110 transition-transform duration-500" />
                </div>
                <div class="rounded-3xl overflow-hidden h-56 shadow-xl">
                  <img src="https://images.unsplash.com/photo-1605807646983-377bc5a76493?w=500" alt="Baker" class="w-full h-full object-cover hover:scale-110 transition-transform duration-500" />
                </div>
              </div>
            </div>

            <!-- Experience Badge -->
            <div class="absolute -bottom-6 left-1/2 -translate-x-1/2 bg-[#78BE20] rounded-2xl p-6 shadow-xl text-white">
              <div class="flex items-center gap-4">
                <div class="w-16 h-16 bg-white/20 rounded-xl flex items-center justify-center">
                  <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 8.25v-1.5m0 1.5c-1.355 0-2.697.056-4.024.166C6.845 8.51 6 9.473 6 10.608v2.513m6-4.871c1.355 0 2.697.056 4.024.166C17.155 8.51 18 9.473 18 10.608v2.513M15 8.25v-1.5m-6 1.5v-1.5m12 9.75-1.5.75a3.354 3.354 0 0 1-3 0 3.354 3.354 0 0 0-3 0 3.354 3.354 0 0 1-3 0 3.354 3.354 0 0 0-3 0 3.354 3.354 0 0 1-3 0L3 16.5" />
                  </svg>
                </div>
                <div>
                  <div class="font-black text-2xl">2025</div>
                  <div class="text-sm text-white/80">{{ isRtl ? 'التأسيس' : 'Founded' }}</div>
                </div>
              </div>
            </div>
          </div>

          <!-- Content -->
          <div>
            <p class="text-gray-600 text-lg leading-relaxed mb-10">{{ content.about.description }}</p>

            <div class="space-y-6">
              <div class="bg-white rounded-3xl p-6 shadow-lg border-r-4 border-[#78BE20] hover:shadow-xl transition-all group">
                <div class="flex items-center gap-4 mb-3">
                  <div class="w-12 h-12 bg-[#78BE20]/10 rounded-xl flex items-center justify-center group-hover:bg-[#78BE20]/20 transition-colors">
                    <svg class="w-6 h-6 text-[#78BE20]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" /></svg>
                  </div>
                  <h4 class="text-xl font-bold text-[#2C1810]">{{ content.about.vision }}</h4>
                </div>
                <p class="text-gray-600">{{ content.about.visionText }}</p>
              </div>

              <div class="bg-white rounded-3xl p-6 shadow-lg border-r-4 border-yellow-500 hover:shadow-xl transition-all group">
                <div class="flex items-center gap-4 mb-3">
                  <div class="w-12 h-12 bg-yellow-500/10 rounded-xl flex items-center justify-center group-hover:bg-yellow-500/20 transition-colors">
                    <svg class="w-6 h-6 text-yellow-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                  </div>
                  <h4 class="text-xl font-bold text-[#2C1810]">{{ content.about.mission }}</h4>
                </div>
                <p class="text-gray-600">{{ content.about.missionText }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Values Grid -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
          <div v-for="(value, i) in content.about.values" :key="i" class="bg-white rounded-3xl p-6 shadow-lg card-hover text-center group">
            <div class="w-16 h-16 mx-auto bg-gradient-to-br from-[#78BE20] to-green-400 rounded-2xl flex items-center justify-center mb-5 text-white group-hover:scale-110 transition-transform shadow-lg shadow-[#78BE20]/30">
              <svg v-if="value.icon === 'wheat'" class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 3v2.25m6.364.386-1.591 1.591M21 12h-2.25m-.386 6.364-1.591-1.591M12 18.75V21m-4.773-4.227-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z" />
              </svg>
              <svg v-else-if="value.icon === 'chef'" class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
              </svg>
              <svg v-else-if="value.icon === 'trophy'" class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M16.5 18.75h-9m9 0a3 3 0 0 1 3 3h-15a3 3 0 0 1 3-3m9 0v-3.375c0-.621-.503-1.125-1.125-1.125h-.871M7.5 18.75v-3.375c0-.621.504-1.125 1.125-1.125h.872m5.007 0H9.497m5.007 0a7.454 7.454 0 0 1-.982-3.172M9.497 14.25a7.454 7.454 0 0 0 .981-3.172M5.25 4.236c-.982.143-1.954.317-2.916.52A6.003 6.003 0 0 0 7.73 9.728M5.25 4.236V4.5c0 2.108.966 3.99 2.48 5.228M5.25 4.236V2.721C7.456 2.41 9.71 2.25 12 2.25c2.291 0 4.545.16 6.75.47v1.516M7.73 9.728a6.726 6.726 0 0 0 2.748 1.35m9.272-5.842V4.5c0 2.108-.966 3.99-2.48 5.228m2.48-5.492a46.32 46.32 0 0 1 2.916.52 6.003 6.003 0 0 1-5.395 4.972m0 0a6.726 6.726 0 0 1-2.749 1.35m0 0a6.772 6.772 0 0 1-3.044 0" />
              </svg>
              <svg v-else class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8.25 18.75a1.5 1.5 0 0 1-3 0m3 0a1.5 1.5 0 0 0-3 0m3 0h6m-9 0H3.375a1.125 1.125 0 0 1-1.125-1.125V14.25m17.25 4.5a1.5 1.5 0 0 1-3 0m3 0a1.5 1.5 0 0 0-3 0m3 0h1.125c.621 0 1.129-.504 1.09-1.124a17.902 17.902 0 0 0-3.213-9.193 2.056 2.056 0 0 0-1.58-.86H14.25M16.5 18.75h-2.25m0-11.177v-.958c0-.568-.422-1.048-.987-1.106a48.554 48.554 0 0 0-10.026 0 1.106 1.106 0 0 0-.987 1.106v7.635m12-6.677v6.677m0 4.5v-4.5m0 0h-12" />
              </svg>
            </div>
            <h4 class="font-bold text-[#2C1810] mb-2 text-lg">{{ value.title }}</h4>
            <p class="text-gray-500 text-sm">{{ value.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Products Section -->
    <section id="products" class="py-32 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 bg-[#78BE20]/10 text-[#78BE20] rounded-full text-sm font-bold mb-6">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09Z" /></svg>
            {{ isRtl ? 'تشكيلتنا' : 'Our Selection' }}
          </span>
          <h2 class="text-4xl md:text-5xl font-black text-[#2C1810] mb-4">{{ content.products.title }}</h2>
          <p class="text-xl text-gray-500">{{ content.products.subtitle }}</p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="(cat, i) in content.products.categories" :key="i" class="group relative rounded-[32px] overflow-hidden bg-white shadow-lg card-hover">
            <div class="relative h-64 overflow-hidden">
              <img :src="cat.image" :alt="cat.title" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500" />
              <div class="absolute inset-0 bg-gradient-to-t from-[#2C1810] via-transparent to-transparent opacity-60"></div>
            </div>
            <div class="p-6">
              <h3 class="text-xl font-bold text-[#2C1810] mb-2">{{ cat.title }}</h3>
              <p class="text-gray-500 text-sm mb-4">{{ cat.desc }}</p>
              <div class="flex flex-wrap gap-2">
                <span v-for="(item, j) in cat.items" :key="j" class="text-xs bg-[#78BE20]/10 text-[#78BE20] px-3 py-1.5 rounded-full font-medium">{{ item }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Branches Section -->
    <section id="branches" class="py-32 bg-[#FEF7ED]">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <span class="inline-flex items-center gap-2 px-5 py-2 bg-[#78BE20]/10 text-[#78BE20] rounded-full text-sm font-bold mb-6">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" /></svg>
            {{ isRtl ? 'مواقعنا' : 'Our Locations' }}
          </span>
          <h2 class="text-4xl md:text-5xl font-black text-[#2C1810] mb-4">{{ content.branches.title }}</h2>
          <p class="text-xl text-gray-500">{{ content.branches.subtitle }}</p>
        </div>

        <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
          <div v-for="(branch, i) in content.branches.locations" :key="i" class="relative rounded-3xl overflow-hidden group shadow-xl">
            <img :src="branch.image" :alt="branch.name" class="w-full h-80 object-cover group-hover:scale-110 transition-transform duration-500" />
            <div class="absolute inset-0 bg-gradient-to-t from-[#2C1810] via-[#2C1810]/50 to-transparent"></div>
            <div class="absolute bottom-0 left-0 right-0 p-8 text-white">
              <div class="flex items-center gap-4 mb-4">
                <div class="w-14 h-14 bg-[#78BE20] rounded-2xl flex items-center justify-center">
                  <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" /></svg>
                </div>
                <div>
                  <h3 class="text-xl font-bold">{{ branch.name }}</h3>
                  <p class="text-white/70 text-sm">{{ branch.address }}</p>
                </div>
              </div>
              <a :href="`tel:${branch.phone}`" class="inline-flex items-center gap-3 bg-white/20 hover:bg-white/30 backdrop-blur-sm px-5 py-3 rounded-xl transition-all" dir="ltr">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" /></svg>
                <span class="font-semibold">{{ branch.phone }}</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-32 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-black text-[#2C1810] mb-4">{{ content.contact.title }}</h2>
          <p class="text-xl text-gray-500">{{ content.contact.subtitle }}</p>
        </div>

        <div class="grid lg:grid-cols-2 gap-12 max-w-5xl mx-auto">
          <!-- Contact Info -->
          <div class="relative overflow-hidden rounded-[32px]">
            <img src="https://images.unsplash.com/photo-1509440159596-0249088772ff?w=800" alt="Contact" class="w-full h-full object-cover absolute inset-0" />
            <div class="absolute inset-0 bg-gradient-to-br from-[#78BE20] to-green-600"></div>
            <div class="relative z-10 p-10 text-white h-full flex flex-col justify-center">
              <h3 class="text-3xl font-bold mb-8">{{ isRtl ? 'معلومات التواصل' : 'Contact Info' }}</h3>

              <div class="space-y-6">
                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-white/20 rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" /></svg>
                  </div>
                  <div>
                    <div class="text-white/70 text-sm mb-1">{{ isRtl ? 'البريد الإلكتروني' : 'Email' }}</div>
                    <div class="font-semibold text-lg">{{ content.contact.email }}</div>
                  </div>
                </div>

                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-white/20 rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" /></svg>
                  </div>
                  <div>
                    <div class="text-white/70 text-sm mb-1">{{ isRtl ? 'الهاتف' : 'Phone' }}</div>
                    <div class="font-semibold text-lg" dir="ltr">{{ content.contact.phone }}</div>
                  </div>
                </div>

                <div class="flex items-center gap-5">
                  <div class="w-14 h-14 bg-white/20 rounded-xl flex items-center justify-center">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" /></svg>
                  </div>
                  <div>
                    <div class="text-white/70 text-sm mb-1">{{ isRtl ? 'ساعات العمل' : 'Hours' }}</div>
                    <div class="font-semibold text-lg">{{ content.contact.hours }}</div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="bg-[#FEF7ED] rounded-[32px] p-10 shadow-xl">
            <form @submit.prevent="submitForm" class="space-y-6">
              <div>
                <label class="block text-sm font-bold text-[#2C1810] mb-3">{{ content.contact.form.name }}</label>
                <input type="text" required class="w-full px-5 py-4 rounded-2xl border-2 border-gray-200 focus:border-[#78BE20] focus:ring-4 focus:ring-[#78BE20]/10 outline-none transition-all bg-white" />
              </div>
              <div>
                <label class="block text-sm font-bold text-[#2C1810] mb-3">{{ content.contact.form.phone }}</label>
                <input type="tel" class="w-full px-5 py-4 rounded-2xl border-2 border-gray-200 focus:border-[#78BE20] focus:ring-4 focus:ring-[#78BE20]/10 outline-none transition-all bg-white" dir="ltr" />
              </div>
              <div>
                <label class="block text-sm font-bold text-[#2C1810] mb-3">{{ content.contact.form.message }}</label>
                <textarea rows="4" class="w-full px-5 py-4 rounded-2xl border-2 border-gray-200 focus:border-[#78BE20] focus:ring-4 focus:ring-[#78BE20]/10 outline-none resize-none transition-all bg-white"></textarea>
              </div>
              <button type="submit" class="w-full btn-primary justify-center text-lg py-5">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5" /></svg>
                {{ content.contact.form.submit }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-[#2C1810]">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <!-- Main Footer -->
        <div class="py-16 grid md:grid-cols-2 lg:grid-cols-4 gap-12">
          <!-- Company Info -->
          <div class="lg:col-span-2">
            <div class="flex items-center gap-4 mb-6">
              <img src="./assets/logo.svg" alt="City Baker Logo" class="h-14 w-auto" />
              <div>
                <h3 class="font-bold text-xl text-white">{{ content.footer.company }}</h3>
                <p class="text-[#78BE20] text-sm">citybaker.iq</p>
              </div>
            </div>
            <p class="text-gray-400 leading-relaxed mb-6 max-w-md">{{ isRtl ? 'شركة متخصصة في إنتاج وتسويق المخبوزات والحلويات، نقدم لكم أشهى المعجنات والحلويات بأعلى معايير الجودة.' : 'A specialized company in producing and marketing baked goods and sweets, offering you the finest pastries with the highest quality standards.' }}</p>
            <!-- Social Links -->
            <div class="flex items-center gap-3">
              <a href="https://www.facebook.com/citybaker.iq" target="_blank" class="w-11 h-11 bg-white/10 rounded-xl flex items-center justify-center hover:bg-[#78BE20] transition-all duration-300 group">
                <svg class="w-5 h-5 text-white/70 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z"/></svg>
              </a>
              <a href="https://www.instagram.com/citybaker.iq" target="_blank" class="w-11 h-11 bg-white/10 rounded-xl flex items-center justify-center hover:bg-[#78BE20] transition-all duration-300 group">
                <svg class="w-5 h-5 text-white/70 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
              </a>
              <a href="https://wa.me/9647863331999" target="_blank" class="w-11 h-11 bg-white/10 rounded-xl flex items-center justify-center hover:bg-[#25D366] transition-all duration-300 group">
                <svg class="w-5 h-5 text-white/70 group-hover:text-white transition-colors" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div>
            <h4 class="text-white font-bold text-lg mb-6">{{ isRtl ? 'روابط سريعة' : 'Quick Links' }}</h4>
            <ul class="space-y-3">
              <li><a href="#home" class="text-gray-400 hover:text-[#78BE20] transition-colors">{{ content.nav.home }}</a></li>
              <li><a href="#about" class="text-gray-400 hover:text-[#78BE20] transition-colors">{{ content.nav.about }}</a></li>
              <li><a href="#products" class="text-gray-400 hover:text-[#78BE20] transition-colors">{{ content.nav.products }}</a></li>
              <li><a href="#branches" class="text-gray-400 hover:text-[#78BE20] transition-colors">{{ content.nav.branches }}</a></li>
              <li><a href="#contact" class="text-gray-400 hover:text-[#78BE20] transition-colors">{{ content.nav.contact }}</a></li>
            </ul>
          </div>

          <!-- Contact Info -->
          <div>
            <h4 class="text-white font-bold text-lg mb-6">{{ isRtl ? 'تواصل معنا' : 'Contact Us' }}</h4>
            <ul class="space-y-4">
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#78BE20] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" /></svg>
                <span class="text-gray-400">{{ content.contact.email }}</span>
              </li>
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#78BE20] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" /></svg>
                <span class="text-gray-400" dir="ltr">{{ content.contact.phone }}</span>
              </li>
              <li class="flex items-start gap-3">
                <svg class="w-5 h-5 text-[#78BE20] mt-0.5 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" /></svg>
                <span class="text-gray-400">{{ content.contact.hours }}</span>
              </li>
            </ul>
          </div>
        </div>

        <!-- Copyright -->
        <div class="py-6 border-t border-white/10 flex flex-col md:flex-row justify-between items-center gap-4">
          <p class="text-gray-500 text-sm">&copy; {{ new Date().getFullYear() }} {{ content.footer.company }}. {{ content.footer.rights }}.</p>
          <p class="text-[#78BE20] text-xs font-medium">{{ isRtl ? 'طعم الجودة في كل لقمة' : 'Quality Taste in Every Bite' }}</p>
        </div>
      </div>
    </footer>

    <!-- WhatsApp Floating Button -->
    <a href="https://wa.me/9647863331999" target="_blank" class="fixed bottom-6 z-50 w-16 h-16 bg-[#25D366] rounded-full flex items-center justify-center shadow-2xl shadow-[#25D366]/40 hover:scale-110 transition-all duration-300 group" :class="isRtl ? 'left-6' : 'right-6'">
      <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      <span class="absolute -top-2 -right-2 w-5 h-5 bg-red-500 rounded-full flex items-center justify-center text-white text-xs font-bold animate-pulse">1</span>
    </a>
  </div>
</template>

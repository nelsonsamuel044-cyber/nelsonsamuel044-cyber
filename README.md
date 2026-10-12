```html
<!DOCTYPE html>
<html lang="id" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NekoVault - Portal Game Visual Novel Bahasa Indonesia</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f5f3ff',
                            100: '#ede9fe',
                            400: '#a78bfa',
                            500: '#8b5cf6',
                            600: '#7c3aed',
                            700: '#6d28d9',
                            800: '#5b21b6',
                            900: '#2e1065',
                            dark: '#0f0b1e',
                            card: '#18122b',
                            cardHover: '#231b3f',
                            accent: '#ec4899'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0b0819;
            color: #e2e8f0;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0b1e;
        }
        ::-webkit-scrollbar-thumb {
            background: #3b2d54;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #7c3aed;
        }

        /* Glassmorphism */
        .glass-panel {
            background: rgba(24, 18, 43, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(139, 92, 246, 0.15);
        }

        .glass-nav {
            background: rgba(15, 11, 30, 0.85);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border-bottom: 1px solid rgba(139, 92, 246, 0.2);
        }

        /* Glow effects */
        .glow-purple {
            box-shadow: 0 0 25px -5px rgba(124, 58, 237, 0.4);
        }
        .glow-pink {
            box-shadow: 0 0 25px -5px rgba(236, 72, 153, 0.4);
        }

        /* Custom line clamp */
        .line-clamp-2 {
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased selection:bg-brand-500 selection:text-white">

    <!-- Header Navigation -->
    <header class="sticky top-0 z-40 glass-nav transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16 sm:h-20">
                <!-- Logo -->
                <div class="flex items-center space-x-3 cursor-pointer" onclick="resetFilters()">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 via-brand-500 to-brand-accent flex items-center justify-center text-white font-black text-xl shadow-lg shadow-brand-600/40">
                        <i class="fa-solid font-bold fa-cat"></i>
                    </div>
                    <div>
                        <span class="text-xl sm:text-2xl font-extrabold bg-gradient-to-r from-white via-brand-100 to-brand-400 bg-clip-text text-transparent">NekoVault</span>
                        <span class="text-xs px-2 py-0.5 ml-1.5 rounded-md bg-brand-600/30 text-brand-400 border border-brand-500/30 font-semibold hidden sm:inline-block">ID Trans</span>
                    </div>
                </div>

                <!-- Desktop Navigation Links & Search -->
                <div class="hidden md:flex items-center space-x-6">
                    <div class="relative w-64 lg:w-80">
                        <input type="text" id="searchInput" oninput="handleSearch()" placeholder="Cari Visual Novel, Genre, atau Modder..." class="w-full bg-brand-dark/80 text-sm text-gray-200 placeholder-gray-400 rounded-xl pl-10 pr-4 py-2.5 border border-brand-500/20 focus:outline-none focus:border-brand-500 focus:ring-1 focus:ring-brand-500 transition">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3 text-gray-400 text-sm"></i>
                    </div>

                    <button onclick="toggleBookmarksOnly()" id="bookmarkToggleBtn" class="flex items-center space-x-2 text-sm font-medium px-4 py-2 rounded-xl bg-brand-card hover:bg-brand-600/20 text-gray-300 hover:text-brand-400 border border-brand-500/20 transition">
                        <i class="fa-solid fa-bookmark text-amber-400"></i>
                        <span>Tersimpan</span>
                        <span id="bookmarkBadge" class="ml-1 bg-brand-600 text-white text-xs px-1.5 py-0.2 rounded-full hidden">0</span>
                    </button>

                    <button onclick="openGuideModal()" class="flex items-center space-x-2 text-sm font-medium text-gray-300 hover:text-brand-400 transition">
                        <i class="fa-solid fa-book-open"></i>
                        <span>Panduan</span>
                    </button>

                    <button onclick="openRequestModal()" class="flex items-center space-x-2 text-sm font-medium bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-600 text-white px-4 py-2 rounded-xl shadow-lg shadow-brand-600/30 hover:shadow-brand-600/50 transition duration-200">
                        <i class="fa-solid fa-paper-plane"></i>
                        <span>Request Game</span>
                    </button>
                </div>

                <!-- Mobile menu button -->
                <div class="flex items-center space-x-3 md:hidden">
                    <button onclick="toggleBookmarksOnly()" class="p-2 rounded-lg bg-brand-card text-amber-400 border border-brand-500/20">
                        <i class="fa-solid fa-bookmark"></i>
                    </button>
                    <button onclick="toggleMobileMenu()" class="text-gray-300 hover:text-white p-2">
                        <i class="fa-solid fa-bars text-xl" id="mobileMenuIcon"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile search & navigation drawer -->
        <div id="mobileMenu" class="hidden md:hidden px-4 pt-2 pb-4 border-t border-brand-500/20 bg-brand-dark/95">
            <div class="my-3">
                <input type="text" id="mobileSearchInput" oninput="handleMobileSearch()" placeholder="Cari Visual Novel..." class="w-full bg-brand-card text-sm text-gray-200 placeholder-gray-400 rounded-xl px-4 py-2.5 border border-brand-500/30 focus:outline-none">
            </div>
            <div class="flex flex-col space-y-2 text-sm">
                <button onclick="openGuideModal(); toggleMobileMenu();" class="flex items-center space-x-3 text-gray-300 hover:text-white py-2 px-3 rounded-lg hover:bg-brand-card">
                    <i class="fa-solid fa-book-open text-brand-400"></i>
                    <span>Panduan Install Game</span>
                </button>
                <button onclick="openRequestModal(); toggleMobileMenu();" class="flex items-center space-x-3 text-gray-300 hover:text-white py-2 px-3 rounded-lg hover:bg-brand-card">
                    <i class="fa-solid fa-paper-plane text-brand-400"></i>
                    <span>Request Game / Laporkan Link Rusak</span>
                </button>
                <button onclick="openDonateModal(); toggleMobileMenu();" class="flex items-center space-x-3 text-gray-300 hover:text-white py-2 px-3 rounded-lg hover:bg-brand-card">
                    <i class="fa-solid fa-heart text-pink-500"></i>
                    <span>Dukung Translator (Traktir)</span>
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow">
        <!-- Hero Featured Carousel -->
        <section class="mb-10 relative">
            <div class="relative rounded-2xl overflow-hidden glass-panel border border-brand-500/30 shadow-2xl min-h-[340px] sm:min-h-[400px]">
                <div id="heroBg" class="absolute inset-0 bg-cover bg-center transition-all duration-700 filter brightness-50 scale-105" style="background-image: url('https://images.unsplash.com/photo-1578632767115-351597cf2477?q=80&w=1200&auto=format&fit=crop');"></div>
                <div class="absolute inset-0 bg-gradient-to-t from-brand-dark via-brand-dark/70 to-transparent"></div>
                <div class="absolute inset-0 bg-gradient-to-r from-brand-dark via-brand-dark/80 to-transparent"></div>

                <div class="relative z-10 p-6 sm:p-10 flex flex-col justify-end h-full min-h-[340px] sm:min-h-[400px] max-w-2xl">
                    <div class="flex items-center space-x-2 mb-3">
                        <span class="bg-brand-accent text-white font-bold text-xs px-2.5 py-1 rounded-md uppercase tracking-wider shadow-lg shadow-brand-accent/40">Rekomendasi Minggu Ini</span>
                        <span id="heroEngine" class="bg-brand-600/80 text-white font-semibold text-xs px-2.5 py-1 rounded-md border border-brand-400/30">Ren'Py Engine</span>
                    </div>
                    <h1 id="heroTitle" class="text-2xl sm:text-4xl font-extrabold text-white tracking-tight mb-2 leading-tight">Summer Memories: Indonesia Translation</h1>
                    <p id="heroDesc" class="text-gray-300 text-xs sm:text-sm mb-4 line-clamp-2 sm:line-clamp-3">Visual novel santai tentang petualangan musim panas yang berkesan. Sepenuhnya diterjemahkan ke Bahasa Indonesia dengan opsi rute percakapan lokal!</p>
                    
                    <div class="flex flex-wrap items-center gap-3">
                        <button id="heroDetailBtn" class="bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-600 text-white font-semibold px-5 py-2.5 rounded-xl flex items-center space-x-2 shadow-lg shadow-brand-600/40 transition">
                            <i class="fa-solid fa-circle-info"></i>
                            <span>Lihat Game & Unduh</span>
                        </button>
                        <div class="flex items-center space-x-2 text-amber-400 text-sm bg-brand-dark/80 px-3 py-2 rounded-xl border border-brand-500/20">
                            <i class="fa-solid fa-star"></i>
                            <span id="heroRating" class="font-bold text-white">4.9 / 5.0</span>
                        </div>
                    </div>
                </div>

                <!-- Slider indicators -->
                <div class="absolute bottom-4 right-4 sm:bottom-6 sm:right-6 flex space-x-2 z-20" id="heroDots">
                    <!-- Dots generated by JS -->
                </div>
            </div>
        </section>

        <!-- Filter and Search Bar -->
        <section class="mb-8">
            <div class="glass-panel p-4 sm:p-5 rounded-2xl border border-brand-500/20 shadow-xl space-y-4">
                <div class="flex flex-wrap items-center justify-between gap-4">
                    <div class="flex items-center space-x-2 text-brand-400 font-semibold">
                        <i class="fa-solid fa-sliders text-lg"></i>
                        <span>Filter Katalog Game</span>
                    </div>
                    <button onclick="resetFilters()" class="text-xs text-gray-400 hover:text-brand-400 underline transition">Reset Semua Filter</button>
                </div>

                <div class="grid grid-cols-2 sm:grid-cols-2 lg:grid-cols-4 gap-3">
                    <!-- Platform Filter -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Platform</label>
                        <select id="filterPlatform" onchange="applyFilters()" class="w-full bg-brand-dark text-sm text-gray-200 rounded-xl px-3 py-2 border border-brand-500/30 focus:outline-none focus:border-brand-500">
                            <option value="ALL">Semua Platform</option>
                            <option value="Android">Android (APK)</option>
                            <option value="PC">Windows PC</option>
                        </select>
                    </div>

                    <!-- Engine Filter -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Game Engine</label>
                        <select id="filterEngine" onchange="applyFilters()" class="w-full bg-brand-dark text-sm text-gray-200 rounded-xl px-3 py-2 border border-brand-500/30 focus:outline-none focus:border-brand-500">
                            <option value="ALL">Semua Engine</option>
                            <option value="Ren'Py">Ren'Py</option>
                            <option value="RPG Maker">RPG Maker</option>
                            <option value="Unity">Unity 3D/2D</option>
                            <option value="KiriKiri">KiriKiri / Tyrano</option>
                        </select>
                    </div>

                    <!-- Genre Filter -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Genre / Tag</label>
                        <select id="filterGenre" onchange="applyFilters()" class="w-full bg-brand-dark text-sm text-gray-200 rounded-xl px-3 py-2 border border-brand-500/30 focus:outline-none focus:border-brand-500">
                            <option value="ALL">Semua Genre</option>
                            <option value="Romance">Romance</option>
                            <option value="School Life">School Life</option>
                            <option value="Mystery">Mystery / Thriller</option>
                            <option value="Fantasy">Fantasy / Isekai</option>
                            <option value="Comedy">Slice of Life / Comedy</option>
                        </select>
                    </div>

                    <!-- Sort Filter -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Urutkan</label>
                        <select id="filterSort" onchange="applyFilters()" class="w-full bg-brand-dark text-sm text-gray-200 rounded-xl px-3 py-2 border border-brand-500/30 focus:outline-none focus:border-brand-500">
                            <option value="newest">Terbaru Ditambahkan</option>
                            <option value="rating">Rating Tertinggi</option>
                            <option value="popular">Paling Populer</option>
                        </select>
                    </div>
                </div>
            </div>
        </section>

        <!-- Catalog Heading & Status -->
        <div class="flex items-center justify-between mb-6">
            <div>
                <h2 class="text-xl sm:text-2xl font-bold text-white flex items-center space-x-2">
                    <span>Koleksi Visual Novel</span>
                    <span id="activeFilterBadge" class="text-xs bg-brand-600/30 text-brand-300 border border-brand-500/30 px-2.5 py-1 rounded-full font-normal hidden">
                        Bookmark Terpilih
                    </span>
                </h2>
                <p id="resultCount" class="text-xs sm:text-sm text-gray-400 mt-1">Menampilkan 0 game</p>
            </div>
            
            <div class="flex items-center space-x-2 bg-brand-card p-1 rounded-xl border border-brand-500/20 text-xs">
                <button id="viewGridBtn" onclick="setViewMode('grid')" class="px-3 py-1.5 rounded-lg bg-brand-600 text-white font-medium shadow"><i class="fa-solid fa-border-all"></i> Grid</button>
                <button id="viewListBtn" onclick="setViewMode('list')" class="px-3 py-1.5 rounded-lg text-gray-400 hover:text-white font-medium"><i class="fa-solid fa-list"></i> List</button>
            </div>
        </div>

        <!-- Catalog Grid Container -->
        <div id="catalogContainer" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
            <!-- Game Cards injected dynamically -->
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden text-center py-16 bg-brand-card/40 rounded-2xl border border-brand-500/10">
            <i class="fa-solid fa-ghost text-5xl text-brand-500/40 mb-4"></i>
            <h3 class="text-lg font-semibold text-gray-300">Game tidak ditemukan</h3>
            <p class="text-sm text-gray-500 mt-1 max-w-sm mx-auto">Coba gunakan kata kunci pencarian lain atau ubah filter pencarian Anda.</p>
            <button onclick="resetFilters()" class="mt-4 px-4 py-2 bg-brand-600 text-white text-sm rounded-xl hover:bg-brand-500 transition">Reset Filter</button>
        </div>
    </main>

    <!-- Community Support Banner -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 my-10">
        <div class="glass-panel rounded-2xl p-6 sm:p-8 border border-brand-500/30 relative overflow-hidden flex flex-col md:flex-row items-center justify-between gap-6">
            <div class="relative z-10 max-w-xl">
                <span class="text-xs font-bold text-pink-400 tracking-wider uppercase mb-1 block">Dukung Translator Lokal</span>
                <h3 class="text-xl sm:text-2xl font-bold text-white mb-2">Suka dengan hasil terjemahan Bahasa Indonesia?</h3>
                <p class="text-gray-300 text-sm">Bantu para translator dan modder untuk terus menghadirkan karya Visual Novel terbaru ber-Bahasa Indonesia melalui donasi ringan.</p>
            </div>
            <div class="relative z-10 flex flex-wrap gap-3">
                <button onclick="openDonateModal()" class="bg-gradient-to-r from-pink-500 to-rose-600 hover:from-pink-600 hover:to-rose-700 text-white font-semibold px-6 py-3 rounded-xl shadow-lg shadow-pink-500/30 flex items-center space-x-2 transition">
                    <i class="fa-solid fa-heart"></i>
                    <span>Traktir Kopi / Saweria</span>
                </button>
                <button onclick="openGuideModal()" class="bg-brand-dark hover:bg-brand-card text-gray-200 border border-brand-500/30 px-5 py-3 rounded-xl text-sm font-semibold transition">
                    <i class="fa-solid fa-circle-question mr-1"></i> Cara Pasang Patch
                </button>
            </div>
            <!-- Background glow decoration -->
            <div class="absolute -right-10 -bottom-10 w-60 h-60 bg-brand-600/20 rounded-full filter blur-3xl"></div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-brand-dark border-t border-brand-500/20 text-gray-400 text-sm py-10 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
                <div class="space-y-3">
                    <div class="flex items-center space-x-2">
                        <div class="w-8 h-8 rounded-lg bg-brand-600 flex items-center justify-center text-white font-bold">
                            <i class="fa-solid fa-cat"></i>
                        </div>
                        <span class="text-lg font-bold text-white">NekoVault</span>
                    </div>
                    <p class="text-xs text-gray-400 leading-relaxed">Katalog & Arsip V

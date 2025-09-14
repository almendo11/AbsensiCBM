<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UKM Catur Benteng Merdeka - Sistem Absensi Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        * {
            font-family: 'Inter', sans-serif;
        }
        
        .chess-bg {
            background-image: 
                linear-gradient(45deg, rgba(0,0,0,0.02) 25%, transparent 25%), 
                linear-gradient(-45deg, rgba(0,0,0,0.02) 25%, transparent 25%), 
                linear-gradient(45deg, transparent 75%, rgba(0,0,0,0.02) 75%), 
                linear-gradient(-45deg, transparent 75%, rgba(0,0,0,0.02) 75%);
            background-size: 60px 60px;
            background-position: 0 0, 0 30px, 30px -30px, -30px 0px;
        }
        
        .gold-gradient {
            background: linear-gradient(135deg, #FFD700, #FFA500);
        }
        
        .chess-piece {
            font-size: 2rem;
            color: #FFD700;
        }
        
        .scan-animation {
            animation: scan 2s ease-in-out infinite;
        }
        
        @keyframes scan {
            0%, 100% { transform: translateY(0); opacity: 1; }
            50% { transform: translateY(-10px); opacity: 0.7; }
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="bg-gray-50 chess-bg min-h-screen">
    <!-- Header -->
    <header class="bg-black shadow-lg">
        <div class="container mx-auto px-4 py-4">
            <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="chess-piece">♔</div>
                    <div>
                        <h1 class="text-white text-xl font-bold">UKM Catur Benteng Merdeka</h1>
                        <p class="text-gray-300 text-sm">Sistem Absensi Digital</p>
                    </div>
                </div>
                <nav class="hidden md:flex space-x-6">
                    <a href="#" onclick="goHome()" class="text-white hover:text-yellow-400 transition-colors cursor-pointer">Home</a>
                    <a href="#" onclick="showLoginSelection()" class="text-white hover:text-yellow-400 transition-colors cursor-pointer">Login</a>
                    <a href="#" onclick="showAbout()" class="text-white hover:text-yellow-400 transition-colors cursor-pointer">Tentang</a>
                    <a href="#" onclick="showContact()" class="text-white hover:text-yellow-400 transition-colors cursor-pointer">Kontak</a>
                </nav>
                <button onclick="toggleMobileMenu()" class="md:hidden text-white">
                    <svg id="hamburgerIcon" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                    </svg>
                    <svg id="closeIcon" class="w-6 h-6 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </div>
            
            <!-- Mobile Menu -->
            <div id="mobileMenu" class="md:hidden hidden bg-gray-900 border-t border-gray-700">
                <div class="px-4 py-4 space-y-3">
                    <a href="#" onclick="goHome(); closeMobileMenu()" class="block text-white hover:text-yellow-400 transition-colors py-2">Home</a>
                    <a href="#" onclick="showLoginSelection(); closeMobileMenu()" class="block text-white hover:text-yellow-400 transition-colors py-2 cursor-pointer">Login</a>
                    <a href="#" onclick="showAbout(); closeMobileMenu()" class="block text-white hover:text-yellow-400 transition-colors py-2">Tentang</a>
                    <a href="#" onclick="showContact(); closeMobileMenu()" class="block text-white hover:text-yellow-400 transition-colors py-2">Kontak</a>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main id="mainContent">
        <!-- Hero Section -->
        <section id="heroSection" class="py-20 bg-gradient-to-br from-gray-900 via-black to-gray-800 relative overflow-hidden">
            <!-- Background Chess Icons -->
            <div class="absolute inset-0 pointer-events-none">
                <div class="absolute top-10 left-10 text-8xl text-white opacity-5 blur-sm">♔</div>
                <div class="absolute top-32 right-20 text-6xl text-white opacity-5 blur-sm">♕</div>
                <div class="absolute bottom-40 left-20 text-7xl text-white opacity-5 blur-sm">♖</div>
                <div class="absolute bottom-20 right-32 text-5xl text-white opacity-5 blur-sm">♗</div>
                <div class="absolute top-1/2 left-1/4 text-9xl text-white opacity-3 blur-md">♘</div>
                <div class="absolute top-1/3 right-1/3 text-4xl text-white opacity-5 blur-sm">♙</div>
                <div class="absolute bottom-1/3 left-1/2 text-6xl text-white opacity-5 blur-sm">♔</div>
                <div class="absolute top-20 left-1/2 text-5xl text-white opacity-5 blur-sm">♕</div>
                <div class="absolute bottom-10 left-10 text-7xl text-white opacity-5 blur-sm">♖</div>
                <div class="absolute top-1/4 right-10 text-8xl text-white opacity-3 blur-md">♗</div>
            </div>
            
            <div class="container mx-auto px-4 text-center relative z-10">
                <div class="max-w-4xl mx-auto">
                    <div class="mb-8">
                        <div class="inline-flex space-x-4 text-6xl mb-6">
                            <span class="chess-piece">♔</span>
                            <span class="chess-piece">♕</span>
                            <span class="chess-piece">♖</span>
                            <span class="chess-piece">♗</span>
                            <span class="chess-piece">♘</span>
                            <span class="chess-piece">♙</span>
                        </div>
                    </div>
                    <h2 class="text-5xl font-bold text-white mb-12">
                        GENS UNA SUMUS
                    </h2>
                    
                    <div class="grid md:grid-cols-3 gap-6 max-w-3xl mx-auto">
                        <button onclick="showLogin('admin')" class="bg-gradient-to-r from-red-600 to-red-700 hover:from-red-700 hover:to-red-800 text-white py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                            <div class="text-2xl mb-2">♔</div>
                            Login Sebagai Admin
                        </button>
                        <button onclick="showLogin('pengurus')" class="gold-gradient hover:from-yellow-500 hover:to-orange-600 text-black py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                            <div class="text-2xl mb-2">♕</div>
                            Login Sebagai Pengurus
                        </button>
                        <button onclick="showLogin('anggota')" class="bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                            <div class="text-2xl mb-2">♙</div>
                            Login Sebagai Anggota
                        </button>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Login Selection Modal -->
    <div id="loginSelectionModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">🔐</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-2">Pilih Jenis Login</h3>
                <p class="text-gray-600">Silakan pilih role sesuai dengan akun Anda</p>
            </div>
            
            <div class="space-y-4">
                <button onclick="selectLoginType('admin')" class="w-full bg-gradient-to-r from-red-600 to-red-700 hover:from-red-700 hover:to-red-800 text-white py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                    <div class="flex items-center justify-center space-x-3">
                        <span class="text-2xl">♔</span>
                        <div class="text-left">
                            <div class="font-bold">Login Sebagai Admin</div>
                            <div class="text-sm opacity-90">Akses penuh sistem</div>
                        </div>
                    </div>
                </button>
                
                <button onclick="selectLoginType('pengurus')" class="w-full gold-gradient hover:from-yellow-500 hover:to-orange-600 text-black py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                    <div class="flex items-center justify-center space-x-3">
                        <span class="text-2xl">♕</span>
                        <div class="text-left">
                            <div class="font-bold">Login Sebagai Pengurus</div>
                            <div class="text-sm opacity-90">Kelola kegiatan UKM</div>
                        </div>
                    </div>
                </button>
                
                <button onclick="selectLoginType('anggota')" class="w-full bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white py-4 px-6 rounded-xl font-semibold transition-all transform hover:scale-105 shadow-lg">
                    <div class="flex items-center justify-center space-x-3">
                        <span class="text-2xl">♙</span>
                        <div class="text-left">
                            <div class="font-bold">Login Sebagai Anggota</div>
                            <div class="text-sm opacity-90">Absensi dan info kegiatan</div>
                        </div>
                    </div>
                </button>
            </div>
            
            <div class="mt-6 p-4 bg-blue-50 rounded-lg">
                <p class="text-blue-700 text-sm text-center">
                    <span class="font-medium">💡 Belum punya akun?</span><br>
                    Hubungi admin untuk pembuatan akun baru
                </p>
            </div>
            
            <button onclick="closeLoginSelection()" class="mt-4 w-full text-gray-500 hover:text-gray-700 transition-colors">
                Batal
            </button>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div id="loginIcon" class="text-4xl mb-4">♔</div>
                <h3 id="loginTitle" class="text-2xl font-bold text-gray-800">Login Admin</h3>
            </div>
            <form onsubmit="handleLogin(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Username</label>
                    <input type="text" id="loginUsername" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan username" onkeypress="handleUsernameKeypress(event)">
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Password</label>
                    <div class="relative">
                        <input type="password" id="loginPassword" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan password" onkeypress="handlePasswordKeypress(event)">
                        <button type="button" onclick="togglePasswordVisibility('loginPassword')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                            <svg id="loginPassword-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                            </svg>
                            <svg id="loginPassword-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                            </svg>
                        </button>
                    </div>
                </div>
                <div id="loginError" class="hidden mb-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded-lg text-sm">
                </div>
                <button type="submit" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Login
                </button>
            </form>
            <button onclick="closeLogin()" class="mt-4 w-full text-gray-500 hover:text-gray-700 transition-colors">
                Batal
            </button>
        </div>
    </div>

    <!-- Dashboard Content (Hidden by default) -->
    <div id="dashboardContent" class="hidden">
        <!-- Admin Dashboard -->
        <div id="adminDashboard" class="hidden">
            <div class="container mx-auto px-4 py-8">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">Dashboard Admin ♔</h2>
                    <p class="text-gray-600">Kelola sistem absensi UKM Catur Benteng Merdeka</p>
                </div>
                
                <div class="grid md:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-lg font-semibold text-gray-800">Total Anggota</h3>
                            <span class="text-2xl">♙</span>
                        </div>
                        <p class="text-3xl font-bold text-blue-600" id="totalAnggotaCount">0</p>
                        <p class="text-sm text-gray-500">Anggota aktif</p>
                    </div>
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-lg font-semibold text-gray-800">Total Pengurus</h3>
                            <span class="text-2xl">♕</span>
                        </div>
                        <p class="text-3xl font-bold text-purple-600" id="totalPengurusCount">0</p>
                        <p class="text-sm text-gray-500">Pengurus aktif</p>
                    </div>
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-lg font-semibold text-gray-800">Kehadiran Hari Ini</h3>
                            <span class="text-2xl">✓</span>
                        </div>
                        <p class="text-3xl font-bold text-green-600">0</p>
                        <p class="text-sm text-gray-500">Dari 0 anggota</p>
                    </div>
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-lg font-semibold text-gray-800">Jadwal Aktif</h3>
                            <span class="text-2xl">📅</span>
                        </div>
                        <p class="text-3xl font-bold text-yellow-600">0</p>
                        <p class="text-sm text-gray-500">Sesi minggu ini</p>
                    </div>
                </div>

                <div class="grid md:grid-cols-3 gap-6">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Buat Jadwal Baru</h3>
                        <form onsubmit="createSchedule(event)" class="space-y-4">
                            <input type="text" id="eventName" placeholder="Nama Kegiatan" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                            <input type="datetime-local" id="eventDateTime" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                            <select id="eventType" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                                <option value="">Pilih Jenis Kegiatan</option>
                                <option value="Latihan Rutin">Latihan Rutin</option>
                                <option value="Rapat">Rapat</option>
                                <option value="Turnamen">Turnamen</option>
                                <option value="Workshop">Workshop</option>
                                <option value="Pertandingan">Pertandingan</option>
                            </select>
                            <button type="submit" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                                Buat Jadwal
                            </button>
                        </form>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Kelola Data Anggota</h3>
                        <div class="space-y-3">
                            <button onclick="showAddMember()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg transition-colors">
                                Tambah Anggota Baru
                            </button>
                            <button onclick="showMemberList()" class="w-full bg-gray-600 hover:bg-gray-700 text-white py-3 rounded-lg transition-colors">
                                Lihat Semua Anggota
                            </button>
                            <button onclick="showUserManagement()" class="w-full bg-red-600 hover:bg-red-700 text-white py-3 rounded-lg transition-colors">
                                Kelola Akun Pengguna
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Laporan & Analisis</h3>
                        <div class="space-y-3">
                            <button onclick="showAttendanceReport('admin')" class="w-full bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-700 hover:to-indigo-700 text-white py-4 rounded-lg font-semibold transition-all transform hover:scale-105 shadow-lg">
                                <div class="flex items-center justify-center space-x-3">
                                    <span class="text-2xl">📊</span>
                                    <span>Laporan Lengkap</span>
                                </div>
                                <div class="text-sm mt-1 opacity-90">
                                    Semua Data & Analisis
                                </div>
                            </button>
                            <div class="grid grid-cols-2 gap-2">
                                <button onclick="showAttendanceReport('pengurus')" class="bg-gradient-to-r from-yellow-500 to-orange-500 hover:from-yellow-600 hover:to-orange-600 text-white py-3 rounded-lg font-medium transition-all text-sm">
                                    <div class="flex items-center justify-center space-x-2">
                                        <span class="text-lg">♕</span>
                                        <span>Pengurus</span>
                                    </div>
                                </button>
                                <button onclick="showAttendanceReport('anggota')" class="bg-gradient-to-r from-purple-500 to-pink-500 hover:from-purple-600 hover:to-pink-600 text-white py-3 rounded-lg font-medium transition-all text-sm">
                                    <div class="flex items-center justify-center space-x-2">
                                        <span class="text-lg">♙</span>
                                        <span>Anggota</span>
                                    </div>
                                </button>
                            </div>
                            <div class="bg-gray-50 rounded-lg p-3">
                                <p class="text-sm text-gray-600 text-center">
                                    <span class="font-medium">Data Terkini</span> siap dianalisis
                                </p>
                                <div class="flex justify-center space-x-4 mt-2 text-xs">
                                    <span class="flex items-center text-blue-600">
                                        <span class="w-2 h-2 bg-blue-600 rounded-full mr-1"></span>
                                        Harian
                                    </span>
                                    <span class="flex items-center text-green-600">
                                        <span class="w-2 h-2 bg-green-600 rounded-full mr-1"></span>
                                        Mingguan
                                    </span>
                                    <span class="flex items-center text-orange-600">
                                        <span class="w-2 h-2 bg-orange-600 rounded-full mr-1"></span>
                                        Bulanan
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="grid md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Pengaturan Admin</h3>
                        <div class="space-y-3">
                            <button onclick="showChangePassword()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg transition-colors">
                                🔐 Ganti Password Admin
                            </button>
                            <button onclick="clearAllData()" class="w-full bg-red-600 hover:bg-red-700 text-white py-3 rounded-lg transition-colors">
                                🗑️ Reset Semua Data
                            </button>
                            <div class="bg-gray-50 rounded-lg p-3">
                                <p class="text-sm text-gray-600">
                                    <span class="font-medium">💡 Tips Keamanan:</span><br>
                                    • Gunakan password yang kuat<br>
                                    • Jangan bagikan password ke orang lain<br>
                                    • Ganti password secara berkala<br>
                                    • Backup data sebelum reset
                                </p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Informasi Admin</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Role</span>
                                <span class="text-red-600 font-bold">♔ Admin</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Status</span>
                                <span class="text-green-600 font-bold">Aktif</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Login Terakhir</span>
                                <span class="text-blue-600 font-bold">Hari ini</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Laporan Kehadiran</h3>
                    <div class="bg-gray-100 rounded-lg p-4 mb-4">
                        <div class="flex justify-between items-center mb-2">
                            <span class="text-sm text-gray-600">Tingkat Kehadiran</span>
                            <span class="text-sm font-semibold text-green-600">0%</span>
                        </div>
                        <div class="w-full bg-gray-300 rounded-full h-2">
                            <div class="bg-green-600 h-2 rounded-full" style="width: 0%"></div>
                        </div>
                    </div>
                    <button class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                        Export Laporan
                    </button>
                </div>
                </div>
            </div>
        </div>

        <!-- Pengurus Dashboard -->
        <div id="pengurusDashboard" class="hidden">
            <div class="container mx-auto px-4 py-8">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">Dashboard Pengurus ♕</h2>
                    <p class="text-gray-600">Selamat datang, <span id="pengurusWelcomeName">Pengurus</span>!</p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-6">Absensi Kehadiran</h3>
                        <div class="space-y-4">
                            <button onclick="showAttendanceSchedule()" class="w-full gold-gradient text-black py-4 rounded-xl font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all transform hover:scale-105 shadow-lg">
                                <div class="flex items-center justify-center space-x-3">
                                    <span class="text-2xl">✋</span>
                                    <span>Absen Kehadiran</span>
                                </div>
                                <div class="text-sm mt-1 opacity-90">
                                    Pilih kegiatan untuk absen
                                </div>
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Status Kehadiran</h3>
                        <div class="space-y-4">
                            <div class="flex justify-between items-center p-3 bg-blue-50 rounded-lg">
                                <span class="font-medium">Bulan Ini</span>
                                <span class="text-blue-600 font-bold">0/0</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-green-50 rounded-lg">
                                <span class="font-medium">Persentase</span>
                                <span class="text-green-600 font-bold">0%</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-yellow-50 rounded-lg">
                                <span class="font-medium">Terakhir Hadir</span>
                                <span class="text-yellow-600 font-bold">-</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Pengaturan Akun</h3>
                        <div class="space-y-3">
                            <button onclick="showChangePassword()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg transition-colors">
                                🔐 Ganti Password
                            </button>
                            <div class="bg-gray-50 rounded-lg p-3">
                                <p class="text-sm text-gray-600">
                                    <span class="font-medium">💡 Tips Keamanan:</span><br>
                                    • Gunakan password yang kuat<br>
                                    • Jangan bagikan password ke orang lain<br>
                                    • Ganti password secara berkala
                                </p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Informasi Akun</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Role</span>
                                <span class="text-purple-600 font-bold">♙ Anggota</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Status</span>
                                <span class="text-green-600 font-bold">Aktif</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Login Terakhir</span>
                                <span class="text-blue-600 font-bold">Hari ini</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Riwayat Kehadiran</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-sm">
                            <thead>
                                <tr class="border-b">
                                    <th class="text-left py-3 px-4">Tanggal</th>
                                    <th class="text-left py-3 px-4">Kegiatan</th>
                                    <th class="text-left py-3 px-4">Waktu</th>
                                    <th class="text-left py-3 px-4">Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td colspan="4" class="py-8 text-center text-gray-500">
                                        Belum ada riwayat kehadiran
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- Anggota Dashboard -->
        <div id="anggotaDashboard" class="hidden">
            <div class="container mx-auto px-4 py-8">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">Dashboard Anggota ♙</h2>
                    <p class="text-gray-600">Selamat datang, <span id="anggotaWelcomeName">Anggota</span>!</p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-6">Absensi Kehadiran</h3>
                        <div class="space-y-4">
                            <button onclick="showAttendanceSchedule()" class="w-full gold-gradient text-black py-4 rounded-xl font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all transform hover:scale-105 shadow-lg">
                                <div class="flex items-center justify-center space-x-3">
                                    <span class="text-2xl">✋</span>
                                    <span>Absen Kehadiran</span>
                                </div>
                                <div class="text-sm mt-1 opacity-90">
                                    Pilih kegiatan untuk absen
                                </div>
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Status Kehadiran</h3>
                        <div class="space-y-4">
                            <div class="flex justify-between items-center p-3 bg-blue-50 rounded-lg">
                                <span class="font-medium">Bulan Ini</span>
                                <span class="text-blue-600 font-bold">0/0</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-green-50 rounded-lg">
                                <span class="font-medium">Persentase</span>
                                <span class="text-green-600 font-bold">0%</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-yellow-50 rounded-lg">
                                <span class="font-medium">Terakhir Hadir</span>
                                <span class="text-yellow-600 font-bold">-</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Pengaturan Akun</h3>
                        <div class="space-y-3">
                            <button onclick="showChangePassword()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg transition-colors">
                                🔐 Ganti Password
                            </button>
                            <div class="bg-gray-50 rounded-lg p-3">
                                <p class="text-sm text-gray-600">
                                    <span class="font-medium">💡 Tips Keamanan:</span><br>
                                    • Gunakan password yang kuat<br>
                                    • Jangan bagikan password ke orang lain<br>
                                    • Ganti password secara berkala
                                </p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-xl p-6 shadow-lg">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Informasi Akun</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Role</span>
                                <span class="text-purple-600 font-bold">♙ Anggota</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Status</span>
                                <span class="text-green-600 font-bold">Aktif</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="font-medium">Login Terakhir</span>
                                <span class="text-blue-600 font-bold">Hari ini</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Riwayat Kehadiran</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-sm">
                            <thead>
                                <tr class="border-b">
                                    <th class="text-left py-3 px-4">Tanggal</th>
                                    <th class="text-left py-3 px-4">Kegiatan</th>
                                    <th class="text-left py-3 px-4">Waktu</th>
                                    <th class="text-left py-3 px-4">Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td colspan="4" class="py-8 text-center text-gray-500">
                                        Belum ada riwayat kehadiran
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Attendance Schedule Modal -->
    <div id="attendanceScheduleModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-2xl w-full mx-4 fade-in max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">✋</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-2">Absensi Kehadiran</h3>
                <p class="text-gray-600">Pilih kegiatan yang ingin Anda ikuti untuk melakukan absensi</p>
            </div>
            
            <div id="attendanceScheduleContent" class="space-y-4">
                <!-- Schedule list will be populated here -->
            </div>
            
            <div class="text-center mt-6">
                <button onclick="closeAttendanceSchedule()" class="w-full bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-colors">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- Success Modal -->
    <div id="successModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center">
                <div class="text-6xl mb-4">✅</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-4">Absensi Berhasil!</h3>
                <p class="text-gray-600 mb-6">Kehadiran Anda telah tercatat pada:</p>
                <div class="bg-green-50 rounded-lg p-4 mb-6">
                    <p class="font-semibold text-green-800" id="attendanceTime"></p>
                    <p class="text-green-600">Latihan Rutin - 16 Desember 2024</p>
                </div>
                <button onclick="closeSuccess()" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- About Modal -->
    <div id="aboutModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-2xl w-full mx-4 fade-in max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">♔</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-6">Tentang Sistem Absensi Digital</h3>
            </div>
            
            <div class="text-left space-y-6">
                <div>
                    <h4 class="text-xl font-semibold text-gray-800 mb-3 flex items-center">
                        <span class="text-2xl mr-2">🎯</span>
                        Tujuan
                    </h4>
                    <p class="text-gray-600 leading-relaxed">
                        Web absensi digital UKM Catur Benteng Merdeka dibuat sebagai sarana modern untuk mendukung kedisiplinan dan profesionalisme anggota. Dengan adanya sistem ini, setiap proses pencatatan kehadiran menjadi lebih cepat, praktis, dan akurat. Selain itu, web ini dirancang agar pengurus dapat lebih mudah mengelola jadwal, memantau kehadiran, serta menyusun laporan secara efisien.
                    </p>
                </div>
                
                <div>
                    <h4 class="text-xl font-semibold text-gray-800 mb-3 flex items-center">
                        <span class="text-2xl mr-2">✨</span>
                        Manfaat
                    </h4>
                    <div class="space-y-4">
                        <div class="bg-blue-50 rounded-lg p-4">
                            <h5 class="font-semibold text-blue-800 mb-2">⚡ Efisiensi Waktu</h5>
                            <p class="text-blue-700 text-sm">Anggota tidak perlu lagi menandatangani daftar hadir manual, cukup login atau scan barcode untuk mencatat kehadiran.</p>
                        </div>
                        
                        <div class="bg-green-50 rounded-lg p-4">
                            <h5 class="font-semibold text-green-800 mb-2">📊 Data Lebih Akurat</h5>
                            <p class="text-green-700 text-sm">Sistem mencatat waktu dan tanggal secara otomatis sehingga meminimalisir kesalahan input.</p>
                        </div>
                        
                        <div class="bg-purple-50 rounded-lg p-4">
                            <h5 class="font-semibold text-purple-800 mb-2">👁️ Transparansi</h5>
                            <p class="text-purple-700 text-sm">Semua anggota, pengurus, dan admin bisa melihat riwayat absensi dengan jelas.</p>
                        </div>
                        
                        <div class="bg-orange-50 rounded-lg p-4">
                            <h5 class="font-semibold text-orange-800 mb-2">📱 Kemudahan Akses</h5>
                            <p class="text-orange-700 text-sm">Bisa diakses melalui laptop maupun smartphone, kapan saja dan di mana saja.</p>
                        </div>
                        
                        <div class="bg-yellow-50 rounded-lg p-4">
                            <h5 class="font-semibold text-yellow-800 mb-2">🏆 Mendukung Profesionalisme</h5>
                            <p class="text-yellow-700 text-sm">Memberikan pengalaman yang modern dan rapi dalam pengelolaan UKM, sejalan dengan semangat Benteng Merdeka untuk terus maju dan berprestasi.</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="text-center mt-8">
                <button onclick="closeAbout()" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- Contact Modal -->
    <div id="contactModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center">
                <div class="text-4xl mb-4">♔</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-6">Kontak UKM Benteng Merdeka</h3>
                
                <div class="space-y-4 mb-6">
                    <div class="bg-green-50 rounded-lg p-4">
                        <div class="flex items-center justify-center space-x-3 mb-2">
                            <span class="text-2xl">📱</span>
                            <span class="font-semibold text-gray-800">WhatsApp</span>
                        </div>
                        <a href="https://wa.me/6282196434417" target="_blank" class="text-green-600 font-medium hover:text-green-700 transition-colors">
                            082196434417
                        </a>
                    </div>
                    
                    <div class="bg-purple-50 rounded-lg p-4">
                        <div class="flex items-center justify-center space-x-3 mb-2">
                            <span class="text-2xl">📷</span>
                            <span class="font-semibold text-gray-800">Instagram</span>
                        </div>
                        <a href="https://instagram.com/benteng_merdeka" target="_blank" class="text-purple-600 font-medium hover:text-purple-700 transition-colors">
                            @benteng_merdeka
                        </a>
                    </div>
                </div>
                
                <button onclick="closeContact()" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- Add Member Modal -->
    <div id="addMemberModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">👤</div>
                <h3 class="text-2xl font-bold text-gray-800">Tambah Anggota Baru</h3>
            </div>
            <form onsubmit="handleAddMember(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Nama Lengkap</label>
                    <input type="text" id="memberName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan nama lengkap" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">NIM/NIS</label>
                    <input type="text" id="memberNim" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan NIM/NIS" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Email</label>
                    <input type="email" id="memberEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan email">
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-medium mb-2">No. Telepon</label>
                    <input type="tel" id="memberPhone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" placeholder="Masukkan no. telepon">
                </div>
                <div class="flex space-x-3">
                    <button type="submit" class="flex-1 gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                        Tambah Anggota
                    </button>
                    <button type="button" onclick="closeAddMember()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-colors">
                        Batal
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Member List Modal -->
    <div id="memberListModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-4xl w-full mx-4 fade-in max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">👥</div>
                <h3 class="text-2xl font-bold text-gray-800">Daftar Anggota UKM</h3>
            </div>
            
            <div class="mb-4">
                <input type="text" id="searchMember" placeholder="Cari anggota..." class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" onkeyup="searchMembers()">
            </div>
            
            <div class="overflow-x-auto">
                <table class="w-full text-sm">
                    <thead>
                        <tr class="border-b bg-gray-50">
                            <th class="text-left py-3 px-4">No</th>
                            <th class="text-left py-3 px-4">Nama</th>
                            <th class="text-left py-3 px-4">NIM/NIS</th>
                            <th class="text-left py-3 px-4">Email</th>
                            <th class="text-left py-3 px-4">Telepon</th>
                            <th class="text-left py-3 px-4">Aksi</th>
                        </tr>
                    </thead>
                    <tbody id="memberTableBody">
                        <!-- Member data will be populated here -->
                    </tbody>
                </table>
            </div>
            
            <div class="text-center mt-6">
                <button onclick="closeMemberList()" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- User Management Modal -->
    <div id="userManagementModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-4xl w-full mx-4 fade-in max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">🔐</div>
                <h3 class="text-2xl font-bold text-gray-800">Kelola Akun Pengguna</h3>
                <p class="text-gray-600">Atur akun login untuk admin, pengurus, dan anggota</p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-6 mb-6">
                <div class="bg-white border-2 border-gray-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-4 flex items-center">
                        <span class="text-2xl mr-2">👤</span>
                        Buat Akun Baru
                    </h4>
                    <form onsubmit="handleCreateUser(event)">
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-medium mb-2">Nama Lengkap</label>
                            <input type="text" id="newUserName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-medium mb-2">Username</label>
                            <input type="text" id="newUsername" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-medium mb-2">Password</label>
                            <div class="relative">
                                <input type="password" id="newPassword" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                                <button type="button" onclick="togglePasswordVisibility('newPassword')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                                    <svg id="newPassword-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                                    </svg>
                                    <svg id="newPassword-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                                    </svg>
                                </button>
                            </div>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-medium mb-2">Role</label>
                            <select id="newUserRole" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                                <option value="">Pilih Role</option>
                                <option value="admin">Admin ♔</option>
                                <option value="pengurus">Pengurus ♕</option>
                                <option value="anggota">Anggota ♙</option>
                            </select>
                        </div>
                        <button type="submit" class="w-full bg-green-600 hover:bg-green-700 text-white py-3 rounded-lg font-semibold transition-colors">
                            Buat Akun
                        </button>
                    </form>
                </div>
                
                <div class="bg-white border-2 border-gray-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-4 flex items-center">
                        <span class="text-2xl mr-2">🔍</span>
                        Cari & Edit Akun
                    </h4>
                    <div class="mb-4">
                        <input type="text" id="searchUser" placeholder="Cari username atau nama..." class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" onkeyup="searchUsers()">
                    </div>
                    <div id="userSearchResults" class="space-y-2 max-h-64 overflow-y-auto">
                        <!-- Search results will appear here -->
                    </div>
                </div>
            </div>
            
            <div class="bg-gray-50 rounded-xl p-6">
                <h4 class="text-lg font-semibold text-gray-800 mb-4 flex items-center">
                    <span class="text-2xl mr-2">📋</span>
                    Daftar Semua Akun
                </h4>
                <div class="overflow-x-auto">
                    <table class="w-full text-sm">
                        <thead>
                            <tr class="border-b bg-white">
                                <th class="text-left py-3 px-4">No</th>
                                <th class="text-left py-3 px-4">Nama</th>
                                <th class="text-left py-3 px-4">Username</th>
                                <th class="text-left py-3 px-4">Role</th>
                                <th class="text-left py-3 px-4">Status</th>
                                <th class="text-left py-3 px-4">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="userTableBody">
                            <!-- User data will be populated here -->
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div class="text-center mt-6">
                <button onclick="closeUserManagement()" class="w-full gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- Edit User Modal -->
    <div id="editUserModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">✏️</div>
                <h3 class="text-2xl font-bold text-gray-800">Edit Akun Pengguna</h3>
            </div>
            <form onsubmit="handleEditUser(event)">
                <input type="hidden" id="editUserId">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Nama Lengkap</label>
                    <input type="text" id="editUserName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Username</label>
                    <input type="text" id="editUsername" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Password Baru (kosongkan jika tidak diubah)</label>
                    <div class="relative">
                        <input type="password" id="editPassword" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400">
                        <button type="button" onclick="togglePasswordVisibility('editPassword')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                            <svg id="editPassword-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                            </svg>
                            <svg id="editPassword-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Role</label>
                    <select id="editUserRole" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                        <option value="admin">Admin ♔</option>
                        <option value="pengurus">Pengurus ♕</option>
                        <option value="anggota">Anggota ♙</option>
                    </select>
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Status</label>
                    <select id="editUserStatus" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400" required>
                        <option value="active">Aktif</option>
                        <option value="inactive">Nonaktif</option>
                    </select>
                </div>
                <div class="flex space-x-3">
                    <button type="submit" class="flex-1 gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                        Simpan Perubahan
                    </button>
                    <button type="button" onclick="closeEditUser()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-colors">
                        Batal
                    </button>
                </div>
            </form>
        </div>
    </div>



    <!-- Attendance Report Modal -->
    <div id="attendanceReportModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-6xl w-full mx-4 fade-in max-h-[95vh] overflow-y-auto">
            <div class="text-center mb-8">
                <div class="text-4xl mb-4">📊</div>
                <h3 id="reportTitle" class="text-3xl font-bold text-gray-800 mb-2">Laporan & Analisis Kehadiran</h3>
                <p id="reportSubtitle" class="text-gray-600">Dashboard analitik kehadiran UKM Catur Benteng Merdeka</p>
            </div>
            
            <!-- Filter Controls -->
            <div class="bg-gray-50 rounded-xl p-6 mb-8">
                <h4 class="text-lg font-semibold text-gray-800 mb-4">Filter Laporan</h4>
                <div class="grid md:grid-cols-5 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Role</label>
                        <select id="reportRole" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400" onchange="updateReport()">
                            <option value="all">Semua Role</option>
                            <option value="pengurus">♕ Pengurus</option>
                            <option value="anggota">♙ Anggota</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Periode</label>
                        <select id="reportPeriod" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400" onchange="updateReport()">
                            <option value="week">Minggu Ini</option>
                            <option value="month" selected>Bulan Ini</option>
                            <option value="quarter">3 Bulan Terakhir</option>
                            <option value="year">Tahun Ini</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Jenis Kegiatan</label>
                        <select id="reportEventType" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400" onchange="updateReport()">
                            <option value="all">Semua Kegiatan</option>
                            <option value="Latihan Rutin">Latihan Rutin</option>
                            <option value="Rapat">Rapat</option>
                            <option value="Turnamen">Turnamen</option>
                            <option value="Workshop">Workshop</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Status</label>
                        <select id="reportStatus" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400" onchange="updateReport()">
                            <option value="all">Semua Status</option>
                            <option value="hadir">Hadir</option>
                            <option value="tidak_hadir">Tidak Hadir</option>
                        </select>
                    </div>
                    <div class="flex items-end">
                        <button onclick="exportReport()" class="w-full bg-green-600 hover:bg-green-700 text-white py-2 px-4 rounded-lg font-medium transition-colors">
                            📥 Export Excel
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- Key Metrics -->
            <div class="grid md:grid-cols-4 gap-6 mb-8">
                <div class="bg-gradient-to-br from-blue-500 to-blue-600 rounded-xl p-6 text-white">
                    <div class="flex items-center justify-between mb-4">
                        <div class="text-3xl">👥</div>
                        <div class="text-right">
                            <div class="text-2xl font-bold" id="totalMembers">0</div>
                            <div class="text-sm opacity-90">Total Anggota</div>
                        </div>
                    </div>
                    <div class="text-xs opacity-75">Anggota terdaftar aktif</div>
                </div>
                
                <div class="bg-gradient-to-br from-green-500 to-green-600 rounded-xl p-6 text-white">
                    <div class="flex items-center justify-between mb-4">
                        <div class="text-3xl">✅</div>
                        <div class="text-right">
                            <div class="text-2xl font-bold" id="totalAttendance">0</div>
                            <div class="text-sm opacity-90">Total Kehadiran</div>
                        </div>
                    </div>
                    <div class="text-xs opacity-75">Periode yang dipilih</div>
                </div>
                
                <div class="bg-gradient-to-br from-yellow-500 to-orange-500 rounded-xl p-6 text-white">
                    <div class="flex items-center justify-between mb-4">
                        <div class="text-3xl">📊</div>
                        <div class="text-right">
                            <div class="text-2xl font-bold" id="avgAttendance">0%</div>
                            <div class="text-sm opacity-90">Rata-rata Kehadiran</div>
                        </div>
                    </div>
                    <div class="text-xs opacity-75">Persentase keseluruhan</div>
                </div>
                
                <div class="bg-gradient-to-br from-purple-500 to-purple-600 rounded-xl p-6 text-white">
                    <div class="flex items-center justify-between mb-4">
                        <div class="text-3xl">📅</div>
                        <div class="text-right">
                            <div class="text-2xl font-bold" id="totalEvents">0</div>
                            <div class="text-sm opacity-90">Total Kegiatan</div>
                        </div>
                    </div>
                    <div class="text-xs opacity-75">Kegiatan terlaksana</div>
                </div>
            </div>
            
            <!-- Charts Section -->
            <div class="grid md:grid-cols-2 gap-8 mb-8">
                <!-- Attendance Trend Chart -->
                <div class="bg-white border-2 border-gray-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                        <span class="text-2xl mr-3">📈</span>
                        Tren Kehadiran Bulanan
                    </h4>
                    <div class="relative h-64">
                        <canvas id="attendanceTrendChart" class="w-full h-full"></canvas>
                    </div>
                </div>
                
                <!-- Event Type Distribution -->
                <div class="bg-white border-2 border-gray-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                        <span class="text-2xl mr-3">🥧</span>
                        Distribusi Jenis Kegiatan
                    </h4>
                    <div class="relative h-64">
                        <canvas id="eventTypeChart" class="w-full h-full"></canvas>
                    </div>
                </div>
            </div>
            
            <!-- Attendance Rate by Member -->
            <div class="bg-white border-2 border-gray-200 rounded-xl p-6 mb-8">
                <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                    <span class="text-2xl mr-3">👤</span>
                    Tingkat Kehadiran per Anggota
                </h4>
                <div class="relative h-80">
                    <canvas id="memberAttendanceChart" class="w-full h-full"></canvas>
                </div>
            </div>
            
            <!-- Weekly Heatmap -->
            <div class="bg-white border-2 border-gray-200 rounded-xl p-6 mb-8">
                <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                    <span class="text-2xl mr-3">🔥</span>
                    Peta Panas Kehadiran Mingguan
                </h4>
                <div id="weeklyHeatmap" class="grid grid-cols-7 gap-2">
                    <!-- Heatmap will be generated here -->
                </div>
                <div class="flex justify-between items-center mt-4 text-sm text-gray-600">
                    <span>Rendah</span>
                    <div class="flex space-x-1">
                        <div class="w-3 h-3 bg-gray-200 rounded"></div>
                        <div class="w-3 h-3 bg-green-200 rounded"></div>
                        <div class="w-3 h-3 bg-green-400 rounded"></div>
                        <div class="w-3 h-3 bg-green-600 rounded"></div>
                        <div class="w-3 h-3 bg-green-800 rounded"></div>
                    </div>
                    <span>Tinggi</span>
                </div>
            </div>
            
            <!-- Top Performers -->
            <div class="grid md:grid-cols-2 gap-8 mb-8">
                <div class="bg-gradient-to-br from-green-50 to-emerald-50 border-2 border-green-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                        <span class="text-2xl mr-3">🏆</span>
                        Anggota Terbaik
                    </h4>
                    <div id="topPerformers" class="space-y-4">
                        <!-- Top performers will be listed here -->
                    </div>
                </div>
                
                <div class="bg-gradient-to-br from-blue-50 to-indigo-50 border-2 border-blue-200 rounded-xl p-6">
                    <h4 class="text-lg font-semibold text-gray-800 mb-6 flex items-center">
                        <span class="text-2xl mr-3">📋</span>
                        Ringkasan Statistik
                    </h4>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center p-3 bg-white rounded-lg">
                            <span class="font-medium">Kehadiran Tertinggi</span>
                            <span class="text-green-600 font-bold" id="highestAttendance">-</span>
                        </div>
                        <div class="flex justify-between items-center p-3 bg-white rounded-lg">
                            <span class="font-medium">Kehadiran Terendah</span>
                            <span class="text-red-600 font-bold" id="lowestAttendance">-</span>
                        </div>
                        <div class="flex justify-between items-center p-3 bg-white rounded-lg">
                            <span class="font-medium">Kegiatan Terpopuler</span>
                            <span class="text-blue-600 font-bold" id="popularEvent">-</span>
                        </div>
                        <div class="flex justify-between items-center p-3 bg-white rounded-lg">
                            <span class="font-medium">Hari Terbaik</span>
                            <span class="text-purple-600 font-bold" id="bestDay">-</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="text-center">
                <button onclick="closeAttendanceReport()" class="w-full md:w-auto px-8 py-3 gold-gradient text-black rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup Laporan
                </button>
            </div>
        </div>
    </div>

    <!-- WhatsApp Announcement Modal -->
    <div id="whatsappAnnouncementModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-2xl w-full mx-4 fade-in max-h-[90vh] overflow-y-auto">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">📢</div>
                <h3 class="text-2xl font-bold text-gray-800 mb-2">Pengumuman WhatsApp</h3>
                <p class="text-gray-600">Salin pesan di bawah untuk dikirim ke grup WhatsApp</p>
            </div>
            
            <div class="bg-green-50 border-2 border-green-200 rounded-xl p-6 mb-6">
                <div class="flex items-center justify-between mb-4">
                    <h4 class="text-lg font-semibold text-green-800 flex items-center">
                        <span class="text-2xl mr-2">💬</span>
                        Pesan Pengumuman
                    </h4>
                    <button onclick="copyAnnouncement()" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        📋 Salin Pesan
                    </button>
                </div>
                <textarea id="announcementText" class="w-full h-64 p-4 border border-green-300 rounded-lg resize-none bg-white text-gray-800 text-sm leading-relaxed" readonly></textarea>
            </div>
            
            <div class="grid md:grid-cols-2 gap-4 mb-6">
                <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
                    <h5 class="font-semibold text-blue-800 mb-2 flex items-center">
                        <span class="text-lg mr-2">📱</span>
                        Kirim via WhatsApp Web
                    </h5>
                    <p class="text-blue-700 text-sm mb-3">Buka WhatsApp Web dan kirim ke grup UKM</p>
                    <button onclick="openWhatsAppWeb()" class="w-full bg-blue-600 hover:bg-blue-700 text-white py-2 px-4 rounded-lg text-sm font-medium transition-colors">
                        Buka WhatsApp Web
                    </button>
                </div>
                
                <div class="bg-purple-50 border border-purple-200 rounded-lg p-4">
                    <h5 class="font-semibold text-purple-800 mb-2 flex items-center">
                        <span class="text-lg mr-2">📲</span>
                        Kirim via Mobile
                    </h5>
                    <p class="text-purple-700 text-sm mb-3">Salin pesan dan kirim melalui HP</p>
                    <button onclick="shareToMobile()" class="w-full bg-purple-600 hover:bg-purple-700 text-white py-2 px-4 rounded-lg text-sm font-medium transition-colors">
                        Bagikan ke Mobile
                    </button>
                </div>
            </div>
            
            <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4 mb-6">
                <h5 class="font-semibold text-yellow-800 mb-2 flex items-center">
                    <span class="text-lg mr-2">💡</span>
                    Tips Pengumuman
                </h5>
                <ul class="text-yellow-700 text-sm space-y-1">
                    <li>• Kirim pengumuman minimal H-1 sebelum kegiatan</li>
                    <li>• Tag @everyone untuk memastikan semua anggota melihat</li>
                    <li>• Sertakan reminder 2-3 jam sebelum kegiatan dimulai</li>
                    <li>• Konfirmasi kehadiran dengan meminta reply dari anggota</li>
                </ul>
            </div>
            
            <div class="text-center">
                <button onclick="closeWhatsAppAnnouncement()" class="w-full md:w-auto px-8 py-3 gold-gradient text-black rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                    Tutup
                </button>
            </div>
        </div>
    </div>

    <!-- Change Password Modal -->
    <div id="changePasswordModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">🔐</div>
                <h3 class="text-2xl font-bold text-gray-800">Ganti Password</h3>
                <p class="text-gray-600">Masukkan password lama dan password baru Anda</p>
            </div>
            <form onsubmit="handleChangePassword(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Password Lama</label>
                    <div class="relative">
                        <input type="password" id="oldPassword" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400 focus:border-transparent" placeholder="Masukkan password lama" required>
                        <button type="button" onclick="togglePasswordVisibility('oldPassword')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                            <svg id="oldPassword-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                            </svg>
                            <svg id="oldPassword-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Password Baru</label>
                    <div class="relative">
                        <input type="password" id="newPasswordChange" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400 focus:border-transparent" placeholder="Masukkan password baru" required minlength="6">
                        <button type="button" onclick="togglePasswordVisibility('newPasswordChange')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                            <svg id="newPasswordChange-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                            </svg>
                            <svg id="newPasswordChange-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Konfirmasi Password Baru</label>
                    <div class="relative">
                        <input type="password" id="confirmPassword" class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-400 focus:border-transparent" placeholder="Konfirmasi password baru" required minlength="6">
                        <button type="button" onclick="togglePasswordVisibility('confirmPassword')" class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-gray-600 transition-colors">
                            <svg id="confirmPassword-eye-open" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                            </svg>
                            <svg id="confirmPassword-eye-closed" class="w-5 h-5 hidden" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                            </svg>
                        </button>
                    </div>
                </div>
                <div id="passwordError" class="hidden mb-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded-lg text-sm">
                </div>
                <div class="bg-blue-50 border border-blue-200 rounded-lg p-3 mb-6">
                    <p class="text-blue-700 text-sm">
                        <span class="font-medium">💡 Tips Password Kuat:</span><br>
                        • Minimal 6 karakter<br>
                        • Kombinasi huruf dan angka<br>
                        • Hindari informasi pribadi<br>
                        • Jangan gunakan password yang sama dengan akun lain
                    </p>
                </div>
                <div class="flex space-x-3">
                    <button type="submit" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-semibold transition-colors">
                        Ganti Password
                    </button>
                    <button type="button" onclick="closeChangePassword()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-colors">
                        Batal
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Member Modal -->
    <div id="editMemberModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 fade-in">
            <div class="text-center mb-6">
                <div class="text-4xl mb-4">✏️</div>
                <h3 class="text-2xl font-bold text-gray-800">Edit Anggota</h3>
            </div>
            <form onsubmit="handleEditMember(event)">
                <input type="hidden" id="editMemberId">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Nama Lengkap</label>
                    <input type="text" id="editMemberName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">NIM/NIS</label>
                    <input type="text" id="editMemberNim" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-medium mb-2">Email</label>
                    <input type="email" id="editMemberEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent">
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-medium mb-2">No. Telepon</label>
                    <input type="tel" id="editMemberPhone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent">
                </div>
                <div class="flex space-x-3">
                    <button type="submit" class="flex-1 gold-gradient text-black py-3 rounded-lg font-semibold hover:from-yellow-500 hover:to-orange-600 transition-all">
                        Simpan Perubahan
                    </button>
                    <button type="button" onclick="closeEditMember()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-colors">
                        Batal
                    </button>
                </div>
            </form>
        </div>
    </div>

    <script>
        let currentUser = null;
        let currentUserData = null; // Store current logged-in user data
        let members = [];
        let nextMemberId = 1;

        let users = [
            { id: 1, name: 'Admin Utama', username: 'catur', password: 'admin', role: 'admin', status: 'active' }
        ];
        let nextUserId = 2;

        let schedules = [
            {
                id: 1,
                name: 'Rapat Pengurus Bulanan',
                datetime: '2024-12-20T19:00',
                type: 'Rapat',
                created: new Date().toISOString()
            },
            {
                id: 2,
                name: 'Latihan Rutin Mingguan',
                datetime: '2024-12-21T15:00',
                type: 'Latihan Rutin',
                created: new Date().toISOString()
            },
            {
                id: 3,
                name: 'Turnamen ELO Rating Internal',
                datetime: '2024-12-22T09:00',
                type: 'Turnamen',
                created: new Date().toISOString()
            }
        ];
        let nextScheduleId = 4;
        let currentQRData = null;

        // Data persistence functions
        function saveDataToStorage() {
            try {
                const data = {
                    members: members,
                    nextMemberId: nextMemberId,
                    users: users,
                    nextUserId: nextUserId,
                    schedules: schedules,
                    nextScheduleId: nextScheduleId,
                    attendanceData: attendanceData,
                    lastUpdated: new Date().toISOString()
                };
                localStorage.setItem('ukmCaturData', JSON.stringify(data));
                console.log('Data berhasil disimpan ke localStorage');
            } catch (error) {
                console.error('Error menyimpan data:', error);
            }
        }

        function loadDataFromStorage() {
            try {
                const savedData = localStorage.getItem('ukmCaturData');
                if (savedData) {
                    const data = JSON.parse(savedData);
                    
                    // Load all data arrays
                    members = data.members || [];
                    nextMemberId = data.nextMemberId || 1;
                    users = data.users || [{ id: 1, name: 'Admin Utama', username: 'catur', password: 'admin', role: 'admin', status: 'active' }];
                    nextUserId = data.nextUserId || 2;
                    schedules = data.schedules || [];
                    nextScheduleId = data.nextScheduleId || 1;
                    attendanceData = data.attendanceData || [];
                    
                    console.log('Data berhasil dimuat dari localStorage');
                    console.log('Total users:', users.length);
                    console.log('Total members:', members.length);
                    console.log('Total schedules:', schedules.length);
                    console.log('Total attendance:', attendanceData.length);
                    
                    // Update dashboard counts if admin dashboard is visible
                    if (document.getElementById('adminDashboard') && !document.getElementById('adminDashboard').classList.contains('hidden')) {
                        updateDashboardCounts();
                    }
                } else {
                    console.log('Tidak ada data tersimpan, menggunakan data default');
                    // Save default data
                    saveDataToStorage();
                }
            } catch (error) {
                console.error('Error memuat data:', error);
                // Reset to default if error
                users = [{ id: 1, name: 'Admin Utama', username: 'catur', password: 'admin', role: 'admin', status: 'active' }];
                members = [];
                schedules = [];
                attendanceData = [];
            }
        }

        function clearAllData() {
            if (confirm('⚠️ PERINGATAN!\n\nApakah Anda yakin ingin menghapus SEMUA data?\n\n• Semua akun pengguna (kecuali admin utama)\n• Semua data anggota\n• Semua jadwal kegiatan\n• Semua data kehadiran\n\nTindakan ini TIDAK DAPAT dibatalkan!')) {
                if (confirm('🔴 KONFIRMASI TERAKHIR\n\nSemua data akan hilang permanen!\nApakah Anda BENAR-BENAR yakin?')) {
                    // Reset to default data
                    users = [{ id: 1, name: 'Admin Utama', username: 'catur', password: 'admin', role: 'admin', status: 'active' }];
                    nextUserId = 2;
                    members = [];
                    nextMemberId = 1;
                    schedules = [];
                    nextScheduleId = 1;
                    attendanceData = [];
                    
                    // Save reset data
                    saveDataToStorage();
                    
                    // Update displays
                    updateDashboardCounts();
                    
                    alert('✅ Semua data berhasil dihapus!\n\nSistem telah direset ke kondisi awal.\nHanya tersisa akun admin utama (username: catur).');
                }
            }
        }

        // Initialize data on page load
        document.addEventListener('DOMContentLoaded', function() {
            loadDataFromStorage();
        });

        function showLoginSelection() {
            const modal = document.getElementById('loginSelectionModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeLoginSelection() {
            const modal = document.getElementById('loginSelectionModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function selectLoginType(userType) {
            closeLoginSelection();
            setTimeout(() => {
                showLogin(userType);
            }, 100);
        }

        function showLogin(userType) {
            const modal = document.getElementById('loginModal');
            const icon = document.getElementById('loginIcon');
            const title = document.getElementById('loginTitle');
            
            currentUser = userType;
            
            const userConfig = {
                admin: { icon: '♔', title: 'Login Admin' },
                pengurus: { icon: '♕', title: 'Login Pengurus' },
                anggota: { icon: '♙', title: 'Login Anggota' }
            };
            
            icon.textContent = userConfig[userType].icon;
            title.textContent = userConfig[userType].title;
            
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            // Auto focus on username field
            setTimeout(() => {
                document.getElementById('loginUsername').focus();
            }, 100);
        }

        function closeLogin() {
            const modal = document.getElementById('loginModal');
            const errorDiv = document.getElementById('loginError');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            errorDiv.classList.add('hidden');
            // Clear form inputs
            document.getElementById('loginUsername').value = '';
            document.getElementById('loginPassword').value = '';
        }

        function showLoginError(message) {
            const errorDiv = document.getElementById('loginError');
            errorDiv.textContent = message;
            errorDiv.classList.remove('hidden');
        }

        function handleUsernameKeypress(event) {
            if (event.key === 'Enter') {
                event.preventDefault();
                document.getElementById('loginPassword').focus();
            }
        }

        function handlePasswordKeypress(event) {
            if (event.key === 'Enter') {
                event.preventDefault();
                // Trigger form submission
                document.querySelector('#loginModal form').dispatchEvent(new Event('submit'));
            }
        }

        function handleLogin(event) {
            event.preventDefault();
            
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            
            // Find user in users array
            const user = users.find(u => u.username === username && u.password === password && u.role === currentUser && u.status === 'active');
            
            if (user) {
                // Store current user data
                currentUserData = user;
                
                // Update welcome message with user's name
                if (currentUser === 'pengurus') {
                    document.getElementById('pengurusWelcomeName').textContent = user.name;
                } else if (currentUser === 'anggota') {
                    document.getElementById('anggotaWelcomeName').textContent = user.name;
                }
                
                // Hide hero section and show dashboard
                document.getElementById('heroSection').style.display = 'none';
                document.getElementById('dashboardContent').classList.remove('hidden');
                
                // Show appropriate dashboard
                const dashboards = ['adminDashboard', 'pengurusDashboard', 'anggotaDashboard'];
                dashboards.forEach(id => document.getElementById(id).classList.add('hidden'));
                
                document.getElementById(currentUser + 'Dashboard').classList.remove('hidden');
                
                // Update dashboard counts if admin
                if (currentUser === 'admin') {
                    updateDashboardCounts();
                }
                
                closeLogin();
            } else {
                // Show error message
                showLoginError('Username atau password salah, atau akun tidak aktif!');
            }
        }

        function showAttendanceSchedule() {
            const modal = document.getElementById('attendanceScheduleModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            populateAttendanceSchedule();
        }

        function closeAttendanceSchedule() {
            const modal = document.getElementById('attendanceScheduleModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function populateAttendanceSchedule() {
            const container = document.getElementById('attendanceScheduleContent');
            container.innerHTML = '';
            
            if (schedules.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <div class="text-4xl mb-4">📅</div>
                        <p class="text-lg font-medium mb-2">Belum ada jadwal kegiatan</p>
                        <p class="text-sm">Jadwal akan muncul setelah admin membuat kegiatan baru</p>
                        <div class="mt-4 p-4 bg-blue-50 rounded-lg">
                            <p class="text-blue-700 text-sm">
                                💡 <strong>Info:</strong> Hubungi pengurus untuk informasi jadwal terbaru
                            </p>
                        </div>
                    </div>
                `;
                return;
            }
            
            // Filter schedules based on user role and event type
            const now = new Date();
            let filteredSchedules = schedules.filter(schedule => {
                const scheduleDate = new Date(schedule.datetime);
                const timeDiff = scheduleDate - now;
                const hoursDiff = timeDiff / (1000 * 60 * 60);
                const minutesDiff = timeDiff / (1000 * 60);
                
                // All events: show if within 5 minutes before start until event duration ends
                const eventDuration = getEventDurationHours(schedule.type);
                const isTimeValid = minutesDiff > -5 && hoursDiff < eventDuration;
                
                // Filter by user role and event type
                if (currentUser === 'anggota') {
                    // Anggota can only see non-meeting events
                    return isTimeValid && schedule.type !== 'Rapat';
                } else if (currentUser === 'pengurus') {
                    // Pengurus can see all events including meetings
                    return isTimeValid;
                } else {
                    // Admin can see all events (for testing purposes)
                    return isTimeValid;
                }
            });
            
            const activeSchedules = filteredSchedules.sort((a, b) => new Date(a.datetime) - new Date(b.datetime));
            
            if (activeSchedules.length === 0) {
                let emptyMessage = '';
                let emptyIcon = '⏰';
                let emptyTitle = 'Tidak ada kegiatan aktif';
                let emptyDescription = 'Semua kegiatan sudah berakhir atau belum waktunya absensi';
                let infoMessage = 'Absensi semua kegiatan: 5 menit sebelum dimulai hingga kegiatan selesai. Absensi setelah 5 menit kegiatan berjalan dianggap terlambat';
                
                if (currentUser === 'anggota') {
                    // Check if there are meetings that anggota cannot see
                    const hasOnlyMeetings = schedules.some(schedule => {
                        const scheduleDate = new Date(schedule.datetime);
                        const timeDiff = scheduleDate - now;
                        const hoursDiff = timeDiff / (1000 * 60 * 60);
                        const eventDuration = getEventDurationHours(schedule.type);
                        return hoursDiff > -eventDuration && schedule.type === 'Rapat';
                    });
                    
                    if (hasOnlyMeetings) {
                        emptyIcon = '👥';
                        emptyTitle = 'Tidak ada kegiatan untuk anggota';
                        emptyDescription = 'Saat ini hanya ada rapat pengurus yang sedang berlangsung';
                        infoMessage = 'Rapat pengurus khusus untuk pengurus saja. Kegiatan umum akan segera diinformasikan';
                    }
                }
                
                container.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <div class="text-4xl mb-4">${emptyIcon}</div>
                        <p class="text-lg font-medium mb-2">${emptyTitle}</p>
                        <p class="text-sm">${emptyDescription}</p>
                        <div class="mt-4 p-4 bg-yellow-50 rounded-lg">
                            <p class="text-yellow-700 text-sm">
                                📋 <strong>Catatan:</strong> ${infoMessage}
                            </p>
                        </div>
                    </div>
                `;
                return;
            }
            
            activeSchedules.forEach(schedule => {
                const scheduleDate = new Date(schedule.datetime);
                const timeDiff = scheduleDate - now;
                const hoursDiff = timeDiff / (1000 * 60 * 60);
                const minutesDiff = timeDiff / (1000 * 60);
                
                let status, statusClass, buttonText, buttonClass, canAttend;
                
                // Unified handling for all events - attendance starts 5 minutes before and ends after event duration
                const eventDuration = getEventDurationHours(schedule.type);
                
                if (minutesDiff > 5) {
                    status = '🔵 Belum Waktunya';
                    statusClass = 'bg-blue-100 text-blue-800';
                    buttonText = '⏰ Absensi 5 Menit Sebelum Dimulai';
                    buttonClass = 'bg-gray-400 text-white cursor-not-allowed';
                    canAttend = false;
                } else if (minutesDiff > -5) {
                    status = '🟢 Waktu Absensi';
                    statusClass = 'bg-green-100 text-green-800';
                    buttonText = '✋ Absen Sekarang';
                    buttonClass = 'bg-green-600 hover:bg-green-700 text-white';
                    canAttend = true;
                } else if (hoursDiff > -eventDuration) {
                    status = '🟠 Absensi Terlambat';
                    statusClass = 'bg-orange-100 text-orange-800';
                    buttonText = '✋ Absen Terlambat';
                    buttonClass = 'bg-orange-600 hover:bg-orange-700 text-white';
                    canAttend = true;
                } else {
                    status = '🔴 Sudah Berakhir';
                    statusClass = 'bg-red-100 text-red-800';
                    buttonText = '❌ Waktu Absensi Berakhir';
                    buttonClass = 'bg-gray-400 text-white cursor-not-allowed';
                    canAttend = false;
                }
                
                const scheduleDiv = document.createElement('div');
                const isMeeting = schedule.type === 'Rapat';
                const borderClass = isMeeting ? 'border-yellow-200' : canAttend ? 'border-green-200 shadow-lg' : 'border-gray-200';
                scheduleDiv.className = `bg-white border-2 rounded-xl p-6 ${borderClass}`;
                
                // Add role indicator for meetings
                const roleIndicator = isMeeting ? `
                    <div class="mb-3 p-2 bg-yellow-50 border border-yellow-200 rounded-lg">
                        <p class="text-yellow-800 text-sm font-medium flex items-center">
                            <span class="text-lg mr-2">♕</span>
                            Khusus Pengurus - Rapat Internal
                        </p>
                    </div>
                ` : '';
                
                scheduleDiv.innerHTML = `
                    ${roleIndicator}
                    <div class="flex justify-between items-start mb-4">
                        <div class="flex-1">
                            <h4 class="text-lg font-semibold text-gray-800 mb-2">${schedule.name}</h4>
                            <div class="space-y-2 text-sm text-gray-600">
                                <p><span class="font-medium">📅 Waktu:</span> ${scheduleDate.toLocaleString('id-ID')}</p>
                                <p><span class="font-medium">📋 Jenis:</span> ${schedule.type}</p>
                                <p><span class="font-medium">⏱️ Durasi:</span> ${getEventDuration(schedule.type)}</p>
                                <p><span class="font-medium">📍 Tempat:</span> ${getEventLocation(schedule.type)}</p>
                            </div>
                        </div>
                        <div class="flex flex-col space-y-2 ml-4">
                            <span class="px-3 py-1 rounded-full text-xs font-medium ${statusClass}">
                                ${status}
                            </span>
                            ${Math.abs(hoursDiff) < 1 ? `
                                <div class="text-xs text-center">
                                    <div class="font-medium text-gray-700">
                                        ${hoursDiff > 0 ? 'Dimulai dalam:' : 'Berakhir:'}
                                    </div>
                                    <div class="text-gray-600" id="countdown-${schedule.id}">
                                        ${Math.abs(Math.round(hoursDiff * 60))} menit
                                    </div>
                                </div>
                            ` : ''}
                        </div>
                    </div>
                    
                    <div class="mb-4 p-3 bg-gray-50 rounded-lg">
                        <p class="text-sm text-gray-700">
                            <span class="font-medium">💡 Info:</span> ${getEventInfo(schedule.type)}
                        </p>
                        <div class="mt-2 p-2 bg-blue-50 border border-blue-200 rounded-lg">
                            <p class="text-xs text-blue-700">
                                ⏰ <strong>Waktu Absensi:</strong> 5 menit sebelum dimulai hingga kegiatan selesai. Absensi setelah 5 menit kegiatan berjalan dianggap terlambat.
                            </p>
                        </div>
                    </div>
                    
                    <button 
                        onclick="${canAttend ? `attendEvent(${schedule.id})` : 'void(0)'}" 
                        class="w-full ${buttonClass} py-3 px-4 rounded-lg text-sm font-medium transition-colors ${canAttend ? 'transform hover:scale-105' : ''}"
                        ${!canAttend ? 'disabled' : ''}
                    >
                        ${buttonText}
                    </button>
                    
                    ${canAttend && minutesDiff < -5 ? `
                        <div class="mt-2 p-2 bg-yellow-50 border border-yellow-200 rounded-lg">
                            <p class="text-xs text-yellow-700 text-center">
                                ⚠️ Absensi terlambat akan dicatat dengan keterangan keterlambatan
                            </p>
                        </div>
                    ` : ''}
                `;
                container.appendChild(scheduleDiv);
            });
        }

        function getEventDuration(eventType) {
            const durations = {
                'Latihan Rutin': '2-3 jam',
                'Rapat': '1-2 jam',
                'Turnamen': '4-6 jam',
                'Workshop': '3-4 jam',
                'Pertandingan': '2-4 jam'
            };
            return durations[eventType] || '2 jam';
        }

        function getEventDurationHours(eventType) {
            const durations = {
                'Latihan Rutin': 3,
                'Rapat': 2,
                'Turnamen': 6,
                'Workshop': 4,
                'Pertandingan': 4
            };
            return durations[eventType] || 2;
        }

        function getEventLocation(eventType) {
            const locations = {
                'Latihan Rutin': 'Sekret UKM Benteng Merdeka',
                'Rapat': 'Sekret UKM Benteng Merdeka',
                'Turnamen': 'Aula UKM Benteng Merdeka',
                'Workshop': 'Aula UKM Benteng Merdeka',
                'Pertandingan': 'Venue Eksternal'
            };
            return locations[eventType] || 'Sekret UKM';
        }

        function getEventInfo(eventType) {
            const infos = {
                'Latihan Rutin': 'Bawa papan catur dan buku catatan. Latihan terbuka untuk semua level.',
                'Rapat': 'Khusus pengurus. Bawa laptop dan catatan rapat sebelumnya.',
                'Turnamen': 'Daftar ulang 30 menit sebelum dimulai. Bawa KTM dan alat tulis.',
                'Workshop': 'Terbuka untuk semua anggota. Sertifikat akan diberikan.',
                'Pertandingan': 'Dukungan untuk tim UKM. Pakai seragam atau atribut UKM.'
            };
            return infos[eventType] || 'Informasi lebih lanjut akan disampaikan saat kegiatan.';
        }

        function simulateScan() {
            closeScanner();
            
            // Show success modal
            const successModal = document.getElementById('successModal');
            const timeElement = document.getElementById('attendanceTime');
            
            const now = new Date();
            timeElement.textContent = now.toLocaleTimeString('id-ID') + ' WIB';
            
            successModal.classList.remove('hidden');
            successModal.classList.add('flex');
        }

        function manualAttendance() {
            const now = new Date();
            const timeElement = document.getElementById('attendanceTime');
            timeElement.textContent = now.toLocaleTimeString('id-ID') + ' WIB';
            
            const successModal = document.getElementById('successModal');
            successModal.classList.remove('hidden');
            successModal.classList.add('flex');
        }

        function closeSuccess() {
            const modal = document.getElementById('successModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function showAbout() {
            const modal = document.getElementById('aboutModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeAbout() {
            const modal = document.getElementById('aboutModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function showContact() {
            const modal = document.getElementById('contactModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeContact() {
            const modal = document.getElementById('contactModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function goHome() {
            // Show hero section and hide dashboard
            document.getElementById('heroSection').style.display = 'block';
            document.getElementById('dashboardContent').classList.add('hidden');
            
            // Hide all dashboards
            const dashboards = ['adminDashboard', 'pengurusDashboard', 'anggotaDashboard'];
            dashboards.forEach(id => document.getElementById(id).classList.add('hidden'));
            
            // Reset welcome names to default
            document.getElementById('pengurusWelcomeName').textContent = 'Pengurus';
            document.getElementById('anggotaWelcomeName').textContent = 'Anggota';
            
            // Reset current user
            currentUser = null;
            currentUserData = null;
        }

        // Password Change Functions
        function showChangePassword() {
            const modal = document.getElementById('changePasswordModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            // Clear form
            document.getElementById('oldPassword').value = '';
            document.getElementById('newPasswordChange').value = '';
            document.getElementById('confirmPassword').value = '';
            document.getElementById('passwordError').classList.add('hidden');
        }

        function closeChangePassword() {
            const modal = document.getElementById('changePasswordModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function showPasswordError(message) {
            const errorDiv = document.getElementById('passwordError');
            errorDiv.textContent = message;
            errorDiv.classList.remove('hidden');
        }

        function handleChangePassword(event) {
            event.preventDefault();
            
            const oldPassword = document.getElementById('oldPassword').value;
            const newPassword = document.getElementById('newPasswordChange').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            
            // Validate current user is logged in
            if (!currentUserData) {
                showPasswordError('Sesi login tidak valid. Silakan login ulang.');
                return;
            }
            
            // Validate old password
            if (oldPassword !== currentUserData.password) {
                showPasswordError('Password lama tidak sesuai!');
                return;
            }
            
            // Validate new password length
            if (newPassword.length < 6) {
                showPasswordError('Password baru minimal 6 karakter!');
                return;
            }
            
            // Validate password confirmation
            if (newPassword !== confirmPassword) {
                showPasswordError('Konfirmasi password tidak sesuai!');
                return;
            }
            
            // Validate new password is different from old password
            if (newPassword === oldPassword) {
                showPasswordError('Password baru harus berbeda dari password lama!');
                return;
            }
            
            // Update password in users array
            const userIndex = users.findIndex(u => u.id === currentUserData.id);
            if (userIndex !== -1) {
                users[userIndex].password = newPassword;
                currentUserData.password = newPassword; // Update current user data
                
                // Save data to localStorage
                saveDataToStorage();
                
                closeChangePassword();
                
                // Show success message
                alert('✅ Password berhasil diubah dan disimpan!\n\n🔐 Password baru Anda telah tersimpan dengan aman.\n\n💡 Jangan lupa untuk mengingat password baru Anda dan jangan bagikan kepada orang lain.');
                
                console.log('Password changed successfully for user:', currentUserData.name);
            } else {
                showPasswordError('Terjadi kesalahan sistem. Silakan coba lagi.');
            }
        }

        function toggleMobileMenu() {
            const mobileMenu = document.getElementById('mobileMenu');
            const hamburgerIcon = document.getElementById('hamburgerIcon');
            const closeIcon = document.getElementById('closeIcon');
            
            if (mobileMenu.classList.contains('hidden')) {
                mobileMenu.classList.remove('hidden');
                hamburgerIcon.classList.add('hidden');
                closeIcon.classList.remove('hidden');
            } else {
                mobileMenu.classList.add('hidden');
                hamburgerIcon.classList.remove('hidden');
                closeIcon.classList.add('hidden');
            }
        }

        function closeMobileMenu() {
            const mobileMenu = document.getElementById('mobileMenu');
            const hamburgerIcon = document.getElementById('hamburgerIcon');
            const closeIcon = document.getElementById('closeIcon');
            
            mobileMenu.classList.add('hidden');
            hamburgerIcon.classList.remove('hidden');
            closeIcon.classList.add('hidden');
        }

        // Member Management Functions
        function showAddMember() {
            const modal = document.getElementById('addMemberModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeAddMember() {
            const modal = document.getElementById('addMemberModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            // Clear form
            document.getElementById('memberName').value = '';
            document.getElementById('memberNim').value = '';
            document.getElementById('memberEmail').value = '';
            document.getElementById('memberPhone').value = '';
        }

        function handleAddMember(event) {
            event.preventDefault();
            
            const name = document.getElementById('memberName').value;
            const nim = document.getElementById('memberNim').value;
            const email = document.getElementById('memberEmail').value;
            const phone = document.getElementById('memberPhone').value;
            
            // Add new member to array
            members.push({
                id: nextMemberId++,
                name: name,
                nim: nim,
                email: email,
                phone: phone
            });
            
            // Save data to localStorage
            saveDataToStorage();
            
            closeAddMember();
            
            // Show success message
            alert('Anggota baru berhasil ditambahkan dan disimpan!');
        }

        function showMemberList() {
            const modal = document.getElementById('memberListModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            // Populate member table
            populateMemberTable();
        }

        function closeMemberList() {
            const modal = document.getElementById('memberListModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function populateMemberTable() {
            const tbody = document.getElementById('memberTableBody');
            tbody.innerHTML = '';
            
            members.forEach((member, index) => {
                const row = document.createElement('tr');
                row.className = 'border-b hover:bg-gray-50';
                row.innerHTML = `
                    <td class="py-3 px-4">${index + 1}</td>
                    <td class="py-3 px-4 font-medium">${member.name}</td>
                    <td class="py-3 px-4">${member.nim}</td>
                    <td class="py-3 px-4">${member.email}</td>
                    <td class="py-3 px-4">${member.phone}</td>
                    <td class="py-3 px-4">
                        <div class="flex space-x-2">
                            <button onclick="editMember(${member.id})" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Edit
                            </button>
                            <button onclick="deleteMember(${member.id})" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Hapus
                            </button>
                        </div>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function searchMembers() {
            const searchTerm = document.getElementById('searchMember').value.toLowerCase();
            const tbody = document.getElementById('memberTableBody');
            tbody.innerHTML = '';
            
            const filteredMembers = members.filter(member => 
                member.name.toLowerCase().includes(searchTerm) ||
                member.nim.toLowerCase().includes(searchTerm) ||
                member.email.toLowerCase().includes(searchTerm)
            );
            
            filteredMembers.forEach((member, index) => {
                const row = document.createElement('tr');
                row.className = 'border-b hover:bg-gray-50';
                row.innerHTML = `
                    <td class="py-3 px-4">${index + 1}</td>
                    <td class="py-3 px-4 font-medium">${member.name}</td>
                    <td class="py-3 px-4">${member.nim}</td>
                    <td class="py-3 px-4">${member.email}</td>
                    <td class="py-3 px-4">${member.phone}</td>
                    <td class="py-3 px-4">
                        <div class="flex space-x-2">
                            <button onclick="editMember(${member.id})" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Edit
                            </button>
                            <button onclick="deleteMember(${member.id})" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Hapus
                            </button>
                        </div>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function editMember(memberId) {
            const member = members.find(m => m.id === memberId);
            if (!member) return;
            
            // Fill edit form
            document.getElementById('editMemberId').value = member.id;
            document.getElementById('editMemberName').value = member.name;
            document.getElementById('editMemberNim').value = member.nim;
            document.getElementById('editMemberEmail').value = member.email;
            document.getElementById('editMemberPhone').value = member.phone;
            
            // Show edit modal
            const modal = document.getElementById('editMemberModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeEditMember() {
            const modal = document.getElementById('editMemberModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function handleEditMember(event) {
            event.preventDefault();
            
            const memberId = parseInt(document.getElementById('editMemberId').value);
            const name = document.getElementById('editMemberName').value;
            const nim = document.getElementById('editMemberNim').value;
            const email = document.getElementById('editMemberEmail').value;
            const phone = document.getElementById('editMemberPhone').value;
            
            // Update member in array
            const memberIndex = members.findIndex(m => m.id === memberId);
            if (memberIndex !== -1) {
                members[memberIndex] = {
                    id: memberId,
                    name: name,
                    nim: nim,
                    email: email,
                    phone: phone
                };
            }
            
            // Save data to localStorage
            saveDataToStorage();
            
            closeEditMember();
            populateMemberTable(); // Refresh the table
            
            // Show success message
            alert('Data anggota berhasil diperbarui dan disimpan!');
        }

        function deleteMember(memberId) {
            if (confirm('Apakah Anda yakin ingin menghapus anggota ini?')) {
                members = members.filter(m => m.id !== memberId);
                
                // Save data to localStorage
                saveDataToStorage();
                
                populateMemberTable(); // Refresh the table
                alert('Anggota berhasil dihapus dan disimpan!');
            }
        }

        // User Management Functions
        function showUserManagement() {
            const modal = document.getElementById('userManagementModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            populateUserTable();
        }

        function closeUserManagement() {
            const modal = document.getElementById('userManagementModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            // Clear forms
            document.getElementById('newUserName').value = '';
            document.getElementById('newUsername').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('newUserRole').value = '';
            document.getElementById('searchUser').value = '';
            document.getElementById('userSearchResults').innerHTML = '';
        }

        function handleCreateUser(event) {
            event.preventDefault();
            
            const name = document.getElementById('newUserName').value;
            const username = document.getElementById('newUsername').value;
            const password = document.getElementById('newPassword').value;
            const role = document.getElementById('newUserRole').value;
            
            // Check if username already exists
            if (users.find(u => u.username === username)) {
                alert('Username sudah digunakan! Pilih username lain.');
                return;
            }
            
            // Add new user
            users.push({
                id: nextUserId++,
                name: name,
                username: username,
                password: password,
                role: role,
                status: 'active'
            });
            
            // Save data to localStorage
            saveDataToStorage();
            
            // Clear form
            document.getElementById('newUserName').value = '';
            document.getElementById('newUsername').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('newUserRole').value = '';
            
            // Refresh table
            populateUserTable();
            updateDashboardCounts();
            
            alert('Akun baru berhasil dibuat dan disimpan!');
        }

        function populateUserTable() {
            const tbody = document.getElementById('userTableBody');
            tbody.innerHTML = '';
            
            users.forEach((user, index) => {
                const roleIcons = {
                    admin: '♔',
                    pengurus: '♕',
                    anggota: '♙'
                };
                
                const statusBadge = user.status === 'active' 
                    ? '<span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">Aktif</span>'
                    : '<span class="bg-red-100 text-red-800 px-2 py-1 rounded-full text-xs">Nonaktif</span>';
                
                const row = document.createElement('tr');
                row.className = 'border-b hover:bg-gray-50';
                row.innerHTML = `
                    <td class="py-3 px-4">${index + 1}</td>
                    <td class="py-3 px-4 font-medium">${user.name}</td>
                    <td class="py-3 px-4">${user.username}</td>
                    <td class="py-3 px-4">${roleIcons[user.role]} ${user.role.charAt(0).toUpperCase() + user.role.slice(1)}</td>
                    <td class="py-3 px-4">${statusBadge}</td>
                    <td class="py-3 px-4">
                        <div class="flex space-x-2">
                            <button onclick="editUser(${user.id})" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Edit
                            </button>
                            <button onclick="toggleUserStatus(${user.id})" class="bg-yellow-500 hover:bg-yellow-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                ${user.status === 'active' ? 'Nonaktifkan' : 'Aktifkan'}
                            </button>
                            <button onclick="deleteUser(${user.id})" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-xs transition-colors">
                                Hapus
                            </button>
                        </div>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Update dashboard counts
            updateDashboardCounts();
        }

        function updateDashboardCounts() {
            // Count active users by role
            const activeAnggota = users.filter(u => u.role === 'anggota' && u.status === 'active').length;
            const activePengurus = users.filter(u => u.role === 'pengurus' && u.status === 'active').length;
            
            // Update the dashboard display
            const anggotaCountElement = document.getElementById('totalAnggotaCount');
            const pengurusCountElement = document.getElementById('totalPengurusCount');
            
            if (anggotaCountElement) {
                anggotaCountElement.textContent = activeAnggota;
            }
            if (pengurusCountElement) {
                pengurusCountElement.textContent = activePengurus;
            }
        }

        function searchUsers() {
            const searchTerm = document.getElementById('searchUser').value.toLowerCase();
            const resultsDiv = document.getElementById('userSearchResults');
            
            if (searchTerm.length < 2) {
                resultsDiv.innerHTML = '<p class="text-gray-500 text-sm">Ketik minimal 2 karakter untuk mencari...</p>';
                return;
            }
            
            const filteredUsers = users.filter(user => 
                user.name.toLowerCase().includes(searchTerm) ||
                user.username.toLowerCase().includes(searchTerm)
            );
            
            if (filteredUsers.length === 0) {
                resultsDiv.innerHTML = '<p class="text-gray-500 text-sm">Tidak ada hasil ditemukan.</p>';
                return;
            }
            
            resultsDiv.innerHTML = '';
            filteredUsers.forEach(user => {
                const roleIcons = {
                    admin: '♔',
                    pengurus: '♕',
                    anggota: '♙'
                };
                
                const statusColor = user.status === 'active' ? 'text-green-600' : 'text-red-600';
                
                const userDiv = document.createElement('div');
                userDiv.className = 'bg-white border rounded-lg p-3 hover:bg-gray-50 cursor-pointer';
                userDiv.innerHTML = `
                    <div class="flex justify-between items-center">
                        <div>
                            <p class="font-medium">${user.name}</p>
                            <p class="text-sm text-gray-600">${roleIcons[user.role]} ${user.username} - ${user.role}</p>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="editUser(${user.id})" class="bg-blue-500 hover:bg-blue-600 text-white px-2 py-1 rounded text-xs">
                                Edit
                            </button>
                        </div>
                    </div>
                `;
                resultsDiv.appendChild(userDiv);
            });
        }

        function editUser(userId) {
            const user = users.find(u => u.id === userId);
            if (!user) return;
            
            // Fill edit form
            document.getElementById('editUserId').value = user.id;
            document.getElementById('editUserName').value = user.name;
            document.getElementById('editUsername').value = user.username;
            document.getElementById('editPassword').value = '';
            document.getElementById('editUserRole').value = user.role;
            document.getElementById('editUserStatus').value = user.status;
            
            // Show edit modal
            const modal = document.getElementById('editUserModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeEditUser() {
            const modal = document.getElementById('editUserModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function handleEditUser(event) {
            event.preventDefault();
            
            const userId = parseInt(document.getElementById('editUserId').value);
            const name = document.getElementById('editUserName').value;
            const username = document.getElementById('editUsername').value;
            const password = document.getElementById('editPassword').value;
            const role = document.getElementById('editUserRole').value;
            const status = document.getElementById('editUserStatus').value;
            
            // Check if username already exists (excluding current user)
            if (users.find(u => u.username === username && u.id !== userId)) {
                alert('Username sudah digunakan! Pilih username lain.');
                return;
            }
            
            // Update user in array
            const userIndex = users.findIndex(u => u.id === userId);
            if (userIndex !== -1) {
                users[userIndex] = {
                    id: userId,
                    name: name,
                    username: username,
                    password: password || users[userIndex].password, // Keep old password if not changed
                    role: role,
                    status: status
                };
            }
            
            // Save data to localStorage
            saveDataToStorage();
            
            closeEditUser();
            populateUserTable();
            updateDashboardCounts();
            
            alert('Akun berhasil diperbarui dan disimpan!');
        }

        function toggleUserStatus(userId) {
            const user = users.find(u => u.id === userId);
            if (!user) return;
            
            const newStatus = user.status === 'active' ? 'inactive' : 'active';
            const action = newStatus === 'active' ? 'mengaktifkan' : 'menonaktifkan';
            
            if (confirm(`Apakah Anda yakin ingin ${action} akun ${user.name}?`)) {
                user.status = newStatus;
                
                // Save data to localStorage
                saveDataToStorage();
                
                populateUserTable();
                updateDashboardCounts();
                alert(`Akun ${user.name} berhasil ${newStatus === 'active' ? 'diaktifkan' : 'dinonaktifkan'} dan disimpan!`);
            }
        }

        function deleteUser(userId) {
            const user = users.find(u => u.id === userId);
            if (!user) {
                alert('❌ Akun tidak ditemukan!');
                return;
            }
            
            // Prevent deletion of main admin account
            if (user.username === 'catur') {
                alert('🚫 Akun admin utama tidak dapat dihapus!\n\nAkun "catur" adalah akun sistem yang harus tetap ada untuk menjaga keamanan sistem.');
                return;
            }
            
            // Prevent deletion of currently logged in user
            if (currentUserData && currentUserData.id === userId) {
                alert('⚠️ Anda tidak dapat menghapus akun yang sedang digunakan!\n\nSilakan logout terlebih dahulu atau gunakan akun admin lain untuk menghapus akun ini.');
                return;
            }
            
            // Show detailed confirmation dialog
            const roleIcon = user.role === 'admin' ? '♔' : user.role === 'pengurus' ? '♕' : '♙';
            const confirmMessage = `🗑️ KONFIRMASI PENGHAPUSAN AKUN\n\n` +
                                 `👤 Nama: ${user.name}\n` +
                                 `🔑 Username: ${user.username}\n` +
                                 `${roleIcon} Role: ${user.role.charAt(0).toUpperCase() + user.role.slice(1)}\n` +
                                 `📊 Status: ${user.status === 'active' ? 'Aktif' : 'Nonaktif'}\n\n` +
                                 `⚠️ PERINGATAN:\n` +
                                 `• Akun akan dihapus secara permanen\n` +
                                 `• Data login akan hilang selamanya\n` +
                                 `• Riwayat aktivitas akan tetap tersimpan\n` +
                                 `• Tindakan ini TIDAK DAPAT dibatalkan\n\n` +
                                 `Apakah Anda yakin ingin menghapus akun ini?`;
            
            if (confirm(confirmMessage)) {
                // Double confirmation for admin accounts
                if (user.role === 'admin') {
                    const doubleConfirm = confirm(`🔴 KONFIRMASI KEDUA - AKUN ADMIN\n\n` +
                                                `Anda akan menghapus akun ADMIN "${user.name}".\n` +
                                                `Akun admin memiliki akses penuh ke sistem.\n\n` +
                                                `Apakah Anda BENAR-BENAR yakin?`);
                    
                    if (!doubleConfirm) {
                        alert('❌ Penghapusan akun dibatalkan.');
                        return;
                    }
                }
                
                // Check if there will be at least one admin left
                const adminCount = users.filter(u => u.role === 'admin' && u.status === 'active').length;
                if (user.role === 'admin' && user.status === 'active' && adminCount <= 1) {
                    alert('🚫 Tidak dapat menghapus akun admin!\n\n' +
                          'Sistem harus memiliki minimal 1 akun admin aktif.\n' +
                          'Silakan buat akun admin baru terlebih dahulu atau aktifkan akun admin lain sebelum menghapus akun ini.');
                    return;
                }
                
                // Store user info for success message
                const deletedUserInfo = {
                    name: user.name,
                    username: user.username,
                    role: user.role
                };
                
                // Remove user from array
                users = users.filter(u => u.id !== userId);
                
                // Save data to localStorage
                saveDataToStorage();
                
                // Refresh the user table
                populateUserTable();
                updateDashboardCounts();
                
                // Clear search results if any
                document.getElementById('searchUser').value = '';
                document.getElementById('userSearchResults').innerHTML = '';
                
                // Show detailed success message
                const roleText = deletedUserInfo.role === 'admin' ? 'Admin ♔' : 
                               deletedUserInfo.role === 'pengurus' ? 'Pengurus ♕' : 'Anggota ♙';
                
                alert(`✅ Akun berhasil dihapus!\n\n` +
                      `👤 Nama: ${deletedUserInfo.name}\n` +
                      `🔑 Username: ${deletedUserInfo.username}\n` +
                      `${roleText}\n\n` +
                      `📊 Status sistem:\n` +
                      `• Total akun tersisa: ${users.length}\n` +
                      `• Admin aktif: ${users.filter(u => u.role === 'admin' && u.status === 'active').length}\n` +
                      `• Pengurus aktif: ${users.filter(u => u.role === 'pengurus' && u.status === 'active').length}\n` +
                      `• Anggota aktif: ${users.filter(u => u.role === 'anggota' && u.status === 'active').length}`);
                
                console.log('User deleted successfully:', deletedUserInfo);
                console.log('Remaining users:', users.length);
            } else {
                alert('❌ Penghapusan akun dibatalkan.');
            }
        }

        // Schedule and QR Code Management Functions
        function createSchedule(event) {
            event.preventDefault();
            
            const eventName = document.getElementById('eventName').value;
            const eventDateTime = document.getElementById('eventDateTime').value;
            const eventType = document.getElementById('eventType').value;
            
            // Create new schedule
            const schedule = {
                id: nextScheduleId++,
                name: eventName,
                datetime: eventDateTime,
                type: eventType,
                created: new Date().toISOString()
            };
            
            schedules.push(schedule);
            
            // Save data to localStorage
            saveDataToStorage();
            
            // Clear form
            document.getElementById('eventName').value = '';
            document.getElementById('eventDateTime').value = '';
            document.getElementById('eventType').value = '';
            
            // Generate and show WhatsApp announcement
            generateWhatsAppAnnouncement(schedule);
        }



        function showActiveSchedules() {
            const modal = document.getElementById('activeSchedulesModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            populateSchedulesList();
        }

        function closeActiveSchedules() {
            const modal = document.getElementById('activeSchedulesModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function populateSchedulesList() {
            const container = document.getElementById('schedulesList');
            container.innerHTML = '';
            
            console.log('Populating schedules list. Total schedules:', schedules.length);
            console.log('Schedules data:', schedules);
            
            if (schedules.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <div class="text-4xl mb-4">📅</div>
                        <p>Belum ada jadwal yang dibuat</p>
                        <p class="text-sm">Buat jadwal baru dari dashboard admin</p>
                    </div>
                `;
                return;
            }
            
            schedules.forEach(schedule => {
                const scheduleDate = new Date(schedule.datetime);
                const now = new Date();
                const isActive = scheduleDate > now;
                
                const scheduleDiv = document.createElement('div');
                scheduleDiv.className = `bg-white border-2 rounded-xl p-6 ${isActive ? 'border-green-200' : 'border-gray-200'}`;
                scheduleDiv.innerHTML = `
                    <div class="flex justify-between items-start mb-4">
                        <div class="flex-1">
                            <h4 class="text-lg font-semibold text-gray-800 mb-2">${schedule.name}</h4>
                            <div class="space-y-1 text-sm text-gray-600">
                                <p><span class="font-medium">📅 Waktu:</span> ${scheduleDate.toLocaleString('id-ID')}</p>
                                <p><span class="font-medium">📋 Jenis:</span> ${schedule.type}</p>
                                <p><span class="font-medium">🕒 Dibuat:</span> ${new Date(schedule.created).toLocaleString('id-ID')}</p>
                            </div>
                        </div>
                        <div class="flex flex-col space-y-2 ml-4">
                            <span class="px-3 py-1 rounded-full text-xs font-medium ${isActive ? 'bg-green-100 text-green-800' : 'bg-gray-100 text-gray-600'}">
                                ${isActive ? '🟢 Aktif' : '🔴 Berakhir'}
                            </span>
                        </div>
                    </div>
                    
                    <div class="flex space-x-2">
                        <button onclick="viewScheduleQR(${schedule.id})" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-2 px-4 rounded-lg text-sm font-medium transition-colors">
                            📱 Lihat QR Code
                        </button>
                        <button onclick="duplicateSchedule(${schedule.id})" class="flex-1 bg-green-600 hover:bg-green-700 text-white py-2 px-4 rounded-lg text-sm font-medium transition-colors">
                            📋 Duplikat
                        </button>
                        <button onclick="deleteSchedule(${schedule.id})" class="flex-1 bg-red-600 hover:bg-red-700 text-white py-2 px-4 rounded-lg text-sm font-medium transition-colors">
                            🗑️ Hapus
                        </button>
                    </div>
                `;
                container.appendChild(scheduleDiv);
            });
        }

        function duplicateSchedule(scheduleId) {
            const schedule = schedules.find(s => s.id === scheduleId);
            if (!schedule) return;
            
            const newSchedule = {
                id: nextScheduleId++,
                name: schedule.name + ' (Copy)',
                datetime: schedule.datetime,
                type: schedule.type,
                created: new Date().toISOString(),
                qrCode: generateQRData(schedule.name + ' (Copy)', schedule.datetime, schedule.type)
            };
            
            schedules.push(newSchedule);
            populateSchedulesList();
            alert('Jadwal berhasil diduplikat!');
        }

        function viewScheduleQR(scheduleId) {
            const schedule = schedules.find(s => s.id === scheduleId);
            if (!schedule) {
                alert('Jadwal tidak ditemukan!');
                return;
            }
            
            // Close active schedules modal first
            closeActiveSchedules();
            
            // Then show QR code modal
            setTimeout(() => {
                showQRCode(schedule);
            }, 100);
        }

        function deleteSchedule(scheduleId) {
            const schedule = schedules.find(s => s.id === scheduleId);
            if (!schedule) {
                alert('Jadwal tidak ditemukan!');
                return;
            }
            
            if (confirm(`Apakah Anda yakin ingin menghapus jadwal "${schedule.name}"?\n\nTindakan ini tidak dapat dibatalkan.`)) {
                // Remove schedule from array
                schedules = schedules.filter(s => s.id !== scheduleId);
                
                // Refresh the schedules list
                populateSchedulesList();
                
                // Show success message
                alert('Jadwal berhasil dihapus!');
                
                console.log('Schedule deleted:', scheduleId);
                console.log('Remaining schedules:', schedules.length);
            }
        }

        // Enhanced attendance function with data recording
        function attendEvent(scheduleId) {
            const schedule = schedules.find(s => s.id === scheduleId);
            if (!schedule) {
                alert('Jadwal tidak ditemukan!');
                return;
            }
            
            const eventDate = new Date(schedule.datetime);
            const now = new Date();
            const timeDiff = eventDate - now;
            const hoursDiff = timeDiff / (1000 * 60 * 60);
            const minutesDiff = timeDiff / (1000 * 60);
            
            // Check if already attended this event
            const currentUserName = getCurrentUserName();
            const existingAttendance = attendanceData.find(a => 
                a.scheduleId === scheduleId && a.memberName === currentUserName
            );
            
            if (existingAttendance) {
                alert('⚠️ Anda sudah melakukan absensi untuk kegiatan ini!\n\n' +
                      `📅 Waktu absen: ${existingAttendance.attendanceTime}\n` +
                      `📋 Status: ${existingAttendance.status === 'hadir' ? 'Hadir' : 'Tidak Hadir'}\n` +
                      `${existingAttendance.note ? `📝 Catatan: ${existingAttendance.note}` : ''}`);
                return;
            }
            
            // Determine attendance status based on timing
            let attendanceStatus = 'hadir';
            let attendanceNote = '';
            const eventDuration = getEventDurationHours(schedule.type);
            
            // Unified validation for all events
            if (minutesDiff > 5) {
                alert('⏰ Absensi belum dapat dilakukan!\n\nAbsensi hanya dapat dilakukan mulai 5 menit sebelum kegiatan dimulai.');
                return;
            } else if (hoursDiff < -eventDuration) {
                alert('❌ Maaf, waktu absensi sudah berakhir!\n\nAbsensi hanya dapat dilakukan hingga kegiatan selesai.');
                return;
            } else if (minutesDiff > -5) {
                // Absen tepat waktu (5 menit sebelum hingga 5 menit setelah dimulai)
                if (minutesDiff > 0) {
                    attendanceNote = 'Absen tepat waktu (sebelum kegiatan dimulai)';
                } else {
                    attendanceNote = 'Absen tepat waktu (kegiatan baru dimulai)';
                }
            } else {
                // Absen terlambat (lebih dari 5 menit setelah kegiatan dimulai)
                const lateMinutes = Math.abs(Math.round(minutesDiff));
                attendanceNote = `Absen terlambat (${lateMinutes} menit setelah kegiatan dimulai)`;
            }
            
            // Record attendance data
            const attendanceRecord = {
                id: attendanceData.length + 1,
                scheduleId: scheduleId,
                memberName: currentUserName,
                eventName: schedule.name,
                eventType: schedule.type,
                eventDate: eventDate.toISOString(),
                attendanceTime: now.toISOString(),
                status: attendanceStatus,
                note: attendanceNote,
                isLate: minutesDiff < -5
            };
            
            attendanceData.push(attendanceRecord);
            
            // Save data to localStorage
            saveDataToStorage();
            
            // Close attendance modal
            closeAttendanceSchedule();
            
            // Show success modal with specific event details
            const successModal = document.getElementById('successModal');
            const timeElement = document.getElementById('attendanceTime');
            timeElement.textContent = now.toLocaleTimeString('id-ID') + ' WIB';
            
            // Update success modal content
            const eventNameElement = successModal.querySelector('.text-green-600');
            if (eventNameElement) {
                eventNameElement.textContent = `${schedule.name} - ${eventDate.toLocaleDateString('id-ID')}`;
            }
            
            // Add special message for different event types
            let specialMessage = '';
            switch (schedule.type) {
                case 'Rapat':
                    specialMessage = '📋 Selamat datang di rapat pengurus! Jangan lupa bawa catatan dan laptop.';
                    break;
                case 'Latihan Rutin':
                    specialMessage = '♟️ Siap untuk latihan! Persiapkan papan catur dan buku analisis.';
                    break;
                case 'Turnamen':
                    specialMessage = '🏆 Turnamen dimulai! Semoga berhasil dan bermain dengan sportif.';
                    break;
                case 'Workshop':
                    specialMessage = '📚 Workshop dimulai! Siapkan catatan dan semangat belajar.';
                    break;
                case 'Pertandingan':
                    specialMessage = '⚔️ Pertandingan dimulai! Berikan dukungan terbaik untuk tim!';
                    break;
                default:
                    specialMessage = '✅ Absensi berhasil dicatat!';
            }
            
            // Add attendance status note
            if (attendanceNote) {
                if (minutesDiff < -5) {
                    specialMessage += `\n\n⚠️ ${attendanceNote}\nKeterlambatan akan dicatat dalam laporan kehadiran.`;
                } else {
                    specialMessage += `\n\n✅ ${attendanceNote}`;
                }
            }
            
            // Show custom alert first
            alert(specialMessage);
            
            successModal.classList.remove('hidden');
            successModal.classList.add('flex');
            
            console.log('Attendance recorded:', attendanceRecord);
        }

        function getCurrentUserName() {
            // Return the actual logged-in user's name
            if (currentUserData && currentUserData.name) {
                return currentUserData.name;
            }
            
            // Fallback to role-based names if no user data
            if (currentUser === 'admin') {
                return 'Admin Utama';
            } else if (currentUser === 'pengurus') {
                return 'Pengurus UKM';
            } else {
                return 'Anggota UKM';
            }
        }



        // Analytics and Reporting Functions
        let attendanceData = [];
        let currentReportFilter = 'all'; // Track current filter

        let charts = {};

        function showAttendanceReport(filterType = 'all') {
            const modal = document.getElementById('attendanceReportModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            // Set current filter
            currentReportFilter = filterType;
            
            // Update title and subtitle based on filter
            const title = document.getElementById('reportTitle');
            const subtitle = document.getElementById('reportSubtitle');
            const roleSelect = document.getElementById('reportRole');
            
            switch(filterType) {
                case 'pengurus':
                    title.textContent = 'Laporan Kehadiran Pengurus ♕';
                    subtitle.textContent = 'Analisis khusus kehadiran pengurus UKM Catur Benteng Merdeka';
                    roleSelect.value = 'pengurus';
                    break;
                case 'anggota':
                    title.textContent = 'Laporan Kehadiran Anggota ♙';
                    subtitle.textContent = 'Analisis khusus kehadiran anggota UKM Catur Benteng Merdeka';
                    roleSelect.value = 'anggota';
                    break;
                case 'admin':
                default:
                    title.textContent = 'Laporan & Analisis Kehadiran Lengkap';
                    subtitle.textContent = 'Dashboard analitik kehadiran semua role UKM Catur Benteng Merdeka';
                    roleSelect.value = 'all';
                    break;
            }
            
            // Initialize analytics
            setTimeout(() => {
                initializeAnalytics();
            }, 100);
        }

        function closeAttendanceReport() {
            const modal = document.getElementById('attendanceReportModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            
            // Destroy existing charts
            Object.values(charts).forEach(chart => {
                if (chart) chart.destroy();
            });
            charts = {};
        }

        function initializeAnalytics() {
            updateMetrics();
            createAttendanceTrendChart();
            createEventTypeChart();
            createMemberAttendanceChart();
            generateWeeklyHeatmap();
            updateTopPerformers();
        }

        function updateMetrics() {
            // Get current role filter
            const roleFilter = document.getElementById('reportRole').value;
            
            // Filter data based on role
            let filteredMembers = members;
            let filteredUsers = users;
            let filteredAttendance = attendanceData;
            
            if (roleFilter !== 'all') {
                // Filter users by role
                filteredUsers = users.filter(user => user.role === roleFilter);
                
                // Get names of users with specific role
                const roleUserNames = filteredUsers.map(user => user.name);
                
                // Filter attendance data by role
                filteredAttendance = attendanceData.filter(record => {
                    // Check if the member name matches any user with the specified role
                    return roleUserNames.includes(record.memberName);
                });
                
                // For members count, we'll use users count for the specific role
                filteredMembers = filteredUsers;
            }
            
            // Calculate metrics from filtered data
            const totalMembers = filteredMembers.length;
            const totalAttendance = filteredAttendance.filter(a => a.status === 'hadir').length;
            const totalRecords = filteredAttendance.length;
            const avgAttendance = totalRecords > 0 ? Math.round((totalAttendance / totalRecords) * 100) : 0;
            
            // Update display
            document.getElementById('totalMembers').textContent = totalMembers;
            document.getElementById('totalAttendance').textContent = totalAttendance;
            document.getElementById('avgAttendance').textContent = avgAttendance + '%';
            document.getElementById('totalEvents').textContent = schedules.length;
        }

        function createAttendanceTrendChart() {
            const ctx = document.getElementById('attendanceTrendChart').getContext('2d');
            
            // Destroy existing chart if it exists
            if (charts.attendanceTrend) {
                charts.attendanceTrend.destroy();
            }
            
            // Generate empty data for 12 months
            const emptyData = new Array(12).fill(0);
            
            charts.attendanceTrend = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun', 'Jul', 'Agu', 'Sep', 'Okt', 'Nov', 'Des'],
                    datasets: [{
                        label: 'Tingkat Kehadiran (%)',
                        data: emptyData,
                        borderColor: 'rgb(59, 130, 246)',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4,
                        pointBackgroundColor: 'rgb(59, 130, 246)',
                        pointBorderColor: '#fff',
                        pointBorderWidth: 2,
                        pointRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: {
                                callback: function(value) {
                                    return value + '%';
                                }
                            },
                            grid: {
                                color: 'rgba(0, 0, 0, 0.1)'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            }
                        }
                    },
                    elements: {
                        point: {
                            hoverRadius: 8
                        }
                    }
                }
            });
        }

        function createEventTypeChart() {
            const ctx = document.getElementById('eventTypeChart').getContext('2d');
            
            if (charts.eventType) {
                charts.eventType.destroy();
            }
            
            // Count event types from schedules
            const eventTypeCounts = {};
            schedules.forEach(schedule => {
                eventTypeCounts[schedule.type] = (eventTypeCounts[schedule.type] || 0) + 1;
            });
            
            const labels = Object.keys(eventTypeCounts);
            const data = Object.values(eventTypeCounts);
            
            // If no data, show empty chart
            if (labels.length === 0) {
                labels.push('Belum ada data');
                data.push(1);
            }
            
            charts.eventType = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: labels,
                    datasets: [{
                        data: data,
                        backgroundColor: [
                            '#3B82F6',
                            '#10B981',
                            '#F59E0B',
                            '#8B5CF6',
                            '#EF4444',
                            '#6B7280'
                        ],
                        borderWidth: 0,
                        hoverOffset: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                usePointStyle: true,
                                font: {
                                    size: 12
                                }
                            }
                        }
                    },
                    cutout: '60%'
                }
            });
        }

        function createMemberAttendanceChart() {
            const ctx = document.getElementById('memberAttendanceChart').getContext('2d');
            
            if (charts.memberAttendance) {
                charts.memberAttendance.destroy();
            }
            
            // Get current role filter
            const roleFilter = document.getElementById('reportRole').value;
            
            // Filter users and attendance data based on role
            let filteredUsers = users;
            let filteredAttendance = attendanceData;
            
            if (roleFilter !== 'all') {
                filteredUsers = users.filter(user => user.role === roleFilter);
                const roleUserNames = filteredUsers.map(user => user.name);
                filteredAttendance = attendanceData.filter(record => 
                    roleUserNames.includes(record.memberName)
                );
            }
            
            // Calculate attendance rates from filtered data
            const memberAttendanceRates = {};
            
            // Initialize filtered users with 0 attendance
            filteredUsers.forEach(user => {
                memberAttendanceRates[user.name] = { total: 0, attended: 0, role: user.role };
            });
            
            // Count attendance for each member
            filteredAttendance.forEach(record => {
                if (memberAttendanceRates[record.memberName]) {
                    memberAttendanceRates[record.memberName].total++;
                    if (record.status === 'hadir') {
                        memberAttendanceRates[record.memberName].attended++;
                    }
                }
            });
            
            // Calculate percentages
            const memberNames = Object.keys(memberAttendanceRates);
            const attendanceRates = memberNames.map(name => {
                const data = memberAttendanceRates[name];
                return data.total > 0 ? Math.round((data.attended / data.total) * 100) : 0;
            });
            
            // If no members, show empty state
            if (memberNames.length === 0) {
                const emptyLabel = roleFilter === 'pengurus' ? 'Belum ada pengurus' : 
                                 roleFilter === 'anggota' ? 'Belum ada anggota' : 'Belum ada data';
                memberNames.push(emptyLabel);
                attendanceRates.push(0);
            }
            
            // Create labels with role indicators
            const chartLabels = memberNames.map(name => {
                if (memberAttendanceRates[name]) {
                    const role = memberAttendanceRates[name].role;
                    const roleIcon = role === 'pengurus' ? '♕' : role === 'anggota' ? '♙' : '♔';
                    const shortName = name.length > 8 ? name.substring(0, 8) + '...' : name;
                    return roleFilter === 'all' ? `${roleIcon} ${shortName}` : shortName;
                }
                return name;
            });
            
            charts.memberAttendance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: chartLabels,
                    datasets: [{
                        label: 'Tingkat Kehadiran (%)',
                        data: attendanceRates,
                        backgroundColor: attendanceRates.map((rate, index) => {
                            // Color based on role if showing all, otherwise based on performance
                            if (roleFilter === 'all' && memberAttendanceRates[memberNames[index]]) {
                                const role = memberAttendanceRates[memberNames[index]].role;
                                if (role === 'pengurus') return '#F59E0B'; // Gold for pengurus
                                if (role === 'anggota') return '#8B5CF6'; // Purple for anggota
                                return '#3B82F6'; // Blue for admin
                            } else {
                                // Performance-based colors
                                if (rate >= 90) return '#10B981';
                                if (rate >= 80) return '#F59E0B';
                                if (rate >= 60) return '#F97316';
                                return '#EF4444';
                            }
                        }),
                        borderRadius: 8,
                        borderSkipped: false
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: {
                                callback: function(value) {
                                    return value + '%';
                                }
                            },
                            grid: {
                                color: 'rgba(0, 0, 0, 0.1)'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            }
                        }
                    }
                }
            });
        }

        function generateWeeklyHeatmap() {
            const heatmapContainer = document.getElementById('weeklyHeatmap');
            heatmapContainer.innerHTML = '';
            
            const days = ['Sen', 'Sel', 'Rab', 'Kam', 'Jum', 'Sab', 'Min'];
            const weeks = 12; // Show 12 weeks
            
            // Add day labels
            days.forEach(day => {
                const dayLabel = document.createElement('div');
                dayLabel.className = 'text-xs text-gray-600 text-center font-medium py-2';
                dayLabel.textContent = day;
                heatmapContainer.appendChild(dayLabel);
            });
            
            // Generate realistic heatmap for chess club (max 3 activities per week)
            // Typical schedule: Tuesday (Latihan), Thursday (Rapat/Workshop), Saturday (Turnamen/Latihan)
            const typicalSchedule = {
                1: 0.7, // Tuesday - Regular training (high activity)
                3: 0.4, // Thursday - Meetings/workshops (medium activity)  
                5: 0.6  // Saturday - Tournaments/training (medium-high activity)
            };
            
            for (let week = 0; week < weeks; week++) {
                for (let day = 0; day < 7; day++) {
                    const cell = document.createElement('div');
                    cell.className = 'w-8 h-8 rounded-sm cursor-pointer transition-all hover:scale-110';
                    
                    // Determine activity level based on typical chess club schedule
                    let activityLevel = 0;
                    let cellClass = 'bg-gray-200';
                    let tooltip = 'Tidak ada kegiatan';
                    
                    if (typicalSchedule[day]) {
                        // Add some randomness to simulate real data
                        const randomFactor = Math.random() * 0.3 + 0.7; // 0.7 to 1.0
                        activityLevel = typicalSchedule[day] * randomFactor;
                        
                        if (activityLevel >= 0.8) {
                            cellClass = 'bg-green-800';
                            tooltip = 'Kehadiran sangat tinggi (>80%)';
                        } else if (activityLevel >= 0.6) {
                            cellClass = 'bg-green-600';
                            tooltip = 'Kehadiran tinggi (60-80%)';
                        } else if (activityLevel >= 0.4) {
                            cellClass = 'bg-green-400';
                            tooltip = 'Kehadiran sedang (40-60%)';
                        } else if (activityLevel >= 0.2) {
                            cellClass = 'bg-green-200';
                            tooltip = 'Kehadiran rendah (20-40%)';
                        }
                        
                        // Add activity type to tooltip
                        if (day === 1) tooltip += ' - Latihan Rutin';
                        else if (day === 3) tooltip += ' - Rapat/Workshop';
                        else if (day === 5) tooltip += ' - Turnamen/Latihan';
                    }
                    
                    // Occasionally skip some weeks to simulate realistic patterns
                    if (Math.random() < 0.15) { // 15% chance of no activity
                        cellClass = 'bg-gray-200';
                        tooltip = 'Tidak ada kegiatan (libur/cuti)';
                    }
                    
                    cell.className += ' ' + cellClass;
                    cell.title = tooltip;
                    heatmapContainer.appendChild(cell);
                }
            }
        }

        function updateTopPerformers() {
            const topPerformersContainer = document.getElementById('topPerformers');
            topPerformersContainer.innerHTML = '';
            
            // Get current role filter
            const roleFilter = document.getElementById('reportRole').value;
            
            // Filter users and attendance data based on role
            let filteredUsers = users;
            let filteredAttendance = attendanceData;
            
            if (roleFilter !== 'all') {
                filteredUsers = users.filter(user => user.role === roleFilter);
                const roleUserNames = filteredUsers.map(user => user.name);
                filteredAttendance = attendanceData.filter(record => 
                    roleUserNames.includes(record.memberName)
                );
            }
            
            // Calculate attendance rates for filtered users
            const memberAttendanceRates = {};
            
            // Initialize filtered users with 0 attendance
            filteredUsers.forEach(user => {
                memberAttendanceRates[user.name] = { total: 0, attended: 0, role: user.role };
            });
            
            // Count attendance for each member
            filteredAttendance.forEach(record => {
                if (memberAttendanceRates[record.memberName]) {
                    memberAttendanceRates[record.memberName].total++;
                    if (record.status === 'hadir') {
                        memberAttendanceRates[record.memberName].attended++;
                    }
                }
            });
            
            // Calculate percentages and sort
            const performers = Object.keys(memberAttendanceRates)
                .map(name => {
                    const data = memberAttendanceRates[name];
                    const rate = data.total > 0 ? Math.round((data.attended / data.total) * 100) : 0;
                    return { name, rate, role: data.role };
                })
                .sort((a, b) => b.rate - a.rate)
                .slice(0, 5); // Top 5
            
            if (performers.length === 0) {
                const emptyMessage = roleFilter === 'pengurus' ? 'Belum ada data pengurus' : 
                                   roleFilter === 'anggota' ? 'Belum ada data anggota' : 'Belum ada data kehadiran';
                topPerformersContainer.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <div class="text-4xl mb-4">🏆</div>
                        <p>${emptyMessage}</p>
                        <p class="text-sm">Ranking akan muncul setelah ada data absensi</p>
                    </div>
                `;
                return;
            }
            
            const badges = ['🥇', '🥈', '🥉', '🏅', '🏅'];
            
            performers.forEach((performer, index) => {
                const roleIcon = performer.role === 'pengurus' ? '♕' : performer.role === 'anggota' ? '♙' : '♔';
                const roleColor = performer.role === 'pengurus' ? 'text-yellow-600' : performer.role === 'anggota' ? 'text-purple-600' : 'text-blue-600';
                
                const performerDiv = document.createElement('div');
                performerDiv.className = 'flex items-center justify-between p-3 bg-white rounded-lg border';
                performerDiv.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <span class="text-2xl">${badges[index] || '🏅'}</span>
                        <div>
                            <div class="font-medium text-gray-800 flex items-center space-x-2">
                                <span>${performer.name}</span>
                                ${roleFilter === 'all' ? `<span class="text-sm ${roleColor}">${roleIcon}</span>` : ''}
                            </div>
                            <div class="text-sm text-gray-500">
                                Peringkat ${index + 1}
                                ${roleFilter === 'all' ? ` • ${performer.role.charAt(0).toUpperCase() + performer.role.slice(1)}` : ''}
                            </div>
                        </div>
                    </div>
                    <div class="text-right">
                        <div class="text-lg font-bold ${performer.rate >= 90 ? 'text-green-600' : performer.rate >= 80 ? 'text-yellow-600' : 'text-red-600'}">${performer.rate}%</div>
                        <div class="text-xs text-gray-500">Kehadiran</div>
                    </div>
                `;
                topPerformersContainer.appendChild(performerDiv);
            });
        }

        function updateReport() {
            // This function would filter data based on selected filters
            // For demo purposes, we'll just reinitialize with the same data
            initializeAnalytics();
        }

        function exportReport() {
            // Check if there's data to export
            if (attendanceData.length === 0 && members.length === 0 && schedules.length === 0) {
                alert('Tidak ada data untuk diexport. Silakan tambahkan data terlebih dahulu.');
                return;
            }
            
            // Create comprehensive Excel data
            const currentDate = new Date().toLocaleDateString('id-ID');
            const currentTime = new Date().toLocaleTimeString('id-ID');
            
            // Header information
            let excelContent = `LAPORAN KEHADIRAN UKM CATUR BENTENG MERDEKA\n`;
            excelContent += `Tanggal Export: ${currentDate} ${currentTime}\n`;
            excelContent += `\n`;
            
            // Summary statistics
            excelContent += `RINGKASAN STATISTIK\n`;
            excelContent += `Total Anggota,${members.length}\n`;
            excelContent += `Total Kehadiran,${attendanceData.filter(a => a.status === 'hadir').length}\n`;
            excelContent += `Total Kegiatan,${schedules.length}\n`;
            const avgAttendance = attendanceData.length > 0 ? Math.round((attendanceData.filter(a => a.status === 'hadir').length / attendanceData.length) * 100) : 0;
            excelContent += `Rata-rata Kehadiran,${avgAttendance}%\n`;
            excelContent += `\n`;
            
            // Attendance data
            if (attendanceData.length > 0) {
                excelContent += `DATA KEHADIRAN\n`;
                excelContent += `No,Nama Anggota,Kegiatan,Tanggal,Status\n`;
                attendanceData.forEach((record, index) => {
                    excelContent += `${index + 1},${record.memberName},${record.eventName},${record.date},${record.status === 'hadir' ? 'Hadir' : 'Tidak Hadir'}\n`;
                });
                excelContent += `\n`;
            }
            
            // Member list
            if (members.length > 0) {
                excelContent += `DAFTAR ANGGOTA\n`;
                excelContent += `No,Nama Lengkap,NIM/NIS,Email,Telepon\n`;
                members.forEach((member, index) => {
                    excelContent += `${index + 1},${member.name},${member.nim},${member.email || '-'},${member.phone || '-'}\n`;
                });
                excelContent += `\n`;
            }
            
            // Schedule list
            if (schedules.length > 0) {
                excelContent += `JADWAL KEGIATAN\n`;
                excelContent += `No,Nama Kegiatan,Tanggal & Waktu,Jenis Kegiatan,Status\n`;
                schedules.forEach((schedule, index) => {
                    const scheduleDate = new Date(schedule.datetime);
                    const isActive = scheduleDate > new Date();
                    excelContent += `${index + 1},${schedule.name},${scheduleDate.toLocaleString('id-ID')},${schedule.type},${isActive ? 'Akan Datang' : 'Selesai'}\n`;
                });
            }
            
            // Create and download file
            const blob = new Blob([excelContent], { type: 'text/csv;charset=utf-8;' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `Laporan_Kehadiran_UKM_Catur_${new Date().toISOString().split('T')[0]}.csv`;
            a.style.display = 'none';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            window.URL.revokeObjectURL(url);
            
            // Show success message with details
            const totalRows = attendanceData.length + members.length + schedules.length;
            alert(`✅ Laporan berhasil diexport!\n\n📊 Detail Export:\n• ${attendanceData.length} data kehadiran\n• ${members.length} data anggota\n• ${schedules.length} jadwal kegiatan\n• Total ${totalRows} baris data\n\n📁 File: Laporan_Kehadiran_UKM_Catur_${new Date().toISOString().split('T')[0]}.csv`);
        }

        // WhatsApp Announcement Functions
        function generateWhatsAppAnnouncement(schedule) {
            const eventDate = new Date(schedule.datetime);
            const dayNames = ['Minggu', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu'];
            const monthNames = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
            
            const dayName = dayNames[eventDate.getDay()];
            const date = eventDate.getDate();
            const month = monthNames[eventDate.getMonth()];
            const year = eventDate.getFullYear();
            const time = eventDate.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
            
            // Generate different announcements based on event type
            let announcement = '';
            
            switch (schedule.type) {
                case 'Latihan Rutin':
                    announcement = `Assalamu'alaikum teman-teman dan kakak-kakak semuanya,

Saya mewakili Ketua Umum UKM Catur Benteng Merdeka mengundang seluruh anggota untuk hadir dalam *${schedule.name}* pada:

Hari                : ${dayName}
Tanggal         : ${date} ${month} ${year}
Waktu            : ${time} WIB
Tempat          : Sekret UKM Benteng Merdeka

*Agenda latihan:*
1. Pembukaan dan presensi kehadiran
2. Pemanasan dengan puzzle taktik
3. Latihan strategi pembukaan
4. Analisis partai master
5. Simulasi pertandingan antar anggota
6. Evaluasi dan diskusi
7. Penutup

*Yang perlu dibawa:*
• Papan catur pribadi (jika ada)
• Buku catatan untuk analisis
• Alat tulis dan pulpen
• Buku referensi catur (opsional)
• Semangat belajar yang tinggi

*Peserta:*
• Seluruh anggota UKM aktif
• Anggota baru dan calon anggota
• Pengurus dan pelatih

*Manfaat latihan:*
• Meningkatkan skill bermain catur
• Mempersiapkan kompetisi mendatang
• Mempererat silaturahmi antar anggota
• Berbagi strategi dan pengalaman

*NB:* Diharapkan semua hadir tepat waktu sesuai yang ditentukan. Latihan rutin sangat penting untuk meningkatkan kemampuan bermain catur kita.

Jika berhalangan hadir, mohon konfirmasi sebelumnya.

Wassalamu'alaikum warahmatullahi wabarakatuh.

Terima kasih 🙏🏼

*Pengurus UKM Catur Benteng Merdeka*
📱 Contact: 082196434417
📷 IG: @benteng_merdeka

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
                    break;
                    
                case 'Rapat':
                    announcement = `Assalamu'alaikum teman-teman dan kakak-kakak semuanya,

Saya mewakili Ketua Umum UKM Catur Benteng Merdeka mengundang seluruh kepengurusan untuk hadir dalam *${schedule.name}* pada:

Hari                : ${dayName}
Tanggal         : ${date} ${month} ${year}
Waktu            : ${time} WIB
Tempat          : Sekret UKM Benteng Merdeka

*Agenda yang akan dibahas:*
1. Laporan kegiatan periode sebelumnya
2. Evaluasi program kerja divisi
3. Perencanaan kegiatan mendatang
4. Pembahasan anggaran dan keuangan UKM
5. Koordinasi antar divisi
6. Persiapan UKM Fest dan kompetisi
7. Program kerja tahunan UKM

*Yang perlu disiapkan:*
• Laporan kegiatan masing-masing divisi
• Proposal kegiatan (jika ada)
• Catatan dan alat tulis
• Laptop/tablet untuk presentasi

*Peserta yang diundang:*
• Seluruh pengurus inti UKM
• Koordinator setiap divisi
• Sekretaris dan bendahara
• Perwakilan anggota senior

*NB:* Diharapkan semua hadir tepat waktu sesuai yang ditentukan. Kehadiran pengurus sangat penting untuk kelancaran koordinasi UKM.

Jika berhalangan hadir, mohon konfirmasi dan kirim delegasi pengganti.

Wassalamu'alaikum warahmatullahi wabarakatuh.

Terima kasih 🙏🏼

*Pengurus UKM Catur Benteng Merdeka*
📱 Contact: 082196434417
📷 IG: @benteng_merdeka

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
                    break;
                    
                case 'Turnamen':
                    announcement = `Assalamu'alaikum teman-teman dan kakak-kakak semuanya,

Saya mewakili Ketua Umum UKM Catur Benteng Merdeka mengundang seluruh anggota untuk berpartisipasi dalam *${schedule.name}* pada:

Hari                : ${dayName}
Tanggal         : ${date} ${month} ${year}
Waktu            : ${time} WIB
Tempat          : Aula UKM Benteng Merdeka

*Informasi turnamen:*
1. Sistem: Swiss System (7 ronde)
2. Kontrol waktu: 15 menit + 10 detik increment
3. Rating: ELO Rating Internal UKM
4. Biaya pendaftaran: Rp 25.000
5. Kuota peserta: 32 pemain (first come first served)
6. Technical meeting: 30 menit sebelum turnamen

*Syarat peserta:*
• Anggota aktif UKM Catur Benteng Merdeka
• Mengisi formulir pendaftaran
• Membayar biaya partisipasi
• Mematuhi aturan turnamen FIDE
• Membawa KTM/kartu identitas

*Yang perlu dibawa:*
• Papan catur dan bidak (jika diminta panitia)
• Jam catur digital (jika ada)
• Alat tulis untuk notasi partai
• KTM atau kartu identitas
• Semangat bertanding yang sportif

*Hadiah juara:*
• Juara 1: Piala + Sertifikat + Uang pembinaan Rp 300.000
• Juara 2: Piala + Sertifikat + Uang pembinaan Rp 200.000
• Juara 3: Piala + Sertifikat + Uang pembinaan Rp 100.000
• Juara harapan: Sertifikat + doorprize
• Semua peserta: Sertifikat partisipasi

*Pendaftaran:*
• Batas pendaftaran: ${date - 2} ${month} ${year} pukul 23:59 WIB
• Konfirmasi dengan reply "DAFTAR" + nama lengkap + NIM
• Transfer biaya ke: BCA 1234567890 a.n UKM Catur
• Kirim bukti transfer ke panitia

*NB:* Diharapkan semua peserta hadir tepat waktu sesuai yang ditentukan. Technical meeting wajib diikuti oleh semua peserta.

Ayo tunjukkan kemampuan terbaik kalian dan raih juara!

Wassalamu'alaikum warahmatullahi wabarakatuh.

Terima kasih 🙏🏼

*Panitia Turnamen UKM Catur Benteng Merdeka*
📱 Contact: 082196434417
📷 IG: @benteng_merdeka

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
                    break;
                    
                case 'Workshop':
                    announcement = `Assalamu'alaikum teman-teman dan kakak-kakak semuanya,

Saya mewakili Ketua Umum UKM Catur Benteng Merdeka mengundang seluruh anggota untuk mengikuti *${schedule.name}* pada:

Hari                : ${dayName}
Tanggal         : ${date} ${month} ${year}
Waktu            : ${time} WIB
Tempat          : Aula UKM Benteng Merdeka

*Materi workshop:*
1. Strategi pembukaan catur modern
2. Taktik dan kombinasi tingkat lanjut
3. Teknik endgame yang efektif
4. Analisis partai master dunia
5. Psikologi dalam bermain catur
6. Tips meningkatkan rating ELO
7. Sesi tanya jawab interaktif

*Narasumber:*
• Master FIDE berpengalaman
• Pelatih catur nasional
• Alumni UKM berprestasi
• Expert catur regional

*Target peserta:*
• Anggota UKM semua level (pemula-mahir)
• Calon peserta kompetisi
• Yang ingin meningkatkan skill bermain
• Pengurus dan pelatih UKM

*Yang perlu dibawa:*
• Papan catur dan bidak lengkap
• Buku catatan dan alat tulis
• Laptop/tablet (jika ada)
• Buku referensi catur (opsional)
• Semangat belajar yang tinggi

*Fasilitas yang disediakan:*
• Materi workshop lengkap (soft copy)
• Sertifikat kehadiran
• Snack dan minuman
• Analisis partai personal
• Konsultasi dengan narasumber

*Biaya:*
• Gratis untuk anggota UKM aktif
• Kontribusi sukarela Rp 10.000 untuk konsumsi

*NB:* Diharapkan semua hadir tepat waktu sesuai yang ditentukan. Tempat terbatas hanya untuk 50 peserta (first come first served).

Jangan lewatkan kesempatan emas untuk meningkatkan skill catur!

Wassalamu'alaikum warahmatullahi wabarakatuh.

Terima kasih 🙏🏼

*Panitia Workshop UKM Catur Benteng Merdeka*
📱 Contact: 082196434417
📷 IG: @benteng_merdeka

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
                    break;
                    
                case 'Pertandingan':
                    announcement = `Assalamu'alaikum teman-teman dan kakak-kakak semuanya,

Saya mewakili Ketua Umum UKM Catur Benteng Merdeka mengundang seluruh anggota untuk mendukung tim kita dalam *${schedule.name}* pada:

Hari                : ${dayName}
Tanggal         : ${date} ${month} ${year}
Waktu            : ${time} WIB
Tempat          : Venue Pertandingan (akan dikonfirmasi)

*Informasi pertandingan:*
1. Format: Team Match (4 board utama + 2 cadangan)
2. Lawan: (akan diinformasikan H-3)
3. Kontrol waktu: 90 menit + 30 detik increment
4. Sistem: Match play (best of 4)
5. Aturan: FIDE Laws of Chess
6. Wasit: Arbiter nasional bersertifikat

*Susunan tim:*
• Board 1: (akan diumumkan H-2)
• Board 2: (akan diumumkan H-2)
• Board 3: (akan diumumkan H-2)
• Board 4: (akan diumumkan H-2)
• Cadangan 1: (akan diumumkan H-2)
• Cadangan 2: (akan diumumkan H-2)

*Persiapan tim:*
• Latihan intensif 3x seminggu
• Briefing strategi tim H-1
• Persiapan mental dan fisik
• Koordinasi dan chemistry antar pemain
• Analisis kekuatan lawan

*Yang perlu dibawa (untuk tim):*
• Seragam resmi UKM Benteng Merdeka
• Papan catur pribadi (jika diminta)
• Jam catur digital (backup)
• Alat tulis untuk notasi partai
• Kartu identitas dan kartu peserta

*Dukungan supporter:*
• Seluruh anggota UKM diharapkan hadir
• Berikan dukungan moral kepada tim
• Tunjukkan solidaritas dan sportivitas
• Pakai atribut UKM (kaos, banner, dll)
• Jaga nama baik UKM di venue

*Target dan harapan:*
• Memberikan penampilan terbaik
• Menunjukkan sportivitas tinggi
• Meraih kemenangan untuk UKM
• Mengharumkan nama Benteng Merdeka

*NB:* Tim wajib hadir 1 jam sebelum pertandingan untuk briefing akhir. Supporter diharapkan hadir untuk memberikan dukungan moral.

Mari kita menang bersama! BENTENG MERDEKA JUARA! 🏆

Wassalamu'alaikum warahmatullahi wabarakatuh.

Terima kasih 🙏🏼

*Official Team UKM Catur Benteng Merdeka*
📱 Contact: 082196434417
📷 IG: @benteng_merdeka

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
                    break;
                    
                default:
                    announcement = `📢 *PENGUMUMAN KEGIATAN UKM* 📢

🏛️ *UKM CATUR BENTENG MERDEKA*
📢 *GENS UNA SUMUS*

━━━━━━━━━━━━━━━━━━━━━━━━━━

📅 *JADWAL KEGIATAN*
🎯 Kegiatan: ${schedule.name}
📆 Hari/Tanggal: ${dayName}, ${date} ${month} ${year}
⏰ Waktu: ${time} WIB
📍 Tempat: (akan dikonfirmasi)
🎪 Jenis: ${schedule.type}

━━━━━━━━━━━━━━━━━━━━━━━━━━

📋 *INFORMASI KEGIATAN:*
• Kegiatan khusus UKM Catur Benteng Merdeka
• Terbuka untuk seluruh anggota
• Agenda akan diinformasikan lebih lanjut
• Partisipasi sangat diharapkan

🎒 *PERSIAPAN:*
• Bawa alat tulis dan catatan
• Datang tepat waktu
• Siapkan semangat dan antusiasme
• Patuhi protokol yang berlaku

⚠️ *PENTING:*
• Konfirmasi kehadiran dengan reply "HADIR" + nama
• Informasi detail akan menyusul
• Hubungi pengurus jika ada pertanyaan
• Kehadiran sangat diharapkan

📱 *KONTAK PENGURUS:*
• WhatsApp: 082196434417
• Instagram: @benteng_merdeka

Mari berpartisipasi aktif dalam kegiatan UKM! 
Sampai jumpa di acara! 🤝

*#UKMCaturBentengMerdeka #GensUnaSumus*`;
            }
            
            // Show the announcement modal
            document.getElementById('announcementText').value = announcement;
            const modal = document.getElementById('whatsappAnnouncementModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            // Show success message first
            alert('✅ Jadwal kegiatan berhasil dibuat!\n📢 Pengumuman WhatsApp telah disiapkan dan siap untuk dikirim ke grup.');
        }

        function closeWhatsAppAnnouncement() {
            const modal = document.getElementById('whatsappAnnouncementModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function copyAnnouncement() {
            const textarea = document.getElementById('announcementText');
            textarea.select();
            textarea.setSelectionRange(0, 99999); // For mobile devices
            
            try {
                document.execCommand('copy');
                
                // Show success feedback
                const button = event.target;
                const originalText = button.innerHTML;
                button.innerHTML = '✅ Tersalin!';
                button.classList.remove('bg-green-600', 'hover:bg-green-700');
                button.classList.add('bg-green-800');
                
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.classList.remove('bg-green-800');
                    button.classList.add('bg-green-600', 'hover:bg-green-700');
                }, 2000);
                
                // Show alert
                alert('📋 Pesan pengumuman berhasil disalin!\n\nSekarang Anda bisa paste di grup WhatsApp UKM.');
                
            } catch (err) {
                alert('❌ Gagal menyalin pesan. Silakan salin manual dengan Ctrl+A lalu Ctrl+C');
            }
        }

        function openWhatsAppWeb() {
            // Open WhatsApp Web in new tab
            window.open('https://web.whatsapp.com/', '_blank');
            
            // Show instruction
            setTimeout(() => {
                alert('📱 WhatsApp Web telah dibuka!\n\n📋 Langkah selanjutnya:\n1. Pilih grup UKM Catur Benteng Merdeka\n2. Paste pesan yang sudah disalin\n3. Kirim pengumuman\n\n💡 Jangan lupa salin pesan terlebih dahulu dengan tombol "Salin Pesan"');
            }, 1000);
        }

        function shareToMobile() {
            const announcement = document.getElementById('announcementText').value;
            
            // Try to use Web Share API if available
            if (navigator.share) {
                navigator.share({
                    title: 'Pengumuman UKM Catur Benteng Merdeka',
                    text: announcement
                }).then(() => {
                    console.log('Berhasil membagikan pengumuman');
                }).catch((error) => {
                    console.log('Error sharing:', error);
                    fallbackShare(announcement);
                });
            } else {
                fallbackShare(announcement);
            }
        }

        function fallbackShare(announcement) {
            // Fallback: copy to clipboard and show instructions
            try {
                navigator.clipboard.writeText(announcement).then(() => {
                    alert('📱 Pesan berhasil disalin!\n\n📋 Langkah selanjutnya:\n1. Buka WhatsApp di HP\n2. Pilih grup UKM\n3. Paste dan kirim pesan\n\n💡 Pesan sudah tersimpan di clipboard HP Anda.');
                });
            } catch (err) {
                alert('📱 Silakan salin pesan secara manual:\n\n1. Pilih semua teks pengumuman\n2. Salin (Ctrl+C atau long press)\n3. Buka WhatsApp di HP\n4. Paste di grup UKM');
            }
        }

        // Password visibility toggle function
        function togglePasswordVisibility(inputId) {
            const input = document.getElementById(inputId);
            const eyeOpen = document.getElementById(inputId + '-eye-open');
            const eyeClosed = document.getElementById(inputId + '-eye-closed');
            
            if (input.type === 'password') {
                input.type = 'text';
                eyeOpen.classList.add('hidden');
                eyeClosed.classList.remove('hidden');
            } else {
                input.type = 'password';
                eyeOpen.classList.remove('hidden');
                eyeClosed.classList.add('hidden');
            }
        }

        // Close modals when clicking outside
        document.addEventListener('click', function(event) {
            const modals = ['loginSelectionModal', 'loginModal', 'attendanceScheduleModal', 'successModal', 'aboutModal', 'contactModal', 'addMemberModal', 'memberListModal', 'editMemberModal', 'userManagementModal', 'editUserModal', 'attendanceReportModal', 'whatsappAnnouncementModal', 'changePasswordModal'];
            modals.forEach(modalId => {
                const modal = document.getElementById(modalId);
                if (event.target === modal) {
                    modal.classList.add('hidden');
                    modal.classList.remove('flex');
                    
                    // Clean up charts when closing attendance report
                    if (modalId === 'attendanceReportModal') {
                        Object.values(charts).forEach(chart => {
                            if (chart) chart.destroy();
                        });
                        charts = {};
                    }
                }
            });
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97ef4acd61a47979',t:'MTc1Nzg0NjY5OS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>


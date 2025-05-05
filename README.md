<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Escola Técnica - Portal Acadêmico</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Custom CSS for elements that need more styling */
        .splash-screen {
            background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%);
        }
        .login-card {
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        .performance-chart {
            height: 200px;
            background: linear-gradient(to right, #3b82f6, #10b981);
            border-radius: 12px;
        }
        .tab-bar {
            box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.1);
        }
        .notification-badge {
            position: absolute;
            top: -5px;
            right: -5px;
        }
        .sidebar {
            transition: transform 0.3s ease-in-out;
        }
        .sidebar-hidden {
            transform: translateX(-100%);
        }
        .dark-mode {
            background-color: #1a202c;
            color: #f7fafc;
        }
        .dark-mode-card {
            background-color: #2d3748;
            color: #f7fafc;
        }
    </style>
</head>
<body class="bg-gray-100 font-sans">
    <!-- App Container -->
    <div id="app" class="relative max-w-md mx-auto min-h-screen overflow-hidden bg-white">
        <!-- Splash Screen -->
        <div id="splash" class="splash-screen flex flex-col items-center justify-center h-screen text-white">
            <div class="animate-bounce">
                <i class="fas fa-graduation-cap text-6xl mb-4"></i>
            </div>
            <h1 class="text-3xl font-bold mb-2">Escola Técnica</h1>
            <p class="text-xl">Portal Acadêmico</p>
            <div class="mt-8">
                <div class="w-64 h-1 bg-white bg-opacity-30 rounded-full overflow-hidden">
                    <div id="loading-bar" class="h-full bg-white rounded-full w-0"></div>
                </div>
            </div>
        </div>

        <!-- Login Screen (initially hidden) -->
        <div id="login-screen" class="hidden p-6 h-screen flex flex-col justify-center">
            <div class="login-card bg-white rounded-xl p-6 shadow-lg">
                <div class="text-center mb-8">
                    <i class="fas fa-graduation-cap text-5xl text-blue-600 mb-4"></i>
                    <h2 class="text-2xl font-bold text-gray-800">Bem-vindo de volta!</h2>
                    <p class="text-gray-600">Faça login para acessar seu portal</p>
                </div>
                
                <form id="login-form" class="space-y-4">
                    <div>
                        <label for="username" class="block text-sm font-medium text-gray-700 mb-1">Usuário</label>
                        <input type="text" id="username" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500" placeholder="Digite seu usuário">
                    </div>
                    <div>
                        <label for="password" class="block text-sm font-medium text-gray-700 mb-1">Senha</label>
                        <input type="password" id="password" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500" placeholder="Digite sua senha">
                    </div>
                    <div class="flex items-center justify-between">
                        <div class="flex items-center">
                            <input id="remember-me" type="checkbox" class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded">
                            <label for="remember-me" class="ml-2 block text-sm text-gray-700">Lembrar-me</label>
                        </div>
                        <a href="#" id="forgot-password" class="text-sm text-blue-600 hover:text-blue-800">Esqueceu a senha?</a>
                    </div>
                    <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                        Entrar
                    </button>
                </form>
                
                <div class="mt-6">
                    <p class="text-center text-sm text-gray-600">Ou entre com</p>
                    <div class="flex justify-center space-x-4 mt-3">
                        <button class="bg-red-500 hover:bg-red-600 text-white p-2 rounded-full">
                            <i class="fab fa-google"></i>
                        </button>
                        <button class="bg-blue-700 hover:bg-blue-800 text-white p-2 rounded-full">
                            <i class="fab fa-facebook-f"></i>
                        </button>
                    </div>
                </div>
                
                <div class="mt-6 text-center">
                    <p class="text-sm text-gray-600">Não tem uma conta? <a href="#" class="text-blue-600 hover:text-blue-800">Fale com a secretaria</a></p>
                </div>
            </div>
        </div>

        <!-- Forgot Password Modal -->
        <div id="forgot-password-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
            <div class="bg-white rounded-lg p-6 w-full max-w-md">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-xl font-bold text-gray-800">Recuperar Senha</h3>
                    <button id="close-forgot-password" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <p class="text-gray-600 mb-4">Digite seu e-mail cadastrado para receber as instruções de recuperação de senha.</p>
                <form id="recovery-form" class="space-y-4">
                    <div>
                        <label for="recovery-email" class="block text-sm font-medium text-gray-700 mb-1">E-mail</label>
                        <input type="email" id="recovery-email" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500" placeholder="seu@email.com">
                    </div>
                    <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-lg transition duration-200">
                        Enviar Instruções
                    </button>
                </form>
            </div>
        </div>

        <!-- Student Dashboard (initially hidden) -->
        <div id="student-dashboard" class="hidden h-screen flex flex-col">
            <!-- Header -->
            <header class="bg-blue-600 text-white p-4 flex justify-between items-center">
                <button id="menu-toggle" class="text-white">
                    <i class="fas fa-bars text-xl"></i>
                </button>
                <h1 class="text-xl font-bold">Portal do Aluno</h1>
                <div class="relative">
                    <button id="notification-btn" class="text-white relative">
                        <i class="fas fa-bell text-xl"></i>
                        <span class="notification-badge bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">3</span>
                    </button>
                </div>
            </header>

            <!-- Sidebar -->
            <div id="sidebar" class="sidebar sidebar-hidden absolute left-0 top-0 h-full w-64 bg-white shadow-lg z-10">
                <div class="p-4 border-b border-gray-200 flex items-center space-x-3">
                    <div class="h-10 w-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600">
                        <i class="fas fa-user"></i>
                    </div>
                    <div>
                        <p class="font-medium">João Silva</p>
                        <p class="text-xs text-gray-500">Aluno - Informática</p>
                    </div>
                </div>
                <nav class="p-2">
                    <a href="#" class="block p-3 rounded-lg hover:bg-blue-50 text-blue-600 font-medium">
                        <i class="fas fa-home mr-2"></i> Dashboard
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-book mr-2"></i> Notas
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-calendar-check mr-2"></i> Frequência
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-money-bill-wave mr-2"></i> Financeiro
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-calendar-alt mr-2"></i> Calendário
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-clock mr-2"></i> Horário de Aulas
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-file-alt mr-2"></i> Materiais
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-comments mr-2"></i> Atendimento
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-cog mr-2"></i> Configurações
                    </a>
                    <button id="logout-btn" class="w-full text-left p-3 rounded-lg hover:bg-gray-100 text-gray-700 mt-4">
                        <i class="fas fa-sign-out-alt mr-2"></i> Sair
                    </button>
                    <div class="p-3 mt-4 border-t border-gray-200">
                        <button id="dark-mode-toggle" class="flex items-center space-x-2 text-gray-700">
                            <i class="fas fa-moon"></i>
                            <span>Modo Escuro</span>
                        </button>
                    </div>
                </nav>
            </div>

            <!-- Main Content -->
            <main class="flex-1 overflow-y-auto p-4">
                <!-- Welcome Card -->
                <div class="bg-blue-50 rounded-xl p-4 mb-4 flex items-center">
                    <div class="h-12 w-12 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 mr-3">
                        <i class="fas fa-user-graduate text-xl"></i>
                    </div>
                    <div>
                        <h2 class="font-bold text-gray-800">Bem-vindo, João!</h2>
                        <p class="text-sm text-gray-600">Matrícula: 2023001234 - Curso: Informática</p>
                    </div>
                </div>

                <!-- Performance Summary -->
                <div class="mb-6">
                    <div class="flex justify-between items-center mb-2">
                        <h2 class="font-bold text-lg text-gray-800">Seu Desempenho</h2>
                        <a href="#" class="text-blue-600 text-sm">Ver detalhes</a>
                    </div>
                    <div class="performance-chart flex items-end justify-center p-4">
                        <div class="text-white text-center">
                            <p class="text-3xl font-bold">7.8</p>
                            <p class="text-sm">Média Geral</p>
                        </div>
                    </div>
                    <div class="grid grid-cols-3 gap-2 mt-3">
                        <div class="bg-green-50 rounded-lg p-2 text-center">
                            <p class="text-green-600 font-bold">85%</p>
                            <p class="text-xs text-gray-600">Frequência</p>
                        </div>
                        <div class="bg-blue-50 rounded-lg p-2 text-center">
                            <p class="text-blue-600 font-bold">2</p>
                            <p class="text-xs text-gray-600">Disciplinas</p>
                        </div>
                        <div class="bg-purple-50 rounded-lg p-2 text-center">
                            <p class="text-purple-600 font-bold">1</p>
                            <p class="text-xs text-gray-600">Pendências</p>
                        </div>
                    </div>
                </div>

                <!-- Quick Access -->
                <div class="mb-6">
                    <h2 class="font-bold text-lg text-gray-800 mb-3">Acesso Rápido</h2>
                    <div class="grid grid-cols-4 gap-3">
                        <a href="#" class="bg-white rounded-xl p-3 shadow-sm text-center hover:shadow-md transition">
                            <div class="h-10 w-10 bg-blue-100 rounded-full flex items-center justify-center text-blue-600 mx-auto mb-1">
                                <i class="fas fa-book"></i>
                            </div>
                            <p class="text-xs font-medium">Notas</p>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-3 shadow-sm text-center hover:shadow-md transition">
                            <div class="h-10 w-10 bg-green-100 rounded-full flex items-center justify-center text-green-600 mx-auto mb-1">
                                <i class="fas fa-calendar-check"></i>
                            </div>
                            <p class="text-xs font-medium">Frequência</p>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-3 shadow-sm text-center hover:shadow-md transition">
                            <div class="h-10 w-10 bg-yellow-100 rounded-full flex items-center justify-center text-yellow-600 mx-auto mb-1">
                                <i class="fas fa-money-bill-wave"></i>
                            </div>
                            <p class="text-xs font-medium">Financeiro</p>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-3 shadow-sm text-center hover:shadow-md transition">
                            <div class="h-10 w-10 bg-purple-100 rounded-full flex items-center justify-center text-purple-600 mx-auto mb-1">
                                <i class="fas fa-file-alt"></i>
                            </div>
                            <p class="text-xs font-medium">Materiais</p>
                        </a>
                    </div>
                </div>

                <!-- Notifications -->
                <div class="mb-6">
                    <div class="flex justify-between items-center mb-3">
                        <h2 class="font-bold text-lg text-gray-800">Avisos Recentes</h2>
                        <a href="#" class="text-blue-600 text-sm">Ver todos</a>
                    </div>
                    <div class="space-y-3">
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-red-100 rounded-full flex items-center justify-center text-red-600 mr-3">
                                    <i class="fas fa-exclamation"></i>
                                </div>
                                <div>
                                    <h3 class="font-medium text-gray-800">Prova Adiada</h3>
                                    <p class="text-sm text-gray-600">A prova de Matemática foi adiada para sexta-feira.</p>
                                    <p class="text-xs text-gray-400 mt-1">2 horas atrás</p>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-blue-100 rounded-full flex items-center justify-center text-blue-600 mr-3">
                                    <i class="fas fa-info-circle"></i>
                                </div>
                                <div>
                                    <h3 class="font-medium text-gray-800">Novo Material</h3>
                                    <p class="text-sm text-gray-600">O professor postou novo material de Programação.</p>
                                    <p class="text-xs text-gray-400 mt-1">Ontem</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Class Schedule -->
                <div>
                    <h2 class="font-bold text-lg text-gray-800 mb-3">Próximas Aulas</h2>
                    <div class="bg-white rounded-xl p-4 shadow-sm">
                        <div class="flex items-center mb-3">
                            <div class="h-10 w-10 bg-blue-100 rounded-lg flex items-center justify-center text-blue-600 mr-3">
                                <i class="fas fa-calendar-day"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Amanhã</h3>
                                <p class="text-sm text-gray-600">Quarta-feira, 15 de Novembro</p>
                            </div>
                        </div>
                        <div class="space-y-3">
                            <div class="flex items-center p-2 rounded-lg bg-blue-50">
                                <div class="text-center mr-3">
                                    <p class="text-sm font-medium">08:00</p>
                                    <p class="text-xs text-gray-500">09:40</p>
                                </div>
                                <div>
                                    <h4 class="font-medium">Programação Web</h4>
                                    <p class="text-sm text-gray-600">Sala 12 - Prof. Carlos</p>
                                </div>
                            </div>
                            <div class="flex items-center p-2 rounded-lg bg-gray-50">
                                <div class="text-center mr-3">
                                    <p class="text-sm font-medium">10:00</p>
                                    <p class="text-xs text-gray-500">11:40</p>
                                </div>
                                <div>
                                    <h4 class="font-medium">Banco de Dados</h4>
                                    <p class="text-sm text-gray-600">Lab. Informática - Prof. Ana</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </main>

            <!-- Tab Bar -->
            <div class="tab-bar bg-white border-t border-gray-200 flex justify-around items-center p-2">
                <a href="#" class="text-blue-600 p-2 rounded-full">
                    <i class="fas fa-home text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-blue-600 p-2 rounded-full">
                    <i class="fas fa-book text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-blue-600 p-2 rounded-full">
                    <i class="fas fa-calendar-alt text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-blue-600 p-2 rounded-full">
                    <i class="fas fa-user text-xl"></i>
                </a>
            </div>
        </div>

        <!-- Teacher Dashboard (initially hidden) -->
        <div id="teacher-dashboard" class="hidden h-screen flex flex-col">
            <!-- Header -->
            <header class="bg-indigo-600 text-white p-4 flex justify-between items-center">
                <button id="teacher-menu-toggle" class="text-white">
                    <i class="fas fa-bars text-xl"></i>
                </button>
                <h1 class="text-xl font-bold">Portal do Professor</h1>
                <div class="relative">
                    <button id="teacher-notification-btn" class="text-white relative">
                        <i class="fas fa-bell text-xl"></i>
                        <span class="notification-badge bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">5</span>
                    </button>
                </div>
            </header>

            <!-- Sidebar -->
            <div id="teacher-sidebar" class="sidebar sidebar-hidden absolute left-0 top-0 h-full w-64 bg-white shadow-lg z-10">
                <div class="p-4 border-b border-gray-200 flex items-center space-x-3">
                    <div class="h-10 w-10 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600">
                        <i class="fas fa-user-tie"></i>
                    </div>
                    <div>
                        <p class="font-medium">Prof. Carlos Silva</p>
                        <p class="text-xs text-gray-500">Matemática/Programação</p>
                    </div>
                </div>
                <nav class="p-2">
                    <a href="#" class="block p-3 rounded-lg hover:bg-indigo-50 text-indigo-600 font-medium">
                        <i class="fas fa-home mr-2"></i> Dashboard
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-users mr-2"></i> Minhas Turmas
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-clipboard-check mr-2"></i> Lançar Notas
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-calendar-check mr-2"></i> Registrar Frequência
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-file-upload mr-2"></i> Enviar Materiais
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-chart-bar mr-2"></i> Estatísticas
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-comments mr-2"></i> Mensagens
                    </a>
                    <a href="#" class="block p-3 rounded-lg hover:bg-gray-100 text-gray-700">
                        <i class="fas fa-cog mr-2"></i> Configurações
                    </a>
                    <button id="teacher-logout-btn" class="w-full text-left p-3 rounded-lg hover:bg-gray-100 text-gray-700 mt-4">
                        <i class="fas fa-sign-out-alt mr-2"></i> Sair
                    </button>
                    <div class="p-3 mt-4 border-t border-gray-200">
                        <button id="teacher-dark-mode-toggle" class="flex items-center space-x-2 text-gray-700">
                            <i class="fas fa-moon"></i>
                            <span>Modo Escuro</span>
                        </button>
                    </div>
                </nav>
            </div>

            <!-- Main Content -->
            <main class="flex-1 overflow-y-auto p-4">
                <!-- Welcome Card -->
                <div class="bg-indigo-50 rounded-xl p-4 mb-4 flex items-center">
                    <div class="h-12 w-12 rounded-full bg-indigo-100 flex items-center justify-center text-indigo-600 mr-3">
                        <i class="fas fa-chalkboard-teacher text-xl"></i>
                    </div>
                    <div>
                        <h2 class="font-bold text-gray-800">Bem-vindo, Professor!</h2>
                        <p class="text-sm text-gray-600">2 turmas - 5 disciplinas</p>
                    </div>
                </div>

                <!-- Classes Summary -->
                <div class="mb-6">
                    <div class="flex justify-between items-center mb-2">
                        <h2 class="font-bold text-lg text-gray-800">Suas Turmas</h2>
                        <a href="#" class="text-indigo-600 text-sm">Ver todas</a>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <h3 class="font-bold text-indigo-600 mb-1">INFO-2023</h3>
                            <p class="text-sm text-gray-600 mb-2">Curso Técnico em Informática</p>
                            <div class="flex justify-between text-xs">
                                <span class="bg-indigo-100 text-indigo-800 px-2 py-1 rounded">32 alunos</span>
                                <span class="bg-green-100 text-green-800 px-2 py-1 rounded">Ativa</span>
                            </div>
                        </div>
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <h3 class="font-bold text-indigo-600 mb-1">ADM-2023</h3>
                            <p class="text-sm text-gray-600 mb-2">Curso Técnico em Administração</p>
                            <div class="flex justify-between text-xs">
                                <span class="bg-indigo-100 text-indigo-800 px-2 py-1 rounded">28 alunos</span>
                                <span class="bg-green-100 text-green-800 px-2 py-1 rounded">Ativa</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Quick Actions -->
                <div class="mb-6">
                    <h2 class="font-bold text-lg text-gray-800 mb-3">Ações Rápidas</h2>
                    <div class="grid grid-cols-2 gap-3">
                        <a href="#" class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition flex items-center">
                            <div class="h-10 w-10 bg-indigo-100 rounded-full flex items-center justify-center text-indigo-600 mr-3">
                                <i class="fas fa-clipboard-check"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Lançar Notas</h3>
                                <p class="text-xs text-gray-600">Prova de Matemática</p>
                            </div>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition flex items-center">
                            <div class="h-10 w-10 bg-green-100 rounded-full flex items-center justify-center text-green-600 mr-3">
                                <i class="fas fa-calendar-check"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Registrar Frequência</h3>
                                <p class="text-xs text-gray-600">Aula de hoje</p>
                            </div>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition flex items-center">
                            <div class="h-10 w-10 bg-blue-100 rounded-full flex items-center justify-center text-blue-600 mr-3">
                                <i class="fas fa-file-upload"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Enviar Material</h3>
                                <p class="text-xs text-gray-600">PDF, links, etc.</p>
                            </div>
                        </a>
                        <a href="#" class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition flex items-center">
                            <div class="h-10 w-10 bg-purple-100 rounded-full flex items-center justify-center text-purple-600 mr-3">
                                <i class="fas fa-chart-bar"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Ver Estatísticas</h3>
                                <p class="text-xs text-gray-600">Desempenho da turma</p>
                            </div>
                        </a>
                    </div>
                </div>

                <!-- Pending Tasks -->
                <div class="mb-6">
                    <div class="flex justify-between items-center mb-3">
                        <h2 class="font-bold text-lg text-gray-800">Tarefas Pendentes</h2>
                        <a href="#" class="text-indigo-600 text-sm">Ver todas</a>
                    </div>
                    <div class="space-y-3">
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-red-100 rounded-full flex items-center justify-center text-red-600 mr-3">
                                    <i class="fas fa-exclamation"></i>
                                </div>
                                <div class="flex-1">
                                    <div class="flex justify-between">
                                        <h3 class="font-medium text-gray-800">Notas Pendentes</h3>
                                        <span class="text-xs bg-red-100 text-red-800 px-2 py-1 rounded">Urgente</span>
                                    </div>
                                    <p class="text-sm text-gray-600">Prova de Programação Web - INFO-2023</p>
                                    <p class="text-xs text-gray-400 mt-1">Prazo: 18/11/2023</p>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white rounded-xl p-4 shadow-sm hover:shadow-md transition">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-yellow-100 rounded-full flex items-center justify-center text-yellow-600 mr-3">
                                    <i class="fas fa-clock"></i>
                                </div>
                                <div>
                                    <h3 class="font-medium text-gray-800">Frequência Atrasada</h3>
                                    <p class="text-sm text-gray-600">Aula de 10/11/2023 - ADM-2023</p>
                                    <p class="text-xs text-gray-400 mt-1">2 dias de atraso</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Upcoming Classes -->
                <div>
                    <h2 class="font-bold text-lg text-gray-800 mb-3">Próximas Aulas</h2>
                    <div class="bg-white rounded-xl p-4 shadow-sm">
                        <div class="flex items-center mb-3">
                            <div class="h-10 w-10 bg-indigo-100 rounded-lg flex items-center justify-center text-indigo-600 mr-3">
                                <i class="fas fa-calendar-day"></i>
                            </div>
                            <div>
                                <h3 class="font-medium">Amanhã</h3>
                                <p class="text-sm text-gray-600">Quarta-feira, 15 de Novembro</p>
                            </div>
                        </div>
                        <div class="space-y-3">
                            <div class="flex items-center p-2 rounded-lg bg-indigo-50">
                                <div class="text-center mr-3">
                                    <p class="text-sm font-medium">08:00</p>
                                    <p class="text-xs text-gray-500">09:40</p>
                                </div>
                                <div>
                                    <h4 class="font-medium">Programação Web</h4>
                                    <p class="text-sm text-gray-600">INFO-2023 - Sala 12</p>
                                </div>
                            </div>
                            <div class="flex items-center p-2 rounded-lg bg-gray-50">
                                <div class="text-center mr-3">
                                    <p class="text-sm font-medium">10:00</p>
                                    <p class="text-xs text-gray-500">11:40</p>
                                </div>
                                <div>
                                    <h4 class="font-medium">Matemática</h4>
                                    <p class="text-sm text-gray-600">ADM-2023 - Sala 8</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </main>

            <!-- Tab Bar -->
            <div class="tab-bar bg-white border-t border-gray-200 flex justify-around items-center p-2">
                <a href="#" class="text-indigo-600 p-2 rounded-full">
                    <i class="fas fa-home text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-indigo-600 p-2 rounded-full">
                    <i class="fas fa-users text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-indigo-600 p-2 rounded-full">
                    <i class="fas fa-clipboard-list text-xl"></i>
                </a>
                <a href="#" class="text-gray-500 hover:text-indigo-600 p-2 rounded-full">
                    <i class="fas fa-user-tie text-xl"></i>
                </a>
            </div>
        </div>

        <!-- Notification Panel -->
        <div id="notification-panel" class="hidden fixed inset-0 bg-black bg-opacity-50 z-40">
            <div class="absolute right-0 top-0 h-full w-80 bg-white shadow-lg">
                <div class="p-4 border-b border-gray-200 flex justify-between items-center">
                    <h3 class="font-bold text-lg">Notificações</h3>
                    <button id="close-notifications" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <div class="overflow-y-auto h-full pb-20">
                    <div class="divide-y divide-gray-200">
                        <div class="p-4 hover:bg-gray-50">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-red-100 rounded-full flex items-center justify-center text-red-600 mr-3">
                                    <i class="fas fa-exclamation"></i>
                                </div>
                                <div>
                                    <h4 class="font-medium">Prova Adiada</h4>
                                    <p class="text-sm text-gray-600">A prova de Matemática foi adiada para sexta-feira.</p>
                                    <p class="text-xs text-gray-400 mt-1">2 horas atrás</p>
                                </div>
                            </div>
                        </div>
                        <div class="p-4 hover:bg-gray-50">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-blue-100 rounded-full flex items-center justify-center text-blue-600 mr-3">
                                    <i class="fas fa-info-circle"></i>
                                </div>
                                <div>
                                    <h4 class="font-medium">Novo Material</h4>
                                    <p class="text-sm text-gray-600">O professor postou novo material de Programação.</p>
                                    <p class="text-xs text-gray-400 mt-1">Ontem</p>
                                </div>
                            </div>
                        </div>
                        <div class="p-4 hover:bg-gray-50">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-green-100 rounded-full flex items-center justify-center text-green-600 mr-3">
                                    <i class="fas fa-check-circle"></i>
                                </div>
                                <div>
                                    <h4 class="font-medium">Pagamento Confirmado</h4>
                                    <p class="text-sm text-gray-600">Seu pagamento de novembro foi confirmado.</p>
                                    <p class="text-xs text-gray-400 mt-1">3 dias atrás</p>
                                </div>
                            </div>
                        </div>
                        <div class="p-4 hover:bg-gray-50">
                            <div class="flex items-start">
                                <div class="h-8 w-8 bg-yellow-100 rounded-full flex items-center justify-center text-yellow-600 mr-3">
                                    <i class="fas fa-calendar-alt"></i>
                                </div>
                                <div>
                                    <h4 class="font-medium">Evento Amanhã</h4>
                                    <p class="text-sm text-gray-600">Palestra sobre carreiras em TI às 14h no auditório.</p>
                                    <p class="text-xs text-gray-400 mt-1">5 dias atrás</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // App State
        let currentUser = null;
        let darkMode = false;

        // DOM Elements
        const splashScreen = document.getElementById('splash');
        const loginScreen = document.getElementById('login-screen');
        const loginForm = document.getElementById('login-form');
        const forgotPasswordLink = document.getElementById('forgot-password');
        const forgotPasswordModal = document.getElementById('forgot-password-modal');
        const closeForgotPassword = document.getElementById('close-forgot-password');
        const recoveryForm = document.getElementById('recovery-form');
        const studentDashboard = document.getElementById('student-dashboard');
        const teacherDashboard = document.getElementById('teacher-dashboard');
        const menuToggle = document.getElementById('menu-toggle');
        const sidebar = document.getElementById('sidebar');
        const notificationBtn = document.getElementById('notification-btn');
        const notificationPanel = document.getElementById('notification-panel');
        const closeNotifications = document.getElementById('close-notifications');
        const logoutBtn = document.getElementById('logout-btn');
        const darkModeToggle = document.getElementById('dark-mode-toggle');
        const teacherMenuToggle = document.getElementById('teacher-menu-toggle');
        const teacherSidebar = document.getElementById('teacher-sidebar');
        const teacherNotificationBtn = document.getElementById('teacher-notification-btn');
        const teacherLogoutBtn = document.getElementById('teacher-logout-btn');
        const teacherDarkModeToggle = document.getElementById('teacher-dark-mode-toggle');
        const loadingBar = document.getElementById('loading-bar');

        // Simulate splash screen loading
        let progress = 0;
        const loadingInterval = setInterval(() => {
            progress += 5;
            loadingBar.style.width = `${progress}%`;
            
            if (progress >= 100) {
                clearInterval(loadingInterval);
                splashScreen.classList.add('hidden');
                loginScreen.classList.remove('hidden');
            }
        }, 100);

        // Login Form Submission
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            // Simple validation
            if (!username || !password) {
                alert('Por favor, preencha todos os campos.');
                return;
            }
            
            // Simulate authentication
            if (username === 'aluno' && password === '123456') {
                currentUser = 'student';
                loginScreen.classList.add('hidden');
                studentDashboard.classList.remove('hidden');
            } else if (username === 'professor' && password === '123456') {
                currentUser = 'teacher';
                loginScreen.classList.add('hidden');
                teacherDashboard.classList.remove('hidden');
            } else {
                alert('Usuário ou senha incorretos.');
            }
        });

        // Forgot Password Flow
        forgotPasswordLink.addEventListener('click', (e) => {
            e.preventDefault();
            forgotPasswordModal.classList.remove('hidden');
        });

        closeForgotPassword.addEventListener('click', () => {
            forgotPasswordModal.classList.add('hidden');
        });

        recoveryForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('recovery-email').value;
            
            if (!email) {
                alert('Por favor, insira seu e-mail.');
                return;
            }
            
            alert(`Instruções de recuperação enviadas para ${email}`);
            forgotPasswordModal.classList.add('hidden');
        });

        // Student Dashboard Interactions
        menuToggle.addEventListener('click', () => {
            sidebar.classList.toggle('sidebar-hidden');
        });

        notificationBtn.addEventListener('click', () => {
            notificationPanel.classList.remove('hidden');
        });

        closeNotifications.addEventListener('click', () => {
            notificationPanel.classList.add('hidden');
        });

        logoutBtn.addEventListener('click', () => {
            currentUser = null;
            studentDashboard.classList.add('hidden');
            loginScreen.classList.remove('hidden');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            sidebar.classList.add('sidebar-hidden');
        });

        darkModeToggle.addEventListener('click', () => {
            darkMode = !darkMode;
            document.body.classList.toggle('dark-mode');
            studentDashboard.classList.toggle('dark-mode');
            
            // Toggle cards dark mode
            const cards = document.querySelectorAll('#student-dashboard .bg-white');
            cards.forEach(card => {
                card.classList.toggle('dark-mode-card');
                card.classList.toggle('bg-white');
            });
        });

        // Teacher Dashboard Interactions
        teacherMenuToggle.addEventListener('click', () => {
            teacherSidebar.classList.toggle('sidebar-hidden');
        });

        teacherNotificationBtn.addEventListener('click', () => {
            notificationPanel.classList.remove('hidden');
        });

        teacherLogoutBtn.addEventListener('click', () => {
            currentUser = null;
            teacherDashboard.classList.add('hidden');
            loginScreen.classList.remove('hidden');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            teacherSidebar.classList.add('sidebar-hidden');
        });

        teacherDarkModeToggle.addEventListener('click', () => {
            darkMode = !darkMode;
            document.body.classList.toggle('dark-mode');
            teacherDashboard.classList.toggle('dark-mode');
            
            // Toggle cards dark mode
            const cards = document.querySelectorAll('#teacher-dashboard .bg-white');
            cards.forEach(card => {
                card.classList.toggle('dark-mode-card');
                card.classList.toggle('bg-white');
            });
        });

        // Close sidebar when clicking outside
        document.addEventListener('click', (e) => {
            if (!sidebar.classList.contains('sidebar-hidden') && 
                !e.target.closest('#sidebar') && 
                !e.target.closest('#menu-toggle')) {
                sidebar.classList.add('sidebar-hidden');
            }
            
            if (!teacherSidebar.classList.contains('sidebar-hidden') && 
                !e.target.closest('#teacher-sidebar') && 
                !e.target.closest('#teacher-menu-toggle')) {
                teacherSidebar.classList.add('sidebar-hidden');
            }
            
            if (!notificationPanel.classList.contains('hidden') && 
                !e.target.closest('#notification-panel') && 
                !e.target.closest('#notification-btn') &&
                !e.target.closest('#teacher-notification-btn')) {
                notificationPanel.classList.add('hidden');
            }
        });
    </script>
</body>

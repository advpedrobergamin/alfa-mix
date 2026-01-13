<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎯 Alfa Mix – Gerenciador de Tarefas</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&family=Nunito:wght@400;500;600;700&display=swap');

        :root {
            --color-primary: #5B7FFF;
            --color-primary-hover: #4A6FE8;
            --color-primary-active: #3860D1;
            --color-secondary: #6B5CFF;
            --color-success: #10B981;
            --color-warning: #F59E0B;
            --color-danger: #EF4444;
            --color-info: #06B6D4;
            --color-bg-light: #F8FAFC;
            --color-bg-white: #FFFFFF;
            --color-text: #1F2937;
            --color-text-muted: #6B7280;
            --color-border: #E5E7EB;
            --color-border-light: #F3F4F6;
            --space-4: 4px;
            --space-8: 8px;
            --space-12: 12px;
            --space-16: 16px;
            --space-24: 24px;
            --space-32: 32px;
            --radius-base: 12px;
            --radius-lg: 16px;
            --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.08);
            --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.12);
            --shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.15);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            font-family: 'Poppins', 'Nunito', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #F5F7FB 0%, #F8FAFC 100%);
            color: var(--color-text);
            height: 100%;
        }

        body {
            display: flex;
        }

        /* Layout Principal */
        .container-main {
            width: 100%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .header {
            background: var(--color-bg-white);
            border-bottom: none;
            padding: var(--space-24);
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: var(--shadow-sm);
        }

        .header-title {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header-user {
            display: flex;
            gap: var(--space-16);
            align-items: center;
            font-size: 14px;
        }

        .content {
            flex: 1;
            padding: var(--space-32);
            overflow-y: auto;
            background: linear-gradient(135deg, #F5F7FB 0%, #F8FAFC 100%);
        }

        /* Tela Inicial */
        .screen {
            display: none;
        }

        .screen.active {
            display: flex;
        }

        .screen-home {
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--space-32);
            text-align: center;
            min-height: 100vh;
        }

        .home-title {
            font-size: 48px;
            font-weight: 700;
            margin-bottom: var(--space-16);
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .home-subtitle {
            font-size: 16px;
            color: var(--color-text-muted);
            margin-bottom: var(--space-32);
        }

        .button-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: var(--space-16);
            max-width: 800px;
        }

        /* Botões */
        .btn {
            padding: var(--space-16) var(--space-24);
            border: none;
            border-radius: var(--radius-base);
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: var(--space-8);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            color: white;
            box-shadow: var(--shadow-md);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-lg);
        }

        .btn-secondary {
            background-color: var(--color-bg-white);
            color: var(--color-text);
            border: 2px solid var(--color-border);
        }

        .btn-secondary:hover {
            background-color: var(--color-bg-light);
            border-color: var(--color-primary);
        }

        .btn-danger {
            background-color: var(--color-danger);
            color: white;
            padding: var(--space-8) var(--space-16);
            font-size: 14px;
        }

        .btn-danger:hover {
            opacity: 0.9;
        }

        .btn-small {
            padding: var(--space-8) var(--space-12);
            font-size: 13px;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--color-bg-white);
            border-radius: var(--radius-lg);
            padding: var(--space-32);
            max-width: 420px;
            width: 90%;
            box-shadow: var(--shadow-lg);
        }

        .modal-title {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: var(--space-24);
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .form-group {
            margin-bottom: var(--space-16);
        }

        .form-label {
            display: block;
            font-size: 14px;
            font-weight: 500;
            margin-bottom: var(--space-8);
        }

        .form-control {
            width: 100%;
            padding: var(--space-12);
            border: 2px solid var(--color-border);
            border-radius: var(--radius-base);
            font-size: 14px;
            font-family: inherit;
            transition: all 0.3s ease;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--color-primary);
            box-shadow: 0 0 0 4px rgba(91, 127, 255, 0.1);
        }

        .form-error {
            color: var(--color-danger);
            font-size: 13px;
            margin-top: var(--space-8);
        }

        /* Cards de Tarefas */
        .task-card {
            background: var(--color-bg-white);
            border: none;
            border-radius: var(--radius-lg);
            padding: var(--space-16);
            margin-bottom: var(--space-16);
            display: flex;
            gap: var(--space-16);
            align-items: flex-start;
            box-shadow: var(--shadow-sm);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .task-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-md);
        }

        .task-checkbox {
            width: 20px;
            height: 20px;
            margin-top: var(--space-8);
            cursor: pointer;
        }

        .task-content {
            flex: 1;
        }

        .task-title {
            font-weight: 600;
            font-size: 15px;
            margin-bottom: var(--space-8);
        }

        .task-priority {
            display: inline-block;
            padding: var(--space-4) var(--space-12);
            border-radius: var(--radius-base);
            font-size: 11px;
            font-weight: 700;
            margin-right: var(--space-8);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .task-priority.alta {
            background: rgba(239, 68, 68, 0.15);
            color: var(--color-danger);
        }

        .task-priority.media {
            background: rgba(245, 158, 11, 0.15);
            color: var(--color-warning);
        }

        .task-priority.baixa {
            background: rgba(16, 185, 129, 0.15);
            color: var(--color-success);
        }

        .task-description {
            font-size: 13px;
            color: var(--color-text-muted);
            margin-bottom: var(--space-8);
        }

        .task-meta {
            font-size: 12px;
            color: var(--color-text-muted);
        }

        .task-actions {
            display: flex;
            gap: var(--space-8);
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 0;
            border-bottom: 2px solid var(--color-border);
            margin-bottom: var(--space-24);
        }

        .tab-button {
            padding: var(--space-12) var(--space-24);
            border: none;
            background: transparent;
            cursor: pointer;
            font-size: 14px;
            font-weight: 500;
            color: var(--color-text-muted);
            border-bottom: 3px solid transparent;
            margin-bottom: -2px;
            transition: all 0.3s ease;
        }

        .tab-button.active {
            color: var(--color-primary);
            border-bottom-color: var(--color-primary);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Filters */
        .filter-bar {
            display: flex;
            gap: var(--space-12);
            margin-bottom: var(--space-24);
        }

        .filter-btn {
            padding: var(--space-8) var(--space-16);
            border: 2px solid var(--color-border);
            background: var(--color-bg-white);
            border-radius: var(--radius-base);
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .filter-btn.active {
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            color: white;
            border-color: transparent;
            box-shadow: var(--shadow-md);
        }

        /* Search */
        .search-box {
            margin-bottom: var(--space-24);
        }

        .search-box input {
            width: 100%;
            max-width: 400px;
        }

        /* Dashboard Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: var(--space-16);
            margin-bottom: var(--space-24);
        }

        .stat-card {
            background: var(--color-bg-white);
            border: none;
            border-radius: var(--radius-lg);
            padding: var(--space-24);
            text-align: center;
            box-shadow: var(--shadow-sm);
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            box-shadow: var(--shadow-md);
            transform: translateY(-2px);
        }

        .stat-number {
            font-size: 36px;
            font-weight: 700;
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: var(--space-12);
        }

        .stat-label {
            font-size: 13px;
            color: var(--color-text-muted);
        }

        /* Form Grid */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: var(--space-16);
            margin-bottom: var(--space-16);
        }

        /* Kanban */
        .kanban-container {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: var(--space-16);
            overflow-x: auto;
        }

        .kanban-column {
            background: var(--color-border-light);
            border-radius: var(--radius-lg);
            padding: var(--space-20);
            min-width: 260px;
            box-shadow: var(--shadow-sm);
            transition: all 0.3s ease;
        }

        .kanban-column.segunda { background: linear-gradient(135deg, #FEF3C7 0%, #FDE68A 100%); border-top: 4px solid #F59E0B; }
        .kanban-column.terca { background: linear-gradient(135deg, #DBEAFE 0%, #BFDBFE 100%); border-top: 4px solid #3B82F6; }
        .kanban-column.quarta { background: linear-gradient(135deg, #DCFCE7 0%, #BBFBEE 100%); border-top: 4px solid #10B981; }
        .kanban-column.quinta { background: linear-gradient(135deg, #F3E8FF 0%, #E9D5FF 100%); border-top: 4px solid #8B5CF6; }
        .kanban-column.sexta { background: linear-gradient(135deg, #FE2E2E0D 0%, #FCA5A5 100%); border-top: 4px solid #EF4444; }
        .kanban-column.sabado { background: linear-gradient(135deg, #FED7AA 0%, #FDBA74 100%); border-top: 4px solid #F97316; }
        .kanban-column.domingo { background: linear-gradient(135deg, #E0E7FF 0%, #C7D2FE 100%); border-top: 4px solid #6366F1; }

        .kanban-title {
            font-weight: 700;
            font-size: 16px;
            margin-bottom: var(--space-20);
            text-align: center;
            color: var(--color-text);
            padding-bottom: var(--space-12);
            border-bottom: 2px solid rgba(0, 0, 0, 0.08);
        }

        /* User List */
        .user-item {
            background: var(--color-bg-white);
            border: none;
            border-radius: var(--radius-lg);
            padding: var(--space-16);
            margin-bottom: var(--space-12);
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: var(--shadow-sm);
            transition: all 0.3s ease;
        }

        .user-item:hover {
            box-shadow: var(--shadow-md);
            transform: translateY(-2px);
        }

        .user-info {
            flex: 1;
        }

        .user-name {
            font-weight: 600;
            font-size: 14px;
        }

        .user-type {
            font-size: 12px;
            color: var(--color-text-muted);
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: var(--space-32);
            color: var(--color-text-muted);
        }

        .empty-state-icon {
            font-size: 48px;
            margin-bottom: var(--space-16);
        }

        /* Logout Button */
        .btn-logout {
            background-color: var(--color-danger);
            color: white;
        }

        .btn-logout:hover {
            opacity: 0.9;
        }

        /* Responsivo */
        @media (max-width: 768px) {
            .button-grid {
                grid-template-columns: 1fr;
            }

            .kanban-container {
                grid-template-columns: repeat(4, 1fr);
            }

            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .form-grid {
                grid-template-columns: 1fr;
            }

            .header {
                flex-direction: column;
                gap: var(--space-16);
            }
        }
    </style>
</head>
<body>
    <div class="container-main">
        <!-- TELA INICIAL -->
        <div id="screen-home" class="screen active screen-home">
            <div>
                <h1 class="home-title">🎯 Alfa Mix</h1>
                <p class="home-subtitle">Gerenciador de Tarefas Operacional</p>
            </div>
            <div class="button-grid">
                <button class="btn btn-primary" onclick="openModal('login-modal'); setLoginType('funcionario')">
                    👥 Sou Funcionário
                </button>
                <button class="btn btn-primary" onclick="openModal('senha-modal')">
                    🔐 Sou Admin
                </button>
                <button class="btn btn-primary" onclick="openModal('login-modal'); setLoginType('gerente')">
                    👔 Sou Gerente
                </button>
                <button class="btn btn-primary" onclick="openModal('login-modal'); setLoginType('lider')">
                    ⭐ Sou Líder
                </button>
            </div>
        </div>

        <!-- PAINEL FUNCIONÁRIO -->
        <div id="screen-funcionario" class="screen">
            <div class="header">
                <div style="display: flex; align-items: center; gap: var(--space-16);">
                    <div>
                        <h1 class="header-title">👥 Painel do Funcionário</h1>
                        <p style="color: var(--color-text-muted); font-size: 13px; margin-top: var(--space-4);">Suas tarefas da semana</p>
                    </div>
                </div>
                <div class="header-user">
                    <span id="user-display" style="font-weight: 600;">Funcionário</span>
                </div>
            </div>
            <div class="content" style="display: flex; flex-direction: column;">
                <!-- RESUMO RÁPIDO -->
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: var(--space-16); margin-bottom: var(--space-32);">
                    <div class="stat-card" style="background: linear-gradient(135deg, #FFEAA7 0%, #FDD835 100%); border: none; cursor: default;">
                        <div style="font-size: 24px; font-weight: 700; color: #F59E0B;">📊</div>
                        <div style="font-size: 20px; font-weight: 700; color: #F59E0B; margin-top: var(--space-8);" id="total-tasks-count">0</div>
                        <div style="font-size: 12px; color: #A67C00; margin-top: var(--space-4);">Total de Tarefas</div>
                    </div>
                    <div class="stat-card" style="background: linear-gradient(135deg, #FFB6C1 0%, #FF6B9D 100%); border: none; cursor: default;">
                        <div style="font-size: 24px; font-weight: 700; color: #EF4444;">⏳</div>
                        <div style="font-size: 20px; font-weight: 700; color: #EF4444; margin-top: var(--space-8);" id="pending-tasks-count">0</div>
                        <div style="font-size: 12px; color: #B91C1C; margin-top: var(--space-4);">Pendentes</div>
                    </div>
                    <div class="stat-card" style="background: linear-gradient(135deg, #A7F3D0 0%, #10B981 100%); border: none; cursor: default;">
                        <div style="font-size: 24px; font-weight: 700; color: #10B981;">✅</div>
                        <div style="font-size: 20px; font-weight: 700; color: #10B981; margin-top: var(--space-8);" id="completed-tasks-count">0</div>
                        <div style="font-size: 12px; color: #047857; margin-top: var(--space-4);">Concluídas</div>
                    </div>
                </div>

                <!-- FILTROS FIXOS -->
                <div style="display: flex; gap: var(--space-12); margin-bottom: var(--space-32); flex-wrap: wrap;">
                    <button class="filter-btn active" onclick="filterTasks('todas', 'funcionario')" style="padding: var(--space-12) var(--space-20); font-size: 14px;">📋 Todas</button>
                    <button class="filter-btn" onclick="filterTasks('pendentes', 'funcionario')" style="padding: var(--space-12) var(--space-20); font-size: 14px;">⏳ Pendentes</button>
                    <button class="filter-btn" onclick="filterTasks('concluidas', 'funcionario')" style="padding: var(--space-12) var(--space-20); font-size: 14px;">✅ Concluídas</button>
                </div>

                <!-- KANBAN COM CORES SUAVES POR DIA -->
                <div class="kanban-container" id="kanban-funcionario" style="flex: 1; margin-bottom: var(--space-32);"></div>

                <!-- BOTÃO SAIR NO FINAL -->
                <div style="display: flex; gap: var(--space-12);">
                    <button class="btn btn-logout" onclick="logout()" style="padding: var(--space-12) var(--space-32); font-size: 14px; width: 100%; max-width: 200px;">🚪 Sair</button>
                </div>
            </div>
        </div>

        <!-- PAINEL ADMIN -->
        <div id="screen-admin" class="screen">
            <div class="header">
                <h1 class="header-title">⚙️ Painel Admin</h1>
                <div class="header-user">
                    <span>Admin</span>
                    <button class="btn btn-secondary btn-small" onclick="salvarBackupLocal()" title="Fazer backup manual agora">💾 Backup</button>
                    <button class="btn btn-logout btn-small" onclick="logout()">🚪 Sair</button>
                </div>
            </div>
            <div class="content">
                <div class="tabs">
                    <button class="tab-button active" onclick="switchTab('dashboard', 'admin')">📊 Dashboard</button>
                    <button class="tab-button" onclick="switchTab('tarefas', 'admin')">📋 Tarefas</button>
                    <button class="tab-button" onclick="switchTab('usuarios', 'admin')">👥 Usuários</button>
                    <button class="tab-button" onclick="switchTab('produtividade', 'admin')">📈 Produtividade</button>
                </div>

                <!-- ABA DASHBOARD -->
                <div id="admin-dashboard" class="tab-content active">
                    <div class="stats-grid" id="dashboard-stats"></div>
                    <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-16);">
                        <h3 style="margin-bottom: var(--space-16);">📜 Últimas Atividades</h3>
                        <div id="activities-list"></div>
                    </div>
                </div>

                <!-- ABA TAREFAS -->
                <div id="admin-tarefas" class="tab-content">
                    <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-16); margin-bottom: var(--space-24);">
                        <div style="display: flex; gap: var(--space-16); margin-bottom: var(--space-16); flex-wrap: wrap; align-items: flex-start;">
                            <div style="flex: 1; min-width: 300px;">
                                <h3 style="margin-bottom: var(--space-16);">➕ Nova Tarefa</h3>
                            </div>
                            <div style="display: flex; gap: var(--space-8); flex-wrap: wrap;">
                                <button class="btn btn-secondary" onclick="downloadExcelTemplate()" title="Baixar modelo em Excel">📥 Baixar Modelo Excel</button>
                                <button class="btn btn-secondary" onclick="document.getElementById('excel-upload-input').click()" title="Importar tarefas de um arquivo Excel">📤 Importar Excel</button>
                                <input type="file" id="excel-upload-input" accept=".xlsx,.xls,.csv" style="display: none;" onchange="handleExcelUpload(event)">
                            </div>
                        </div>
                        <form id="form-nova-tarefa" onsubmit="addTask(event)">
                            <div class="form-grid">
                                <div class="form-group">
                                    <label class="form-label">Título</label>
                                    <input class="form-control" type="text" id="task-title" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Atribuir</label>
                                    <select class="form-control" id="task-assign" required>
                                        <option value="">Selecionar usuário</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Dia da Semana</label>
                                    <select class="form-control" id="task-day">
                                        <option>Segunda</option>
                                        <option>Terça</option>
                                        <option>Quarta</option>
                                        <option>Quinta</option>
                                        <option>Sexta</option>
                                        <option>Sábado</option>
                                        <option>Domingo</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Data Limite</label>
                                    <input class="form-control" type="date" id="task-date" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Prioridade</label>
                                    <select class="form-control" id="task-priority">
                                        <option>alta</option>
                                        <option>media</option>
                                        <option>baixa</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Tipo</label>
                                    <select class="form-control" id="task-type">
                                        <option value="funcionario">Funcionário</option>
                                        <option value="lider">Líder</option>
                                    </select>
                                </div>
                            </div>
                            <div class="form-group">
                                <label class="form-label">Descrição</label>
                                <textarea class="form-control" id="task-description" style="resize: vertical; min-height: 80px;"></textarea>
                            </div>
                            <div style="display: flex; gap: var(--space-12);">
                                <button type="submit" class="btn btn-primary">💾 Adicionar Tarefa</button>
                                <button type="button" class="btn btn-secondary" onclick="openModal('modal-semana-completa')">📅 Semana Completa</button>
                                <button type="button" class="btn btn-secondary" onclick="openModal('modal-replicar-semana')">📄 Replicar Semana</button>
                            </div>
                        </form>
                    </div>

                    <div class="search-box">
                        <input class="form-control" type="text" placeholder="🔍 Buscar tarefa…" id="search-tasks" onkeyup="searchTasks('admin')">
                    </div>
                    <div class="filter-bar">
                        <button class="filter-btn active" onclick="filterTasks('todas', 'admin')">Todas</button>
                        <button class="filter-btn" onclick="filterTasks('pendentes', 'admin')">⏳ Pendentes</button>
                        <button class="filter-btn" onclick="filterTasks('concluidas', 'admin')">✅ Concluídas</button>
                    </div>
                    <div id="tasks-admin"></div>
                </div>

                <!-- ABA PRODUTIVIDADE -->
                <div id="admin-produtividade" class="tab-content">
                    <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-24); margin-bottom: var(--space-24);">
                        <h3 style="margin-bottom: var(--space-16); font-size: 18px; font-weight: 700;">📈 Análise de Produtividade</h3>
                        <div class="form-grid" style="margin-bottom: var(--space-24);">
                            <div class="form-group">
                                <label class="form-label">Selecione um Usuário</label>
                                <select class="form-control" id="filtro-usuario-produtividade" onchange="renderProdutividade()">
                                    <option value="">📊 Todos os Usuários</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label class="form-label">Período de Análise</label>
                                <select class="form-control" id="filtro-periodo-produtividade" onchange="renderProdutividade()">
                                    <option value="semana">📅 Semana Atual</option>
                                    <option value="mes">📅 Mês Atual</option>
                                    <option value="30dias">📅 Últimos 30 Dias</option>
                                    <option value="todos">📅 Todos os Períodos</option>
                                </select>
                            </div>
                        </div>

                        <!-- Métricas em Cards -->
                        <div class="stats-grid" id="produtividade-stats" style="margin-bottom: var(--space-32);"></div>

                        <!-- Gráfico de Produtividade -->
                        <div style="background: linear-gradient(135deg, #F5F7FB 0%, #F8FAFC 100%); border: 1px solid var(--color-border); border-radius: var(--radius-lg); padding: var(--space-24); margin-top: var(--space-24);">
                            <h4 style="margin-bottom: var(--space-16); font-weight: 700;">📊 Tarefas Concluídas por Dia</h4>
                            <div id="grafico-produtividade" style="display: flex; align-items: flex-end; justify-content: center; gap: var(--space-8); height: 250px; padding: var(--space-16); background: var(--color-bg-white); border-radius: var(--radius-base);"></div>
                        </div>

                        <!-- Tabela Detalhada -->
                        <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-lg); padding: var(--space-24); margin-top: var(--space-24);">
                            <h4 style="margin-bottom: var(--space-16); font-weight: 700;">📋 Detalhes das Tarefas</h4>
                            <div id="tabela-produtividade"></div>
                        </div>
                    </div>
                </div>

                <!-- ABA USUÁRIOS -->
                <div id="admin-usuarios" class="tab-content">
                    <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-16); margin-bottom: var(--space-24);">
                        <h3 style="margin-bottom: var(--space-16);">➕ Novo Usuário</h3>
                        <form id="form-novo-usuario" onsubmit="addUser(event)">
                            <div class="form-grid">
                                <div class="form-group">
                                    <label class="form-label">Nome</label>
                                    <input class="form-control" type="text" id="user-name" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Login</label>
                                    <input class="form-control" type="text" id="user-login" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Senha</label>
                                    <input class="form-control" type="password" id="user-password" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Perfil</label>
                                    <select class="form-control" id="user-profile">
                                        <option value="funcionario">Funcionário</option>
                                        <option value="gerente">Gerente</option>
                                        <option value="lider">Líder</option>
                                    </select>
                                </div>
                            </div>
                            <div class="form-group">
                                <label style="display: flex; align-items: center; gap: var(--space-8); cursor: pointer;">
                                    <input type="checkbox" id="user-proprietaria" style="cursor: pointer;">
                                    <span>É proprietária?</span>
                                </label>
                            </div>
                            <button type="submit" class="btn btn-primary">➕ Criar Usuário</button>
                        </form>
                    </div>

                    <div class="search-box">
                        <input class="form-control" type="text" placeholder="🔍 Buscar usuário…" id="search-users" onkeyup="searchUsers()">
                    </div>
                    <div id="users-list"></div>
                </div>
            </div>
        </div>

        <!-- PAINEL GERENTE -->
        <div id="screen-gerente" class="screen">
            <div class="header">
                <h1 class="header-title">👔 Painel do Gerente</h1>
                <div class="header-user">
                    <span id="user-display-gerente">Gerente</span>
                    <button class="btn btn-logout btn-small" onclick="logout()">🚪 Sair</button>
                </div>
            </div>
            <div class="content">
                <div class="tabs">
                    <button class="tab-button active" onclick="switchTab('kanban', 'gerente')">📊 Kanban</button>
                    <button class="tab-button" onclick="switchTab('por-pessoa', 'gerente')">👥 Por Pessoa</button>
                </div>

                <!-- ABA KANBAN -->
                <div id="gerente-kanban" class="tab-content active">
                    <div style="background: var(--color-bg-white); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-16); margin-bottom: var(--space-24);">
                        <h3 style="margin-bottom: var(--space-16);">➕ Nova Tarefa</h3>
                        <form id="form-tarefa-gerente" onsubmit="addTaskGerente(event)">
                            <div class="form-grid">
                                <div class="form-group">
                                    <label class="form-label">Título</label>
                                    <input class="form-control" type="text" id="gerente-task-title" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Atribuir</label>
                                    <select class="form-control" id="gerente-task-assign" required></select>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Dia da Semana</label>
                                    <select class="form-control" id="gerente-task-day">
                                        <option>Segunda</option>
                                        <option>Terça</option>
                                        <option>Quarta</option>
                                        <option>Quinta</option>
                                        <option>Sexta</option>
                                        <option>Sábado</option>
                                        <option>Domingo</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Data Limite</label>
                                    <input class="form-control" type="date" id="gerente-task-date" required>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">Prioridade</label>
                                    <select class="form-control" id="gerente-task-priority">
                                        <option>alta</option>
                                        <option>media</option>
                                        <option>baixa</option>
                                    </select>
                                </div>
                            </div>
                            <div class="form-group">
                                <label class="form-label">Descrição</label>
                                <textarea class="form-control" id="gerente-task-description" style="resize: vertical; min-height: 80px;"></textarea>
                            </div>
                            <button type="submit" class="btn btn-primary">💾 Adicionar Tarefa</button>
                        </form>
                    </div>

                    <h3 style="margin-bottom: var(--space-16);">📊 Visualização Semanal</h3>
                    <div class="kanban-container" id="kanban-board"></div>
                </div>

                <!-- ABA POR PESSOA -->
                <div id="gerente-por-pessoa" class="tab-content">
                    <div class="form-group" style="max-width: 300px; margin-bottom: var(--space-24);">
                        <label class="form-label">Selecionar Pessoa</label>
                        <select class="form-control" id="select-pessoa" onchange="filterTasksByPerson()"></select>
                    </div>
                    <div id="tasks-por-pessoa"></div>
                </div>
            </div>
        </div>

        <!-- PAINEL LÍDER -->
        <div id="screen-lider" class="screen">
            <div class="header">
                <h1 class="header-title">⭐ Painel do Líder</h1>
                <div class="header-user">
                    <span id="user-display-lider">Líder</span>
                    <button class="btn btn-logout btn-small" onclick="logout()">🚪 Sair</button>
                </div>
            </div>
            <div class="content">
                <div id="tasks-lider"></div>
            </div>
        </div>
    </div>

    <!-- MODAL LOGIN -->
    <div id="login-modal" class="modal">
        <div class="modal-content">
            <h2 class="modal-title">Fazer Login</h2>
            <form onsubmit="handleLogin(event)">
                <div class="form-group">
                    <label class="form-label">Login</label>
                    <input class="form-control" type="text" id="login-input" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Senha</label>
                    <input class="form-control" type="password" id="password-input" required>
                </div>
                <div id="login-error" class="form-error" style="display: none;"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">Entrar</button>
                <button type="button" class="btn btn-secondary" style="width: 100%; margin-top: var(--space-12);" onclick="closeModal('login-modal')">Cancelar</button>
            </form>
        </div>
    </div>

    <!-- MODAL SENHA ADMIN -->
    <div id="senha-modal" class="modal">
        <div class="modal-content">
            <h2 class="modal-title">Login Admin</h2>
            <form onsubmit="handleAdminLogin(event)">
                <div class="form-group">
                    <label class="form-label">Senha de Administrador</label>
                    <input class="form-control" type="password" id="admin-password-input" required>
                </div>
                <div id="admin-error" class="form-error" style="display: none;"></div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">Entrar</button>
                <button type="button" class="btn btn-secondary" style="width: 100%; margin-top: var(--space-12);" onclick="closeModal('senha-modal')">Cancelar</button>
            </form>
        </div>
    </div>

    <!-- MODAL CONFIRMAÇÃO DELETAR -->
    <div id="delete-modal" class="modal">
        <div class="modal-content" style="max-width: 350px;">
            <h2 class="modal-title">Confirmar Deleção</h2>
            <p style="margin-bottom: var(--space-24); color: var(--color-text-muted);">Tem certeza que deseja deletar este item?</p>
            <div style="display: flex; gap: var(--space-12);">
                <button class="btn btn-secondary" onclick="closeModal('delete-modal')" style="flex: 1;">Cancelar</button>
                <button class="btn btn-danger" onclick="confirmDelete()" style="flex: 1;">Deletar</button>
            </div>
        </div>
    </div>

    <!-- MODAL SEMANA COMPLETA -->
    <div id="modal-semana-completa" class="modal">
        <div class="modal-content" style="max-width: 600px; max-height: 80vh; overflow-y: auto;">
            <h2 class="modal-title">📅 Criar Semana Completa</h2>
            <form onsubmit="createWeeklyTasks(event)">
                <div class="form-group">
                    <label class="form-label">Atribuir Semana Para</label>
                    <select class="form-control" id="semana-assign" required>
                        <option value="">Selecionar funcionário</option>
                    </select>
                </div>

                <h4 style="margin-top: var(--space-24); margin-bottom: var(--space-16); font-weight: 700;">Tarefas por Dia</h4>

                <div id="dias-semana-container"></div>

                <div style="display: flex; gap: var(--space-12); margin-top: var(--space-24);">
                    <button type="submit" class="btn btn-primary" style="flex: 1;">✅ Criar Semana</button>
                    <button type="button" class="btn btn-secondary" style="flex: 1;" onclick="closeModal('modal-semana-completa')">Cancelar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL REPLICAR SEMANA -->
    <div id="modal-replicar-semana" class="modal">
        <div class="modal-content" style="max-width: 420px;">
            <h2 class="modal-title">📄 Replicar Semana</h2>
            <form onsubmit="replicateWeeklyTasks(event)">
                <div class="form-group">
                    <label class="form-label">Funcionário Origem</label>
                    <select class="form-control" id="replica-origem" required>
                        <option value="">Selecionar origem</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label">Funcionário Destino</label>
                    <select class="form-control" id="replica-destino" required>
                        <option value="">Selecionar destino</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label">Período de Cópia</label>
                    <select class="form-control" id="replica-periodo" required>
                        <option value="semana">Semana Atual</option>
                        <option value="proxima">Próxima Semana</option>
                        <option value="mes">Este Mês</option>
                    </select>
                </div>
                <div style="display: flex; gap: var(--space-12); margin-top: var(--space-24);">
                    <button type="submit" class="btn btn-primary" style="flex: 1;">📋 Replicar</button>
                    <button type="button" class="btn btn-secondary" style="flex: 1;" onclick="closeModal('modal-replicar-semana')">Cancelar</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // DADOS
        let currentUser = null;
        let currentProfile = null;
        let loginType = null;
        let deleteTarget = null;
        let currentFilter = 'todas';
        let currentSearchQuery = '';
        const ADMIN_PASSWORD = 'admin123';

        // Base de dados mockada
        const database = {
            funcionarios: [
                { id: 1, nome: 'João Silva', login: 'joao', senha: '123456', perfil: 'funcionario', proprietaria: false },
                { id: 2, nome: 'Maria Santos', login: 'maria', senha: '123456', perfil: 'funcionario', proprietaria: true },
                { id: 3, nome: 'Pedro Gerente', login: 'pedro', senha: '123456', perfil: 'gerente', proprietaria: false },
                { id: 4, nome: 'Ana Líder', login: 'ana', senha: '123456', perfil: 'lider', proprietaria: false }
            ],
            tarefas: [
                { id: 1, titulo: 'Revisar relatório', descricao: 'Verificar dados do mês', atribuido: 1, data: '2026-01-20', dia: 'Segunda', prioridade: 'alta', tipo: 'funcionario', concluida: false, criadaEm: '2026-01-13T08:00:00', concluidaEm: null },
                { id: 2, titulo: 'Preparar apresentação', descricao: 'Slides para reunião com cliente', atribuido: 2, data: '2026-01-21', dia: 'Terça', prioridade: 'media', tipo: 'funcionario', concluida: false, criadaEm: '2026-01-13T09:30:00', concluidaEm: null },
                { id: 3, titulo: 'Validar dados', descricao: 'Conferir valores no sistema', atribuido: 1, data: '2026-01-22', dia: 'Quarta', prioridade: 'baixa', tipo: 'funcionario', concluida: true, criadaEm: '2026-01-10T10:00:00', concluidaEm: '2026-01-12T14:30:00' }
            ],
            atividades: [],
            filtrodeProdutividade: {
                usuarioSelecionado: null,
                periodoBuscado: 'semana'
            }
        };

        // FUNÇÕES MODAIS
        function openModal(id) {
            document.getElementById(id).classList.add('active');
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
        }

        function setLoginType(type) {
            loginType = type;
        }

        // AUTENTICAÇÃO
        function handleLogin(e) {
            e.preventDefault();
            const login = document.getElementById('login-input').value;
            const senha = document.getElementById('password-input').value;
            const errorDiv = document.getElementById('login-error');

            const user = database.funcionarios.find(u => u.login === login && u.senha === senha && u.perfil === loginType);

            if (user) {
                currentUser = user;
                currentProfile = loginType;
                loadUserPanel();
                closeModal('login-modal');
                document.getElementById('login-input').value = '';
                document.getElementById('password-input').value = '';
                errorDiv.style.display = 'none';
            } else {
                errorDiv.textContent = '❌ Login ou senha inválidos';
                errorDiv.style.display = 'block';
            }
        }

        function handleAdminLogin(e) {
            e.preventDefault();
            const senha = document.getElementById('admin-password-input').value;
            const errorDiv = document.getElementById('admin-error');

            if (senha === ADMIN_PASSWORD) {
                currentUser = { id: 0, nome: 'Admin', login: 'admin', perfil: 'admin' };
                currentProfile = 'admin';
                loadUserPanel();
                closeModal('senha-modal');
                document.getElementById('admin-password-input').value = '';
            } else {
                errorDiv.textContent = '❌ Senha incorreta';
                errorDiv.style.display = 'block';
            }
        }

        function logout() {
            currentUser = null;
            currentProfile = null;
            showScreen('screen-home');
        }

        // NAVEGAÇÃO TELAS
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(screenId).classList.add('active');
        }

        function loadUserPanel() {
            switch (currentProfile) {
                case 'funcionario':
                    showScreen('screen-funcionario');
                    document.getElementById('user-display').textContent = currentUser.nome;
                    renderTasksFuncionario();
                    break;
                case 'admin':
                    showScreen('screen-admin');
                    populateUserSelects();
                    renderDashboard();
                    renderTasksAdmin();
                    renderUsersList();
                    break;
                case 'gerente':
                    showScreen('screen-gerente');
                    document.getElementById('user-display-gerente').textContent = currentUser.nome;
                    populateGerenteSelects();
                    renderKanban();
                    break;
                case 'lider':
                    showScreen('screen-lider');
                    document.getElementById('user-display-lider').textContent = currentUser.nome;
                    renderTasksLider();
                    break;
            }
        }

        // RENDERIZAR TAREFAS FUNCIONÁRIO EM KANBAN
        function renderTasksFuncionario() {
            const container = document.getElementById('kanban-funcionario');
            const days = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];
            const daysClass = ['segunda', 'terca', 'quarta', 'quinta', 'sexta', 'sabado', 'domingo'];
            let tarefas = database.tarefas.filter(t => t.atribuido === currentUser.id && t.tipo === 'funcionario');

            // Atualizar contadores
            const totalTasks = tarefas.length;
            const pendenteTasks = tarefas.filter(t => !t.concluida).length;
            const completedTasks = tarefas.filter(t => t.concluida).length;
            
            document.getElementById('total-tasks-count').textContent = totalTasks;
            document.getElementById('pending-tasks-count').textContent = pendenteTasks;
            document.getElementById('completed-tasks-count').textContent = completedTasks;

            if (currentFilter === 'pendentes') {
                tarefas = tarefas.filter(t => !t.concluida);
            } else if (currentFilter === 'concluidas') {
                tarefas = tarefas.filter(t => t.concluida);
            }

            // Verifica se há tarefas em qualquer dia
            if (tarefas.length === 0) {
                container.innerHTML = '<div class="empty-state" style="grid-column: 1 / -1;"><div class="empty-state-icon">📭</div><p style="margin-top: var(--space-16); font-size: 16px; font-weight: 600;">Você não possui tarefas no momento.</p><p style="margin-top: var(--space-8); font-size: 13px; color: var(--color-text-muted);">Aproveite este tempo para descansar ou se preparar para novos desafios! 🎉</p></div>';
                return;
            }

            container.innerHTML = days.map((day, idx) => {
                const tasksOfDay = tarefas.filter(t => t.dia === day);
                return `
                    <div class="kanban-column ${daysClass[idx]}">
                        <div class="kanban-title">${day}</div>
                        <div style="min-height: 100px;">
                            ${tasksOfDay.length === 0 ? `
                                <div style="text-align: center; color: var(--color-text-muted); font-size: 12px; padding: var(--space-12);">
                                    <div style="font-size: 32px; margin-bottom: var(--space-8);">✨</div>
                                    Nenhuma tarefa
                                </div>
                            ` : `
                                ${tasksOfDay.map(task => `
                                    <div class="task-card" style="margin-bottom: var(--space-12); flex-direction: column; padding: var(--space-12); background: white; border-left: 4px solid ${task.prioridade === 'alta' ? '#EF4444' : task.prioridade === 'media' ? '#F59E0B' : '#10B981'};">
                                        <div style="display: flex; align-items: flex-start; gap: var(--space-8); width: 100%;">
                                            <input type="checkbox" class="task-checkbox" ${task.concluida ? 'checked' : ''} onchange="toggleTask(${task.id}, 'funcionario')" style="flex-shrink: 0; margin-top: 2px;">
                                            <div class="task-content" style="flex: 1;">
                                                <div class="task-title" style="font-size: 14px; font-weight: 700; margin-bottom: var(--space-6); color: ${task.concluida ? 'var(--color-text-muted)' : 'var(--color-text)'}; text-decoration: ${task.concluida ? 'line-through' : 'none'};">${task.titulo}</div>
                                                <span class="task-priority ${task.prioridade}" style="font-size: 9px; letter-spacing: 0.5px;">${task.prioridade.toUpperCase()}</span>
                                                <div class="task-description" style="font-size: 11px; margin-top: var(--space-8); line-height: 1.4;">${task.descricao}</div>
                                                <div class="task-meta" style="font-size: 10px; margin-top: var(--space-10); display: flex; align-items: center; gap: var(--space-8);">
                                                    <span>📅 ${new Date(task.data).toLocaleDateString('pt-BR')}</span>
                                                    <span style="display: inline-block; width: 4px; height: 4px; background: var(--color-text-muted); border-radius: 50%;"></span>
                                                    <span>${task.concluida ? '✅ Concluída' : '⏳ Pendente'}</span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                `).join('')}
                            `}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // RENDERIZAR TAREFAS ADMIN
        function renderTasksAdmin() {
            const container = document.getElementById('tasks-admin');
            let tarefas = database.tarefas;

            if (currentFilter === 'pendentes') {
                tarefas = tarefas.filter(t => !t.concluida);
            } else if (currentFilter === 'concluidas') {
                tarefas = tarefas.filter(t => t.concluida);
            }

            if (currentSearchQuery) {
                tarefas = tarefas.filter(t => t.titulo.toLowerCase().includes(currentSearchQuery.toLowerCase()));
            }

            if (tarefas.length === 0) {
                container.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📭</div>Nenhuma tarefa encontrada.</div>';
                return;
            }

            container.innerHTML = tarefas.map(task => {
                const usuario = database.funcionarios.find(u => u.id === task.atribuido);
                return `
                    <div class="task-card">
                        <input type="checkbox" class="task-checkbox" ${task.concluida ? 'checked' : ''} onchange="toggleTask(${task.id}, 'admin')">
                        <div class="task-content">
                            <div class="task-title">${task.titulo}</div>
                            <span class="task-priority ${task.prioridade}">${task.prioridade.toUpperCase()}</span>
                            <div class="task-description">${task.descricao}</div>
                            <div class="task-meta">
                                👤 ${usuario?.nome || 'N/A'} • ${task.dia} • ${new Date(task.data).toLocaleDateString('pt-BR')}
                            </div>
                        </div>
                        <button class="btn btn-danger btn-small" onclick="openDeleteModal('task', ${task.id})">🗑️</button>
                    </div>
                `;
            }).join('');
        }

        // RENDERIZAR TAREFAS LÍDER
        function renderTasksLider() {
            const container = document.getElementById('tasks-lider');
            const tarefas = database.tarefas.filter(t => t.atribuido === currentUser.id && t.tipo === 'lider');

            if (tarefas.length === 0) {
                container.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📭</div>Nenhuma tarefa atribuída.</div>';
                return;
            }

            container.innerHTML = tarefas.map(task => `
                <div class="task-card">
                    <div class="task-content">
                        <div class="task-title">${task.titulo}</div>
                        <span class="task-priority ${task.prioridade}">${task.prioridade.toUpperCase()}</span>
                        <div class="task-description">${task.descricao}</div>
                        <div class="task-meta">
                            ${task.dia} • ${new Date(task.data).toLocaleDateString('pt-BR')} • ${task.concluida ? '✅ Concluída' : '⏳ Pendente'}
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // ADICIONAR TAREFA ADMIN
        function addTask(e) {
            e.preventDefault();
            const newTask = {
                id: Math.max(...database.tarefas.map(t => t.id), 0) + 1,
                titulo: document.getElementById('task-title').value,
                descricao: document.getElementById('task-description').value,
                atribuido: parseInt(document.getElementById('task-assign').value),
                data: document.getElementById('task-date').value,
                dia: document.getElementById('task-day').value,
                prioridade: document.getElementById('task-priority').value,
                tipo: document.getElementById('task-type').value,
                concluida: false,
                criadaEm: new Date().toISOString(),
                concluidaEm: null
            };

            database.tarefas.push(newTask);
            database.atividades.unshift({ tipo: 'Tarefa criada', descricao: newTask.titulo, data: new Date().toLocaleString('pt-BR') });
            salvarBackupLocal();
            document.getElementById('form-nova-tarefa').reset();
            renderTasksAdmin();
            renderProdutividade();
        }

        // ADICIONAR TAREFA GERENTE
        function addTaskGerente(e) {
            e.preventDefault();
            const newTask = {
                id: Math.max(...database.tarefas.map(t => t.id), 0) + 1,
                titulo: document.getElementById('gerente-task-title').value,
                descricao: document.getElementById('gerente-task-description').value,
                atribuido: parseInt(document.getElementById('gerente-task-assign').value),
                data: document.getElementById('gerente-task-date').value,
                dia: document.getElementById('gerente-task-day').value,
                prioridade: document.getElementById('gerente-task-priority').value,
                tipo: 'funcionario',
                concluida: false,
                criadaEm: new Date().toISOString(),
                concluidaEm: null
            };

            database.tarefas.push(newTask);
            database.atividades.unshift({ tipo: 'Tarefa criada', descricao: newTask.titulo, data: new Date().toLocaleString('pt-BR') });
            salvarBackupLocal();
            document.getElementById('form-tarefa-gerente').reset();
            renderKanban();
            renderProdutividade();
        }

        // KANBAN
        function renderKanban() {
            const container = document.getElementById('kanban-board');
            const days = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];

            container.innerHTML = days.map(day => {
                const tasksOfDay = database.tarefas.filter(t => t.dia === day);
                return `
                    <div class="kanban-column">
                        <div class="kanban-title">${day}</div>
                        ${tasksOfDay.map(task => `
                            <div class="task-card" style="margin-bottom: var(--space-12);">
                                <div class="task-content">
                                    <div class="task-title" style="font-size: 13px;">${task.titulo}</div>
                                    <span class="task-priority ${task.prioridade}" style="font-size: 10px;">${task.prioridade.toUpperCase()}</span>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                `;
            }).join('');
        }

        // FILTRO POR PESSOA (GERENTE)
        function filterTasksByPerson() {
            const personId = parseInt(document.getElementById('select-pessoa').value);
            const container = document.getElementById('tasks-por-pessoa');

            if (!personId) {
                container.innerHTML = '';
                return;
            }

            const tarefas = database.tarefas.filter(t => t.atribuido === personId);

            if (tarefas.length === 0) {
                container.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📭</div>Nenhuma tarefa atribuída.</div>';
                return;
            }

            container.innerHTML = tarefas.map(task => {
                const usuario = database.funcionarios.find(u => u.id === task.atribuido);
                return `
                    <div class="task-card">
                        <div class="task-content">
                            <div class="task-title">${task.titulo}</div>
                            <span class="task-priority ${task.prioridade}">${task.prioridade.toUpperCase()}</span>
                            <div class="task-description">${task.descricao}</div>
                            <div class="task-meta">
                                ${task.dia} • ${new Date(task.data).toLocaleDateString('pt-BR')} • ${task.concluida ? '✅' : '⏳'}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // DASHBOARD
        function renderDashboard() {
            const total = database.tarefas.length;
            const pendentes = database.tarefas.filter(t => !t.concluida).length;
            const concluidas = database.tarefas.filter(t => t.concluida).length;
            const atrasadas = database.tarefas.filter(t => !t.concluida && new Date(t.data) < new Date()).length;
            const taxa = total > 0 ? Math.round((concluidas / total) * 100) : 0;

            document.getElementById('dashboard-stats').innerHTML = `
                <div class="stat-card">
                    <div class="stat-number">${total}</div>
                    <div class="stat-label">Total de Tarefas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${pendentes}</div>
                    <div class="stat-label">⏳ Pendentes</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${concluidas}</div>
                    <div class="stat-label">✅ Concluídas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${atrasadas}</div>
                    <div class="stat-label">⚠️ Atrasadas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${taxa}%</div>
                    <div class="stat-label">Taxa de Conclusão</div>
                </div>
            `;

            const activitiesList = document.getElementById('activities-list');
            const activities = database.atividades.slice(0, 5);

            if (activities.length === 0) {
                activitiesList.innerHTML = '<p style="color: var(--color-text-muted);">Nenhuma atividade registrada.</p>';
                return;
            }

            activitiesList.innerHTML = activities.map(act => `
                <div style="padding: var(--space-8) 0; border-bottom: 1px solid var(--color-border);">
                    <strong>${act.tipo}</strong>: ${act.descricao}<br>
                    <small style="color: var(--color-text-muted);">${act.data}</small>
                </div>
            `).join('');
        }

        // GERENCIAR USUÁRIOS
        function renderUsersList() {
            const container = document.getElementById('users-list');
            let usuarios = database.funcionarios;

            const searchTerm = document.getElementById('search-users')?.value || '';
            if (searchTerm) {
                usuarios = usuarios.filter(u => u.nome.toLowerCase().includes(searchTerm.toLowerCase()));
            }

            container.innerHTML = usuarios.map(user => `
                <div class="user-item">
                    <div class="user-info">
                        <div class="user-name">${user.nome}</div>
                        <div class="user-type">${user.perfil} • ${user.login}</div>
                    </div>
                    <div class="task-actions">
                        <button class="btn btn-secondary btn-small" onclick="editUser(${user.id})">✏️ Editar</button>
                        <button class="btn btn-danger btn-small" onclick="openDeleteModal('user', ${user.id})">🗑️ Deletar</button>
                    </div>
                </div>
            `).join('');
        }

        function addUser(e) {
            e.preventDefault();
            const newUser = {
                id: Math.max(...database.funcionarios.map(u => u.id), 0) + 1,
                nome: document.getElementById('user-name').value,
                login: document.getElementById('user-login').value,
                senha: document.getElementById('user-password').value,
                perfil: document.getElementById('user-profile').value,
                proprietaria: document.getElementById('user-proprietaria').checked
            };

            database.funcionarios.push(newUser);
            database.atividades.unshift({ tipo: 'Usuário criado', descricao: newUser.nome, data: new Date().toLocaleString('pt-BR') });
            salvarBackupLocal();
            document.getElementById('form-novo-usuario').reset();
            renderUsersList();
            populateUserSelects();
        }

        // UTILITY FUNCTIONS
        function populateUserSelects() {
            const select = document.getElementById('task-assign');
            const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
            select.innerHTML = '<option value="">Selecionar usuário</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
        }

        // FUNÇÃO PARA CALCULAR PERÍODO
        function calcularPeriodo(periodo) {
            const hoje = new Date();
            hoje.setHours(0, 0, 0, 0);
            let dataInicio, dataFim;

            if (periodo === 'semana') {
                const dia = hoje.getDay();
                const diff = hoje.getDate() - dia + (dia === 0 ? -6 : 1);
                dataInicio = new Date(hoje.setDate(diff));
                dataFim = new Date(dataInicio);
                dataFim.setDate(dataFim.getDate() + 6);
            } else if (periodo === 'mes') {
                dataInicio = new Date(hoje.getFullYear(), hoje.getMonth(), 1);
                dataFim = new Date(hoje.getFullYear(), hoje.getMonth() + 1, 0);
            } else if (periodo === '30dias') {
                dataFim = new Date(hoje);
                dataInicio = new Date(hoje);
                dataInicio.setDate(dataInicio.getDate() - 30);
            } else {
                dataInicio = new Date(1970, 0, 1);
                dataFim = new Date(2099, 11, 31);
            }

            return { dataInicio, dataFim };
        }

        // FUNÇÃO RENDERIZAR PRODUTIVIDADE
        function renderProdutividade() {
            const usuarioId = parseInt(document.getElementById('filtro-usuario-produtividade').value) || null;
            const periodo = document.getElementById('filtro-periodo-produtividade').value || 'semana';
            const { dataInicio, dataFim } = calcularPeriodo(periodo);

            // Filtrar tarefas pelo usuário e período
            let tarefasFiltradas = database.tarefas.filter(t => {
                if (usuarioId && t.atribuido !== usuarioId) return false;
                const criadaEm = new Date(t.criadaEm);
                return criadaEm >= dataInicio && criadaEm <= dataFim;
            });

            // Calcular métricas
            const total = tarefasFiltradas.length;
            const concluidas = tarefasFiltradas.filter(t => t.concluida).length;
            const pendentes = total - concluidas;
            const atrasadas = tarefasFiltradas.filter(t => !t.concluida && new Date(t.data) < new Date()).length;
            const taxaConclusao = total > 0 ? Math.round((concluidas / total) * 100) : 0;

            // Calcular tempo médio de conclusão
            const tarefasComConclusao = tarefasFiltradas.filter(t => t.concluidaEm);
            let tempoMedioExec = 0;
            if (tarefasComConclusao.length > 0) {
                const tempoTotal = tarefasComConclusao.reduce((sum, t) => {
                    const inicio = new Date(t.criadaEm);
                    const fim = new Date(t.concluidaEm);
                    return sum + (fim - inicio) / (1000 * 60 * 60 * 24);
                }, 0);
                tempoMedioExec = Math.round(tempoTotal / tarefasComConclusao.length);
            }

            // Renderizar cards de métricas
            const statsContainer = document.getElementById('produtividade-stats');
            statsContainer.innerHTML = `
                <div class="stat-card">
                    <div class="stat-number">${total}</div>
                    <div class="stat-label">📊 Total de Tarefas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${concluidas}</div>
                    <div class="stat-label">✅ Concluídas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${pendentes}</div>
                    <div class="stat-label">⏳ Pendentes</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${atrasadas}</div>
                    <div class="stat-label">⚠️ Atrasadas</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${taxaConclusao}%</div>
                    <div class="stat-label">🎯 Taxa de Conclusão</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">${tempoMedioExec}</div>
                    <div class="stat-label">⏱️ Dias Médios Execução</div>
                </div>
            `;

            // Renderizar gráfico
            renderGraficoProdutividade(tarefasFiltradas, dataInicio, dataFim);

            // Renderizar tabela detalhada
            renderTabelaProdutividade(tarefasFiltradas);

            // Atualizar selects
            atualizarSelectProdutividade();
        }

        // GRÁFICO DE PRODUTIVIDADE
        function renderGraficoProdutividade(tarefas, dataInicio, dataFim) {
            const graficoContainer = document.getElementById('grafico-produtividade');
            const dias = [];
            let dataAtual = new Date(dataInicio);

            while (dataAtual <= dataFim) {
                dias.push(new Date(dataAtual));
                dataAtual.setDate(dataAtual.getDate() + 1);
            }

            const dadosGrafico = dias.map(dia => {
                const diaStr = dia.toISOString().split('T')[0];
                const tarefasDodia = tarefas.filter(t => {
                    if (!t.concluidaEm) return false;
                    const concluidaStr = t.concluidaEm.split('T')[0];
                    return concluidaStr === diaStr;
                }).length;
                return { dia, quantidade: tarefasDodia };
            });

            const maxQuantidade = Math.max(...dadosGrafico.map(d => d.quantidade), 1);
            const largura = Math.max(30, 100 / dadosGrafico.length);

            graficoContainer.innerHTML = dadosGrafico.map(d => `
                <div style="display: flex; flex-direction: column; align-items: center; flex: 1; max-width: ${largura}px;">
                    <div style="width: 100%; background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%); border-radius: var(--radius-base); height: ${(d.quantidade / maxQuantidade) * 200}px; min-height: 4px; transition: all 0.3s ease; cursor: pointer;" title="${d.quantidade} tarefas"></div>
                    <div style="font-size: 10px; text-align: center; margin-top: var(--space-8); color: var(--color-text-muted); font-weight: 600;">${d.dia.toLocaleDateString('pt-BR', { weekday: 'short', month: 'numeric', day: 'numeric' })}</div>
                    <div style="font-size: 12px; font-weight: 700; color: var(--color-primary); margin-top: 2px;">${d.quantidade}</div>
                </div>
            `).join('');
        }

        // TABELA DETALHADA DE TAREFAS
        function renderTabelaProdutividade(tarefas) {
            const container = document.getElementById('tabela-produtividade');

            if (tarefas.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: var(--color-text-muted); padding: var(--space-24);">Nenhuma tarefa encontrada neste período.</p>';
                return;
            }

            container.innerHTML = `
                <div style="overflow-x: auto;">
                    <table style="width: 100%; border-collapse: collapse; font-size: 13px;">
                        <thead>
                            <tr style="border-bottom: 2px solid var(--color-border);">
                                <th style="padding: var(--space-12); text-align: left; font-weight: 700;">Título</th>
                                <th style="padding: var(--space-12); text-align: left; font-weight: 700;">Atribuído</th>
                                <th style="padding: var(--space-12); text-align: center; font-weight: 700;">Prioridade</th>
                                <th style="padding: var(--space-12); text-align: center; font-weight: 700;">Status</th>
                                <th style="padding: var(--space-12); text-align: right; font-weight: 700;">Dias Execução</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${tarefas.map(t => {
                                const usuario = database.funcionarios.find(u => u.id === t.atribuido);
                                let diasExec = '-';
                                if (t.concluidaEm) {
                                    const inicio = new Date(t.criadaEm);
                                    const fim = new Date(t.concluidaEm);
                                    diasExec = Math.round((fim - inicio) / (1000 * 60 * 60 * 24));
                                }
                                return `
                                    <tr style="border-bottom: 1px solid var(--color-border-light); transition: all 0.2s ease;">
                                        <td style="padding: var(--space-12);">${t.titulo}</td>
                                        <td style="padding: var(--space-12);">${usuario?.nome || 'N/A'}</td>
                                        <td style="padding: var(--space-12); text-align: center;"><span class="task-priority ${t.prioridade}" style="font-size: 10px;">${t.prioridade.toUpperCase()}</span></td>
                                        <td style="padding: var(--space-12); text-align: center;">${t.concluida ? '✅ Concluída' : '⏳ Pendente'}</td>
                                        <td style="padding: var(--space-12); text-align: right; font-weight: 600; color: ${diasExec === '-' ? 'var(--color-text-muted)' : 'var(--color-primary)'};">${diasExec}</td>
                                    </tr>
                                `;
                            }).join('')}
                        </tbody>
                    </table>
                </div>
            `;
        }

        // ATUALIZAR SELECT DE USUÁRIOS
        function atualizarSelectProdutividade() {
            const select = document.getElementById('filtro-usuario-produtividade');
            if (!select) return;
            const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
            const valorAtual = select.value;
            select.innerHTML = '<option value="">📊 Todos os Usuários</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
            select.value = valorAtual;
        }

        function populateGerenteSelects() {
            const select = document.getElementById('gerente-task-assign');
            const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
            const pessoaSelect = document.getElementById('select-pessoa');

            select.innerHTML = funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
            pessoaSelect.innerHTML = '<option value="">Selecionar pessoa</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
        }

        function switchTab(tabName, section) {
            document.querySelectorAll(`#${section}-${tabName}`).forEach(t => t.parentElement.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active')));
            document.getElementById(`${section}-${tabName}`).classList.add('active');

            document.querySelectorAll(`#${section}-${tabName}`).forEach(t => t.parentElement.parentElement.querySelectorAll('.tab-button').forEach(b => b.classList.remove('active')));
            event.target.classList.add('active');
        }

        function filterTasks(filter, context) {
            currentFilter = filter;
            document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
            event.target.classList.add('active');

            if (context === 'funcionario') renderTasksFuncionario();
            else if (context === 'admin') renderTasksAdmin();
        }

        function searchTasks(context) {
            currentSearchQuery = document.getElementById('search-tasks').value;
            if (context === 'admin') renderTasksAdmin();
        }

        function searchUsers() {
            renderUsersList();
        }

        function toggleTask(taskId, context) {
            const task = database.tarefas.find(t => t.id === taskId);
            if (task) {
                task.concluida = !task.concluida;
                if (task.concluida) {
                    task.concluidaEm = new Date().toISOString();
                } else {
                    task.concluidaEm = null;
                }
                database.atividades.unshift({ tipo: 'Tarefa atualizada', descricao: task.titulo, data: new Date().toLocaleString('pt-BR') });
                salvarBackupLocal();
                
                if (context === 'funcionario') renderTasksFuncionario();
                else if (context === 'admin') renderTasksAdmin();
                renderProdutividade();
            }
        }

        function openDeleteModal(type, id) {
            deleteTarget = { type, id };
            openModal('delete-modal');
        }

        function confirmDelete() {
            if (!deleteTarget) return;

            if (deleteTarget.type === 'task') {
                database.tarefas = database.tarefas.filter(t => t.id !== deleteTarget.id);
                database.atividades.unshift({ tipo: 'Tarefa deletada', descricao: 'Tarefa removida', data: new Date().toLocaleString('pt-BR') });
                salvarBackupLocal();
                renderTasksAdmin();
            } else if (deleteTarget.type === 'user') {
                database.funcionarios = database.funcionarios.filter(u => u.id !== deleteTarget.id);
                salvarBackupLocal();
                renderUsersList();
                populateUserSelects();
            }

            closeModal('delete-modal');
            deleteTarget = null;
        }

        function editUser(userId) {
            alert('Função de edição será implementada em uma próxima versão!');
        }

        // ===== FUNÇÕES DE BACKUP E PERSISTÊNCIA =====
        function salvarBackupLocal() {
            try {
                localStorage.setItem('ALFAMIX_DATABASE_V1', JSON.stringify(database));
            } catch (e) {
                console.error('Erro ao salvar backup local:', e);
            }
        }

        function carregarBackupLocal() {
            try {
                const salvo = localStorage.getItem('ALFAMIX_DATABASE_V1');
                if (salvo) {
                    const data = JSON.parse(salvo);
                    Object.assign(database, data);
                    console.log('✅ Backup restaurado do localStorage');
                }
            } catch (e) {
                console.error('Erro ao carregar backup:', e);
            }
        }

        function setupAutoSave() {
            setInterval(() => {
                salvarBackupLocal();
                console.log('🔄 Autosave executado');
            }, 900000);

            window.addEventListener('beforeunload', () => {
                salvarBackupLocal();
            });

            console.log('🔄 Sistema de autosave ativado (a cada 15 minutos)');
        }

        // ===== SEMANA COMPLETA =====
        function renderDiasSemana() {
            const container = document.getElementById('dias-semana-container');
            const dias = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];
            const emojis = ['📌', '📌', '📌', '📌', '📌', '📌', '📌'];

            container.innerHTML = dias.map((dia, idx) => `
                <div style="background: var(--color-bg-light); border: 1px solid var(--color-border); border-radius: var(--radius-base); padding: var(--space-16); margin-bottom: var(--space-16);">
                    <h5 style="margin-bottom: var(--space-12); font-weight: 700; color: var(--color-primary);">${emojis[idx]} ${dia}</h5>
                    <div class="form-grid" style="grid-template-columns: 1fr 1fr;">
                        <div class="form-group">
                            <label class="form-label">Título</label>
                            <input class="form-control semana-titulo" type="text" data-dia="${dia}" placeholder="Ex: Reunião">
                        </div>
                        <div class="form-group">
                            <label class="form-label">Data</label>
                            <input class="form-control semana-data" type="date" data-dia="${dia}">
                        </div>
                    </div>
                    <div class="form-grid" style="grid-template-columns: 1fr 1fr;">
                        <div class="form-group">
                            <label class="form-label">Prioridade</label>
                            <select class="form-control semana-prioridade" data-dia="${dia}">
                                <option>alta</option>
                                <option selected>media</option>
                                <option>baixa</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label class="form-label">Descrição (opcional)</label>
                            <input class="form-control semana-descricao" type="text" data-dia="${dia}" placeholder="Detalhes da tarefa">
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function createWeeklyTasks(e) {
            e.preventDefault();
            const userId = parseInt(document.getElementById('semana-assign').value);
            if (!userId) {
                alert('❌ Selecione um funcionário');
                return;
            }

            const dias = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];
            let tarefasCriadas = 0;

            dias.forEach(dia => {
                const titulo = document.querySelector(`.semana-titulo[data-dia="${dia}"]`)?.value || '';
                const data = document.querySelector(`.semana-data[data-dia="${dia}"]`)?.value || '';
                const prioridade = document.querySelector(`.semana-prioridade[data-dia="${dia}"]`)?.value || 'media';
                const descricao = document.querySelector(`.semana-descricao[data-dia="${dia}"]`)?.value || '';

                if (titulo && data) {
                    const newTask = {
                        id: Math.max(...database.tarefas.map(t => t.id), 0) + 1,
                        titulo,
                        descricao,
                        atribuido: userId,
                        data,
                        dia,
                        prioridade,
                        tipo: 'funcionario',
                        concluida: false,
                        criadaEm: new Date().toISOString(),
                        concluidaEm: null
                    };
                    database.tarefas.push(newTask);
                    tarefasCriadas++;
                }
            });

            if (tarefasCriadas > 0) {
                const usuario = database.funcionarios.find(u => u.id === userId);
                database.atividades.unshift({ 
                    tipo: 'Semana criada', 
                    descricao: `${tarefasCriadas} tarefas para ${usuario?.nome}`, 
                    data: new Date().toLocaleString('pt-BR') 
                });
                alert(`✅ ${tarefasCriadas} tarefas criadas com sucesso!`);
                closeModal('modal-semana-completa');
                document.getElementById('form-nova-tarefa').reset();
                renderTasksAdmin();
                renderKanban();
                renderProdutividade();
            } else {
                alert('⚠️ Preencha pelo menos o título e data de uma tarefa');
            }
        }

        // ===== REPLICAR SEMANA =====
        function replicateWeeklyTasks(e) {
            e.preventDefault();
            const origemId = parseInt(document.getElementById('replica-origem').value);
            const destinoId = parseInt(document.getElementById('replica-destino').value);
            const periodo = document.getElementById('replica-periodo').value;

            if (!origemId || !destinoId || origemId === destinoId) {
                alert('❌ Selecione dois funcionários diferentes');
                return;
            }

            const { dataInicio, dataFim } = calcularPeriodo(periodo);

            // Filtrar tarefas da origem no período
            const tarefasOrigem = database.tarefas.filter(t => 
                t.atribuido === origemId && 
                new Date(t.data) >= dataInicio && 
                new Date(t.data) <= dataFim
            );

            if (tarefasOrigem.length === 0) {
                alert('⚠️ Nenhuma tarefa encontrada para replicar neste período');
                return;
            }

            // Criar cópias das tarefas
            tarefasOrigem.forEach(t => {
                const newTask = {
                    id: Math.max(...database.tarefas.map(task => task.id), 0) + 1,
                    titulo: t.titulo,
                    descricao: t.descricao,
                    atribuido: destinoId,
                    data: t.data,
                    dia: t.dia,
                    prioridade: t.prioridade,
                    tipo: t.tipo,
                    concluida: false,
                    criadaEm: new Date().toISOString(),
                    concluidaEm: null
                };
                database.tarefas.push(newTask);
            });

            const usuarioOrigem = database.funcionarios.find(u => u.id === origemId);
            const usuarioDestino = database.funcionarios.find(u => u.id === destinoId);
            database.atividades.unshift({ 
                tipo: 'Semana replicada', 
                descricao: `${tarefasOrigem.length} tarefas de ${usuarioOrigem?.nome} para ${usuarioDestino?.nome}`, 
                data: new Date().toLocaleString('pt-BR') 
            });

            alert(`✅ ${tarefasOrigem.length} tarefas replicadas para ${usuarioDestino?.nome}!`);
            closeModal('modal-replicar-semana');
            renderTasksAdmin();
            renderKanban();
            renderProdutividade();
        }

        // Inicializar
        carregarBackupLocal();
        populateUserSelects();
        atualizarSelectProdutividade();
        renderDiasSemana();
        setupAutoSave();

        // Preencher selects dos modais
        document.getElementById('semana-assign').addEventListener('load', () => {
            const select = document.getElementById('semana-assign');
            const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
            select.innerHTML = '<option value="">Selecionar funcionário</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
        });

        // Observer para popular selects quando modal abre
        const modal1 = document.getElementById('modal-semana-completa');
        const modal2 = document.getElementById('modal-replicar-semana');

        const observer = new MutationObserver(() => {
            if (modal1.classList.contains('active')) {
                const select = document.getElementById('semana-assign');
                if (select.children.length === 1) {
                    const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
                    select.innerHTML = '<option value="">Selecionar funcionário</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
                }
            }
            if (modal2.classList.contains('active')) {
                const origem = document.getElementById('replica-origem');
                const destino = document.getElementById('replica-destino');
                if (origem.children.length === 1) {
                    const funcionarios = database.funcionarios.filter(u => u.perfil === 'funcionario');
                    origem.innerHTML = '<option value="">Selecionar origem</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
                    destino.innerHTML = '<option value="">Selecionar destino</option>' + funcionarios.map(u => `<option value="${u.id}">${u.nome}</option>`).join('');
                }
            }
        });

        observer.observe(document, { attributes: true, subtree: true });

        // ===== FUNÇÕES DE IMPORTAÇÃO E EXPORTAÇÃO EXCEL =====
        function downloadExcelTemplate() {
            // Criar workbook e worksheets
            const worksheetData = [];
            
            // Cabeçalho com instruções
            worksheetData.push(['🎯 ALFA MIX - MODELO DE IMPORTAÇÃO DE TAREFAS']);
            worksheetData.push(['Instruções: Preencha os dados abaixo e faça upload do arquivo Excel no sistema']);
            worksheetData.push(['']);
            
            // Cabeçalhos das colunas
            worksheetData.push([
                'Título da Tarefa',
                'Descrição',
                'Data Limite',
                'Dia da Semana',
                'Prioridade',
                'Atribuir Para (Nome)',
                'Tipo'
            ]);
            
            // Linhas de exemplo preenchidas
            const diasSemana = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];
            const hoje = new Date();
            
            for (let i = 0; i < 7; i++) {
                const data = new Date(hoje);
                data.setDate(data.getDate() + i);
                const dataStr = data.toLocaleDateString('pt-BR');
                
                worksheetData.push([
                    `Tarefa Exemplo ${i + 1}`,
                    `Descrição da tarefa ${i + 1}`,
                    dataStr,
                    diasSemana[i],
                    i % 3 === 0 ? 'alta' : i % 3 === 1 ? 'media' : 'baixa',
                    database.funcionarios.find(u => u.perfil === 'funcionario')?.nome || 'João Silva',
                    'funcionario'
                ]);
            }
            
            // Adicionar linha de referência de usuários disponíveis
            worksheetData.push(['']);
            worksheetData.push(['REFERÊNCIA DE USUÁRIOS DISPONÍVEIS:']);
            database.funcionarios.forEach(u => {
                if (u.perfil !== 'admin') {
                    worksheetData.push([`${u.nome} (${u.perfil.toUpperCase()})`]);
                }
            });
            
            // Converter para CSV para compatibilidade universal
            const csvContent = worksheetData.map(row => 
                row.map(cell => 
                    typeof cell === 'string' && cell.includes(',') 
                        ? `"${cell}"` 
                        : cell
                ).join(',')
            ).join('\n');
            
            // Criar e baixar arquivo
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', `alfa_mix_modelo_tarefas_${new Date().toISOString().split('T')[0]}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            alert('✅ Modelo de Excel baixado! Preencha os dados e faça upload novamente.');
        }

        function handleExcelUpload(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = (e) => {
                try {
                    const csv = e.target.result;
                    const linhas = csv.split('\n').filter(l => l.trim());
                    
                    // Pular linhas de cabeçalho e instruções
                    let startRow = 0;
                    for (let i = 0; i < linhas.length; i++) {
                        if (linhas[i].includes('Título da Tarefa')) {
                            startRow = i + 1;
                            break;
                        }
                    }
                    
                    let tarefasImportadas = 0;
                    let erros = [];
                    
                    // Processar cada linha
                    for (let i = startRow; i < linhas.length; i++) {
                        const linha = linhas[i].trim();
                        
                        // Pular linhas vazias ou que começam com REFERÊNCIA
                        if (!linha || linha.includes('REFERÊNCIA')) break;
                        
                        const colunas = parseCSVLine(linha);
                        
                        if (colunas.length < 7) continue;
                        
                        const [titulo, descricao, dataStr, dia, prioridade, nomeUsuario, tipo] = colunas;
                        
                        // Validação básica
                        if (!titulo || !nomeUsuario) {
                            erros.push(`Linha ${i + 1}: Título e Usuário são obrigatórios`);
                            continue;
                        }
                        
                        // Encontrar usuário pelo nome
                        const usuario = database.funcionarios.find(u => 
                            u.nome.toLowerCase().includes(nomeUsuario.toLowerCase().trim())
                        );
                        
                        if (!usuario) {
                            erros.push(`Linha ${i + 1}: Usuário "${nomeUsuario}" não encontrado`);
                            continue;
                        }
                        
                        // Validar data
                        let dataTarefa = dataStr.trim();
                        if (!dataTarefa.match(/^\d{4}-\d{2}-\d{2}$/)) {
                            // Tentar converter formato DD/MM/YYYY para YYYY-MM-DD
                            const partes = dataTarefa.split('/');
                            if (partes.length === 3) {
                                dataTarefa = `${partes[2]}-${partes[1]}-${partes[0]}`;
                            }
                        }
                        
                        // Criar tarefa
                        const novaTarefa = {
                            id: Math.max(...database.tarefas.map(t => t.id), 0) + 1,
                            titulo: titulo.trim(),
                            descricao: descricao.trim(),
                            atribuido: usuario.id,
                            data: dataTarefa,
                            dia: dia.trim() || 'Segunda',
                            prioridade: prioridade.toLowerCase().trim() || 'media',
                            tipo: tipo.toLowerCase().trim() || 'funcionario',
                            concluida: false,
                            criadaEm: new Date().toISOString(),
                            concluidaEm: null
                        };
                        
                        // Validação adicional
                        if (!['alta', 'media', 'baixa'].includes(novaTarefa.prioridade)) {
                            novaTarefa.prioridade = 'media';
                        }
                        
                        database.tarefas.push(novaTarefa);
                        tarefasImportadas++;
                    }
                    
                    database.atividades.unshift({ 
                        tipo: 'Importação Excel', 
                        descricao: `${tarefasImportadas} tarefas importadas`, 
                        data: new Date().toLocaleString('pt-BR') 
                    });
                    
                    salvarBackupLocal();
                    
                    let mensagem = `✅ ${tarefasImportadas} tarefas importadas com sucesso!`;
                    if (erros.length > 0) {
                        mensagem += `\n\n⚠️ ${erros.length} linhas com erro:\n${erros.slice(0, 5).join('\n')}`;
                        if (erros.length > 5) mensagem += `\n... e mais ${erros.length - 5} erros`;
                    }
                    
                    alert(mensagem);
                    renderTasksAdmin();
                    renderProdutividade();
                    
                } catch (error) {
                    alert(`❌ Erro ao processar arquivo: ${error.message}`);
                    console.error(error);
                }
            };
            
            reader.readAsText(file);
            
            // Limpar input
            event.target.value = '';
        }

        function parseCSVLine(line) {
            const result = [];
            let current = '';
            let insideQuotes = false;
            
            for (let i = 0; i < line.length; i++) {
                const char = line[i];
                const nextChar = line[i + 1];
                
                if (char === '"') {
                    if (insideQuotes && nextChar === '"') {
                        current += '"';
                        i++;
                    } else {
                        insideQuotes = !insideQuotes;
                    }
                } else if (char === ',' && !insideQuotes) {
                    result.push(current.trim());
                    current = '';
                } else {
                    current += char;
                }
            }
            
            result.push(current.trim());
            return result;
        }
    </script>
</body>
</html>

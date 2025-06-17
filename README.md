# Organizador 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Organizer</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6e48aa;
            --secondary: #9d50bb;
            --dark: #1a1a2e;
            --darker: #16213e;
            --text: #e6e6e6;
            --accent: #00dbde;
            --success: #4CAF50;
            --warning: #FFC107;
            --danger: #F44336;
            --bubble1: #FF6B6B;
            --bubble2: #4ECDC4;
            --bubble3: #45B7D1;
            --bubble4: #FFBE0B;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--dark), var(--darker));
            color: var(--text);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .app-container {
            display: none;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header */
        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .app-title {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(to right, var(--accent), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .user-menu {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-weight: bold;
        }

        /* Navigation */
        .top-nav {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            gap: 10px;
        }

        .nav-item {
            padding: 12px 25px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s ease;
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1);
        }

        .nav-item.active {
            background: var(--primary);
            box-shadow: 0 4px 15px rgba(110, 72, 170, 0.4);
        }

        .nav-item:hover {
            transform: translateY(-2px);
        }

        /* Content Sections */
        .content-section {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .content-section.active {
            display: block;
        }

        .section-card {
            background: rgba(255,255,255,0.05);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 30px;
            border: 1px solid rgba(255,255,255,0.1);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            backdrop-filter: blur(10px);
        }

        .section-title {
            font-size: 22px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-title i {
            color: var(--accent);
        }

        /* Forms */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: rgba(255,255,255,0.8);
        }

        input, select, textarea {
            width: 100%;
            padding: 12px 15px;
            background: rgba(255,255,255,0.1);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 12px;
            color: var(--text);
            font-size: 14px;
            transition: all 0.3s;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 2px rgba(0, 219, 222, 0.2);
        }

        .btn {
            padding: 12px 25px;
            border-radius: 12px;
            border: none;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--secondary);
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: rgba(255,255,255,0.1);
            color: white;
            border: 1px solid rgba(255,255,255,0.2);
        }

        .btn-secondary:hover {
            background: rgba(255,255,255,0.2);
        }

        /* Tables */
        .data-table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-bottom: 20px;
        }

        .data-table th {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            text-align: left;
            font-weight: 500;
            border-bottom: 2px solid rgba(255,255,255,0.2);
        }

        .data-table td {
            padding: 15px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .data-table tr:last-child td {
            border-bottom: none;
        }

        .data-table tr:hover td {
            background: rgba(255,255,255,0.05);
        }

        .badge {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 500;
        }

        .badge-low {
            background: rgba(75, 192, 192, 0.2);
            color: #4bc0c0;
        }

        .badge-medium {
            background: rgba(255, 206, 86, 0.2);
            color: #ffce56;
        }

        .badge-high {
            background: rgba(255, 99, 132, 0.2);
            color: #ff6384;
        }

        /* Charts */
        .chart-container {
            height: 300px;
            margin-top: 30px;
            background: rgba(255,255,255,0.05);
            border-radius: 15px;
            padding: 15px;
            border: 1px solid rgba(255,255,255,0.1);
        }

        /* Progress */
        .progress-container {
            width: 100%;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            height: 10px;
            margin-top: 5px;
        }

        .progress-bar {
            height: 100%;
            border-radius: 10px;
            background: linear-gradient(to right, var(--primary), var(--accent));
            transition: width 0.5s ease;
        }

        /* Login/Settings */
        .auth-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            background: linear-gradient(135deg, var(--dark), var(--darker));
        }

        .auth-card {
            background: rgba(255,255,255,0.05);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            animation: fadeInUp 0.5s ease;
        }

        .auth-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .auth-title {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(to right, var(--accent), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .auth-subtitle {
            color: rgba(255,255,255,0.7);
            font-size: 14px;
        }

        .auth-footer {
            text-align: center;
            margin-top: 20px;
            font-size: 14px;
            color: rgba(255,255,255,0.7);
        }

        .auth-link {
            color: var(--accent);
            text-decoration: none;
            font-weight: 500;
        }

        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .tab {
            padding: 10px 20px;
            cursor: pointer;
            font-weight: 500;
            color: rgba(255,255,255,0.7);
            border-bottom: 2px solid transparent;
            transition: all 0.3s;
        }

        .tab.active {
            color: var(--accent);
            border-bottom-color: var(--accent);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Settings */
        .settings-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }

        .settings-modal.show {
            opacity: 1;
            visibility: visible;
        }

        .settings-content {
            background: rgba(30,30,46,0.95);
            border-radius: 20px;
            padding: 30px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 10px 40px rgba(0,0,0,0.4);
            border: 1px solid rgba(255,255,255,0.1);
        }

        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        .settings-header h3 {
            font-size: 24px;
            background: linear-gradient(to right, var(--accent), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .close-settings {
            font-size: 28px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .close-settings:hover {
            color: var(--accent);
        }

        .settings-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .settings-tab {
            padding: 10px 20px;
            cursor: pointer;
            font-weight: 500;
            color: rgba(255,255,255,0.7);
            border-bottom: 2px solid transparent;
            transition: all 0.3s;
        }

        .settings-tab.active {
            color: var(--accent);
            border-bottom-color: var(--accent);
        }

        .settings-tab-content {
            display: none;
        }

        .settings-tab-content.active {
            display: block;
        }

        .color-picker {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }

        .color-option {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid transparent;
            transition: all 0.3s;
        }

        .color-option:hover {
            transform: scale(1.1);
        }

        .color-option.selected {
            border-color: white;
            transform: scale(1.1);
        }

        /* Routine Table */
        .routine-grid {
            display: grid;
            grid-template-columns: 100px repeat(7, 1fr);
            gap: 1px;
            background: rgba(255,255,255,0.1);
            border-radius: 12px;
            overflow: hidden;
        }

        .routine-header {
            background: rgba(255,255,255,0.2);
            padding: 12px;
            text-align: center;
            font-weight: 500;
        }

        .routine-cell {
            background: rgba(255,255,255,0.05);
            padding: 10px;
            min-height: 60px;
            border-right: 1px solid rgba(255,255,255,0.1);
            border-bottom: 1px solid rgba(255,255,255,0.1);
            position: relative;
        }

        .routine-time {
            font-size: 12px;
            color: rgba(255,255,255,0.7);
            margin-bottom: 5px;
            text-align: center;
            font-weight: 500;
        }

        .routine-activity {
            background: var(--primary);
            padding: 5px 8px;
            border-radius: 6px;
            font-size: 12px;
            margin-bottom: 5px;
            display: inline-block;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
        }

        .routine-activity:hover {
            opacity: 0.8;
        }

        .delete-activity {
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 10px;
            opacity: 0;
            transition: all 0.3s;
        }

        .routine-cell:hover .delete-activity {
            opacity: 1;
        }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .routine-grid {
                grid-template-columns: 80px repeat(7, 120px);
                overflow-x: auto;
            }
            
            .top-nav {
                flex-wrap: wrap;
            }
            
            .nav-item {
                padding: 10px 15px;
                font-size: 14px;
            }
            
            .section-card {
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <!-- Authentication Screens -->
    <div class="auth-container" id="authContainer">
        <div class="auth-card">
            <div class="auth-header">
                <div class="auth-title">Nexus Organizer</div>
                <div class="auth-subtitle">Sua vida organizada em um só lugar</div>
            </div>
            
            <div class="tabs">
                <div class="tab active" data-tab="login">Login</div>
                <div class="tab" data-tab="register">Registrar</div>
                <div class="tab" data-tab="recover">Recuperar</div>
            </div>
            
            <div class="tab-content active" id="loginTab">
                <div class="form-group">
                    <label>E-mail</label>
                    <input type="email" id="loginEmail" placeholder="seu@email.com">
                </div>
                <div class="form-group">
                    <label>Senha</label>
                    <input type="password" id="loginPassword" placeholder="••••••••">
                </div>
                <button class="btn btn-primary" id="loginBtn" style="width: 100%;">Entrar</button>
                <div class="auth-footer">
                    <a href="#" class="auth-link" id="forgotPasswordLink">Esqueceu a senha?</a>
                </div>
            </div>
            
            <div class="tab-content" id="registerTab">
                <div class="form-group">
                    <label>Nome</label>
                    <input type="text" id="registerName" placeholder="Seu nome">
                </div>
                <div class="form-group">
                    <label>E-mail</label>
                    <input type="email" id="registerEmail" placeholder="seu@email.com">
                </div>
                <div class="form-group">
                    <label>Senha</label>
                    <input type="password" id="registerPassword" placeholder="••••••••">
                </div>
                <div class="form-group">
                    <label>Confirmar Senha</label>
                    <input type="password" id="registerConfirmPassword" placeholder="••••••••">
                </div>
                <button class="btn btn-primary" id="registerBtn" style="width: 100%;">Criar Conta</button>
            </div>
            
            <div class="tab-content" id="recoverTab">
                <div class="form-group">
                    <label>E-mail</label>
                    <input type="email" id="recoverEmail" placeholder="seu@email.com">
                </div>
                <button class="btn btn-primary" id="recoverBtn" style="width: 100%;">Enviar Link de Recuperação</button>
                <div class="auth-footer">
                    Lembre-se de verificar sua caixa de spam
                </div>
            </div>
        </div>
    </div>
    
    <!-- Main App -->
    <div class="app-container" id="appContainer">
        <div class="app-header">
            <div class="app-title">Nexus Organizer</div>
            <div class="user-menu">
                <div class="btn btn-secondary" id="settingsBtn">
                    <i>⚙️</i> Configurações
                </div>
                <div class="user-avatar" id="userAvatar">U</div>
            </div>
        </div>
        
        <div class="top-nav">
            <div class="nav-item active" data-section="goals">Metas</div>
            <div class="nav-item" data-section="finance">Finanças</div>
            <div class="nav-item" data-section="routine">Rotina</div>
            <div class="nav-item" data-section="reminders">Lembretes</div>
        </div>
        
        <!-- Goals Section -->
        <div class="content-section active" id="goalsSection">
            <div class="section-card">
                <div class="section-title">
                    <i>🎯</i> Minhas Metas
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Nome da Meta</label>
                        <input type="text" id="goalName" placeholder="Ex: Aprender JavaScript">
                    </div>
                    <div class="form-group">
                        <label>Prioridade</label>
                        <select id="goalPriority">
                            <option value="low">Baixa</option>
                            <option value="medium">Média</option>
                            <option value="high">Alta</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Data Limite</label>
                        <input type="date" id="goalDate">
                    </div>
                    <div class="form-group">
                        <label>Progresso (%)</label>
                        <input type="number" id="goalProgress" min="0" max="100" placeholder="0-100">
                    </div>
                </div>
                
                <div class="form-group">
                    <label>Descrição</label>
                    <textarea id="goalDescription" rows="3" placeholder="Detalhes sobre esta meta..."></textarea>
                </div>
                
                <button class="btn btn-primary" id="addGoalBtn">
                    <i>➕</i> Adicionar Meta
                </button>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📊</i> Progresso das Metas
                </div>
                
                <table class="data-table">
                    <thead>
                        <tr>
                            <th>Meta</th>
                            <th>Prioridade</th>
                            <th>Progresso</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody id="goalsTableBody"></tbody>
                </table>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📈</i> Estatísticas de Metas
                </div>
                <div class="chart-container">
                    <canvas id="goalsChart"></canvas>
                </div>
            </div>
        </div>
        
        <!-- Finance Section -->
        <div class="content-section" id="financeSection">
            <div class="section-card">
                <div class="section-title">
                    <i>💰</i> Minhas Finanças
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Renda Mensal</label>
                        <input type="number" id="monthlyIncome" placeholder="R$">
                    </div>
                    <div class="form-group">
                        <label>Renda Diária</label>
                        <input type="number" id="dailyIncome" placeholder="R$">
                    </div>
                </div>
                
                <div class="section-title" style="margin-top: 30px; font-size: 18px;">
                    <i>📉</i> Despesas Fixas
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Nome da Despesa</label>
                        <input type="text" id="expenseName" placeholder="Ex: Aluguel">
                    </div>
                    <div class="form-group">
                        <label>Valor (R$)</label>
                        <input type="number" id="expenseAmount" placeholder="0,00">
                    </div>
                    <div class="form-group">
                        <label>Data de Vencimento</label>
                        <input type="date" id="expenseDate">
                    </div>
                </div>
                
                <button class="btn btn-primary" id="addExpenseBtn">
                    <i>➕</i> Adicionar Despesa
                </button>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>🧾</i> Minhas Despesas
                </div>
                
                <table class="data-table">
                    <thead>
                        <tr>
                            <th>Despesa</th>
                            <th>Valor</th>
                            <th>Vencimento</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody id="expensesTableBody"></tbody>
                </table>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📊</i> Resumo Financeiro
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Total de Renda</label>
                        <input type="text" id="totalIncome" readonly>
                    </div>
                    <div class="form-group">
                        <label>Total de Despesas</label>
                        <input type="text" id="totalExpenses" readonly>
                    </div>
                    <div class="form-group">
                        <label>Saldo Disponível</label>
                        <input type="text" id="availableBalance" readonly>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="financeChart"></canvas>
                </div>
            </div>
        </div>
        
        <!-- Routine Section -->
        <div class="content-section" id="routineSection">
            <div class="section-card">
                <div class="section-title">
                    <i>⏰</i> Minha Rotina Semanal
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Dia da Semana</label>
                        <select id="routineDay">
                            <option value="monday">Segunda-feira</option>
                            <option value="tuesday">Terça-feira</option>
                            <option value="wednesday">Quarta-feira</option>
                            <option value="thursday">Quinta-feira</option>
                            <option value="friday">Sexta-feira</option>
                            <option value="saturday">Sábado</option>
                            <option value="sunday">Domingo</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Horário</label>
                        <input type="time" id="routineTime">
                    </div>
                    <div class="form-group">
                        <label>Atividade</label>
                        <input type="text" id="routineActivity" placeholder="O que você vai fazer?">
                    </div>
                </div>
                
                <button class="btn btn-primary" id="addRoutineBtn">
                    <i>➕</i> Adicionar à Rotina
                </button>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📅</i> Grade de Rotina
                </div>
                
                <div class="routine-grid" id="routineGrid">
                    <!-- Generated by JavaScript -->
                </div>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📊</i> Estatísticas de Rotina
                </div>
                <div class="chart-container">
                    <canvas id="routineChart"></canvas>
                </div>
            </div>
        </div>
        
        <!-- Reminders Section -->
        <div class="content-section" id="remindersSection">
            <div class="section-card">
                <div class="section-title">
                    <i>🔔</i> Meus Lembretes
                </div>
                
                <div class="form-grid">
                    <div class="form-group">
                        <label>Título</label>
                        <input type="text" id="reminderTitle" placeholder="Ex: Pagar conta">
                    </div>
                    <div class="form-group">
                        <label>Data e Hora</label>
                        <input type="datetime-local" id="reminderDate">
                    </div>
                </div>
                
                <div class="form-group">
                    <label>Detalhes</label>
                    <textarea id="reminderNote" rows="3" placeholder="Descrição do lembrete..."></textarea>
                </div>
                
                <button class="btn btn-primary" id="addReminderBtn">
                    <i>➕</i> Adicionar Lembrete
                </button>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📋</i> Lista de Lembretes
                </div>
                
                <table class="data-table">
                    <thead>
                        <tr>
                            <th>Título</th>
                            <th>Data/Hora</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody id="remindersTableBody"></tbody>
                </table>
            </div>
            
            <div class="section-card">
                <div class="section-title">
                    <i>📊</i> Visão Geral
                </div>
                <div class="chart-container">
                    <canvas id="overviewChart"></canvas>
                </div>
            </div>
        </div>
        
        <!-- Settings Modal -->
        <div class="settings-modal" id="settingsModal">
            <div class="settings-content">
                <div class="settings-header">
                    <h3>Configurações</h3>
                    <span class="close-settings">&times;</span>
                </div>
                
                <div class="settings-body">
                    <div class="settings-tabs">
                        <div class="settings-tab active" data-tab="appearance">Aparência</div>
                        <div class="settings-tab" data-tab="account">Conta</div>
                        <div class="settings-tab" data-tab="privacy">Privacidade</div>
                    </div>
                    
                    <div class="settings-tab-content active" id="appearanceTab">
                        <div class="form-group">
                            <label>Tema</label>
                            <select id="themeSelect">
                                <option value="dark">Escuro</option>
                                <option value="light">Claro</option>
                                <option value="auto">Automático</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label>Cores Principais</label>
                            <div class="color-picker">
                                <div class="color-option selected" style="background-color: #6e48aa;" data-color="primary"></div>
                                <div class="color-option" style="background-color: #9d50bb;" data-color="secondary"></div>
                                <div class="color-option" style="background-color: #00dbde;" data-color="accent"></div>
                                <div class="color-option" style="background-color: #1a1a2e;" data-color="dark"></div>
                                <div class="color-option" style="background-color: #16213e;" data-color="darker"></div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Cores dos Módulos</label>
                            <div class="color-picker">
                                <div class="color-option selected" style="background-color: #FF6B6B;" data-bubble="1"></div>
                                <div class="color-option" style="background-color: #4ECDC4;" data-bubble="2"></div>
                                <div class="color-option" style="background-color: #45B7D1;" data-bubble="3"></div>
                                <div class="color-option" style="background-color: #FFBE0B;" data-bubble="4"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="settings-tab-content" id="accountTab">
                        <div class="form-group">
                            <label>Nome</label>
                            <input type="text" id="userName" placeholder="Seu nome">
                        </div>
                        
                        <div class="form-group">
                            <label>E-mail</label>
                            <input type="email" id="userEmail" placeholder="seu@email.com">
                        </div>
                        
                        <div class="form-group">
                            <label>Idioma</label>
                            <select id="languageSelect">
                                <option value="pt">Português</option>
                                <option value="en">Inglês</option>
                                <option value="es">Espanhol</option>
                            </select>
                        </div>
                        
                        <div class="form-group">
                            <label>Alterar Senha</label>
                            <input type="password" id="currentPassword" placeholder="Senha atual">
                            <input type="password" id="newPassword" placeholder="Nova senha" style="margin-top: 10px;">
                            <input type="password" id="confirmNewPassword" placeholder="Confirmar nova senha" style="margin-top: 10px;">
                        </div>
                        
                        <button class="btn btn-primary" id="saveAccountBtn">
                            Salvar Alterações
                        </button>
                    </div>
                    
                    <div class="settings-tab-content" id="privacyTab">
                        <div class="form-group">
                            <label>
                                <input type="checkbox" id="privateAccount">
                                Tornar minha conta privada
                            </label>
                            <small>Contas privadas não aparecem em buscas</small>
                        </div>
                        
                        <div class="form-group">
                            <label>
                                <input type="checkbox" id="dataCollection">
                                Permitir coleta de dados anônimos
                            </label>
                            <small>Nos ajuda a melhorar o aplicativo</small>
                        </div>
                        
                        <div class="form-group">
                            <label>Exportar Dados</label>
                            <button class="btn btn-secondary" id="exportDataBtn">
                                Exportar para JSON
                            </button>
                        </div>
                        
                        <div class="form-group">
                            <label>Excluir Conta</label>
                            <button class="btn btn-danger" id="deleteAccountBtn">
                                Excluir Minha Conta Permanentemente
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global Data
        let appData = {
            user: {
                name: '',
                email: '',
                avatar: 'U',
                language: 'pt',
                theme: 'dark',
                colors: {
                    primary: '#6e48aa',
                    secondary: '#9d50bb',
                    accent: '#00dbde',
                    dark: '#1a1a2e',
                    darker: '#16213e',
                    bubble1: '#FF6B6B',
                    bubble2: '#4ECDC4',
                    bubble3: '#45B7D1',
                    bubble4: '#FFBE0B'
                },
                settings: {
                    private: false,
                    dataCollection: true
                }
            },
            goals: [],
            finances: {
                income: {
                    monthly: 0,
                    daily: 0
                },
                expenses: []
            },
            routine: [],
            reminders: [],
            history: {
                goals: [],
                finances: [],
                routine: [],
                reminders: []
            }
        };

        // Charts
        let goalsChart, financeChart, routineChart, overviewChart;

        // DOM Elements
        const authContainer = document.getElementById('authContainer');
        const appContainer = document.getElementById('appContainer');
        const loginBtn = document.getElementById('loginBtn');
        const registerBtn = document.getElementById('registerBtn');
        const recoverBtn = document.getElementById('recoverBtn');
        const forgotPasswordLink = document.getElementById('forgotPasswordLink');

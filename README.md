<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pedidos Vetorizar - Sistema de Gestão</title>
    <style>
        :root {
            --primary-color: #2563eb;
            --secondary-color: #1e40af;
            --accent-color: #3b82f6;
            --success-color: #10b981;
            --warning-color: #f59e0b;
            --danger-color: #ef4444;
            --light-color: #f8fafc;
            --dark-color: #1e293b;
            --gray-color: #64748b;
            --border-color: #e2e8f0;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f1f5f9;
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            letter-spacing: 1px;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logout-btn {
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 500;
            transition: background 0.3s;
        }
        
        .logout-btn:hover {
            background: rgba(255,255,255,0.3);
        }
        
        .sidebar {
            width: 250px;
            background-color: white;
            height: calc(100vh - 72px);
            position: fixed;
            top: 72px;
            left: 0;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            padding: 20px 0;
            overflow-y: auto;
        }
        
        .sidebar-menu {
            list-style: none;
        }
        
        .sidebar-menu li {
            margin-bottom: 5px;
        }
        
        .sidebar-menu a {
            display: block;
            padding: 12px 20px;
            color: var(--dark-color);
            text-decoration: none;
            transition: all 0.3s;
            border-left: 4px solid transparent;
        }
        
        .sidebar-menu a:hover, .sidebar-menu a.active {
            background-color: #f1f5f9;
            border-left-color: var(--primary-color);
            color: var(--primary-color);
        }
        
        .main-content {
            margin-left: 250px;
            padding: 20px;
            min-height: calc(100vh - 72px);
        }
        
        .page-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: var(--dark-color);
            padding-bottom: 10px;
            border-bottom: 2px solid var(--border-color);
        }
        
        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark-color);
        }
        
        .form-control {
            width: 100%;
            padding: 10px 15px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            font-size: 1rem;
            transition: border 0.3s;
        }
        
        .form-control:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }
        
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
            font-size: 1rem;
        }
        
        .btn-primary {
            background-color: var(--primary-color);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: var(--secondary-color);
        }
        
        .btn-secondary {
            background-color: var(--gray-color);
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #475569;
        }
        
        .btn-success {
            background-color: var(--success-color);
            color: white;
        }
        
        .btn-success:hover {
            background-color: #059669;
        }
        
        .btn-danger {
            background-color: var(--danger-color);
            color: white;
        }
        
        .btn-danger:hover {
            background-color: #dc2626;
        }
        
        .table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .table th, .table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid var(--border-color);
        }
        
        .table th {
            background-color: #f8fafc;
            font-weight: 600;
            color: var(--dark-color);
        }
        
        .table tbody tr:hover {
            background-color: #f8fafc;
        }
        
        .image-preview {
            max-width: 150px;
            max-height: 150px;
            margin-top: 10px;
            border-radius: 4px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 8px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--border-color);
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray-color);
        }
        
        .close-modal:hover {
            color: var(--danger-color);
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid var(--border-color);
        }
        
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            margin-right: 5px;
            font-weight: 500;
        }
        
        .tab.active {
            border-bottom-color: var(--primary-color);
            color: var(--primary-color);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .alert {
            padding: 15px;
            border-radius: 4px;
            margin-bottom: 20px;
            font-weight: 500;
        }
        
        .alert-success {
            background-color: #d1fae5;
            color: #065f46;
            border: 1px solid #a7f3d0;
        }
        
        .alert-danger {
            background-color: #fee2e2;
            color: #991b1b;
            border: 1px solid #fecaca;
        }
        
        .alert-warning {
            background-color: #fef3c7;
            color: #92400e;
            border: 1px solid #fde68a;
        }
        
        .chart-container {
            height: 300px;
            margin: 20px 0;
        }
        
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #3b82f6, #1d4ed8);
        }
        
        .login-card {
            background: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            width: 100%;
            max-width: 400px;
        }
        
        .login-title {
            text-align: center;
            margin-bottom: 30px;
            color: var(--dark-color);
            font-size: 1.8rem;
        }
        
        .login-form .form-group {
            margin-bottom: 20px;
        }
        
        .login-btn {
            width: 100%;
            padding: 12px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        .login-btn:hover {
            background-color: var(--secondary-color);
        }
        
        .password-toggle {
            position: relative;
        }
        
        .toggle-password {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            cursor: pointer;
            color: var(--gray-color);
        }
        
        @media (max-width: 768px) {
            .sidebar {
                width: 70px;
                padding: 20px 5px;
            }
            
            .sidebar-menu a span {
                display: none;
            }
            
            .sidebar-menu a {
                text-align: center;
                padding: 15px 5px;
            }
            
            .main-content {
                margin-left: 70px;
            }
            
            .header-content {
                padding: 0 15px;
            }
        }
    </style>
</head>
<body>
    <div id="login-page" class="login-container">
        <div class="login-card">
            <h2 class="login-title">Pedidos Vetorizar</h2>
            <form id="login-form" class="login-form">
                <div class="form-group">
                    <label for="username">Login:</label>
                    <input type="text" id="username" class="form-control" required>
                </div>
                <div class="form-group password-toggle">
                    <label for="password">Senha:</label>
                    <input type="password" id="password" class="form-control" required>
                    <button type="button" class="toggle-password" onclick="togglePassword()">👁️</button>
                </div>
                <button type="submit" class="login-btn">Entrar</button>
            </form>
            <div id="login-error" class="alert alert-danger" style="display: none; margin-top: 20px;">
                Login ou senha inválidos!
            </div>
        </div>
    </div>

    <div id="main-app" style="display: none;">
        <header>
            <div class="header-content">
                <div class="logo">Pedidos Vetorizar</div>
                <div class="user-info">
                    <span id="current-user">Administrador</span>
                    <button class="logout-btn" onclick="logout()">Sair</button>
                </div>
            </div>
        </header>

        <div class="sidebar">
            <ul class="sidebar-menu">
                <li><a href="#" onclick="showPage('dashboard')" class="active">Dashboard</a></li>
                <li><a href="#" onclick="showPage('clientes')">Clientes</a></li>
                <li><a href="#" onclick="showPage('produtos')">Produtos</a></li>
                <li><a href="#" onclick="showPage('pedidos')">Pedidos</a></li>
                <li><a href="#" onclick="showPage('estoque')">Estoque</a></li>
                <li><a href="#" onclick="showPage('relatorios')">Relatórios</a></li>
                <li><a href="#" onclick="showPage('usuarios')">Usuários</a></li>
            </ul>
        </div>

        <div class="main-content">
            <!-- Dashboard -->
            <div id="dashboard" class="page active">
                <h2 class="page-title">Dashboard</h2>
                <div class="card">
                    <div class="tabs">
                        <div class="tab active" onclick="switchTab('dashboard-overview')">Visão Geral</div>
                        <div class="tab" onclick="switchTab('dashboard-analytics')">Analytics</div>
                    </div>
                    <div id="dashboard-overview" class="tab-content active">
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 30px;">
                            <div class="card" style="text-align: center; background: linear-gradient(135deg, #3b82f6, #2563eb); color: white;">
                                <h3>Total de Clientes</h3>
                                <h2 id="total-clientes" style="font-size: 2.5rem; margin: 15px 0;">0</h2>
                                <p>Clientes cadastrados</p>
                            </div>
                            <div class="card" style="text-align: center; background: linear-gradient(135deg, #10b981, #059669); color: white;">
                                <h3>Total de Produtos</h3>
                                <h2 id="total-produtos" style="font-size: 2.5rem; margin: 15px 0;">0</h2>
                                <p>Produtos em estoque</p>
                            </div>
                            <div class="card" style="text-align: center; background: linear-gradient(135deg, #f59e0b, #d97706); color: white;">
                                <h3>Pedidos Ativos</h3>
                                <h2 id="total-pedidos" style="font-size: 2.5rem; margin: 15px 0;">0</h2>
                                <p>Pedidos em aberto</p>
                            </div>
                            <div class="card" style="text-align: center; background: linear-gradient(135deg, #ef4444, #dc2626); color: white;">
                                <h3>Valor em Vendas</h3>
                                <h2 id="total-vendas" style="font-size: 2.5rem; margin: 15px 0;">R$ 0,00</h2>
                                <p>Últimos 30 dias</p>
                            </div>
                        </div>
                        <div class="card">
                            <h3>Últimos Pedidos</h3>
                            <table class="table">
                                <thead>
                                    <tr>
                                        <th>ID</th>
                                        <th>Cliente</th>
                                        <th>Data</th>
                                        <th>Valor</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody id="ultimos-pedidos">
                                    <tr>
                                        <td colspan="5" style="text-align: center;">Nenhum pedido encontrado</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div id="dashboard-analytics" class="tab-content">
                        <div class="card">
                            <h3>Vendas por Mês</h3>
                            <div class="chart-container">
                                <canvas id="vendas-chart"></canvas>
                            </div>
                        </div>
                        <div class="card">
                            <h3>Produtos Mais Vendidos</h3>
                            <div class="chart-container">
                                <canvas id="produtos-chart"></canvas>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Clientes -->
            <div id="clientes" class="page" style="display: none;">
                <h2 class="page-title">Cadastro de Clientes</h2>
                <div class="card">
                    <button class="btn btn-primary" onclick="openModal('clienteModal')">Novo Cliente</button>
                    <table class="table" id="clientes-table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Nome</th>
                                <th>Email</th>
                                <th>Telefone</th>
                                <th>Endereço</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody id="clientes-list">
                            <tr>
                                <td colspan="6" style="text-align: center;">Nenhum cliente cadastrado</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Produtos -->
            <div id="produtos" class="page" style="display: none;">
                <h2 class="page-title">Cadastro de Produtos</h2>
                <div class="card">
                    <button class="btn btn-primary" onclick="openModal('produtoModal')">Novo Produto</button>
                    <table class="table" id="produtos-table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Nome</th>
                                <th>Preço</th>
                                <th>Estoque</th>
                                <th>Imagem</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody id="produtos-list">
                            <tr>
                                <td colspan="6" style="text-align: center;">Nenhum produto cadastrado</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Pedidos -->
            <div id="pedidos" class="page" style="display: none;">
                <h2 class="page-title">Pedidos</h2>
                <div class="card">
                    <button class="btn btn-primary" onclick="openModal('pedidoModal')">Novo Pedido</button>
                    <table class="table" id="pedidos-table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Cliente</th>
                                <th>Data</th>
                                <th>Valor Total</th>
                                <th>Status</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody id="pedidos-list">
                            <tr>
                                <td colspan="6" style="text-align: center;">Nenhum pedido cadastrado</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Estoque -->
            <div id="estoque" class="page" style="display: none;">
                <h2 class="page-title">Controle de Estoque</h2>
                <div class="card">
                    <div class="tabs">
                        <div class="tab active" onclick="switchTab('estoque-lista')">Lista de Produtos</div>
                        <div class="tab" onclick="switchTab('estoque-movimentacao')">Movimentação</div>
                    </div>
                    <div id="estoque-lista" class="tab-content active">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Produto</th>
                                    <th>Quantidade</th>
                                    <th>Valor Unitário</th>
                                    <th>Valor Total</th>
                                    <th>Ações</th>
                                </tr>
                            </thead>
                            <tbody id="estoque-list">
                                <tr>
                                    <td colspan="6" style="text-align: center;">Nenhum produto em estoque</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <div id="estoque-movimentacao" class="tab-content">
                        <button class="btn btn-primary" onclick="openModal('movimentacaoModal')">Nova Movimentação</button>
                        <table class="table" style="margin-top: 20px;">
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Produto</th>
                                    <th>Tipo</th>
                                    <th>Quantidade</th>
                                    <th>Data</th>
                                    <th>Responsável</th>
                                </tr>
                            </thead>
                            <tbody id="movimentacao-list">
                                <tr>
                                    <td colspan="6" style="text-align: center;">Nenhuma movimentação registrada</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Relatórios -->
            <div id="relatorios" class="page" style="display: none;">
                <h2 class="page-title">Relatórios</h2>
                <div class="tabs">
                    <div class="tab active" onclick="switchTab('rel-vendas')">Vendas</div>
                    <div class="tab" onclick="switchTab('rel-estoque')">Estoque</div>
                    <div class="tab" onclick="switchTab('rel-clientes')">Clientes</div>
                </div>
                
                <div id="rel-vendas" class="tab-content active">
                    <div class="card">
                        <h3>Relatório de Vendas</h3>
                        <div class="form-group" style="display: flex; gap: 20px; flex-wrap: wrap;">
                            <div style="flex: 1; min-width: 200px;">
                                <label for="data-inicio-vendas">Data Início:</label>
                                <input type="date" id="data-inicio-vendas" class="form-control">
                            </div>
                            <div style="flex: 1; min-width: 200px;">
                                <label for="data-fim-vendas">Data Fim:</label>
                                <input type="date" id="data-fim-vendas" class="form-control">
                            </div>
                            <div style="align-self: flex-end;">
                                <button class="btn btn-primary" onclick="gerarRelatorioVendas()">Gerar Relatório</button>
                            </div>
                        </div>
                        <div id="relatorio-vendas-content">
                            <table class="table">
                                <thead>
                                    <tr>
                                        <th>Data</th>
                                        <th>Cliente</th>
                                        <th>Produto</th>
                                        <th>Quantidade</th>
                                        <th>Valor Unitário</th>
                                        <th>Valor Total</th>
                                    </tr>
                                </thead>
                                <tbody id="relatorio-vendas-body">
                                    <tr>
                                        <td colspan="6" style="text-align: center;">Selecione um período para gerar o relatório</td>
                                    </tr>
                                </tbody>
                            </table>
                            <div style="margin-top: 20px; text-align: right;">
                                <button class="btn btn-success" onclick="exportarRelatorio('vendas')">Exportar PDF</button>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div id="rel-estoque" class="tab-content">
                    <div class="card">
                        <h3>Relatório de Estoque</h3>
                        <button class="btn btn-primary" onclick="gerarRelatorioEstoque()" style="margin-bottom: 20px;">Gerar Relatório</button>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Produto</th>
                                    <th>Quantidade</th>
                                    <th>Valor Unitário</th>
                                    <th>Valor Total</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody id="relatorio-estoque-body">
                                <tr>
                                    <td colspan="5" style="text-align: center;">Clique em Gerar Relatório</td>
                                </tr>
                            </tbody>
                        </table>
                        <div style="margin-top: 20px; text-align: right;">
                            <button class="btn btn-success" onclick="exportarRelatorio('estoque')">Exportar PDF</button>
                        </div>
                    </div>
                </div>
                
                <div id="rel-clientes" class="tab-content">
                    <div class="card">
                        <h3>Relatório de Clientes</h3>
                        <button class="btn btn-primary" onclick="gerarRelatorioClientes()" style="margin-bottom: 20px;">Gerar Relatório</button>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Nome</th>
                                    <th>Email</th>
                                    <th>Telefone</th>
                                    <th>Endereço</th>
                                    <th>Data Cadastro</th>
                                </tr>
                            </thead>
                            <tbody id="relatorio-clientes-body">
                                <tr>
                                    <td colspan="5" style="text-align: center;">Clique em Gerar Relatório</td>
                                </tr>
                            </tbody>
                        </table>
                        <div style="margin-top: 20px; text-align: right;">
                            <button class="btn btn-success" onclick="exportarRelatorio('clientes')">Exportar PDF</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Usuários -->
            <div id="usuarios" class="page" style="display: none;">
                <h2 class="page-title">Controle de Usuários e Senhas</h2>
                <div class="card">
                    <button class="btn btn-primary" onclick="openModal('usuarioModal')">Novo Usuário</button>
                    <table class="table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Nome</th>
                                <th>Login</th>
                                <th>Nível de Acesso</th>
                                <th>Data Cadastro</th>
                                <th>Ações</th>
                            </tr>
                        </thead>
                        <tbody id="usuarios-list">
                            <tr>
                                <td>1</td>
                                <td>Administrador</td>
                                <td>adm</td>
                                <td>Administrador</td>
                                <td>01/01/2024</td>
                                <td>
                                    <button class="btn btn-secondary" onclick="editarUsuario(1)">Editar</button>
                                    <button class="btn btn-danger" onclick="excluirUsuario(1)" disabled>Excluir</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Cliente -->
    <div id="clienteModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Cadastro de Cliente</h3>
                <button class="close-modal" onclick="closeModal('clienteModal')">&times;</button>
            </div>
            <form id="clienteForm">
                <input type="hidden" id="clienteId">
                <div class="form-group">
                    <label for="clienteNome">Nome:</label>
                    <input type="text" id="clienteNome" class="form-control">
                </div>
                <div class="form-group">
                    <label for="clienteEmail">Email:</label>
                    <input type="email" id="clienteEmail" class="form-control">
                </div>
                <div class="form-group">
                    <label for="clienteTelefone">Telefone:</label>
                    <input type="text" id="clienteTelefone" class="form-control">
                </div>
                <div class="form-group">
                    <label for="clienteEndereco">Endereço:</label>
                    <input type="text" id="clienteEndereco" class="form-control">
                </div>
                <div class="form-group">
                    <label for="clienteCidade">Cidade:</label>
                    <input type="text" id="clienteCidade" class="form-control">
                </div>
                <div class="form-group">
                    <label for="clienteEstado">Estado:</label>
                    <input type="text" id="clienteEstado" class="form-control">
                </div>
                <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('clienteModal')">Cancelar</button>
                    <button type="submit" class="btn btn-primary">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Produto -->
    <div id="produtoModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Cadastro de Produto</h3>
                <button class="close-modal" onclick="closeModal('produtoModal')">&times;</button>
            </div>
            <form id="produtoForm">
                <input type="hidden" id="produtoId">
                <div class="form-group">
                    <label for="produtoNome">Nome:</label>
                    <input type="text" id="produtoNome" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="produtoDescricao">Descrição:</label>
                    <textarea id="produtoDescricao" class="form-control" rows="3"></textarea>
                </div>
                <div class="form-group">
                    <label for="produtoPreco">Preço (R$):</label>
                    <input type="number" id="produtoPreco" class="form-control" step="0.01" min="0" required>
                </div>
                <div class="form-group">
                    <label for="produtoEstoque">Quantidade em Estoque:</label>
                    <input type="number" id="produtoEstoque" class="form-control" min="0" required>
                </div>
                <div class="form-group">
                    <label for="produtoImagem">Imagem do Produto:</label>
                    <input type="file" id="produtoImagem" class="form-control" accept="image/*">
                    <img id="previewImagem" class="image-preview" style="display: none;">
                </div>
                <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('produtoModal')">Cancelar</button>
                    <button type="submit" class="btn btn-primary">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Pedido -->
    <div id="pedidoModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Cadastro de Pedido</h3>
                <button class="close-modal" onclick="closeModal('pedidoModal')">&times;</button>
            </div>
            <form id="pedidoForm">
                <input type="hidden" id="pedidoId">
                <div class="form-group">
                    <label for="pedidoCliente">Cliente:</label>
                    <select id="pedidoCliente" class="form-control" required>
                        <option value="">Selecione um cliente</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="pedidoData">Data do Pedido:</label>
                    <input type="date" id="pedidoData" class="form-control" required>
                </div>
                <div class="form-group">
                    <label>Itens do Pedido:</label>
                    <div id="itensPedidoContainer">
                        <div class="form-group" style="display: flex; gap: 10px; align-items: center; flex-wrap: wrap;">
                            <div style="flex: 1; min-width: 200px;">
                                <select class="form-control itemProduto" required>
                                    <option value="">Selecione um produto</option>
                                </select>
                            </div>
                            <div style="flex: 1; min-width: 100px;">
                                <input type="number" class="form-control itemQuantidade" placeholder="Qtd" min="1" value="1" required>
                            </div>
                            <div style="flex: 1; min-width: 100px;">
                                <input type="number" class="form-control itemPreco" placeholder="Preço" step="0.01" min="0" readonly>
                            </div>
                            <button type="button" class="btn btn-danger" onclick="removerItemPedido(this)">Remover</button>
                        </div>
                    </div>
                    <button type="button" class="btn btn-secondary" onclick="adicionarItemPedido()" style="margin-top: 10px;">Adicionar Item</button>
                </div>
                <div class="form-group">
                    <label for="pedidoStatus">Status:</label>
                    <select id="pedidoStatus" class="form-control" required>
                        <option value="pendente">Pendente</option>
                        <option value="processando">Processando</option>
                        <option value="enviado">Enviado</option>
                        <option value="entregue">Entregue</option>
                        <option value="cancelado">Cancelado</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="pedidoObservacoes">Observações:</label>
                    <textarea id="pedidoObservacoes" class="form-control" rows="3"></textarea>
                </div>
                <div class="form-group">
                    <label>Valor Total: R$ <span id="valorTotalPedido">0,00</span></label>
                </div>
                <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('pedidoModal')">Cancelar</button>
                    <button type="submit" class="btn btn-primary">Salvar Pedido</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Movimentação de Estoque -->
    <div id="movimentacaoModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Movimentação de Estoque</h3>
                <button class="close-modal" onclick="closeModal('movimentacaoModal')">&times;</button>
            </div>
            <form id="movimentacaoForm">
                <div class="form-group">
                    <label for="movProduto">Produto:</label>
                    <select id="movProduto" class="form-control" required>
                        <option value="">Selecione um produto</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="movTipo">Tipo de Movimentação:</label>
                    <select id="movTipo" class="form-control" required onchange="atualizarPlaceholderQuantidade()">
                        <option value="entrada">Entrada</option>
                        <option value="saida">Saída</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="movQuantidade">Quantidade:</label>
                    <input type="number" id="movQuantidade" class="form-control" min="1" required>
                </div>
                <div class="form-group">
                    <label for="movObservacoes">Observações:</label>
                    <textarea id="movObservacoes" class="form-control" rows="3"></textarea>
                </div>
                <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('movimentacaoModal')">Cancelar</button>
                    <button type="submit" class="btn btn-primary">Registrar Movimentação</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Usuário -->
    <div id="usuarioModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Cadastro de Usuário</h3>
                <button class="close-modal" onclick="closeModal('usuarioModal')">&times;</button>
            </div>
            <form id="usuarioForm">
                <input type="hidden" id="usuarioId">
                <div class="form-group">
                    <label for="usuarioNome">Nome Completo:</label>
                    <input type="text" id="usuarioNome" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="usuarioLogin">Login:</label>
                    <input type="text" id="usuarioLogin" class="form-control" required>
                </div>
                <div class="form-group password-toggle">
                    <label for="usuarioSenha">Senha:</label>
                    <input type="password" id="usuarioSenha" class="form-control" required>
                    <button type="button" class="toggle-password" onclick="togglePasswordUsuario()">👁️</button>
                </div>
                <div class="form-group">
                    <label for="usuarioNivel">Nível de Acesso:</label>
                    <select id="usuarioNivel" class="form-control" required>
                        <option value="administrador">Administrador</option>
                        <option value="operador">Operador</option>
                        <option value="visualizador">Visualizador</option>
                    </select>
                </div>
                <div style="display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px;">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('usuarioModal')">Cancelar</button>
                    <button type="submit" class="btn btn-primary">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // Dados em memória (simulando banco de dados)
        let db = {
            clientes: [],
            produtos: [],
            pedidos: [],
            movimentacoes: [],
            usuarios: [
                { id: 1, nome: "Administrador", login: "adm", senha: "c3382g", nivel: "administrador", dataCadastro: "01/01/2024" }
            ],
            usuarioLogado: null
        };

        // Funções de autenticação
        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const type = passwordInput.type === 'password' ? 'text' : 'password';
            passwordInput.type = type;
        }

        function togglePasswordUsuario() {
            const passwordInput = document.getElementById('usuarioSenha');
            const type = passwordInput.type === 'password' ? 'text' : 'password';
            passwordInput.type = type;
        }

        document.getElementById('login-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            const usuario = db.usuarios.find(u => u.login === username && u.senha === password);
            
            if (usuario) {
                db.usuarioLogado = usuario;
                document.getElementById('current-user').textContent = usuario.nome;
                document.getElementById('login-page').style.display = 'none';
                document.getElementById('main-app').style.display = 'block';
                document.getElementById('login-error').style.display = 'none';
                atualizarDashboard();
                carregarDadosSelects();
            } else {
                document.getElementById('login-error').style.display = 'block';
            }
        });

        function logout() {
            db.usuarioLogado = null;
            document.getElementById('login-page').style.display = 'block';
            document.getElementById('main-app').style.display = 'none';
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        }

        // Funções de navegação
        function showPage(pageId) {
            // Esconder todas as páginas
            document.querySelectorAll('.page').forEach(page => {
                page.style.display = 'none';
            });
            
            // Remover classe active de todos os links do menu
            document.querySelectorAll('.sidebar-menu a').forEach(link => {
                link.classList.remove('active');
            });
            
            // Mostrar a página selecionada
            document.getElementById(pageId).style.display = 'block';
            
            // Adicionar classe active ao link clicado
            event.target.classList.add('active');
            
            // Atualizar título da página
            document.querySelector('.page-title').textContent = 
                pageId === 'dashboard' ? 'Dashboard' :
                pageId === 'clientes' ? 'Cadastro de Clientes' :
                pageId === 'produtos' ? 'Cadastro de Produtos' :
                pageId === 'pedidos' ? 'Pedidos' :
                pageId === 'estoque' ? 'Controle de Estoque' :
                pageId === 'relatorios' ? 'Relatórios' :
                pageId === 'usuarios' ? 'Controle de Usuários e Senhas' : 'Página';
        }

        function switchTab(tabId) {
            // Esconder todos os conteúdos de tab
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // Remover classe active de todas as tabs
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Mostrar o conteúdo da tab selecionada
            document.getElementById(tabId).classList.add('active');
            
            // Adicionar classe active à tab clicada
            event.target.classList.add('active');
        }

        // Funções de modal
        function openModal(modalId) {
            document.getElementById(modalId).style.display = 'flex';
        }

        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
            // Limpar formulários quando fechar o modal
            if (modalId === 'clienteModal') {
                document.getElementById('clienteForm').reset();
                document.getElementById('clienteId').value = '';
            } else if (modalId === 'produtoModal') {
                document.getElementById('produtoForm').reset();
                document.getElementById('produtoId').value = '';
                document.getElementById('previewImagem').style.display = 'none';
            } else if (modalId === 'pedidoModal') {
                document.getElementById('pedidoForm').reset();
                document.getElementById('pedidoId').value = '';
                document.getElementById('itensPedidoContainer').innerHTML = '';
                document.getElementById('valorTotalPedido').textContent = '0,00';
                adicionarItemPedido(); // Adicionar um item vazio
            } else if (modalId === 'movimentacaoModal') {
                document.getElementById('movimentacaoForm').reset();
            } else if (modalId === 'usuarioModal') {
                document.getElementById('usuarioForm').reset();
                document.getElementById('usuarioId').value = '';
            }
        }

        // Fechar modal ao clicar fora do conteúdo
        window.addEventListener('click', function(event) {
            if (event.target.classList.contains('modal')) {
                closeModal(event.target.id);
            }
        });

        // Funções para Clientes
        document.getElementById('clienteForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const id = document.getElementById('clienteId').value || Date.now().toString();
            const cliente = {
                id: id,
                nome: document.getElementById('clienteNome').value,
                email: document.getElementById('clienteEmail').value,
                telefone: document.getElementById('clienteTelefone').value,
                endereco: document.getElementById('clienteEndereco').value,
                cidade: document.getElementById('clienteCidade').value,
                estado: document.getElementById('clienteEstado').value,
                dataCadastro: new Date().toLocaleDateString('pt-BR')
            };
            
            if (document.getElementById('clienteId').value) {
                // Editar cliente existente
                const index = db.clientes.findIndex(c => c.id === id);
                if (index !== -1) {
                    db.clientes[index] = cliente;
                }
            } else {
                // Adicionar novo cliente
                db.clientes.push(cliente);
            }
            
            atualizarListaClientes();
            closeModal('clienteModal');
            atualizarDashboard();
            carregarDadosSelects();
        });

        function atualizarListaClientes() {
            const tbody = document.getElementById('clientes-list');
            tbody.innerHTML = '';
            
            if (db.clientes.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhum cliente cadastrado</td></tr>';
                return;
            }
            
            db.clientes.forEach(cliente => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${cliente.id}</td>
                    <td>${cliente.nome || '-'}</td>
                    <td>${cliente.email || '-'}</td>
                    <td>${cliente.telefone || '-'}</td>
                    <td>${cliente.endereco ? `${cliente.endereco}, ${cliente.cidade || ''} - ${cliente.estado || ''}` : '-'}</td>
                    <td>
                        <button class="btn btn-secondary" onclick="editarCliente('${cliente.id}')">Editar</button>
                        <button class="btn btn-danger" onclick="excluirCliente('${cliente.id}')">Excluir</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function editarCliente(id) {
            const cliente = db.clientes.find(c => c.id === id);
            if (cliente) {
                document.getElementById('clienteId').value = cliente.id;
                document.getElementById('clienteNome').value = cliente.nome || '';
                document.getElementById('clienteEmail').value = cliente.email || '';
                document.getElementById('clienteTelefone').value = cliente.telefone || '';
                document.getElementById('clienteEndereco').value = cliente.endereco || '';
                document.getElementById('clienteCidade').value = cliente.cidade || '';
                document.getElementById('clienteEstado').value = cliente.estado || '';
                
                openModal('clienteModal');
            }
        }

        function excluirCliente(id) {
            if (confirm('Tem certeza que deseja excluir este cliente?')) {
                db.clientes = db.clientes.filter(c => c.id !== id);
                atualizarListaClientes();
                atualizarDashboard();
                carregarDadosSelects();
            }
        }

        // Funções para Produtos
        document.getElementById('produtoImagem').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const preview = document.getElementById('previewImagem');
                    preview.src = e.target.result;
                    preview.style.display = 'block';
                }
                reader.readAsDataURL(file);
            }
        });

        document.getElementById('produtoForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const id = document.getElementById('produtoId').value || Date.now().toString();
            const produto = {
                id: id,
                nome: document.getElementById('produtoNome').value,
                descricao: document.getElementById('produtoDescricao').value,
                preco: parseFloat(document.getElementById('produtoPreco').value),
                estoque: parseInt(document.getElementById('produtoEstoque').value),
                imagem: document.getElementById('previewImagem').src || '',
                dataCadastro: new Date().toLocaleDateString('pt-BR')
            };
            
            if (document.getElementById('produtoId').value) {
                // Editar produto existente
                const index = db.produtos.findIndex(p => p.id === id);
                if (index !== -1) {
                    db.produtos[index] = produto;
                }
            } else {
                // Adicionar novo produto
                db.produtos.push(produto);
            }
            
            atualizarListaProdutos();
            closeModal('produtoModal');
            atualizarDashboard();
            carregarDadosSelects();
        });

        function atualizarListaProdutos() {
            const tbody = document.getElementById('produtos-list');
            tbody.innerHTML = '';
            
            if (db.produtos.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhum produto cadastrado</td></tr>';
                return;
            }
            
            db.produtos.forEach(produto => {
                const row = document.createElement('tr');
                const imagemHTML = produto.imagem ? `<img src="${produto.imagem}" class="image-preview">` : '-';
                
                row.innerHTML = `
                    <td>${produto.id}</td>
                    <td>${produto.nome}</td>
                    <td>R$ ${produto.preco.toFixed(2).replace('.', ',')}</td>
                    <td>${produto.estoque}</td>
                    <td>${imagemHTML}</td>
                    <td>
                        <button class="btn btn-secondary" onclick="editarProduto('${produto.id}')">Editar</button>
                        <button class="btn btn-danger" onclick="excluirProduto('${produto.id}')">Excluir</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function editarProduto(id) {
            const produto = db.produtos.find(p => p.id === id);
            if (produto) {
                document.getElementById('produtoId').value = produto.id;
                document.getElementById('produtoNome').value = produto.nome;
                document.getElementById('produtoDescricao').value = produto.descricao || '';
                document.getElementById('produtoPreco').value = produto.preco;
                document.getElementById('produtoEstoque').value = produto.estoque;
                
                if (produto.imagem) {
                    const preview = document.getElementById('previewImagem');
                    preview.src = produto.imagem;
                    preview.style.display = 'block';
                }
                
                openModal('produtoModal');
            }
        }

        function excluirProduto(id) {
            if (confirm('Tem certeza que deseja excluir este produto?')) {
                // Verificar se o produto está em algum pedido
                const emUso = db.pedidos.some(p => 
                    p.itens && p.itens.some(item => item.produtoId === id)
                );
                
                if (emUso) {
                    alert('Não é possível excluir este produto pois ele está sendo usado em pedidos.');
                    return;
                }
                
                db.produtos = db.produtos.filter(p => p.id !== id);
                atualizarListaProdutos();
                atualizarDashboard();
                carregarDadosSelects();
            }
        }

        // Funções para Pedidos
        function adicionarItemPedido() {
            const container = document.getElementById('itensPedidoContainer');
            const div = document.createElement('div');
            div.className = 'form-group';
            div.style.display = 'flex';
            div.style.gap = '10px';
            div.style.alignItems = 'center';
            div.style.flexWrap = 'wrap';
            
            div.innerHTML = `
                <div style="flex: 1; min-width: 200px;">
                    <select class="form-control itemProduto" required>
                        <option value="">Selecione um produto</option>
                    </select>
                </div>
                <div style="flex: 1; min-width: 100px;">
                    <input type="number" class="form-control itemQuantidade" placeholder="Qtd" min="1" value="1" required>
                </div>
                <div style="flex: 1; min-width: 100px;">
                    <input type="number" class="form-control itemPreco" placeholder="Preço" step="0.01" min="0" readonly>
                </div>
                <button type="button" class="btn btn-danger" onclick="removerItemPedido(this)">Remover</button>
            `;
            
            container.appendChild(div);
            
            // Preencher os produtos no select
            const select = div.querySelector('.itemProduto');
            db.produtos.forEach(produto => {
                const option = document.createElement('option');
                option.value = produto.id;
                option.textContent = `${produto.nome} - R$ ${produto.preco.toFixed(2).replace('.', ',')}`;
                option.setAttribute('data-preco', produto.preco);
                select.appendChild(option);
            });
            
            // Adicionar evento de mudança para atualizar preço
            select.addEventListener('change', function() {
                const precoInput = this.parentElement.querySelector('.itemPreco');
                const option = this.options[this.selectedIndex];
                if (option.value) {
                    precoInput.value = parseFloat(option.getAttribute('data-preco')).toFixed(2).replace('.', ',');
                } else {
                    precoInput.value = '';
                }
                calcularValorTotalPedido();
            });
            
            // Adicionar evento para quantidade
            div.querySelector('.itemQuantidade').addEventListener('input', calcularValorTotalPedido);
        }

        function removerItemPedido(button) {
            if (document.querySelectorAll('.itemProduto').length > 1) {
                button.parentElement.remove();
                calcularValorTotalPedido();
            } else {
                alert('Deve haver pelo menos um item no pedido.');
            }
        }

        function calcularValorTotalPedido() {
            let total = 0;
            document.querySelectorAll('.itemProduto').forEach((select, index) => {
                const produtoId = select.value;
                if (produtoId) {
                    const quantidade = parseFloat(document.querySelectorAll('.itemQuantidade')[index].value) || 0;
                    const preco = parseFloat(document.querySelectorAll('.itemPreco')[index].value.replace(',', '.')) || 0;
                    total += quantidade * preco;
                }
            });
            
            document.getElementById('valorTotalPedido').textContent = total.toFixed(2).replace('.', ',');
        }

        document.getElementById('pedidoForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Validar se pelo menos um item foi adicionado
            const itens = [];
            let temItemValido = false;
            
            document.querySelectorAll('.itemProduto').forEach((select, index) => {
                const produtoId = select.value;
                if (produtoId) {
                    const produto = db.produtos.find(p => p.id === produtoId);
                    if (produto) {
                        const quantidade = parseInt(document.querySelectorAll('.itemQuantidade')[index].value) || 0;
                        const preco = parseFloat(document.querySelectorAll('.itemPreco')[index].value.replace(',', '.')) || 0;
                        
                        if (quantidade > 0 && preco > 0) {
                            itens.push({
                                produtoId: produtoId,
                                produtoNome: produto.nome,
                                quantidade: quantidade,
                                preco: preco,
                                subtotal: quantidade * preco
                            });
                            temItemValido = true;
                        }
                    }
                }
            });
            
            if (!temItemValido) {
                alert('Adicione pelo menos um item válido ao pedido.');
                return;
            }
            
            const id = document.getElementById('pedidoId').value || Date.now().toString();
            const pedido = {
                id: id,
                clienteId: document.getElementById('pedidoCliente').value,
                clienteNome: db.clientes.find(c => c.id === document.getElementById('pedidoCliente').value)?.nome || 'Cliente não encontrado',
                data: document.getElementById('pedidoData').value,
                status: document.getElementById('pedidoStatus').value,
                observacoes: document.getElementById('pedidoObservacoes').value,
                itens: itens,
                valorTotal: parseFloat(document.getElementById('valorTotalPedido').textContent.replace(',', '.')),
                dataCadastro: new Date().toLocaleDateString('pt-BR')
            };
            
            if (document.getElementById('pedidoId').value) {
                // Editar pedido existente
                const index = db.pedidos.findIndex(p => p.id === id);
                if (index !== -1) {
                    db.pedidos[index] = pedido;
                }
            } else {
                // Adicionar novo pedido
                db.pedidos.push(pedido);
            }
            
            atualizarListaPedidos();
            closeModal('pedidoModal');
            atualizarDashboard();
        });

        function atualizarListaPedidos() {
            const tbody = document.getElementById('pedidos-list');
            tbody.innerHTML = '';
            
            if (db.pedidos.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhum pedido cadastrado</td></tr>';
                return;
            }
            
            db.pedidos.forEach(pedido => {
                const statusText = {
                    'pendente': 'Pendente',
                    'processando': 'Processando',
                    'enviado': 'Enviado',
                    'entregue': 'Entregue',
                    'cancelado': 'Cancelado'
                };
                
                const statusClass = {
                    'pendente': 'background-color: #f59e0b; color: white;',
                    'processando': 'background-color: #3b82f6; color: white;',
                    'enviado': 'background-color: #6366f1; color: white;',
                    'entregue': 'background-color: #10b981; color: white;',
                    'cancelado': 'background-color: #ef4444; color: white;'
                };
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${pedido.id}</td>
                    <td>${pedido.clienteNome}</td>
                    <td>${pedido.data}</td>
                    <td>R$ ${pedido.valorTotal.toFixed(2).replace('.', ',')}</td>
                    <td><span style="padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; ${statusClass[pedido.status]}">${statusText[pedido.status]}</span></td>
                    <td>
                        <button class="btn btn-secondary" onclick="editarPedido('${pedido.id}')">Editar</button>
                        <button class="btn btn-danger" onclick="excluirPedido('${pedido.id}')">Excluir</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function editarPedido(id) {
            const pedido = db.pedidos.find(p => p.id === id);
            if (pedido) {
                document.getElementById('pedidoId').value = pedido.id;
                document.getElementById('pedidoCliente').value = pedido.clienteId;
                document.getElementById('pedidoData').value = pedido.data;
                document.getElementById('pedidoStatus').value = pedido.status;
                document.getElementById('pedidoObservacoes').value = pedido.observacoes || '';
                
                // Limpar itens existentes
                document.getElementById('itensPedidoContainer').innerHTML = '';
                
                // Adicionar itens do pedido
                pedido.itens.forEach((item, index) => {
                    if (index > 0) {
                        adicionarItemPedido();
                    }
                    
                    const selects = document.querySelectorAll('.itemProduto');
                    const select = selects[index];
                    const option = Array.from(select.options).find(opt => opt.value === item.produtoId);
                    if (option) {
                        select.value = item.produtoId;
                    }
                    
                    document.querySelectorAll('.itemQuantidade')[index].value = item.quantidade;
                    document.querySelectorAll('.itemPreco')[index].value = item.preco.toFixed(2).replace('.', ',');
                });
                
                // Calcular valor total
                calcularValorTotalPedido();
                
                openModal('pedidoModal');
            }
        }

        function excluirPedido(id) {
            if (confirm('Tem certeza que deseja excluir este pedido?')) {
                db.pedidos = db.pedidos.filter(p => p.id !== id);
                atualizarListaPedidos();
                atualizarDashboard();
            }
        }

        // Funções para Estoque
        function atualizarListaEstoque() {
            const tbody = document.getElementById('estoque-list');
            tbody.innerHTML = '';
            
            if (db.produtos.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhum produto em estoque</td></tr>';
                return;
            }
            
            db.produtos.forEach(produto => {
                const status = produto.estoque < 5 ? 'Baixo estoque' : 
                              produto.estoque < 10 ? 'Estoque médio' : 'Estoque adequado';
                const statusClass = produto.estoque < 5 ? 'background-color: #ef4444; color: white;' : 
                                  produto.estoque < 10 ? 'background-color: #f59e0b; color: white;' : 'background-color: #10b981; color: white;';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${produto.id}</td>
                    <td>${produto.nome}</td>
                    <td>${produto.estoque}</td>
                    <td>R$ ${produto.preco.toFixed(2).replace('.', ',')}</td>
                    <td>R$ ${(produto.estoque * produto.preco).toFixed(2).replace('.', ',')}</td>
                    <td>
                        <span style="padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; ${statusClass}">${status}</span>
                        <button class="btn btn-secondary" style="margin-top: 5px;" onclick="abrirMovimentacaoEstoque('${produto.id}')">Movimentar</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function abrirMovimentacaoEstoque(produtoId) {
            const produto = db.produtos.find(p => p.id === produtoId);
            if (produto) {
                document.getElementById('movProduto').value = produtoId;
                openModal('movimentacaoModal');
            }
        }

        function atualizarPlaceholderQuantidade() {
            const tipo = document.getElementById('movTipo').value;
            const input = document.getElementById('movQuantidade');
            input.placeholder = tipo === 'entrada' ? 'Quantidade a entrar' : 'Quantidade a sair';
        }

        document.getElementById('movimentacaoForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const produtoId = document.getElementById('movProduto').value;
            const tipo = document.getElementById('movTipo').value;
            const quantidade = parseInt(document.getElementById('movQuantidade').value);
            const observacoes = document.getElementById('movObservacoes').value;
            
            const produto = db.produtos.find(p => p.id === produtoId);
            if (!produto) {
                alert('Produto não encontrado');
                return;
            }
            
            if (tipo === 'saida' && produto.estoque < quantidade) {
                alert('Quantidade insuficiente em estoque');
                return;
            }
            
            // Atualizar estoque
            if (tipo === 'entrada') {
                produto.estoque += quantidade;
            } else {
                produto.estoque -= quantidade;
            }
            
            // Registrar movimentação
            const movimentacao = {
                id: Date.now().toString(),
                produtoId: produtoId,
                produtoNome: produto.nome,
                tipo: tipo,
                quantidade: quantidade,
                observacoes: observacoes,
                data: new Date().toLocaleDateString('pt-BR'),
                responsavel: db.usuarioLogado?.nome || 'Sistema'
            };
            
            db.movimentacoes.push(movimentacao);
            
            atualizarListaEstoque();
            atualizarListaMovimentacoes();
            atualizarListaProdutos(); // Atualizar lista de produtos também
            closeModal('movimentacaoModal');
            alert(`Movimentação de ${tipo === 'entrada' ? 'entrada' : 'saída'} registrada com sucesso!`);
        });

        function atualizarListaMovimentacoes() {
            const tbody = document.getElementById('movimentacao-list');
            tbody.innerHTML = '';
            
            if (db.movimentacoes.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhuma movimentação registrada</td></tr>';
                return;
            }
            
            // Ordenar movimentações por data (mais recentes primeiro)
            const movimentacoesOrdenadas = [...db.movimentacoes].sort((a, b) => b.id - a.id);
            
            movimentacoesOrdenadas.forEach(mov => {
                const tipoText = mov.tipo === 'entrada' ? 'Entrada' : 'Saída';
                const tipoClass = mov.tipo === 'entrada' ? 'background-color: #10b981; color: white;' : 'background-color: #ef4444; color: white;';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${mov.id}</td>
                    <td>${mov.produtoNome}</td>
                    <td><span style="padding: 3px 8px; border-radius: 15px; font-size: 0.8rem; ${tipoClass}">${tipoText}</span></td>
                    <td>${mov.quantidade}</td>
                    <td>${mov.data}</td>
                    <td>${mov.responsavel}</td>
                `;
                tbody.appendChild(row);
            });
        }

        // Funções para Usuários
        document.getElementById('usuarioForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Verificar se o login já existe (exceto para edição)
            const login = document.getElementById('usuarioLogin').value;
            const usuarioId = document.getElementById('usuarioId').value;
            
            const usuarioExistente = db.usuarios.find(u => u.login === login && u.id !== usuarioId);
            if (usuarioExistente) {
                alert('Este login já está em uso. Escolha outro.');
                return;
            }
            
            const id = usuarioId || Date.now().toString();
            const usuario = {
                id: id,
                nome: document.getElementById('usuarioNome').value,
                login: login,
                senha: document.getElementById('usuarioSenha').value,
                nivel: document.getElementById('usuarioNivel').value,
                dataCadastro: usuarioId ? db.usuarios.find(u => u.id === id)?.dataCadastro : new Date().toLocaleDateString('pt-BR')
            };
            
            if (usuarioId) {
                // Editar usuário existente
                const index = db.usuarios.findIndex(u => u.id === id);
                if (index !== -1) {
                    db.usuarios[index] = usuario;
                }
            } else {
                // Adicionar novo usuário
                db.usuarios.push(usuario);
            }
            
            atualizarListaUsuarios();
            closeModal('usuarioModal');
        });

        function atualizarListaUsuarios() {
            const tbody = document.getElementById('usuarios-list');
            tbody.innerHTML = '';
            
            db.usuarios.forEach(usuario => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${usuario.id}</td>
                    <td>${usuario.nome}</td>
                    <td>${usuario.login}</td>
                    <td>${usuario.nivel === 'administrador' ? 'Administrador' : usuario.nivel === 'operador' ? 'Operador' : 'Visualizador'}</td>
                    <td>${usuario.dataCadastro}</td>
                    <td>
                        <button class="btn btn-secondary" onclick="editarUsuario('${usuario.id}')">Editar</button>
                        <button class="btn btn-danger" onclick="excluirUsuario('${usuario.id}')" ${usuario.id === '1' ? 'disabled' : ''}>Excluir</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function editarUsuario(id) {
            const usuario = db.usuarios.find(u => u.id === id);
            if (usuario) {
                document.getElementById('usuarioId').value = usuario.id;
                document.getElementById('usuarioNome').value = usuario.nome;
                document.getElementById('usuarioLogin').value = usuario.login;
                document.getElementById('usuarioSenha').value = usuario.senha;
                document.getElementById('usuarioNivel').value = usuario.nivel;
                
                openModal('usuarioModal');
            }
        }

        function excluirUsuario(id) {
            if (id === '1') {
                alert('Não é possível excluir o usuário administrador padrão.');
                return;
            }
            
            if (confirm('Tem certeza que deseja excluir este usuário?')) {
                db.usuarios = db.usuarios.filter(u => u.id !== id);
                atualizarListaUsuarios();
            }
        }

        // Funções para Relatórios
        function gerarRelatorioVendas() {
            const dataInicio = document.getElementById('data-inicio-vendas').value;
            const dataFim = document.getElementById('data-fim-vendas').value;
            
            const tbody = document.getElementById('relatorio-vendas-body');
            tbody.innerHTML = '';
            
            if (!dataInicio || !dataFim) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Por favor, selecione um período válido</td></tr>';
                return;
            }
            
            // Filtrar pedidos pelo período
            const pedidosFiltrados = db.pedidos.filter(pedido => {
                if (!pedido.data) return false;
                return pedido.data >= dataInicio && pedido.data <= dataFim;
            });
            
            if (pedidosFiltrados.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" style="text-align: center;">Nenhuma venda encontrada no período selecionado</td></tr>';
                return;
            }
            
            // Gerar linhas do relatório
            pedidosFiltrados.forEach(pedido => {
                pedido.itens.forEach(item => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${pedido.data}</td>
                        <td>${pedido.clienteNome}</td>
                        <td>${item.produtoNome}</td>
                        <td>${item.quantidade}</td>
                        <td>R$ ${item.preco.toFixed(2).replace('.', ',')}</td>
                        <td>R$ ${(item.quantidade * item.preco).toFixed(2).replace('.', ',')}</td>
                    `;
                    tbody.appendChild(row);
                });
            });
        }

        function gerarRelatorioEstoque() {
            const tbody = document.getElementById('relatorio-estoque-body');
            tbody.innerHTML = '';
            
            if (db.produtos.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" style="text-align: center;">Nenhum produto cadastrado</td></tr>';
                return;
            }
            
            db.produtos.forEach(produto => {
                const status = produto.estoque < 5 ? 'Crítico' : 
                              produto.estoque < 10 ? 'Alerta' : 'Normal';
                const statusClass = produto.estoque < 5 ? 'background-color: #ef4444; color: white;' : 
                                  produto.estoque < 10 ? 'background-color: #f59e0b; color: white;' : 'background-color: #10b981; color: white;';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${produto.nome}</td>
                    <td>${produto.estoque}</td>
                    <td>R$ ${produto.preco.toFixed(2).replace('.', ',')}</td>
                    <td>R$ ${(produto.estoque * produto.preco).toFixed(2).replace('.', ',')}</td>
                    <td><span style="padding: 3px 8px; border-radius: 15px; font-size: 0.8rem; ${statusClass}">${status}</span></td>
                `;
                tbody.appendChild(row);
            });
        }

        function gerarRelatorioClientes() {
            const tbody = document.getElementById('relatorio-clientes-body');
            tbody.innerHTML = '';
            
            if (db.clientes.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" style="text-align: center;">Nenhum cliente cadastrado</td></tr>';
                return;
            }
            
            db.clientes.forEach(cliente => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${cliente.nome || '-'}</td>
                    <td>${cliente.email || '-'}</td>
                    <td>${cliente.telefone || '-'}</td>
                    <td>${cliente.endereco ? `${cliente.endereco}, ${cliente.cidade || ''} - ${cliente.estado || ''}` : '-'}</td>
                    <td>${cliente.dataCadastro || '-'}</td>
                `;
                tbody.appendChild(row);
            });
        }

        function exportarRelatorio(tipo) {
            alert(`Funcionalidade de exportar relatório em PDF para ${tipo} será implementada na versão completa.`);
            // Em uma implementação real, aqui seria gerado um PDF usando uma biblioteca como jsPDF
        }

        // Funções auxiliares
        function carregarDadosSelects() {
            // Carregar clientes no select de pedidos
            const clienteSelect = document.getElementById('pedidoCliente');
            if (clienteSelect) {
                // Salvar valor atual
                const valorAtual = clienteSelect.value;
                
                // Limpar options
                clienteSelect.innerHTML = '<option value="">Selecione um cliente</option>';
                
                // Adicionar clientes
                db.clientes.forEach(cliente => {
                    const option = document.createElement('option');
                    option.value = cliente.id;
                    option.textContent = cliente.nome || `Cliente ${cliente.id}`;
                    clienteSelect.appendChild(option);
                });
                
                // Restaurar valor
                clienteSelect.value = valorAtual;
            }
            
            // Carregar produtos nos selects de itens de pedido (se houver)
            document.querySelectorAll('.itemProduto').forEach(select => {
                // Salvar valor atual
                const valorAtual = select.value;
                
                // Limpar options
                select.innerHTML = '<option value="">Selecione um produto</option>';
                
                // Adicionar produtos
                db.produtos.forEach(produto => {
                    const option = document.createElement('option');
                    option.value = produto.id;
                    option.textContent = `${produto.nome} - R$ ${produto.preco.toFixed(2).replace('.', ',')}`;
                    option.setAttribute('data-preco', produto.preco);
                    select.appendChild(option);
                });
                
                // Restaurar valor
                select.value = valorAtual;
                
                // Se tiver valor, atualizar preço
                if (valorAtual) {
                    const precoInput = select.parentElement.querySelector('.itemPreco');
                    const option = select.options[select.selectedIndex];
                    if (option && option.value) {
                        precoInput.value = parseFloat(option.getAttribute('data-preco')).toFixed(2).replace('.', ',');
                    }
                }
            });
            
            // Carregar produtos no select de movimentação
            const movProdutoSelect = document.getElementById('movProduto');
            if (movProdutoSelect) {
                // Salvar valor atual
                const valorAtual = movProdutoSelect.value;
                
                // Limpar options
                movProdutoSelect.innerHTML = '<option value="">Selecione um produto</option>';
                
                // Adicionar produtos
                db.produtos.forEach(produto => {
                    const option = document.createElement('option');
                    option.value = produto.id;
                    option.textContent = `${produto.nome} (Estoque: ${produto.estoque})`;
                    movProdutoSelect.appendChild(option);
                });
                
                // Restaurar valor
                movProdutoSelect.value = valorAtual;
            }
        }

        function atualizarDashboard() {
            // Atualizar números do dashboard
            document.getElementById('total-clientes').textContent = db.clientes.length;
            document.getElementById('total-produtos').textContent = db.produtos.length;
            document.getElementById('total-pedidos').textContent = db.pedidos.length;
            
            // Calcular valor total de vendas (últimos 30 dias)
            const trintaDiasAtras = new Date();
            trintaDiasAtras.setDate(trintaDiasAtras.getDate() - 30);
            const dataLimite = trintaDiasAtras.toISOString().split('T')[0];
            
            const vendas30dias = db.pedidos
                .filter(p => p.data >= dataLimite)
                .reduce((total, p) => total + p.valorTotal, 0);
            
            document.getElementById('total-vendas').textContent = `R$ ${vendas30dias.toFixed(2).replace('.', ',')}`;
            
            // Atualizar últimos pedidos
            const ultimosPedidosBody = document.getElementById('ultimos-pedidos');
            ultimosPedidosBody.innerHTML = '';
            
            if (db.pedidos.length === 0) {
                ultimosPedidosBody.innerHTML = '<tr><td colspan="5" style="text-align: center;">Nenhum pedido encontrado</td></tr>';
            } else {
                // Pegar os 5 últimos pedidos
                const ultimosPedidos = [...db.pedidos]
                    .sort((a, b) => b.id - a.id)
                    .slice(0, 5);
                
                ultimosPedidos.forEach(pedido => {
                    const statusText = {
                        'pendente': 'Pendente',
                        'processando': 'Processando',
                        'enviado': 'Enviado',
                        'entregue': 'Entregue',
                        'cancelado': 'Cancelado'
                    };
                    
                    const statusClass = {
                        'pendente': 'background-color: #f59e0b; color: white;',
                        'processando': 'background-color: #3b82f6; color: white;',
                        'enviado': 'background-color: #6366f1; color: white;',
                        'entregue': 'background-color: #10b981; color: white;',
                        'cancelado': 'background-color: #ef4444; color: white;'
                    };
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${pedido.id}</td>
                        <td>${pedido.clienteNome}</td>
                        <td>${pedido.data}</td>
                        <td>R$ ${pedido.valorTotal.toFixed(2).replace('.', ',')}</td>
                        <td><span style="padding: 3px 8px; border-radius: 15px; font-size: 0.8rem; ${statusClass[pedido.status]}">${statusText[pedido.status]}</span></td>
                    `;
                    ultimosPedidosBody.appendChild(row);
                });
            }
            
            // Atualizar listas
            atualizarListaEstoque();
            atualizarListaMovimentacoes();
        }

        // Inicialização
        document.addEventListener('DOMContentLoaded', function() {
            // Adicionar um item de pedido vazio ao abrir o modal de pedido
            document.getElementById('pedidoModal').addEventListener('click', function(e) {
                if (e.target.id === 'pedidoModal' && document.querySelectorAll('.itemProduto').length === 0) {
                    adicionarItemPedido();
                }
            });
            
            // Inicializar gráficos (simulados)
            if (typeof Chart !== 'undefined') {
                // Gráfico de vendas por mês (simulado)
                const vendasCtx = document.getElementById('vendas-chart');
                if (vendasCtx) {
                    new Chart(vendasCtx, {
                        type: 'line',
                        data: {
                            labels: ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez'],
                            datasets: [{
                                label: 'Vendas (R$)',
                                data: [1250, 1900, 3200, 5100, 4200, 6800, 7500, 6900, 8200, 7800, 9100, 10500],
                                borderColor: '#3b82f6',
                                backgroundColor: 'rgba(59, 130, 246, 0.1)',
                                tension: 0.3
                            }]
                        },
                        options: {
                            responsive: true,
                            plugins: {
                                legend: {
                                    position: 'top',
                                }
                            }
                        }
                    });
                }
                
                // Gráfico de produtos mais vendidos (simulado)
                const produtosCtx = document.getElementById('produtos-chart');
                if (produtosCtx) {
                    new Chart(produtosCtx, {
                        type: 'bar',
                        data: {
                            labels: ['Produto A', 'Produto B', 'Produto C', 'Produto D', 'Produto E'],
                            datasets: [{
                                label: 'Quantidade Vendida',
                                data: [150, 230, 180, 90, 120],
                                backgroundColor: [
                                    '#3b82f6',
                                    '#10b981',
                                    '#f59e0b',
                                    '#ef4444',
                                    '#8b5cf6'
                                ]
                            }]
                        },
                        options: {
                            responsive: true,
                            plugins: {
                                legend: {
                                    position: 'top',
                                }
                            }
                        }
                    });
                }
            }
        });

        // Dados de exemplo para demonstração
        function carregarDadosExemplo() {
            // Clientes de exemplo
            db.clientes = [
                { id: "1001", nome: "João Silva", email: "joao@email.com", telefone: "(11) 98765-4321", endereco: "Rua A, 123", cidade: "São Paulo", estado: "SP", dataCadastro: "15/01/2024" },
                { id: "1002", nome: "Maria Santos", email: "maria@email.com", telefone: "(21) 91234-5678", endereco: "Av. B, 456", cidade: "Rio de Janeiro", estado: "RJ", dataCadastro: "20/01/2024" },
                { id: "1003", nome: "Carlos Oliveira", email: "carlos@email.com", telefone: "(31) 99876-5432", endereco: "Rua C, 789", cidade: "Belo Horizonte", estado: "MG", dataCadastro: "25/01/2024" }
            ];
            
            // Produtos de exemplo
            db.produtos = [
                { 
                    id: "2001", 
                    nome: "Produto A", 
                    descricao: "Descrição do Produto A", 
                    preco: 150.00, 
                    estoque: 25,
                    imagem: "https://placehold.co/150x150/3b82f6/ffffff?text=Produto+A",
                    dataCadastro: "10/01/2024"
                },
                { 
                    id: "2002", 
                    nome: "Produto B", 
                    descricao: "Descrição do Produto B", 
                    preco: 89.90, 
                    estoque: 15,
                    imagem: "https://placehold.co/150x150/10b981/ffffff?text=Produto+B",
                    dataCadastro: "12/01/2024"
                },
                { 
                    id: "2003", 
                    nome: "Produto C", 
                    descricao: "Descrição do Produto C", 
                    preco: 249.99, 
                    estoque: 8,
                    imagem: "https://placehold.co/150x150/f59e0b/ffffff?text=Produto+C",
                    dataCadastro: "18/01/2024"
                }
            ];
            
            // Pedidos de exemplo
            db.pedidos = [
                {
                    id: "3001",
                    clienteId: "1001",
                    clienteNome: "João Silva",
                    data: "2024-02-01",
                    status: "entregue",
                    observacoes: "Entrega realizada com sucesso",
                    itens: [
                        { produtoId: "2001", produtoNome: "Produto A", quantidade: 2, preco: 150.00, subtotal: 300.00 },
                        { produtoId: "2002", produtoNome: "Produto B", quantidade: 1, preco: 89.90, subtotal: 89.90 }
                    ],
                    valorTotal: 389.90,
                    dataCadastro: "01/02/2024"
                },
                {
                    id: "3002",
                    clienteId: "1002",
                    clienteNome: "Maria Santos",
                    data: "2024-02-05",
                    status: "processando",
                    observacoes: "Aguardando confirmação de pagamento",
                    itens: [
                        { produtoId: "2003", produtoNome: "Produto C", quantidade: 1, preco: 249.99, subtotal: 249.99 }
                    ],
                    valorTotal: 249.99,
                    dataCadastro: "05/02/2024"
                }
            ];
            
            // Movimentações de exemplo
            db.movimentacoes = [
                { id: "4001", produtoId: "2001", produtoNome: "Produto A", tipo: "entrada", quantidade: 50, observacoes: "Compra de estoque", data: "05/01/2024", responsavel: "Administrador" },
                { id: "4002", produtoId: "2001", produtoNome: "Produto A", tipo: "saida", quantidade: 25, observacoes: "Venda #3001", data: "01/02/2024", responsavel: "Administrador" },
                { id: "4003", produtoId: "2002", produtoNome: "Produto B", tipo: "entrada", quantidade: 30, observacoes: "Compra de estoque", data: "10/01/2024", responsavel: "Administrador" },
                { id: "4004", produtoId: "2002", produtoNome: "Produto B", tipo: "saida", quantidade: 15, observacoes: "Venda #3001", data: "01/02/2024", responsavel: "Administrador" }
            ];
            
            // Atualizar todas as listas
            atualizarListaClientes();
            atualizarListaProdutos();
            atualizarListaPedidos();
            atualizarListaEstoque();
            atualizarListaMovimentacoes();
            atualizarListaUsuarios();
            atualizarDashboard();
            carregarDadosSelects();
        }

        // Carregar dados de exemplo (opcional)
        // carregarDadosExemplo();
    </script>
</body>
</html>

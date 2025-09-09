# sitedoprojetohtml

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mercadinho da Dona Ana</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEJISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEWIH" crossorigin="anonymous">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --komprao-blue: #004D99;
            --komprao-red: #E01E25;
            --komprao-green: #28A745;
            --komprao-light-blue: #1A7ADF;
            --komprao-light-red: #FF4A4F;
            --komprao-text-dark: #333;
            --komprao-text-light: #f8f9fa;
            --komprao-gray-dark: #343a40;
            --komprao-gray-medium: #6c757d;
            --komprao-gray-light: #e9ecef;
        }

        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background-color: #f0f2f5;
        }

        .navbar {
            background-color: var(--komprao-blue);
        }

        .navbar-brand {
            color: var(--komprao-text-light);
            font-weight: bold;
        }

        .container-fluid {
            padding-top: 20px;
        }

        h2.text-center {
            margin-bottom: 30px;
            color: var(--komprao-text-dark);
            font-weight: 600;
        }

        .action-buttons .btn {
            padding: 15px 25px;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 8px;
            margin: 5px; /* Espaçamento entre os botões */
            min-width: 180px; /* Largura mínima para botões */
        }

        .btn-komprao-blue {
            background-color: var(--komprao-blue);
            color: white;
            border: none;
            transition: background-color 0.2s;
        }
        .btn-komprao-blue:hover {
            background-color: var(--komprao-light-blue);
            color: white;
        }

        .btn-komprao-red {
            background-color: var(--komprao-red);
            color: white;
            border: none;
            transition: background-color 0.2s;
        }
        .btn-komprao-red:hover {
            background-color: var(--komprao-light-red);
            color: white;
        }

        .btn-komprao-green {
            background-color: var(--komprao-green);
            color: white;
            border: none;
            transition: background-color 0.2s;
        }
        .btn-komprao-green:hover {
            background-color: #218838; /* Um verde um pouco mais escuro */
            color: white;
        }

        .btn-komprao-dark {
            background-color: var(--komprao-gray-dark);
            color: white;
            border: none;
            transition: background-color 0.2s;
        }
        .btn-komprao-dark:hover {
            background-color: #23272b;
            color: white;
        }

        .btn-komprao-light {
            background-color: var(--komprao-gray-light);
            color: var(--komprao-text-dark);
            border: 1px solid #ced4da;
            transition: background-color 0.2s, color 0.2s;
        }
        .btn-komprao-light:hover {
            background-color: #dae0e5;
            color: var(--komprao-text-dark);
        }

        .btn-komprao-medium {
            background-color: var(--komprao-gray-medium);
            color: white;
            border: none;
            transition: background-color 0.2s;
        }
        .btn-komprao-medium:hover {
            background-color: #5a6268;
            color: white;
        }

        .saldo-box {
            background-color: white;
            padding: 15px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            margin-top: 30px;
            margin-bottom: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--komprao-text-dark);
        }
        .saldo-box input {
            border: 1px solid #ced4da;
            border-radius: 5px;
            padding: 8px 12px;
            margin-left: 10px;
            width: 150px;
            text-align: right;
            font-size: 1.1rem;
        }

        .estoque-atual-header {
            background-color: var(--komprao-blue);
            color: var(--komprao-text-light);
            padding: 15px 20px;
            border-top-left-radius: 12px;
            border-top-right-radius: 12px;
            font-size: 1.4rem;
            font-weight: 600;
            margin-top: 30px;
            display: flex;
            align-items: center;
        }

        .search-bar {
            background-color: white;
            padding: 20px;
            border-bottom-left-radius: 12px;
            border-bottom-right-radius: 12px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
        }
        .search-bar input {
            flex-grow: 1;
            border-radius: 8px;
            padding: 10px 15px;
            border: 1px solid #ced4da;
        }
        .search-bar .btn {
            border-radius: 8px;
            padding: 10px 20px;
        }

        .product-list {
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        .product-list .product-item {
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 10px;
            background-color: #fcfcfc;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .product-list .product-item:last-child {
            margin-bottom: 0;
        }
        .product-list .product-item h5 {
            margin-bottom: 5px;
            color: var(--komprao-blue);
            font-weight: 600;
        }
        .product-list .product-item p {
            margin-bottom: 3px;
            font-size: 0.9rem;
            color: var(--komprao-text-dark);
        }
        .product-list .product-item .badge {
            font-size: 0.85rem;
            padding: 5px 10px;
        }

        /* Cores dos badges/ícones */
        .badge-info { background-color: #17a2b8 !important; }
        .badge-success { background-color: var(--komprao-green) !important; }
        .badge-danger { background-color: var(--komprao-red) !important; }
    </style>
</head>
<body>
    <nav class="navbar navbar-expand-lg shadow-sm">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Mercadinho da Dona Ana</a>
        </div>
    </nav>

    <div class="container mt-5">
        <h2 class="text-center">Controle de Estoque</h2>

        <div class="action-buttons text-center mb-4">
            <button class="btn btn-komprao-blue">Ver Estoque</button>
            <button class="btn btn-komprao-red">Registrar Venda</button>
            <button class="btn btn-primary">Registrar Compra/Reposição</button>
            <button class="btn btn-komprao-green">Cadastrar Produto</button>
            <button class="btn btn-komprao-dark">Ver Histórico</button>
            <button class="btn btn-dark">Relatórios</button>
            <button class="btn btn-komprao-light">Desfazer</button>
            <button class="btn btn-komprao-medium">Fornecedores</button>
        </div>

        <div class="row justify-content-center mb-5">
            <div class="col-md-6">
                <div class="saldo-box">
                    Saldo da Loja (R$): <input type="text" value="1000,00" readonly>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="col-12">
                <div class="estoque-atual-header">
                    <i class="fas fa-boxes me-3"></i>Estoque Atual
                </div>
                <div class="search-bar">
                    <input type="text" placeholder="Pesquisar por nome, ID ou fornecedor...">
                    <button class="btn btn-komprao-blue">Filtrar</button>
                </div>
                <div class="product-list">
                    <div class="product-item">
                        <div>
                            <h5>[1] Queijo <span class="badge bg-primary">10 unidades</span></h5>
                            <p>Venda: R$ 5.50 / Compra: R$ 4.00</p>
                            <p>Fornecedor: N/A</p>
                        </div>
                        <div>
                            <button class="btn btn-sm btn-info me-2"><i class="fas fa-info-circle"></i></button>
                            <button class="btn btn-sm btn-success"><i class="fas fa-plus"></i></button>
                        </div>
                    </div>
                    <div class="product-item">
                        <div>
                            <h5>[2] Presunto <span class="badge bg-primary">15 unidades</span></h5>
                            <p>Venda: R$ 8.00 / Compra: R$ 6.50</p>
                            <p>Fornecedor: N/A</p>
                        </div>
                        <div>
                            <button class="btn btn-sm btn-info me-2"><i class="fas fa-info-circle"></i></button>
                            <button class="btn btn-sm btn-success"><i class="fas fa-plus"></i></button>
                        </div>
                    </div>
                    <div class="product-item">
                        <div>
                            <h5>[3] Água Mineral <span class="badge bg-primary">20 unidades</span></h5>
                            <p>Venda: R$ 2.00 / Compra: R$ 1.50</p>
                            <p>Fornecedor: N/A</p>
                        </div>
                        <div>
                            <button class="btn btn-sm btn-info me-2"><i class="fas fa-info-circle"></i></button>
                            <button class="btn btn-sm btn-success"><i class="fas fa-plus"></i></button>
                        </div>
                    </div>
                    </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="adicionarProdutoModal" tabindex="-1" aria-labelledby="adicionarProdutoModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title" id="adicionarProdutoModalLabel"><i class="fas fa-box me-2"></i>Adicionar Produto</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form id="adicionarProdutoForm">
                        <div class="mb-3">
                            <label for="nome" class="form-label">Nome do Produto</label>
                            <input type="text" class="form-control" id="nome" required>
                        </div>
                        <div class="mb-3">
                            <label for="codigoBarras" class="form-label">Código de Barras</label>
                            <input type="text" class="form-control" id="codigoBarras">
                        </div>
                        <div class="mb-3">
                            <label for="categoria" class="form-label">Categoria</label>
                            <select class="form-select" id="categoria" required>
                                <option value="">Selecione uma categoria</option>
                            </select>
                        </div>
                        <div class="mb-3">
                            <label for="unidadeMedida" class="form-label">Unidade de Medida</label>
                            <input type="text" class="form-control" id="unidadeMedida" required>
                        </div>
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="precoVenda" class="form-label">Preço de Venda</label>
                                <input type="number" class="form-control" id="precoVenda" step="0.01" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="custoReposicao" class="form-label">Custo de Reposição</label>
                                <input type="number" class="form-control" id="custoReposicao" step="0.01" required>
                            </div>
                        </div>
                        <div class="mb-3">
                            <label for="quantidade" class="form-label">Quantidade Inicial</label>
                            <input type="number" class="form-control" id="quantidade" required>
                        </div>
                        <div class="d-grid">
                            <button type="submit" class="btn btn-primary"><i class="fas fa-save me-2"></i>Salvar Produto</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="detalhesProdutoModal" tabindex="-1" aria-labelledby="detalhesProdutoModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header bg-info text-white">
                    <h5 class="modal-title" id="detalhesProdutoModalLabel"><i class="fas fa-info-circle me-2"></i>Detalhes do Produto</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <h4 id="detalhes-nome-produto" class="mb-3 text-primary"></h4>
                    <p><strong><i class="fas fa-barcode me-2"></i>Código de Barras:</strong> <span id="detalhes-codigo-barras"></span></p>
                    <p><strong><i class="fas fa-tag me-2"></i>Categoria:</strong> <span id="detalhes-categoria"></span></p>
                    <p><strong><i class="fas fa-ruler me-2"></i>Unidade:</strong> <span id="detalhes-unidade-medida"></span></p>
                    <p><strong><i class="fas fa-money-bill-wave me-2"></i>Preço de Venda:</strong> <span class="fw-bold text-success">R$ <span id="detalhes-preco-venda"></span></span></p>
                    <p><strong><i class="fas fa-coins me-2"></i>Custo de Reposição:</strong> <span class="fw-bold text-danger">R$ <span id="detalhes-custo-reposicao"></span></span></p>
                    <p><strong><i class="fas fa-warehouse me-2"></i>Quantidade em Estoque:</strong> <span id="detalhes-quantidade" class="badge bg-primary fs-6"></span></p>
                    <hr>
                    <h5><i class="fas fa-cubes me-2"></i>Lotes</h5>
                    <ul id="listaLotes" class="list-group">
                        </ul>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                </div>
            </div>
        </div>
    </div>


    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
    <script>
        let estoque = JSON.parse(localStorage.getItem('estoque')) || {};
        let categorias = JSON.parse(localStorage.getItem('categorias')) || {};
        let fornecedores = JSON.parse(localStorage.getItem('fornecedores')) || {};
        let nextProdutoId = parseInt(localStorage.getItem('nextProdutoId')) || 1;
        let nextFornecedorId = parseInt(localStorage.getItem('nextFornecedorId')) || 1;
        let nextLoteId = parseInt(localStorage.getItem('nextLoteId')) || 1;
        let saldo = parseFloat(localStorage.getItem('saldo')) || 1000.00; // Saldo inicial ajustado para 1000,00
        let carrinhoItens = {};
        let reposicaoItens = {};
        let modoOperacao = ''; // 'venda', 'reposicao', 'nenhum'

        function salvarDados() {
            localStorage.setItem('estoque', JSON.stringify(estoque));
            localStorage.setItem('categorias', JSON.stringify(categorias));
            localStorage.setItem('fornecedores', JSON.stringify(fornecedores));
            localStorage.setItem('nextProdutoId', nextProdutoId);
            localStorage.setItem('nextFornecedorId', nextFornecedorId);
            localStorage.setItem('nextLoteId', nextLoteId);
            localStorage.setItem('saldo', saldo.toFixed(2));
        }

        // Função para carregar um logo se houver uma URL disponível
        function carregarLogo() {
            const logoUrl = 'https://i.ibb.co/6y4Y6n4/logo-komprao.png'; // Substitua pela URL do seu logo
            const navbarBrand = document.querySelector('.navbar-brand');
            if (navbarBrand) {
                navbarBrand.innerHTML = `<img src="${logoUrl}" alt="Logo Komprão" height="40" class="me-2">Komprão Koch Atacadista`;
            }
        }

        function renderizarEstoque() {
            const listaProdutos = document.getElementById('listaProdutos'); // ID de lista de produtos no layout antigo
            const productListDiv = document.querySelector('.product-list'); // Classe do novo layout
            
            // Limpa o conteúdo existente, seja na lista antiga ou na div do novo layout
            if (listaProdutos) listaProdutos.innerHTML = '';
            if (productListDiv) productListDiv.innerHTML = '';


            const pesquisa = document.getElementById('pesquisa-input') ? document.getElementById('pesquisa-input').value.toLowerCase() : ''; // Novo ID do input
            const filtroCategoria = document.getElementById('filtroCategoria') ? document.getElementById('filtroCategoria').value : 'todos'; // Se existir

            // Adiciona produtos de exemplo se o estoque estiver vazio para o novo layout
            if (Object.keys(estoque).length === 0) {
                // Adiciona produtos de exemplo no estoque
                estoque['1'] = { id: 1, nome: 'Queijo', codigoBarras: '123456789', categoria: 'Laticínios', unidadeMedida: 'unidades', precoVenda: 5.50, custoReposicao: 4.00, quantidade: 10, lotes: [{ id: 1, quantidade: 10, dataEntrada: '2023-01-01', validade: '2024-01-01', fornecedorId: 'N/A' }] };
                estoque['2'] = { id: 2, nome: 'Presunto', codigoBarras: '987654321', categoria: 'Frios', unidadeMedida: 'unidades', precoVenda: 8.00, custoReposicao: 6.50, quantidade: 15, lotes: [{ id: 2, quantidade: 15, dataEntrada: '2023-01-01', validade: '2024-01-01', fornecedorId: 'N/A' }] };
                estoque['3'] = { id: 3, nome: 'Água Mineral', codigoBarras: '112233445', categoria: 'Bebidas', unidadeMedida: 'unidades', precoVenda: 2.00, custoReposicao: 1.50, quantidade: 20, lotes: [{ id: 3, quantidade: 20, dataEntrada: '2023-01-01', validade: '2024-01-01', fornecedorId: 'N/A' }] };
                salvarDados();
            }


            for (const id in estoque) {
                const produto = estoque[id];
                const categoriaNome = categorias[produto.categoria] || produto.categoria || 'N/A'; // Pega o nome da categoria ou 'N/A'
                const fornecedorNome = produto.lotes && produto.lotes.length > 0 && fornecedores[produto.lotes[0].fornecedorId] ? fornecedores[produto.lotes[0].fornecedorId].nome : 'N/A';


                if ((produto.nome.toLowerCase().includes(pesquisa) || (produto.codigoBarras && produto.codigoBarras.includes(pesquisa)) || fornecedorNome.toLowerCase().includes(pesquisa)) && (filtroCategoria === 'todos' || produto.categoria === filtroCategoria)) {
                    
                    const productItemDiv = document.createElement('div');
                    productItemDiv.className = 'product-item';
                    productItemDiv.innerHTML = `
                        <div>
                            <h5>[${produto.id}] ${produto.nome} <span class="badge bg-primary">${produto.quantidade} ${produto.unidadeMedida}</span></h5>
                            <p>Venda: R$ ${produto.precoVenda.toFixed(2)} / Compra: R$ ${produto.custoReposicao.toFixed(2)}</p>
                            <p>Fornecedor: ${fornecedorNome}</p>
                        </div>
                        <div>
                            <button class="btn btn-sm btn-info me-2" onclick="verDetalhesProduto(${id})"><i class="fas fa-info-circle"></i></button>
                            <button class="btn btn-sm btn-success" onclick="adicionarAoCarrinho(${id}, '${produto.nome}', ${produto.precoVenda})"><i class="fas fa-plus"></i></button>
                        </div>
                    `;
                    productListDiv.appendChild(productItemDiv);
                }
            }
        }

        function renderizarCategorias() {
            const selectCategoria = document.getElementById('categoria');
            if (selectCategoria) selectCategoria.innerHTML = '<option value="">Selecione uma categoria</option>';
            const filtroCategoria = document.getElementById('filtroCategoria');
            if (filtroCategoria) filtroCategoria.innerHTML = '<option value="todos">Todas as Categorias</option>';
            const listaCategorias = document.getElementById('listaCategorias');
            if (listaCategorias) listaCategorias.innerHTML = '';

            for (const id in categorias) {
                const categoria = categorias[id];
                if (selectCategoria) {
                    const option = document.createElement('option');
                    option.value = id;
                    option.textContent = categoria;
                    selectCategoria.appendChild(option);
                }
                if (filtroCategoria) {
                    const filtroOption = document.createElement('option');
                    filtroOption.value = id;
                    filtroOption.textContent = categoria;
                    filtroCategoria.appendChild(filtroOption);
                }
                if (listaCategorias) {
                    const li = document.createElement('li');
                    li.className = 'list-group-item';
                    li.innerHTML = `${categoria} <button class="btn btn-sm btn-danger float-end btn-icon btn-icon-sm" onclick="excluirCategoria(${id})"><i class="fas fa-trash-alt"></i></button>`;
                    listaCategorias.appendChild(li);
                }
            }
        }

        function adicionarProduto() {
            const form = document.getElementById('adicionarProdutoForm');
            const nome = document.getElementById('nome').value;
            const codigoBarras = document.getElementById('codigoBarras').value;
            const categoriaId = document.getElementById('categoria').value;
            const unidadeMedida = document.getElementById('unidadeMedida').value;
            const precoVenda = parseFloat(document.getElementById('precoVenda').value);
            const custoReposicao = parseFloat(document.getElementById('custoReposicao').value);
            const quantidade = parseInt(document.getElementById('quantidade').value);

            if (!nome || !categoriaId || !unidadeMedida || isNaN(precoVenda) || isNaN(custoReposicao) || isNaN(quantidade)) {
                alert('Por favor, preencha todos os campos obrigatórios.');
                return;
            }

            const novoProduto = {
                id: nextProdutoId,
                nome: nome,
                codigoBarras: codigoBarras,
                categoria: categoriaId,
                unidadeMedida: unidadeMedida,
                precoVenda: precoVenda,
                custoReposicao: custoReposicao,
                quantidade: quantidade,
                lotes: []
            };

            estoque[nextProdutoId] = novoProduto;

            const loteInicial = {
                id: nextLoteId++,
                quantidade: quantidade,
                dataEntrada: new Date().toISOString().split('T')[0],
                validade: 'N/A',
                fornecedorId: 'N/A'
            };
            novoProduto.lotes.push(loteInicial);

            nextProdutoId++;
            salvarDados();
            renderizarEstoque();
            verificarLogin();

            const modal = bootstrap.Modal.getInstance(document.getElementById('adicionarProdutoModal'));
            modal.hide();
            form.reset();
        }

        function adicionarCategoria() {
            const nomeCategoria = document.getElementById('nomeCategoria').value;
            if (nomeCategoria) {
                const id = Object.keys(categorias).length > 0 ? Math.max(...Object.keys(categorias).map(Number)) + 1 : 1;
                categorias[id] = nomeCategoria;
                salvarDados();
                renderizarCategorias();
                document.getElementById('nomeCategoria').value = '';
            }
        }

        function excluirCategoria(id) {
            if (confirm(`Tem certeza que deseja excluir a categoria '${categorias[id]}'?`)) {
                delete categorias[id];
                salvarDados();
                renderizarCategorias();
            }
        }

        function adicionarFornecedor() {
            const nome = document.getElementById('nomeFornecedor').value;
            const contato = document.getElementById('contatoFornecedor').value;
            if (nome) {
                fornecedores[nextFornecedorId] = { nome: nome, contato: contato };
                alert(`Fornecedor '${nome}' adicionado com ID ${nextFornecedorId}.`);
                nextFornecedorId++;
                document.getElementById('nomeFornecedor').value = '';
                document.getElementById('contatoFornecedor').value = '';
                renderizarFornecedores();
            }
        }

        function excluirFornecedor(id) {
            if (confirm(`Tem certeza que deseja excluir o fornecedor ID ${id}: ${fornecedores[id].nome}?`)) {
                delete fornecedores[id];
                salvarDados();
                renderizarFornecedores();
            }
        }

        function renderizarFornecedores() {
            const listaFornecedores = document.getElementById('listaFornecedores');
            if (listaFornecedores) listaFornecedores.innerHTML = '';
            
            if (listaFornecedores && Object.keys(fornecedores).length === 0) {
                listaFornecedores.innerHTML = '<li class="list-group-item text-center text-muted">Nenhum fornecedor cadastrado.</li>';
                return;
            }
            if (listaFornecedores) {
                for (const id in fornecedores) {
                    const fornecedor = fornecedores[id];
                    const li = document.createElement('li');
                    li.className = 'list-group-item';
                    li.innerHTML = `
                        <div class="item-details">
                            <h5>${fornecedor.nome}</h5>
                            <p class="mb-0 text-muted"><small>Contato: ${fornecedor.contato || 'N/A'}</small></p>
                        </div>
                        <div class="item-actions">
                            <button class="btn btn-sm btn-danger btn-icon btn-icon-sm" onclick="excluirFornecedor(${id})"><i class="fas fa-trash-alt"></i></button>
                        </div>
                    `;
                    listaFornecedores.appendChild(li);
                }
            }
        }

        function verDetalhesProduto(id) {
            const produto = estoque[id];
            if (!produto) return;

            document.getElementById('detalhes-nome-produto').textContent = produto.nome;
            document.getElementById('detalhes-codigo-barras').textContent = produto.codigoBarras || 'N/A';
            document.getElementById('detalhes-categoria').textContent = categorias[produto.categoria] || 'N/A';
            document.getElementById('detalhes-unidade-medida').textContent = produto.unidadeMedida;
            document.getElementById('detalhes-preco-venda').textContent = produto.precoVenda.toFixed(2);
            document.getElementById('detalhes-custo-reposicao').textContent = produto.custoReposicao.toFixed(2);
            document.getElementById('detalhes-quantidade').textContent = produto.quantidade;

            const listaLotes = document.getElementById('listaLotes');
            if (listaLotes) listaLotes.innerHTML = '';
            
            if (listaLotes) {
                if (produto.lotes.length === 0) {
                    listaLotes.innerHTML = '<li class="list-group-item text-center text-muted">Nenhum lote registrado.</li>';
                } else {
                    produto.lotes.forEach(lote => {
                        const li = document.createElement('li');
                        li.className = 'list-group-item';
                        li.innerHTML = `
                            <div>
                                <strong><i class="fas fa-tag me-2"></i>Lote ID:</strong> ${lote.id}<br>
                                <strong><i class="fas fa-box-open me-2"></i>Quantidade:</strong> ${lote.quantidade}<br>
                                <strong><i class="fas fa-calendar-alt me-2"></i>Entrada:</strong> ${lote.dataEntrada}<br>
                                <strong><i class="fas fa-calendar-check me-2"></i>Validade:</strong> ${lote.validade || 'N/A'}<br>
                                <strong><i class="fas fa-truck-loading me-2"></i>Fornecedor:</strong> ${fornecedores[lote.fornecedorId] ? fornecedores[lote.fornecedorId].nome : 'N/A'}
                            </div>
                        `;
                        listaLotes.appendChild(li);
                    });
                }
            }

            const modal = new bootstrap.Modal(document.getElementById('detalhesProdutoModal'));
            modal.show();
        }

        // Funções do carrinho
        function adicionarAoCarrinho(id, nome, preco) {
            const quantidade = parseInt(prompt(`Quantos ${nome} deseja adicionar ao carrinho?`));
            if (isNaN(quantidade) || quantidade <= 0) {
                return;
            }

            if (estoque[id].quantidade < quantidade) {
                alert(`Estoque insuficiente. Disponível: ${estoque[id].quantidade}`);
                return;
            }

            if (carrinhoItens[id]) {
                carrinhoItens[id].quantidade += quantidade;
            } else {
                carrinhoItens[id] = { nome: nome, preco: preco, quantidade: quantity };
            }
            renderizarCarrinho();
        }

        function adicionarAoCarrinhoReposicao(id, nome, custo) {
            const quantidade = parseInt(prompt(`Quantos ${nome} deseja repor?`));
            if (isNaN(quantidade) || quantidade <= 0) {
                return;
            }

            if (reposicaoItens[id]) {
                reposicaoItens[id].quantidade += quantidade;
            } else {
                reposicaoItens[id] = { nome: nome, custo: custo, quantidade: quantidade };
            }
            renderizarCarrinhoReposicao();
        }

        function renderizarCarrinho() {
            const carrinhoItensLista = document.getElementById('carrinhoItens');
            if (carrinhoItensLista) carrinhoItensLista.innerHTML = '';
            let total = 0;
            if (carrinhoItensLista) {
                for (const id in carrinhoItens) {
                    const item = carrinhoItens[id];
                    const subtotal = item.preco * item.quantidade;
                    total += subtotal;
                    const li = document.createElement('li');
                    li.className = 'list-group-item';
                    li.innerHTML = `
                        <div class="item-details">
                            <h6 class="mb-0">${item.nome}</h6>
                            <small class="text-muted">${item.quantidade} x R$ ${item.preco.toFixed(2)}</small>
                        </div>
                        <div class="item-actions">
                            <span class="badge bg-success me-2">R$ ${subtotal.toFixed(2)}</span>
                            <button class="btn btn-sm btn-danger btn-icon-sm" onclick="removerDoCarrinho(${id})"><i class="fas fa-trash-alt"></i></button>
                        </div>
                    `;
                    carrinhoItensLista.appendChild(li);
                }
            }
            const totalVendaSpan = document.getElementById('totalVenda');
            if (totalVendaSpan) totalVendaSpan.textContent = total.toFixed(2);
        }

        function renderizarCarrinhoReposicao() {
            const carrinhoItensLista = document.getElementById('carrinhoItens');
            if (carrinhoItensLista) carrinhoItensLista.innerHTML = '';
            let total = 0;
            if (carrinhoItensLista) {
                for (const id in reposicaoItens) {
                    const item = reposicaoItens[id];
                    const subtotal = item.custo * item.quantidade;
                    total += subtotal;
                    const li = document.createElement('li');
                    li.className = 'list-group-item';
                    li.innerHTML = `
                        <div class="item-details">
                            <h6 class="mb-0">${item.nome}</h6>
                            <small class="text-muted">${item.quantidade} x R$ ${item.custo.toFixed(2)}</small>
                        </div>
                        <div class="item-actions">
                            <span class="badge bg-danger me-2">R$ ${subtotal.toFixed(2)}</span>
                            <button class="btn btn-sm btn-danger btn-icon-sm" onclick="removerDoCarrinhoReposicao(${id})"><i class="fas fa-trash-alt"></i></button>
                        </div>
                    `;
                    carrinhoItensLista.appendChild(li);
                }
            }
            const totalVendaSpan = document.getElementById('totalVenda');
            if (totalVendaSpan) totalVendaSpan.textContent = total.toFixed(2);
        }

        function removerDoCarrinho(id) {
            delete carrinhoItens[id];
            renderizarCarrinho();
        }

        function removerDoCarrinhoReposicao(id) {
            delete reposicaoItens[id];
            renderizarCarrinhoReposicao();
        }

        function limparCarrinho() {
            carrinhoItens = {};
            reposicaoItens = {};
            renderizarCarrinho();
            renderizarCarrinhoReposicao();
            toggleCard('opcoesCard', false);
            renderizarEstoque();
        }

        function iniciarRetiradaMultipla() {
            modoOperacao = 'retirada';
            toggleCard('opcoesCard', true, '<i class="fas fa-shopping-cart me-2"></i>Carrinho de Venda');
            const btnConfirmarVenda = document.getElementById('btnConfirmarVenda');
            if (btnConfirmarVenda) btnConfirmarVenda.style.display = 'inline-block';
            const btnConfirmarReposicao = document.getElementById('btnConfirmarReposicao');
            if (btnConfirmarReposicao) btnConfirmarReposicao.style.display = 'none';
            renderizarEstoque();
            renderizarCarrinho();
        }

        function iniciarReposicaoMultipla() {
            modoOperacao = 'reposicao';
            toggleCard('opcoesCard', true, '<i class="fas fa-truck me-2"></i>Carrinho de Reposição');
            const btnConfirmarVenda = document.getElementById('btnConfirmarVenda');
            if (btnConfirmarVenda) btnConfirmarVenda.style.display = 'none';
            const btnConfirmarReposicao = document.getElementById('btnConfirmarReposicao');
            if (btnConfirmarReposicao) btnConfirmarReposicao.style.display = 'inline-block';
            renderizarEstoque();
            renderizarCarrinhoReposicao();
        }

        function confirmarVendaComPagamento() {
            const totalVendaSpan = document.getElementById('totalVenda');
            const totalVenda = totalVendaSpan ? parseFloat(totalVendaSpan.textContent) : 0;
            if (totalVenda === 0) {
                alert("O carrinho de venda está vazio.");
                return;
            }

            const formaPagamento = prompt("Selecione a forma de pagamento (Dinheiro, Cartão, PIX):");
            if (!formaPagamento) return;

            if (formaPagamento === "Dinheiro") {
                const dinheiroRecebido = parseFloat(prompt(`Total a pagar: R$ ${totalVenda.toFixed(2)}. Digite o valor recebido:`));
                if (isNaN(dinheiroRecebido) || dinheiroRecebido < totalVenda) {
                    alert("Valor insuficiente. Venda cancelada.");
                    return;
                }
                const troco = dinheiroRecebido - totalVenda;
                alert(`Venda concluída! Troco: R$ ${troco.toFixed(2)}`);
                saldo += totalVenda;
            } else {
                alert(`Venda concluída com pagamento via ${formaPagamento}.`);
                saldo += totalVenda;
            }

            for (const id in carrinhoItens) {
                const quantidadeVendida = carrinhoItens[id].quantidade;
                if (estoque[id]) {
                    estoque[id].quantidade -= quantidadeVendida;
                }
            }
            salvarDados();
            verificarLogin();
            renderizarEstoque();
            limparCarrinho();
        }

        function confirmarReposicaoComPagamento() {
            const totalVendaSpan = document.getElementById('totalVenda');
            const totalAPagar = totalVendaSpan ? parseFloat(totalVendaSpan.textContent) : 0;
            if (totalAPagar === 0) {
                alert("O carrinho de reposição está vazio.");
                return;
            }
            
            const formaPagamento = prompt("Selecione a forma de pagamento da reposição (Dinheiro, Cartão, PIX):");
            if (!formaPagamento) return;

            if (formaPagamento === "Dinheiro") {
                if (saldo < totalAPagar) {
                    alert("Saldo da loja insuficiente para esta compra de reposição em dinheiro.");
                    limparCarrinho();
                    return;
                }
            }

            if (formaPagamento === "Dinheiro") {
                saldo -= totalAPagar;
            }
            const saldoInput = document.getElementById('saldo-loja-input');
            if (saldoInput) saldoInput.value = saldo.toFixed(2).replace('.', ','); // Atualiza o input de saldo
            const saldoNavbarSpan = document.getElementById('saldo');
            if (saldoNavbarSpan) saldoNavbarSpan.textContent = saldo.toFixed(2);


            for (const id in reposicaoItens) {
                const quantidade = reposicaoItens[id].quantidade;
                const produto = estoque[id];
                
                if (produto) {
                    produto.quantidade += quantidade;
                    
                    const novoLote = {
                        id: nextLoteId++,
                        quantidade: quantidade,
                        dataEntrada: new Date().toISOString().split('T')[0],
                        validade: 'N/A', // Pode ser solicitado no prompt se necessário
                        fornecedorId: 'N/A' // Pode ser solicitado no prompt se necessário
                    };
                    produto.lotes.push(novoLote);
                }
            }
            
            alert(`Reposição concluída com sucesso! Total: R$ ${totalAPagar.toFixed(2)}.`);
            salvarDados();
            verificarLogin();
            renderizarEstoque();
            limparCarrinho();
        }

        function toggleCard(cardId, show, headerText = null) {
            const card = document.getElementById(cardId);
            const header = document.getElementById(`${cardId}Header`);
            if (card) {
                if (show) {
                    card.style.display = 'block';
                    if (headerText && header) {
                        header.innerHTML = headerText;
                    }
                } else {
                    card.style.display = 'none';
                }
            }
        }

        function verificarLogin() {
            const saldoSpanNavbar = document.getElementById('saldo');
            if (saldoSpanNavbar) {
                saldoSpanNavbar.textContent = saldo.toFixed(2);
            }
            const saldoInputLoja = document.getElementById('saldo-loja-input');
            if (saldoInputLoja) {
                saldoInputLoja.value = saldo.toFixed(2).replace('.', ',');
            }
        }
        
        function exportarEstoque() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(estoque, null, 2));
            const downloadAnchorNode = document.createElement('a');
            downloadAnchorNode.setAttribute("href", dataStr);
            downloadAnchorNode.setAttribute("download", "estoque.json");
            document.body.appendChild(downloadAnchorNode);
            downloadAnchorNode.click();
            downloadAnchorNode.remove();
        }

        // Funções para os botões do novo layout
        document.addEventListener('DOMContentLoaded', () => {
            // Carrega logo e inicia dados
            // carregarLogo(); // Descomente se for usar o logo

            renderizarCategorias();
            renderizarFornecedores();
            renderizarEstoque();
            verificarLogin();

            // Adiciona listeners para os novos elementos de pesquisa
            const pesquisaInput = document.getElementById('pesquisa-input');
            if (pesquisaInput) {
                pesquisaInput.addEventListener('input', renderizarEstoque);
            }
            const filtroCategoriaSelect = document.getElementById('filtroCategoria');
            if (filtroCategoriaSelect) {
                filtroCategoriaSelect.addEventListener('change', renderizarEstoque);
            }
            const adicionarProdutoForm = document.getElementById('adicionarProdutoForm');
            if (adicionarProdutoForm) {
                adicionarProdutoForm.addEventListener('submit', function (e) {
                    e.preventDefault();
                    adicionarProduto();
                });
            }
        });

    </script>
</body>
</html>

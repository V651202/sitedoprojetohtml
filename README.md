# sitedoprojetohtml

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Estoque Komprão Koch Atacadista</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEJISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEWIH" crossorigin="anonymous">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --komprao-blue: #004D99;
            --komprao-red: #E01E25;
            --komprao-light-blue: #1A7ADF;
            --komprao-light-red: #FF4A4F;
            --komprao-text-dark: #333;
            --komprao-text-light: #f8f9fa;
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

        .card {
            border-radius: 12px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
        }

        .card-header {
            background-color: var(--komprao-blue);
            color: var(--komprao-text-light);
            font-weight: bold;
            border-top-left-radius: 12px;
            border-top-right-radius: 12px;
            padding: 1rem 1.25rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .list-group-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-radius: 0;
            transition: background-color 0.2s;
        }

        .list-group-item:hover {
            background-color: #e9ecef;
        }

        .btn-komprao-red {
            background-color: var(--komprao-red);
            color: white;
            border: none;
            border-radius: 8px;
            transition: background-color 0.2s;
        }

        .btn-komprao-red:hover {
            background-color: var(--komprao-light-red);
        }

        .btn-komprao-blue {
            background-color: var(--komprao-blue);
            color: white;
            border: none;
            border-radius: 8px;
            transition: background-color 0.2s;
        }

        .btn-komprao-blue:hover {
            background-color: var(--komprao-light-blue);
        }

        #opcoesCard {
            display: none;
        }

        .form-control, .form-select {
            border-radius: 8px;
            transition: border-color 0.2s;
        }

        .form-control:focus, .form-select:focus {
            border-color: var(--komprao-blue);
            box-shadow: 0 0 0 0.25rem rgba(0, 77, 153, 0.25);
        }

        .badge-komprao {
            background-color: var(--komprao-red);
            color: white;
            padding: 0.5em 0.8em;
            border-radius: 50rem;
            font-weight: normal;
        }

        .btn-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border: none;
        }

        .btn-icon-sm {
            width: 30px;
            height: 30px;
        }

        .btn-success {
            background-color: #28a745;
            border-color: #28a745;
        }

        .btn-success:hover {
            background-color: #218838;
            border-color: #1e7e34;
        }

        .btn-info {
            background-color: #17a2b8;
            border-color: #17a2b8;
        }

        .btn-info:hover {
            background-color: #138496;
            border-color: #117a8b;
        }
    </style>
</head>

<body>
    <nav class="navbar navbar-expand-lg shadow-sm">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
                <img src="https://i.ibb.co/6y4Y6n4/logo-komprao.png" alt="Logo Komprão" height="40">
                Sistema de Estoque
            </a>
            <div class="d-flex ms-auto align-items-center">
                <span class="navbar-text me-3 text-white fw-bold">
                    <i class="fas fa-sack-dollar me-2"></i>Saldo: R$ <span id="saldo">0.00</span>
                </span>
            </div>
        </div>
    </nav>

    <div class="container-fluid mt-4">
        <div class="row">
            <div class="col-md-8">
                <div class="card mb-4">
                    <div class="card-header">
                        <div><i class="fas fa-boxes me-2"></i>Gestão de Produtos</div>
                        <div class="d-flex">
                            <button class="btn btn-info me-2" onclick="iniciarReposicaoMultipla()"><i class="fas fa-cart-arrow-down me-2"></i>Registrar Reposição</button>
                            <button class="btn btn-success me-2" onclick="iniciarRetiradaMultipla()"><i class="fas fa-cash-register me-2"></i>Registrar Venda</button>
                            <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#adicionarProdutoModal"><i class="fas fa-plus-circle me-2"></i>Adicionar Produto</button>
                        </div>
                    </div>
                    <div class="card-body">
                        <div class="row mb-3 g-2">
                            <div class="col-md-6">
                                <input type="text" class="form-control" id="pesquisa" placeholder="Pesquisar produto ou código...">
                            </div>
                            <div class="col-md-3">
                                <select class="form-select" id="filtroCategoria">
                                    <option value="todos">Todas as Categorias</option>
                                </select>
                            </div>
                            <div class="col-md-3 d-grid">
                                <button class="btn btn-outline-secondary" onclick="exportarEstoque()"><i class="fas fa-file-export me-2"></i>Exportar Estoque</button>
                            </div>
                        </div>
                        <ul class="list-group" id="listaProdutos">
                            </ul>
                    </div>
                </div>
            </div>

            <div class="col-md-4">
                <div class="card mb-4" id="opcoesCard">
                    <div class="card-header" id="opcoesCardHeader">Carrinho de Venda</div>
                    <div class="card-body">
                        <ul class="list-group" id="carrinhoItens">
                            </ul>
                        <div class="mt-3 text-end">
                            <h4 class="fw-bold text-success">Total: R$ <span id="totalVenda">0.00</span></h4>
                            <hr>
                            <button class="btn btn-success me-2" id="btnConfirmarVenda" onclick="confirmarVendaComPagamento()"><i class="fas fa-check-circle me-2"></i>Confirmar Venda</button>
                            <button class="btn btn-primary me-2" id="btnConfirmarReposicao" onclick="confirmarReposicaoComPagamento()" style="display:none;"><i class="fas fa-check-circle me-2"></i>Confirmar Reposição</button>
                            <button class="btn btn-secondary" onclick="limparCarrinho()"><i class="fas fa-trash-alt me-2"></i>Limpar</button>
                        </div>
                    </div>
                </div>

                <div class="card mb-4">
                    <div class="card-header"><i class="fas fa-truck-moving me-2"></i>Gestão de Fornecedores</div>
                    <div class="card-body">
                        <div class="mb-3">
                            <label for="nomeFornecedor" class="form-label">Nome do Fornecedor</label>
                            <input type="text" class="form-control" id="nomeFornecedor">
                        </div>
                        <div class="mb-3">
                            <label for="contatoFornecedor" class="form-label">Contato</label>
                            <input type="text" class="form-control" id="contatoFornecedor">
                        </div>
                        <button class="btn btn-komprao-blue w-100" onclick="adicionarFornecedor()"><i class="fas fa-plus me-2"></i>Adicionar Fornecedor</button>
                        <hr>
                        <ul class="list-group" id="listaFornecedores">
                            </ul>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header"><i class="fas fa-tags me-2"></i>Gestão de Categorias</div>
                    <div class="card-body">
                        <div class="mb-3">
                            <label for="nomeCategoria" class="form-label">Nome da Categoria</label>
                            <input type="text" class="form-control" id="nomeCategoria">
                        </div>
                        <button class="btn btn-komprao-blue w-100" onclick="adicionarCategoria()"><i class="fas fa-plus me-2"></i>Adicionar Categoria</button>
                        <hr>
                        <ul class="list-group" id="listaCategorias">
                            </ul>
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
        let saldo = parseFloat(localStorage.getItem('saldo')) || 0.00;
        let carrinhoItens = {};
        let reposicaoItens = {};
        let modoOperacao = '';

        function salvarDados() {
            localStorage.setItem('estoque', JSON.stringify(estoque));
            localStorage.setItem('categorias', JSON.stringify(categorias));
            localStorage.setItem('fornecedores', JSON.stringify(fornecedores));
            localStorage.setItem('nextProdutoId', nextProdutoId);
            localStorage.setItem('nextFornecedorId', nextFornecedorId);
            localStorage.setItem('nextLoteId', nextLoteId);
            localStorage.setItem('saldo', saldo.toFixed(2));
        }

        function renderizarEstoque() {
            const listaProdutos = document.getElementById('listaProdutos');
            listaProdutos.innerHTML = '';
            const pesquisa = document.getElementById('pesquisa').value.toLowerCase();
            const filtroCategoria = document.getElementById('filtroCategoria').value;

            for (const id in estoque) {
                const produto = estoque[id];
                if ((produto.nome.toLowerCase().includes(pesquisa) || (produto.codigoBarras && produto.codigoBarras.includes(pesquisa))) && (filtroCategoria === 'todos' || produto.categoria === filtroCategoria)) {
                    const li = document.createElement('li');
                    li.className = 'list-group-item';
                    li.innerHTML = `
                        <div class="item-details">
                            <h5>${produto.nome} <small class="text-muted">(${produto.unidadeMedida})</small></h5>
                            <p class="mb-1"><small>Cód. Barras: ${produto.codigoBarras || 'N/A'}</small></p>
                            <p class="mb-1"><small>Estoque: <span class="badge badge-komprao">${produto.quantidade}</span></small></p>
                            <p class="mb-0"><small>Preço: <span class="fw-bold text-success">R$ ${produto.precoVenda.toFixed(2)}</span></small></p>
                        </div>
                        <div class="item-actions">
                            <button class="btn btn-sm btn-outline-info me-2" onclick="verDetalhesProduto(${id})"><i class="fas fa-info-circle"></i></button>
                            ${modoOperacao === 'retirada' ? `<button class="btn btn-sm btn-success" onclick="adicionarAoCarrinho(${id}, '${produto.nome}', ${produto.precoVenda})"><i class="fas fa-plus"></i></button>` : ''}
                            ${modoOperacao === 'reposicao' ? `<button class="btn btn-sm btn-primary" onclick="adicionarAoCarrinhoReposicao(${id}, '${produto.nome}', ${produto.custoReposicao})"><i class="fas fa-plus"></i></button>` : ''}
                        </div>
                    `;
                    listaProdutos.appendChild(li);
                }
            }
        }

        function renderizarCategorias() {
            const selectCategoria = document.getElementById('categoria');
            selectCategoria.innerHTML = '<option value="">Selecione uma categoria</option>';
            const filtroCategoria = document.getElementById('filtroCategoria');
            filtroCategoria.innerHTML = '<option value="todos">Todas as Categorias</option>';
            const listaCategorias = document.getElementById('listaCategorias');
            listaCategorias.innerHTML = '';
            for (const id in categorias) {
                const categoria = categorias[id];
                const option = document.createElement('option');
                option.value = id;
                option.textContent = categoria;
                selectCategoria.appendChild(option);
                const filtroOption = document.createElement('option');
                filtroOption.value = id;
                filtroOption.textContent = categoria;
                filtroCategoria.appendChild(filtroOption);
                const li = document.createElement('li');
                li.className = 'list-group-item';
                li.innerHTML = `${categoria} <button class="btn btn-sm btn-danger float-end btn-icon btn-icon-sm" onclick="excluirCategoria(${id})"><i class="fas fa-trash-alt"></i></button>`;
                listaCategorias.appendChild(li);
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
            listaFornecedores.innerHTML = '';
            if (Object.keys(fornecedores).length === 0) {
                listaFornecedores.innerHTML = '<li class="list-group-item text-center text-muted">Nenhum fornecedor cadastrado.</li>';
                return;
            }
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
            listaLotes.innerHTML = '';
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
                carrinhoItens[id] = { nome: nome, preco: preco, quantidade: quantidade };
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
            carrinhoItensLista.innerHTML = '';
            let total = 0;
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
            document.getElementById('totalVenda').textContent = total.toFixed(2);
        }

        function renderizarCarrinhoReposicao() {
            const carrinhoItensLista = document.getElementById('carrinhoItens');
            carrinhoItensLista.innerHTML = '';
            let total = 0;
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
            document.getElementById('totalVenda').textContent = total.toFixed(2);
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
            document.getElementById('btnConfirmarVenda').style.display = 'inline-block';
            document.getElementById('btnConfirmarReposicao').style.display = 'none';
            renderizarEstoque();
            renderizarCarrinho();
        }

        function iniciarReposicaoMultipla() {
            modoOperacao = 'reposicao';
            toggleCard('opcoesCard', true, '<i class="fas fa-truck me-2"></i>Carrinho de Reposição');
            document.getElementById('btnConfirmarVenda').style.display = 'none';
            document.getElementById('btnConfirmarReposicao').style.display = 'inline-block';
            renderizarEstoque();
            renderizarCarrinhoReposicao();
        }

        function confirmarVendaComPagamento() {
            const totalVenda = parseFloat(document.getElementById('totalVenda').textContent);
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
                estoque[id].quantidade -= quantidadeVendida;
            }
            salvarDados();
            verificarLogin();
            renderizarEstoque();
            limparCarrinho();
        }

        function confirmarReposicaoComPagamento() {
            const totalAPagar = parseFloat(document.getElementById('totalVenda').textContent);
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
            document.getElementById('saldo').textContent = saldo.toFixed(2);

            for (const id in reposicaoItens) {
                const quantidade = reposicaoItens[id].quantidade;
                const produto = estoque[id];
                
                produto.quantidade += quantidade;
                
                const novoLote = {
                    id: nextLoteId++,
                    quantidade: quantidade,
                    dataEntrada: new Date().toISOString().split('T')[0],
                    validade: 'N/A',
                    fornecedorId: 'N/A'
                };
                produto.lotes.push(novoLote);
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
            if (show) {
                card.style.display = 'block';
                if (headerText) {
                    header.innerHTML = headerText;
                }
            } else {
                card.style.display = 'none';
            }
        }

        function verificarLogin() {
            const saldoSpan = document.getElementById('saldo');
            if (saldoSpan) {
                saldoSpan.textContent = saldo.toFixed(2);
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

        document.getElementById('adicionarProdutoForm').addEventListener('submit', function (e) {
            e.preventDefault();
            adicionarProduto();
        });

        document.getElementById('pesquisa').addEventListener('input', renderizarEstoque);
        document.getElementById('filtroCategoria').addEventListener('change', renderizarEstoque);

        document.addEventListener('DOMContentLoaded', () => {
            renderizarCategorias();
            renderizarFornecedores();
            renderizarEstoque();
            verificarLogin();
        });
    </script>
</body>
</html>

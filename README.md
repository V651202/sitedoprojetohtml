<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Estoque Komprão Koch Atacadista</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <style>
        :root {
            --komprao-blue: #004D99; /* Azul escuro do "Koch" e detalhes */
            --komprao-red: #E01E25; /* Vermelho do "Komprão" */
            --komprao-light-blue: #1A7ADF; /* Um azul mais claro para botões ou destaques */
            --komprao-light-red: #FF4A4F; /* Um vermelho mais claro */
            --komprao-text-dark: #333;
            --komprao-text-light: #f8f9fa;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
        }

        .navbar {
            background-color: var(--komprao-blue);
        }

        .navbar-brand {
            color: var(--komprao-text-light) !important;
            font-weight: bold;
        }

        .btn-primary {
            background-color: var(--komprao-blue);
            border-color: var(--komprao-blue);
        }
        .btn-primary:hover {
            background-color: var(--komprao-light-blue);
            border-color: var(--komprao-light-blue);
        }

        .btn-danger {
            background-color: var(--komprao-red);
            border-color: var(--komprao-red);
        }
        .btn-danger:hover {
            background-color: var(--komprao-light-red);
            border-color: var(--komprao-light-red);
        }

        .btn-warning { /* Para Venda */
            background-color: var(--komprao-red);
            border-color: var(--komprao-red);
            color: var(--komprao-text-light);
        }
        .btn-warning:hover {
            background-color: var(--komprao-light-red);
            border-color: var(--komprao-light-red);
            color: var(--komprao-text-light);
        }

        .btn-info { /* Para Reposição */
            background-color: var(--komprao-blue);
            border-color: var(--komprao-blue);
            color: var(--komprao-text-light);
        }
        .btn-info:hover {
            background-color: var(--komprao-light-blue);
            border-color: var(--komprao-light-blue);
            color: var(--komprao-text-light);
        }

        .btn-success { /* Para adicionar produto, pode ser um verde padrão ou um tone de azul/vermelho */
            background-color: #28a745; /* Verde padrão Bootstrap */
            border-color: #28a745;
        }
        .btn-success:hover {
            background-color: #218838;
            border-color: #1e7e34;
        }

        .btn-dark { /* Para histórico e relatórios */
            background-color: var(--komprao-text-dark);
            border-color: var(--komprao-text-dark);
        }
        .btn-dark:hover {
            background-color: #555;
            border-color: #555;
        }

        .card-header {
            background-color: var(--komprao-blue);
            color: var(--komprao-text-light);
            font-weight: bold;
        }

        .list-group-item.low-stock {
            background-color: #fff3cd; /* Amarelo claro Bootstrap */
            border-left: 5px solid #ffc107; /* Borda amarela */
        }

        .list-group-item.critical-stock {
            background-color: #f8d7da; /* Vermelho claro Bootstrap */
            border-left: 5px solid #dc3545; /* Borda vermelha */
        }

        .list-group-item.expired-soon {
             background-color: #f8d7da; /* Vermelho claro Bootstrap */
            border-left: 5px solid #dc3545; /* Borda vermelha */
        }
         .list-group-item.expiring {
            background-color: #fff3cd; /* Amarelo claro Bootstrap */
            border-left: 5px solid #ffc107; /* Borda amarela */
        }

        .modal-header {
            background-color: var(--komprao-blue);
            color: var(--komprao-text-light);
        }

        .modal-footer .btn-primary {
            background-color: var(--komprao-blue);
            border-color: var(--komprao-blue);
        }
         .modal-footer .btn-warning { /* Para vendas no modal */
            background-color: var(--komprao-red);
            border-color: var(--komprao-red);
            color: var(--komprao-text-light);
        }
        .modal-footer .btn-info { /* Para reposição no modal */
            background-color: var(--komprao-blue);
            border-color: var(--komprao-blue);
            color: var(--komprao-text-light);
        }
    </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
                Komprão Koch Atacadista
            </a>
        </div>
    </nav>

    <div class="container mt-4">
        <h1 class="mb-4 text-center">Controle de Estoque</h1>

        <div class="d-grid gap-2 d-md-flex justify-content-md-center mb-4">
            <button class="btn btn-primary me-md-2" onclick="verEstoque()">Ver Estoque</button>
            <button class="btn btn-warning me-md-2" onclick="iniciarRetiradaMultipla()">Registrar Venda</button>
            <button class="btn btn-info me-md-2" onclick="iniciarReposicaoMultipla()">Registrar Compra/Reposição</button>
            <button class="btn btn-success me-md-2" onclick="adicionarProduto()">Cadastrar Produto</button>
            <button class="btn btn-dark me-md-2" onclick="verHistoricoTransacoes()">Ver Histórico</button>
            <button class="btn btn-dark me-md-2" onclick="verRelatorios()">Relatórios</button>
            <button class="btn btn-outline-secondary me-md-2" onclick="desfazerUltimaTransacao()" id="btnDesfazer">Desfazer</button>
            <button class="btn btn-secondary me-md-2" onclick="gerenciarFornecedores()">Fornecedores</button>
        </div>

        <div class="row mb-4 justify-content-center">
            <div class="col-md-6">
                <div class="input-group">
                    <label for="saldo" class="input-group-text">Saldo da Loja (R$):</label>
                    <input type="number" id="saldo" class="form-control" value="0.00" step="0.01" readonly>
                </div>
            </div>
        </div>

        <div class="card mb-4">
            <div class="card-header">
                <h2 class="card-title mb-0">Estoque Atual</h2>
            </div>
            <div class="card-body">
                <div class="input-group mb-3">
                    <input type="text" id="campoPesquisa" class="form-control" placeholder="Pesquisar por nome, ID ou fornecedor...">
                    <button class="btn btn-outline-secondary" type="button" onclick="verEstoque()">Filtrar</button>
                </div>
                <ul class="list-group" id="listaEstoque">
                </ul>
            </div>
        </div>

        <div class="card d-none" id="opcoesCard">
            <div class="card-header">
                <h3 class="card-title mb-0" id="opcoesTitulo"></h3>
            </div>
            <div class="card-body" id="opcoes">
            </div>
        </div>

        <div class="card d-none" id="historicoCard">
            <div class="card-header">
                <h2 class="card-title mb-0">Histórico de Transações</h2>
            </div>
            <div class="card-body">
                <ul class="list-group" id="listaHistorico">
                </ul>
            </div>
        </div>

        <div class="card d-none" id="relatoriosCard">
            <div class="card-header">
                <h2 class="card-title mb-0">Relatórios de Vendas e Lucratividade</h2>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-md-6 mb-3">
                        <h5>Relatório de Vendas por Período</h5>
                        <label for="dataInicioVendas" class="form-label">Data Início:</label>
                        <input type="date" id="dataInicioVendas" class="form-control mb-2">
                        <label for="dataFimVendas" class="form-label">Data Fim:</label>
                        <input type="date" id="dataFimVendas" class="form-control mb-3">
                        <button class="btn btn-primary w-100" onclick="gerarRelatorioVendas()">Gerar Relatório de Vendas</button>
                        <div class="mt-3" id="resultadoVendas"></div>
                    </div>
                    <div class="col-md-6 mb-3">
                        <h5>Relatório de Lucratividade por Produto</h5>
                        <button class="btn btn-primary w-100" onclick="gerarRelatorioLucratividade()">Gerar Relatório de Lucratividade</button>
                        <div class="mt-3" id="resultadoLucratividade"></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="card d-none" id="fornecedoresCard">
            <div class="card-header">
                <h2 class="card-title mb-0">Gerenciamento de Fornecedores</h2>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="nomeFornecedor" class="form-label">Nome do Fornecedor:</label>
                    <input type="text" id="nomeFornecedor" class="form-control mb-2" placeholder="Nome do fornecedor">
                    <label for="contatoFornecedor" class="form-label">Contato:</label>
                    <input type="text" id="contatoFornecedor" class="form-control mb-2" placeholder="Telefone, E-mail, etc.">
                    <button class="btn btn-primary" onclick="adicionarFornecedor()">Adicionar Fornecedor</button>
                </div>
                <hr>
                <h5>Fornecedores Cadastrados:</h5>
                <ul class="list-group" id="listaFornecedores">
                </ul>
            </div>
        </div>

        <div class="card mt-4 d-none" id="carrinhoCard">
            <div class="card-header">
                <h3 class="card-title mb-0" id="carrinhoTitulo">Carrinho de Compras / Itens em Lote</h3>
            </div>
            <div class="card-body">
                <ul id="listaItensCarrinho" class="list-group mb-3">
                    </ul>
                <p class="fs-5">Total: <strong id="carrinhoTotal">R$ 0.00</strong></p>
                <div class="d-flex justify-content-between">
                    <button class="btn btn-secondary" onclick="limparCarrinho()">Limpar Carrinho</button>
                    <button class="btn btn-primary" id="btnFinalizarCarrinho">Finalizar Operação</button>
                </div>
            </div>
        </div>

    </div>

    <div class="modal fade" id="pagamentoModalVenda" tabindex="-1" aria-labelledby="pagamentoModalVendaLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="pagamentoModalVendaLabel">Confirmar Venda e Pagamento</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <p>Itens da venda:</p>
                    <ul id="modalListaItensVenda" class="list-group mb-3">
                    </ul>
                    <p>Total a receber: <strong id="modalTotalReceber"></strong></p>
                    <hr>
                    <p>Selecione a forma de pagamento:</p>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoVenda" id="pagamentoDinheiroVenda" value="Dinheiro" checked>
                        <label class="form-check-label" for="pagamentoDinheiroVenda">Dinheiro</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoVenda" id="pagamentoCartaoCreditoVenda" value="Cartão de Crédito">
                        <label class="form-check-label" for="pagamentoCartaoCreditoVenda">Cartão de Crédito</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoVenda" id="pagamentoCartaoDebitoVenda" value="Cartão de Débito">
                        <label class="form-check-label" for="pagamentoCartaoDebitoVenda">Cartão de Débito</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoVenda" id="pagamentoPixVenda" value="Pix">
                        <label class="form-check-label" for="pagamentoPixVenda">Pix</label>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button type="button" class="btn btn-warning" id="confirmarVendaBtn">Finalizar Venda</button>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="pagamentoModalReposicao" tabindex="-1" aria-labelledby="pagamentoModalReposicaoLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="pagamentoModalReposicaoLabel">Confirmar Compra para Reposição</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <p>Itens da compra para reposição:</p>
                    <ul id="modalListaItensReposicao" class="list-group mb-3">
                    </ul>
                    <p>Total a pagar: <strong id="modalTotalPagarReposicao"></strong></p>
                    <hr>
                    <p>Selecione a forma de pagamento:</p>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoReposicao" id="pagamentoDinheiroReposicao" value="Dinheiro" checked>
                        <label class="form-check-label" for="pagamentoDinheiroReposicao">Dinheiro</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoReposicao" id="pagamentoCartaoCreditoReposicao" value="Cartão de Crédito">
                        <label class="form-check-label" for="pagamentoCartaoCreditoReposicao">Cartão de Crédito</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoReposicao" id="pagamentoCartaoDebitoReposicao" value="Cartão de Débito">
                        <label class="form-check-label" for="pagamentoCartaoDebitoReposicao">Cartão de Débito</label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="radio" name="formaPagamentoReposicao" id="pagamentoPixReposicao" value="Pix">
                        <label class="form-check-label" for="pagamentoPixReposicao">Pix</label>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button type="button" class="btn btn-info" id="confirmarReposicaoBtn">Confirmar Compra</button>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="loteValidadeModal" tabindex="-1" aria-labelledby="loteValidadeModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="loteValidadeModalLabel">Informações de Lote e Validade</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label for="inputLote" class="form-label">Número do Lote (opcional):</label>
                        <input type="text" class="form-control" id="inputLote">
                    </div>
                    <div class="mb-3">
                        <label for="inputValidade" class="form-label">Data de Validade (opcional):</label>
                        <input type="date" class="form-control" id="inputValidade">
                    </div>
                     <div class="mb-3">
                        <label for="inputFornecedorId" class="form-label">Fornecedor (ID ou Nome):</label>
                        <input type="text" class="form-control" id="inputFornecedorId" placeholder="ID ou Nome do Fornecedor">
                        <small class="form-text text-muted">Será registrado o ID do fornecedor.</small>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                    <button type="button" class="btn btn-primary" id="confirmarLoteValidadeBtn">Confirmar</button>
                </div>
            </div>
        </div>
    </div>


    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>

    <script>
        // Dados do sistema
        let saldo = 1000.00; // Saldo inicial da loja

        // Estrutura do estoque: { id: { nome, quantidade, preco, custoReposicao, fornecedorId, lotes: [{ numLote, validade, quantidade }] } }
        const estoque = {
            1: { nome: 'Queijo', quantidade: 10, preco: 5.50, custoReposicao: 4.00, fornecedorId: null, lotes: [] },
            2: { nome: 'Presunto', quantidade: 15, preco: 8.00, custoReposicao: 6.50, fornecedorId: null, lotes: [] },
            3: { nome: 'Água Mineral', quantidade: 20, preco: 2.00, custoReposicao: 1.50, fornecedorId: null, lotes: [] },
            4: { nome: 'Margarina', quantidade: 5, preco: 3.50, custoReposicao: 2.80, fornecedorId: null, lotes: [] }
        };

        // Adicionar alguns lotes de exemplo para os produtos existentes
        estoque[1].lotes.push({ numLote: 'QJ001', validade: '2025-12-31', quantidade: 5 });
        estoque[1].lotes.push({ numLote: 'QJ002', validade: '2026-03-15', quantidade: 5 });
        estoque[2].lotes.push({ numLote: 'PR001', validade: '2025-10-20', quantidade: 15 });

        let historicoTransacoes = []; // Array para armazenar o histórico de transações
        let ultimaTransacao = null; // Para a funcionalidade de desfazer

        let itensCarrinho = {}; // {id: quantidade} dos itens selecionados para VENDA ou REPOSIÇÃO
        let tipoOperacaoCarrinho = ''; // 'venda' ou 'reposicao'

        let fornecedores = {
            1: { nome: 'Laticínios Boa Vaca', contato: '(11) 9876-5432' },
            2: { nome: 'Distribuidora Frios & Cia', contato: 'contato@frios.com' }
        };
        let nextFornecedorId = 3; // Próximo ID para novos fornecedores

        // Modais do Bootstrap
        let pagamentoModalVenda;
        let pagamentoModalReposicao;
        let loteValidadeModal;

        document.addEventListener('DOMContentLoaded', function() {
            pagamentoModalVenda = new bootstrap.Modal(document.getElementById('pagamentoModalVenda'));
            pagamentoModalReposicao = new bootstrap.Modal(document.getElementById('pagamentoModalReposicao'));
            loteValidadeModal = new bootstrap.Modal(document.getElementById('loteValidadeModal'));

            // Atualiza o saldo inicial no input
            document.getElementById('saldo').value = saldo.toFixed(2);
            
            // Exibe o estoque ao carregar (já que não tem login)
            verEstoque();
            atualizarBotoesDesfazer(); // Habilita/Desabilita o botão desfazer inicialmente

            // Listener para o botão "Finalizar Venda" dentro do modal de Venda
            document.getElementById('confirmarVendaBtn').addEventListener('click', function() {
                const formaPagamento = document.querySelector('input[name="formaPagamentoVenda"]:checked').value;
                confirmarVendaComPagamento(itensCarrinho, formaPagamento);
                pagamentoModalVenda.hide();
                limparCarrinho();
            });

            // Listener para o botão "Confirmar Compra" dentro do modal de Reposição
            document.getElementById('confirmarReposicaoBtn').addEventListener('click', function() {
                const formaPagamento = document.querySelector('input[name="formaPagamentoReposicao"]:checked').value;
                confirmarReposicaoComPagamento(itensCarrinho, formaPagamento);
                pagamentoModalReposicao.hide();
                limparCarrinho();
            });

            // Listener para o botão "Finalizar Operação" no carrinho
            document.getElementById('btnFinalizarCarrinho').addEventListener('click', function() {
                if (Object.keys(itensCarrinho).length === 0) {
                    alert("O carrinho está vazio. Adicione itens antes de finalizar.");
                    return;
                }
                if (tipoOperacaoCarrinho === 'venda') {
                    prepararVendaMultipla();
                } else if (tipoOperacaoCarrinho === 'reposicao') {
                    prepararReposicaoMultipla();
                }
            });

             // Listener para o botão de confirmação do modal de Lote/Validade
             document.getElementById('confirmarLoteValidadeBtn').addEventListener('click', function() {
                // Esta lógica será tratada dentro de adicionarProduto ou iniciarReposicaoMultipla
                loteValidadeModal.hide();
             });
        });

        // --- FUNÇÕES GERAIS DE UI ---

        // Função para exibir ou ocultar cards
        function toggleCard(cardId, show, title = '') {
            const cards = ['opcoesCard', 'historicoCard', 'relatoriosCard', 'fornecedoresCard', 'carrinhoCard'];
            cards.forEach(id => {
                document.getElementById(id).classList.add('d-none');
            });

            const card = document.getElementById(cardId);
            const cardTitleElement = card.querySelector('.card-title');

            if (show) {
                if (cardTitleElement && title) {
                    cardTitleElement.textContent = title;
                }
                card.classList.remove('d-none');
            } else {
                card.classList.add('d-none');
            }
        }

        // Função para ver o estoque
        function verEstoque() {
            toggleCard('opcoesCard', false);
            toggleCard('historicoCard', false);
            toggleCard('relatoriosCard', false);
            toggleCard('fornecedoresCard', false);
            toggleCard('carrinhoCard', false);

            const listaEstoque = document.getElementById('listaEstoque');
            listaEstoque.innerHTML = '';

            const termoPesquisa = document.getElementById('campoPesquisa').value.toLowerCase();
            const hoje = new Date();
            const umMesDepois = new Date();
            umMesDepois.setMonth(hoje.getMonth() + 1);

            for (let id in estoque) {
                const produto = estoque[id];
                const fornecedorNome = produto.fornecedorId ? (fornecedores[produto.fornecedorId]?.nome || 'Desconhecido') : 'N/A';

                // Lógica de filtro: verifica se o nome, ID ou nome do fornecedor do produto inclui o termo de pesquisa
                if (
                    produto.nome.toLowerCase().includes(termoPesquisa) ||
                    id.toString().includes(termoPesquisa) ||
                    fornecedorNome.toLowerCase().includes(termoPesquisa)
                ) {
                    let classeEstoque = '';
                    if (produto.quantidade <= 2) { // Exemplo: 2 ou menos unidades é crítico
                        classeEstoque = 'critical-stock';
                    } else if (produto.quantidade <= 5) { // Exemplo: 5 ou menos unidades é baixo
                        classeEstoque = 'low-stock';
                    }

                    let validadeInfo = '';
                    let hasExpiredSoon = false;
                    let hasExpiring = false;

                    // Verifica as datas de validade dos lotes
                    if (produto.lotes && produto.lotes.length > 0) {
                        const lotesExpirados = [];
                        const lotesVencemEmBreve = [];
                        const lotesVencemProximoMes = [];

                        produto.lotes.forEach(lote => {
                            // Certifica-se de que a data de validade é um formato válido para Date
                            const validade = new Date(lote.validade + 'T00:00:00'); // Adiciona T00:00:00 para evitar problemas de fuso horário
                            if (isNaN(validade.getTime())) { // Verifica se a data é inválida
                                validadeInfo += `<br><span class="text-danger">Lote ${lote.numLote || 'N/A'}: Data de validade inválida</span>`;
                                return;
                            }

                            if (validade < hoje) {
                                lotesExpirados.push(`${lote.numLote || 'N/A'} (Exp: ${new Date(lote.validade).toLocaleDateString()})`);
                                hasExpiredSoon = true; // Considera expirado como "em breve" para visual
                            } else if (validade <= umMesDepois) {
                                lotesVencemEmBreve.push(`${lote.numLote || 'N/A'} (Exp: ${new Date(lote.validade).toLocaleDateString()})`);
                                hasExpiring = true;
                            }
                        });

                        if (lotesExpirados.length > 0) {
                            validadeInfo += `<br><span class="text-danger">VENCIDOS: ${lotesExpirados.join('; ')}</span>`;
                        }
                        if (lotesVencemEmBreve.length > 0) {
                            validadeInfo += `<br><span class="text-warning">VENCEM EM BREVE: ${lotesVencemEmBreve.join('; ')}</span>`;
                        }

                        if (hasExpiredSoon) classeEstoque += ' expired-soon';
                        else if (hasExpiring) classeEstoque += ' expiring';

                    } else {
                        validadeInfo = '<br><small class="text-muted">Sem informações de lote/validade</small>';
                    }


                    listaEstoque.innerHTML += `
                        <li class="list-group-item d-flex justify-content-between align-items-center ${classeEstoque}">
                            <div>
                                <span>[${id}] <strong>${produto.nome}</strong>: ${produto.quantidade} unidades</span>
                                <small class="d-block text-muted">Venda: R$ ${produto.preco.toFixed(2)} / Compra: R$ ${produto.custoReposicao.toFixed(2)}</small>
                                <small class="d-block text-muted">Fornecedor: ${fornecedorNome}</small>
                                ${validadeInfo}
                            </div>
                        </li>
                    `;
                }
            }
        }

        // --- CARRINHO DE COMPRAS E OPERAÇÕES EM LOTE ---
        function exibirCarrinho(tipo) {
            tipoOperacaoCarrinho = tipo;
            toggleCard('carrinhoCard', true, `Carrinho de ${tipo === 'venda' ? 'Vendas' : 'Reposição'}`);
            toggleCard('opcoesCard', false); // Esconde outras opções

            const opcoes = document.getElementById('opcoes');
            opcoes.innerHTML = ''; // Limpa as opções anteriores

            const carrinhoList = document.getElementById('listaItensCarrinho');
            carrinhoList.innerHTML = ''; // Limpa o carrinho

            document.getElementById('carrinhoTotal').textContent = 'R$ 0.00'; // Reseta o total

            // Preenche a área de seleção de produtos
            for (let id in estoque) {
                const produto = estoque[id];
                const labelPrecoCusto = tipo === 'venda' ? `Preço de Venda: R$ ${produto.preco.toFixed(2)}` : `Custo de Compra: R$ ${produto.custoReposicao.toFixed(2)}`;
                const maxQuantity = tipo === 'venda' ? produto.quantidade : ''; // Limite de venda pelo estoque

                opcoes.innerHTML += `
                    <div class="card mb-2">
                        <div class="card-body d-flex justify-content-between align-items-center">
                            <div>
                                <h5 class="card-title mb-0">[${id}] ${produto.nome}</h5>
                                <p class="card-text mb-0">(${produto.quantidade} unidades em estoque) - ${labelPrecoCusto}</p>
                            </div>
                            <div class="d-flex align-items-center">
                                <input type="number" id="quantidade${id}" class="form-control form-control-sm me-2" placeholder="Qtd" min="0" ${maxQuantity ? `max="${maxQuantity}"` : ''} value="${itensCarrinho[id] || 0}" style="width: 70px;" onchange="atualizarItemCarrinho(${id}, this.value, '${tipo}')" />
                            </div>
                        </div>
                    </div>
                `;
            }
            opcoes.innerHTML += `
                <hr>
                <button class="btn ${tipo === 'venda' ? 'btn-warning' : 'btn-info'} mt-3 w-100" onclick="document.getElementById('btnFinalizarCarrinho').click()">Adicionar ao Carrinho</button>
            `; // O botão "Adicionar ao Carrinho" aqui apenas para fins de UI, a atualização é onChange

            // Re-renderiza o carrinho com os itens já selecionados
            renderizarCarrinho();
            toggleCard('opcoesCard', true, `Adicionar Itens ao Carrinho para ${tipo === 'venda' ? 'Venda' : 'Reposição'}`);
        }

        function atualizarItemCarrinho(id, quantidadeStr, tipo) {
            const quantidade = parseInt(quantidadeStr);
            const produto = estoque[id];
            const campoInput = document.getElementById(`quantidade${id}`);

            if (isNaN(quantidade) || quantidade < 0) {
                alert("Por favor, insira uma quantidade válida.");
                campoInput.value = itensCarrinho[id] || 0; // Volta para o valor anterior
                return;
            }

            if (tipo === 'venda' && quantidade > produto.quantidade) {
                alert(`Você não pode vender mais de ${produto.quantidade} unidades de ${produto.nome}.`);
                campoInput.value = produto.quantidade;
                itensCarrinho[id] = produto.quantidade;
            } else if (quantidade > 0) {
                itensCarrinho[id] = quantidade;
            } else {
                delete itensCarrinho[id];
            }
            renderizarCarrinho();
        }

        function renderizarCarrinho() {
            const carrinhoList = document.getElementById('listaItensCarrinho');
            carrinhoList.innerHTML = '';
            let totalCarrinho = 0;

            if (Object.keys(itensCarrinho).length === 0) {
                carrinhoList.innerHTML = '<li class="list-group-item text-muted">Carrinho vazio.</li>';
                document.getElementById('carrinhoTotal').textContent = 'R$ 0.00';
                return;
            }

            for (const id in itensCarrinho) {
                const quantidade = itensCarrinho[id];
                const produto = estoque[id];
                const precoUnitario = tipoOperacaoCarrinho === 'venda' ? produto.preco : produto.custoReposicao;
                const subtotal = precoUnitario * quantidade;
                totalCarrinho += subtotal;

                carrinhoList.innerHTML += `
                    <li class="list-group-item d-flex justify-content-between align-items-center">
                        <span>[${id}] ${produto.nome} (x${quantidade})</span>
                        <span>R$ ${subtotal.toFixed(2)}</span>
                    </li>
                `;
            }
            document.getElementById('carrinhoTotal').textContent = `R$ ${totalCarrinho.toFixed(2)}`;
        }

        function limparCarrinho() {
            itensCarrinho = {};
            renderizarCarrinho();
            // Reseta os inputs de quantidade na tela de seleção
            for (let id in estoque) {
                const campoInput = document.getElementById(`quantidade${id}`);
                if (campoInput) {
                    campoInput.value = 0;
                }
            }
        }

        // --- OPERAÇÕES DE VENDA (RETIRADA DO ESTOQUE) ---

        function iniciarRetiradaMultipla() {
            exibirCarrinho('venda');
        }

        function prepararVendaMultipla() {
            const modalListaItens = document.getElementById('modalListaItensVenda');
            modalListaItens.innerHTML = '';
            let totalDaVenda = 0;

            if (Object.keys(itensCarrinho).length === 0) {
                alert("Selecione pelo menos um produto para a venda.");
                return;
            }

            for (const id in itensCarrinho) {
                const quantidade = itensCarrinho[id];
                const produto = estoque[id];
                if (produto.quantidade < quantidade) {
                    alert(`Erro: Estoque insuficiente para ${produto.nome}. Disponível: ${produto.quantidade}, Tentou vender: ${quantidade}.`);
                    return;
                }
                const subtotal = produto.preco * quantidade;
                totalDaVenda += subtotal;

                modalListaItens.innerHTML += `
                    <li class="list-group-item d-flex justify-content-between align-items-center">
                        ${produto.nome} (x${quantidade})
                        <span>R$ ${subtotal.toFixed(2)}</span>
                    </li>
                `;
            }

            document.getElementById('modalTotalReceber').textContent = `R$ ${totalDaVenda.toFixed(2)}`;
            pagamentoModalVenda.show();
        }

        function confirmarVendaComPagamento(vendaItens, formaPagamento) {
            let totalRecebido = 0;
            let resumoVenda = "Venda realizada:\n";
            let itensVendidos = []; // Para o histórico

            const saldoAntes = saldo;

            for (const id in vendaItens) {
                const quantidade = vendaItens[id]; // AQUI ESTÁ A CORREÇÃO
                const produto = estoque[id];
                const subtotal = produto.preco * quantidade;

                produto.quantidade -= quantidade; // AQUI ESTÁ A CORREÇÃO: Usando 'quantidade'

                // Lógica de retirada por lotes (FIFO - First In, First Out)
                let qtdRestante = quantidade;
                produto.lotes.sort((a, b) => new Date(a.validade) - new Date(b.validade)); // Ordena por validade
                for (let i = 0; i < produto.lotes.length && qtdRestante > 0; i++) {
                    const lote = produto.lotes[i];
                    const qtdRetiradaDoLote = Math.min(qtdRestante, lote.quantidade);
                    lote.quantidade -= qtdRetiradaDoLote;
                    qtdRestante -= qtdRetiradaDoLote;

                    // Remove o lote se a quantidade for 0
                    if (lote.quantidade === 0) {
                        produto.lotes.splice(i, 1);
                        i--; // Ajusta o índice após remover
                    }
                }

                totalRecebido += subtotal;

                resumoVenda += `- ${quantidade}x ${produto.nome} (R$ ${subtotal.toFixed(2)})\n`;
                itensVendidos.push({ id: parseInt(id), nome: produto.nome, quantidade: quantidade, precoUnitario: produto.preco });
            }

            saldo += totalRecebido;
            document.getElementById('saldo').value = saldo.toFixed(2);

            resumoVenda += `\nTotal: R$ ${totalRecebido.toFixed(2)}. Pago com: ${formaPagamento}. Novo Saldo da Loja: R$ ${saldo.toFixed(2)}`;
            alert(resumoVenda);

            ultimaTransacao = {
                tipo: 'Venda',
                data: new Date().toLocaleString('pt-BR'),
                itens: itensVendidos,
                valorTotal: totalRecebido,
                formaPagamento: formaPagamento,
                saldoAntes: saldoAntes,
                saldoDepois: saldo,
                usuario: 'Sistema' // Pode definir um usuário padrão ou deixar como vazio
            };
            historicoTransacoes.unshift(ultimaTransacao);
            atualizarBotoesDesfazer(); // Habilita o botão Desfazer

            verEstoque();
            toggleCard('opcoesCard', false);
        }

        // --- OPERAÇÕES DE REPOSIÇÃO (COMPRA PARA ESTOQUE) ---

        function iniciarReposicaoMultipla() {
            exibirCarrinho('reposicao');
        }

        function prepararReposicaoMultipla() {
            const modalListaItens = document.getElementById('modalListaItensReposicao');
            modalListaItens.innerHTML = '';
            let totalDaReposicao = 0;

            if (Object.keys(itensCarrinho).length === 0) {
                alert("Selecione pelo menos um produto para repor.");
                return;
            }

            for (const id in itensCarrinho) {
                const quantidade = itensCarrinho[id];
                const produto = estoque[id];
                const subtotal = produto.custoReposicao * quantidade;
                totalDaReposicao += subtotal;

                modalListaItens.innerHTML += `
                    <li class="list-group-item d-flex justify-content-between align-items-center">
                        ${produto.nome} (x${quantidade})
                        <span>R$ ${subtotal.toFixed(2)}</span>
                    </li>
                `;
            }

            document.getElementById('modalTotalPagarReposicao').textContent = `R$ ${totalDaReposicao.toFixed(2)}`;
            pagamentoModalReposicao.show();
        }

        function confirmarReposicaoComPagamento(reposicaoItens, formaPagamento) {
            let totalAPagar = 0;
            let resumoReposicao = "Compra para reposição realizada:\n";
            let itensComprados = [];

            for (const id in reposicaoItens) {
                const quantidade = reposicaoItens[id];
                const produto = estoque[id];
                totalAPagar += produto.custoReposicao * quantidade;
            }

            if (formaPagamento === "Dinheiro" && saldo < totalAPagar) {
                alert("Saldo da loja insuficiente para esta compra de reposição em dinheiro.");
                verEstoque();
                toggleCard('opcoesCard', false);
                return;
            }

            const saldoAntes = saldo;

            // Exibir modal de lote/validade para cada item reposto
            let itemIndex = 0;
            function processarLoteItem() {
                if (itemIndex < Object.keys(reposicaoItens).length) {
                    const id = Object.keys(reposicaoItens)[itemIndex];
                    const produto = estoque[id];
                    document.getElementById('loteValidadeModalLabel').textContent = `Lote/Validade para ${produto.nome} (ID: ${id})`;
                    document.getElementById('inputLote').value = '';
                    document.getElementById('inputValidade').value = '';
                    document.getElementById('inputFornecedorId').value = produto.fornecedorId ? (fornecedores[produto.fornecedorId]?.nome || produto.fornecedorId) : '';

                    loteValidadeModal.show();

                    // Adiciona um listener temporário para o botão de confirmação do modal
                    const confirmarBtn = document.getElementById('confirmarLoteValidadeBtn');
                    const oldClickHandler = confirmarBtn.onclick; // Salva o handler antigo
                    confirmarBtn.onclick = function() {
                        const numLote = document.getElementById('inputLote').value;
                        const validade = document.getElementById('inputValidade').value;
                        const fornecedorInput = document.getElementById('inputFornecedorId').value;
                        
                        let fornecedorRealId = null;
                        if (fornecedorInput) {
                            if (!isNaN(fornecedorInput) && fornecedores[parseInt(fornecedorInput)]) {
                                fornecedorRealId = parseInt(fornecedorInput);
                            } else {
                                const foundFornecedor = Object.values(fornecedores).find(f => f.nome.toLowerCase() === fornecedorInput.toLowerCase());
                                if (foundFornecedor) {
                                    fornecedorRealId = Object.keys(fornecedores).find(key => fornecedores[key] === foundFornecedor);
                                }
                            }
                        }
                        produto.fornecedorId = fornecedorRealId;

                        const quantidadeReposta = reposicaoItens[id]; // Quantidade que está sendo reposta agora

                        if (!produto.lotes) produto.lotes = [];
                        // Adiciona o novo lote ou atualiza um existente
                        if (numLote || validade) {
                             const existingLote = produto.lotes.find(l => l.numLote === numLote && l.validade === validade);
                             if (existingLote) {
                                 existingLote.quantidade += quantidadeReposta;
                             } else {
                                 produto.lotes.push({ numLote: numLote, validade: validade, quantidade: quantidadeReposta });
                             }
                        }
                        
                        // Atualiza a quantidade total do produto
                        produto.quantidade += quantidadeReposta;
                        itensComprados.push({ id: parseInt(id), nome: produto.nome, quantidade: quantidadeReposta, custoUnitario: produto.custoReposicao });

                        confirmarBtn.onclick = oldClickHandler; // Restaura o handler antigo
                        loteValidadeModal.hide();
                        itemIndex++;
                        processarLoteItem(); // Processa o próximo item
                    };
                } else {
                    // Todos os itens foram processados, agora finaliza a transação
                    if (formaPagamento === "Dinheiro") {
                        saldo -= totalAPagar;
                        document.getElementById('saldo').value = saldo.toFixed(2);
                    }

                    resumoReposicao += `\nTotal Gasto: R$ ${totalAPagar.toFixed(2)}. Pago com: ${formaPagamento}. Novo Saldo da Loja: R$ ${saldo.toFixed(2)}`;
                    alert(resumoReposicao);

                    ultimaTransacao = {
                        tipo: 'Reposição',
                        data: new Date().toLocaleString('pt-BR'),
                        itens: itensComprados,
                        valorTotal: totalAPagar,
                        formaPagamento: formaPagamento,
                        saldoAntes: saldoAntes,
                        saldoDepois: saldo,
                        usuario: 'Sistema'
                    };
                    historicoTransacoes.unshift(ultimaTransacao);
                    atualizarBotoesDesfazer(); // Habilita o botão Desfazer

                    verEstoque();
                    toggleCard('opcoesCard', false);
                }
            }
            processarLoteItem(); // Inicia o processo de lote/validade para o primeiro item
        }


        // --- ADICIONAR NOVO PRODUTO ---
        async function adicionarProduto() {
            toggleCard('opcoesCard', false);
            toggleCard('historicoCard', false);
            toggleCard('relatoriosCard', false);
            toggleCard('fornecedoresCard', false);
            toggleCard('carrinhoCard', false);

            const nome = prompt("Nome do produto:");
            if (!nome) { alert("Nome do produto é obrigatório."); return; }

            const precoStr = prompt("Preço de Venda unitário do produto (R$):");
            const preco = parseFloat(precoStr);
            if (isNaN(preco) || preco <= 0) { alert("Preço de venda inválido."); return; }

            const custoStr = prompt("Custo de Reposição unitário do produto (R$):");
            const custoReposicao = parseFloat(custoStr);
            if (isNaN(custoReposicao) || custoReposicao <= 0) { alert("Custo de reposição inválido."); return; }

            const quantidadeStr = prompt("Quantidade inicial:");
            const quantidade = parseInt(quantidadeStr);
            if (isNaN(quantidade) || quantidade <= 0) { alert("Quantidade inicial inválida."); return; }

            const idsExistentes = Object.keys(estoque).map(Number);
            const newId = idsExistentes.length > 0 ? Math.max(...idsExistentes) + 1 : 1;

            // Abre o modal de lote/validade para o novo produto
            document.getElementById('loteValidadeModalLabel').textContent = `Lote/Validade para ${nome}`;
            document.getElementById('inputLote').value = '';
            document.getElementById('inputValidade').value = '';
            document.getElementById('inputFornecedorId').value = ''; // Limpa o fornecedor

            loteValidadeModal.show();

            await new Promise(resolve => {
                const confirmarBtn = document.getElementById('confirmarLoteValidadeBtn');
                const oldClickHandler = confirmarBtn.onclick; // Salva o handler antigo
                confirmarBtn.onclick = function() {
                    const numLote = document.getElementById('inputLote').value;
                    const validade = document.getElementById('inputValidade').value;
                    const fornecedorInput = document.getElementById('inputFornecedorId').value;
                    
                    let fornecedorRealId = null;
                    if (fornecedorInput) {
                        if (!isNaN(fornecedorInput) && fornecedores[parseInt(fornecedorInput)]) {
                            fornecedorRealId = parseInt(fornecedorInput);
                        } else {
                            const foundFornecedor = Object.values(fornecedores).find(f => f.nome.toLowerCase() === fornecedorInput.toLowerCase());
                            if (foundFornecedor) {
                                fornecedorRealId = Object.keys(fornecedores).find(key => fornecedores[key] === foundFornecedor);
                            }
                        }
                    }

                    estoque[newId] = {
                        nome,
                        quantidade,
                        preco,
                        custoReposicao,
                        fornecedorId: fornecedorRealId,
                        lotes: []
                    };

                    if (numLote || validade) {
                        estoque[newId].lotes.push({ numLote, validade, quantidade });
                    }

                    confirmarBtn.onclick = oldClickHandler; // Restaura o handler antigo
                    loteValidadeModal.hide();
                    resolve();
                };
            });

            alert(`Produto '${nome}' adicionado ao estoque com ID ${newId}!`);

            ultimaTransacao = {
                tipo: 'Adição de Produto',
                data: new Date().toLocaleString('pt-BR'),
                itens: [{ id: newId, nome: nome, quantidade: quantidade, custoUnitario: custoReposicao }],
                valorTotal: custoReposicao * quantidade,
                formaPagamento: 'N/A',
                saldoAntes: saldo,
                saldoDepois: saldo,
                usuario: 'Sistema'
            };
            historicoTransacoes.unshift(ultimaTransacao);
            atualizarBotoesDesfazer(); // Habilita o botão Desfazer

            verEstoque();
        }

        // --- DESFAZER ÚLTIMA TRANSAÇÃO ---
        function desfazerUltimaTransacao() {
            if (!ultimaTransacao) {
                alert("Não há transações para desfazer.");
                return;
            }

            if (confirm(`Tem certeza que deseja desfazer a última transação (${ultimaTransacao.tipo})?`)) {
                const transacaoDesfeita = historicoTransacoes.shift(); // Remove a última transação do histórico
                ultimaTransacao = historicoTransacoes.length > 0 ? historicoTransacoes[0] : null; // Atualiza a última transação

                const tipo = transacaoDesfeita.tipo;
                const saldoAnterior = transacaoDesfeita.saldoAntes;
                const valorTotal = transacaoDesfeita.valorTotal;

                if (tipo === 'Venda') {
                    // Reverte o saldo e a quantidade no estoque
                    saldo -= valorTotal; // Tira o dinheiro que tinha entrado
                    transacaoDesfeita.itens.forEach(item => {
                        estoque[item.id].quantidade += item.quantidade; // Devolve os itens ao estoque
                        // A reversão de lotes é mais complexa e precisaria de um registro mais detalhado para ser perfeita.
                        // Aqui, simplesmente adicionamos de volta à quantidade total.
                        // Para um sistema real, você registraria os lotes retirados para poder reintroduzi-los.
                    });
                    alert(`Venda desfeita! Saldo revertido para R$ ${saldo.toFixed(2)}. Itens devolvidos ao estoque.`);
                } else if (tipo === 'Reposição') {
                    // Reverte o saldo e a quantidade no estoque
                    if (transacaoDesfeita.formaPagamento === "Dinheiro") {
                        saldo += valorTotal; // Devolve o dinheiro que tinha saído
                    }
                    transacaoDesfeita.itens.forEach(item => {
                        estoque[item.id].quantidade -= item.quantidade; // Retira os itens do estoque
                        // Lotes: Remove a quantidade do lote específico se possível, ou do mais recente.
                        const produto = estoque[item.id];
                        let qtdRemover = item.quantidade;
                        // Remove dos lotes mais recentes (Last In, First Out para desfazer reposição)
                        for (let i = produto.lotes.length - 1; i >= 0 && qtdRemover > 0; i--) {
                            const lote = produto.lotes[i];
                            const qtdRemovidaDoLote = Math.min(qtdRemover, lote.quantidade);
                            lote.quantidade -= qtdRemovidaDoLote;
                            qtdRemover -= qtdRemovidaDoLote;

                             if (lote.quantidade === 0) {
                                produto.lotes.splice(i, 1);
                             }
                        }
                    });
                    alert(`Reposição desfeita! Saldo revertido para R$ ${saldo.toFixed(2)}. Itens removidos do estoque.`);
                } else if (tipo === 'Adição de Produto') {
                    const idProdutoAdicionado = transacaoDesfeita.itens[0].id;
                    delete estoque[idProdutoAdicionado]; // Remove o produto do estoque
                    alert(`Adição do produto ${transacaoDesfeita.itens[0].nome} desfeita!`);
                }

                document.getElementById('saldo').value = saldo.toFixed(2);
                verEstoque(); // Atualiza a visualização do estoque
                atualizarBotoesDesfazer(); // Atualiza o estado do botão
                verHistoricoTransacoes(); // Atualiza o histórico
            }
        }

        function atualizarBotoesDesfazer() {
            const btnDesfazer = document.getElementById('btnDesfazer');
            if (historicoTransacoes.length > 0) {
                btnDesfazer.disabled = false;
                btnDesfazer.textContent = `Desfazer (${historicoTransacoes[0].tipo})`;
            } else {
                btnDesfazer.disabled = true;
                btnDesfazer.textContent = 'Desfazer';
            }
        }

        // --- VISUALIZAÇÃO DO HISTÓRICO ---
        function verHistoricoTransacoes() {
            toggleCard('opcoesCard', false);
            toggleCard('relatoriosCard', false);
            toggleCard('fornecedoresCard', false);
            toggleCard('carrinhoCard', false);
            toggleCard('historicoCard', true);
            const listaHistorico = document.getElementById('listaHistorico');
            listaHistorico.innerHTML = '';

            if (historicoTransacoes.length === 0) {
                listaHistorico.innerHTML = '<li class="list-group-item text-center">Nenhuma transação registrada ainda.</li>';
                return;
            }

            historicoTransacoes.forEach(transacao => {
                let itensHtml = transacao.itens.map(item => {
                    const precoOuCusto = item.precoUnitario ? `R$ ${item.precoUnitario.toFixed(2)}` : (item.custoUnitario ? `R$ ${item.custoUnitario.toFixed(2)}` : '');
                    return `${item.nome} (x${item.quantidade}${precoOuCusto ? ' @ ' + precoOuCusto : ''})`;
                }).join(', ');

                const tipoBadge = transacao.tipo === 'Venda' ? 'bg-warning text-dark' : (transacao.tipo === 'Reposição' ? 'bg-info text-dark' : 'bg-success text-white');
                const valorCor = transacao.tipo === 'Venda' ? 'text-success' : 'text-danger';
                const sinalValor = transacao.tipo === 'Venda' ? '+' : '-';
                const valorDisplay = transacao.valorTotal ? `${sinalValor} R$ ${transacao.valorTotal.toFixed(2)}` : 'N/A';

                listaHistorico.innerHTML += `
                    <li class="list-group-item">
                        <div class="d-flex justify-content-between align-items-center">
                            <div>
                                <span class="badge ${tipoBadge}">${transacao.tipo}</span>
                                <strong>${itensHtml}</strong>
                                <small class="d-block text-muted">Data: ${transacao.data} por ${transacao.usuario || 'Sistema'}</small>
                                <small class="d-block text-muted">Pago com: ${transacao.formaPagamento}</small>
                            </div>
                            <div class="text-end">
                                <span class="${valorCor} fs-5">${valorDisplay}</span>
                                <small class="d-block text-muted">Saldo anterior: R$ ${transacao.saldoAntes.toFixed(2)}</small>
                                <small class="d-block text-muted">Saldo atual: R$ ${transacao.saldoDepois.toFixed(2)}</smal
                            </div>
                        </div>
                    </li>
                `;
            });
        }

        // --- RELATÓRIOS DE VENDAS E LUCRATIVIDADE ---
        function verRelatorios() {
            toggleCard('opcoesCard', false);
            toggleCard('historicoCard', false);
            toggleCard('fornecedoresCard', false);
            toggleCard('carrinhoCard', false);
            toggleCard('relatoriosCard', true);
            document.getElementById('resultadoVendas').innerHTML = '';
            document.getElementById('resultadoLucratividade').innerHTML = '';
        }

        function gerarRelatorioVendas() {
            const dataInicioStr = document.getElementById('dataInicioVendas').value;
            const dataFimStr = document.getElementById('dataFimVendas').value;
            const resultadoVendasDiv = document.getElementById('resultadoVendas');
            resultadoVendasDiv.innerHTML = '';

            if (!dataInicioStr || !dataFimStr) {
                resultadoVendasDiv.innerHTML = '<p class="text-danger">Por favor, selecione as datas de início e fim.</p>';
                return;
            }

            const dataInicio = new Date(dataInicioStr + 'T00:00:00'); // Garante que a hora seja 00:00:00
            const dataFim = new Date(dataFimStr + 'T23:59:59'); // Garante que a hora seja 23:59:59

            let totalVendas = 0;
            let vendasPorProduto = {};

            historicoTransacoes.filter(t => t.tipo === 'Venda').forEach(transacao => {
                // Reverte a data para um formato Date compatível
                const dataPartes = transacao.data.split(' ')[0].split('/');
                const dataFormatada = `${dataPartes[2]}-${dataPartes[1]}-${dataPartes[0]}`;
                const transacaoData = new Date(dataFormatada + 'T' + transacao.data.split(' ')[1]);
                
                if (transacaoData >= dataInicio && transacaoData <= dataFim) {
                    totalVendas += transacao.valorTotal;
                    transacao.itens.forEach(item => {
                        if (!vendasPorProduto[item.nome]) {
                            vendasPorProduto[item.nome] = { quantidade: 0, total: 0 };
                        }
                        vendasPorProduto[item.nome].quantidade += item.quantidade;
                        vendasPorProduto[item.nome].total += (item.precoUnitario * item.quantidade);
                    });
                }
            });

            if (totalVendas === 0) {
                resultadoVendasDiv.innerHTML = '<p>Nenhuma venda encontrada para o período selecionado.</p>';
                return;
            }

            let relatorioHtml = `
                <p><strong>Total de Vendas no Período: R$ ${totalVendas.toFixed(2)}</strong></p>
                <h6>Vendas por Produto:</h6>
                <ul class="list-group">
            `;
            for (const produtoNome in vendasPorProduto) {
                relatorioHtml += `
                    <li class="list-group-item d-flex justify-content-between align-items-center">
                        ${produtoNome}: ${vendasPorProduto[produtoNome].quantidade} unidades
                        <span class="badge bg-primary rounded-pill">R$ ${vendasPorProduto[produtoNome].total.toFixed(2)}</span>
                    </li>
                `;
            }
            relatorioHtml += '</ul>';
            resultadoVendasDiv.innerHTML = relatorioHtml;
        }

        function gerarRelatorioLucratividade() {
            const resultadoLucratividadeDiv = document.getElementById('resultadoLucratividade');
            resultadoLucratividadeDiv.innerHTML = '';

            let lucratividadePorProduto = {}; // { nomeProduto: { receita, custo, lucro } }

            historicoTransacoes.filter(t => t.tipo === 'Venda').forEach(transacao => {
                transacao.itens.forEach(itemVendido => {
                    if (!lucratividadePorProduto[itemVendido.nome]) {
                        lucratividadePorProduto[itemVendido.nome] = { receita: 0, custo: 0, lucro: 0 };
                    }
                    const custoUnitario = estoque[itemVendido.id] ? estoque[itemVendido.id].custoReposicao : 0; // Pega o custo atual
                    lucratividadePorProduto[itemVendido.nome].receita += (itemVendido.precoUnitario * itemVendido.quantidade);
                    lucratividadePorProduto[itemVendido.nome].custo += (custoUnitario * itemVendido.quantidade);
                });
            });

            if (Object.keys(lucratividadePorProduto).length === 0) {
                resultadoLucratividadeDiv.innerHTML = '<p>Nenhuma venda registrada para calcular a lucratividade.</p>';
                return;
            }

            let totalLucroGeral = 0;
            let relatorioHtml = `
                <h6>Lucratividade por Produto Vendido:</h6>
                <ul class="list-group">
            `;
            for (const produtoNome in lucratividadePorProduto) {
                const dados = lucratividadePorProduto[produtoNome];
                dados.lucro = dados.receita - dados.custo;
                totalLucroGeral += dados.lucro;
                const lucroCor = dados.lucro >= 0 ? 'text-success' : 'text-danger';

                relatorioHtml += `
                    <li class="list-group-item">
                        ${produtoNome}: Receita: R$ ${dados.receita.toFixed(2)}, Custo: R$ ${dados.custo.toFixed(2)}, Lucro: <span class="${lucroCor}">R$ ${dados.lucro.toFixed(2)}</span>
                    </li>
                `;
            }
            relatorioHtml += '</ul>';
            relatorioHtml += `<p class="mt-3"><strong>Lucro Total Geral das Vendas: <span class="${totalLucroGeral >= 0 ? 'text-success' : 'text-danger'}">R$ ${totalLucroGeral.toFixed(2)}</span></strong></p>`;
            resultadoLucratividadeDiv.innerHTML = relatorioHtml;
        }

        // --- GERENCIAMENTO DE FORNECEDORES ---
        function gerenciarFornecedores() {
            toggleCard('opcoesCard', false);
            toggleCard('historicoCard', false);
            toggleCard('relatoriosCard', false);
            toggleCard('carrinhoCard', false);
            toggleCard('fornecedoresCard', true);
            renderizarFornecedores();
        }

        function renderizarFornecedores() {
            const listaFornecedores = document.getElementById('listaFornecedores');
            listaFornecedores.innerHTML = '';

            if (Object.keys(fornecedores).length === 0) {
                listaFornecedores.innerHTML = '<li class="list-group-item text-center">Nenhum fornecedor cadastrado.</li>';
                return;
            }

            for (const id in fornecedores) {
                const fornecedor = fornecedores[id];
                listaFornecedores.innerHTML += `
                    <li class="list-group-item d-flex justify-content-between align-items-center">
                        <span>[${id}] ${fornecedor.nome} - Contato: ${fornecedor.contato}</span>
                        <button class="btn btn-sm btn-danger" onclick="excluirFornecedor(${id})">Excluir</button>
                    </li>
                `;
            }
        }

        function adicionarFornecedor() {
            const nome = document.getElementById('nomeFornecedor').value.trim();
            const contato = document.getElementById('contatoFornecedor').value.trim();

            if (!nome) {
                alert("O nome do fornecedor é obrigatório.");
                return;
            }

            fornecedores[nextFornecedorId] = { nome, contato };
            alert(`Fornecedor '${nome}' adicionado com ID ${nextFornecedorId}.`);
            nextFornecedorId++;

            document.getElementById('nomeFornecedor').value = '';
            document.getElementById('contatoFornecedor').value = '';
            renderizarFornecedores();
        }

        function excluirFornecedor(id) {
            if (confirm(`Tem certeza que deseja excluir o fornecedor ID ${id} (${fornecedores[id].nome})?`)) {
                // Verificar se há produtos associados a este fornecedor
                const produtosAssociados = Object.values(estoque).filter(p => p.fornecedorId == id);
                if (produtosAssociados.length > 0) {
                    const confirmacao = confirm(`Existem produtos associados a este fornecedor: ${produtosAssociados.map(p => p.nome).join(', ')}. Deseja desassociá-los e excluir o fornecedor?`);
                    if (!confirmacao) {
                        return;
                    }
                    // Desassociar produtos
                    produtosAssociados.forEach(p => p.fornecedorId = null);
                }

                delete fornecedores[id];
                alert("Fornecedor excluído com sucesso.");
                renderizarFornecedores();
                verEstoque(); // Atualiza o estoque para refletir a remoção do fornecedor
            }
        }
    </script>

</body>
</html>

# Fazzo PDV Lite — Arquitetura

## Para Replicar
Copie a pasta inteira. Edite **apenas** `config.js` (Firebase + nome).

## Estrutura
```
fazzo-lite/
├── config.js              ← ÚNICO ARQUIVO para trocar ao replicar
├── server.js              ← Firebase module (referência, compatível)
├── pdv.html / pdv.css / pdv.js  ← PDV principal
├── caixa.html             ← Controle de caixa (popup lateral)
├── dashboard.html / .css / .js  ← KPIs, charts, rankings, estoque, usuários
├── estoque.html           ← CRUD + entrada/saída + import/export .fazzo
├── gestao.html            ← Cancelar, reimprimir, devolver vendas
├── produto/produto.html   ← Cadastro de produtos (popup lateral)
└── modules/
    ├── modal.js           ← Modal unificado (show/close/confirm/toast)
    ├── sync-manager.js    ← Firebase ↔ localStorage (data/keys + coleções)
    ├── caixa.js           ← Abrir/fechar caixa + bloqueio tela
    ├── cliente.js         ← Busca, seleção, cadastro rápido
    └── nav.js             ← Navegação + PopupLateral
```

## Conexão com Servidor
- Produtos, config, usuarios → `data/keys` (documento único no Firestore)
- Vendas, clientes → coleções individuais no Firestore
- sync-manager.js faz `pullFromServer()` lendo `data/keys` na abertura
- Auto-sync periódico (60s default, configurável em config.js)

## Navegação
- PDV → footer com botões: Caixa, Produto, Estoque, Dashboard, Gestão
- Dashboard, Estoque, Gestão → link "← Voltar ao PDV" no header
- Caixa e Produto → abrem como popup lateral (iframe) dentro do PDV

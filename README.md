<div align="center">

# 💰 QDD × Lei + Créditos

**Comparador de despesa orçamentária** — concilia o Quadro de Detalhamento da Despesa (QDD/SIOF) com a Listagem Lei + Créditos (SPG), calcula o delay entre as duas fontes e gera relatórios para auditoria e gestão.

[![Versão](https://img.shields.io/badge/versão-1.3.1-4f46e5?style=flat-square)](https://github.com/wendellmoura)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/pt-BR/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)
[![Zero Build](https://img.shields.io/badge/build-zero-success?style=flat-square)](#-arquitetura)
[![Client-side](https://img.shields.io/badge/processamento-100%25%20local-16a34a?style=flat-square)](#-privacidade)

[Funcionalidades](#-funcionalidades) · [Como usar](#-como-usar) · [Formatos de entrada](#-formatos-de-entrada) · [Relatórios](#-relatórios) · [Arquitetura](#-arquitetura)

</div>

---

## 📋 Sobre

O **QDD × Lei + Créditos** é uma aplicação web single-file (HTML + CSS + JavaScript) que resolve um problema recorrente na gestão orçamentária: comparar o que está registrado no **SIOF** (via QDD) com o que está na **Lei + Créditos** (via SPG), identificar divergências e gerar relatórios prontos para auditoria e apresentação à gestão.

Toda a análise roda **no navegador** — nenhum arquivo sai do computador do usuário. Não há backend, banco de dados, autenticação ou coleta de telemetria.

> ⚠️ **Projeto independente.** Sem vínculo oficial, endosso ou homologação de qualquer órgão governamental.

---

## ✨ Funcionalidades

### Conciliação e análise

- **Conciliação por dotação** — casamento `QDD.dotacao_id ↔ Listagem.Dotação` (string exata).
- **Classificação em 6 estados:** Sincronizado · Atraso leve (< 1%) · Atraso moderado (1–5%) · Atraso crítico (≥ 5%) · Apenas na Listagem · Apenas no QDD.
- **Métrica Delay** = `(SPG Saldo) − (QDD Saldo)` — principal indicador de divergência.
- **Comparativo por fonte** agregado por grupo macro (Tesouro, Saúde Vinculada, Educação Vinculada, Transferências, RPPS, Extraorçamentários, etc.).
- **Comparativo agregado** total com as três métricas (Lei + Créditos, Empenhado, Saldo) e DNP.

### Escopo automático

Quando o QDD é enviado filtrado por **uma única UO**, o app detecta o escopo e restringe a Listagem às dotações daquela unidade, evitando milhares de falsos "Apenas na Listagem".

Detecção em cascata:

1. **Prefixo = código da UO** — se todas as dotações iniciam com o código da UO (após normalização).
2. **Maior prefixo comum (LCP)** — entre as dotações do QDD.
3. **Entrada manual** — campo para informar o prefixo.

### Decodificação de domínios

| Nível | Exemplo | Descrição |
|---|---|---|
| **Fonte** (3 dígitos) | `500` | Recursos não Vinculados de Impostos |
| **Subfonte** (10 dígitos) | `500.9100100` | Recursos não Vinculados de Impostos — **Contrapartida de Convênios** |
| **Grupo macro** | Tesouro | Alinhado ao "Grupo de Fonte" do SIOF |
| **Região** | Cariri | 15 regiões do Ceará |

Catálogo de fontes e subfontes extraído do SIOF (2026).

### Despesa Não Programada (DNP)

- Lançamento por **dotação** ou por **ação**.
- Sinal: **positivo** = valor suplementado · **negativo** = déficit orçamentário.
- **Persistência automática** em `localStorage`.
- **Backup/restore** via JSON versionado.

### Exportações

| Formato | Escopo | Uso |
|---|---|---|
| **CSV** consolidado | Filtros ativos | Análise em Excel/BI |
| **CSV** por ação | 1 ação | Detalhamento específico |
| **PDF** de ação | 1 ação | Relatório técnico completo |
| **PDF** consolidado | Filtros ativos | Relatório técnico agregado |
| **RLTS** (Relatório Simples) | 1 ação | Apresentação gerencial |
| **Backup JSON** | DNP global | Portabilidade entre máquinas |

### UX

- Busca global (ação, dotação, UO, natureza, fonte, região).
- Chips de filtro por classificação.
- Ordenação por 8 critérios.
- Seletor de colunas visíveis.
- Atalhos de teclado (`↑ ↓ Enter Esc`).
- Drawer lateral com detalhamento por ação.
- Tooltips contextuais em todas as métricas.
- Documentação integrada no modal `?`.

---

## 🚀 Como usar

### Pré-requisitos

- Navegador moderno (Chrome, Edge, Firefox ou Safari — versão dos últimos 2 anos).
- Conexão com a internet na **primeira carga** (SheetJS é carregado via CDN).

### Passo a passo

1. **Clone o repositório** ou baixe o `index.html`:

   ```bash
   git clone https://github.com/wendellmoura/<repo>.git
   cd <repo>

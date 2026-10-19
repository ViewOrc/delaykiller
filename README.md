<div align="center">

# 💰 QDD × Lei + Créditos

**Comparador de despesa orçamentária** — concilia o Quadro de Detalhamento da Despesa (QDD/SIOF) com a Listagem Lei + Créditos (SPG), evidencia diferenças entre as fontes e apoia o acompanhamento da execução orçamentária, com controles de Despesa Não Programada, Gasto Pretendido e projeção para o encerramento do exercício.

[![Versão](https://img.shields.io/badge/versão-1.6.0-4f46e5?style=flat-square)](https://github.com/wendellmoura)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/pt-BR/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)
[![Zero Build](https://img.shields.io/badge/build-zero-success?style=flat-square)](#-arquitetura)
[![Client-side](https://img.shields.io/badge/processamento-local-16a34a?style=flat-square)](#-privacidade)

[Funcionalidades](#-funcionalidades) · [Como usar](#-como-usar) · [Entradas](#-formatos-de-entrada) · [Indicadores](#-indicadores-e-cálculos) · [Exportações](#-exportações) · [Arquitetura](#-arquitetura)

</div>

---

## 📋 Sobre

O **QDD × Lei + Créditos** é uma aplicação web independente, distribuída em um único arquivo HTML, para comparar os dados do **Quadro de Detalhamento da Despesa (QDD), obtido no SIOF**, com a **Listagem Lei + Créditos, obtida no SPG**.

A aplicação cruza as dotações, compara os valores de Lei + Créditos, Empenhado e Saldo, classifica divergências e disponibiliza indicadores para análise por ação, dotação, unidade orçamentária e grupo de fonte. Também permite registrar valores de **Despesa Não Programada (DNP)** e **Gasto Pretendido (GP)**, calcular uma projeção de encerramento do exercício e exportar os resultados para Excel ou CSV.

> ⚠️ **Projeto independente.** Não possui vínculo oficial, endosso ou homologação de órgão governamental. Os resultados dependem da consistência, da data e do escopo dos arquivos fornecidos; devem ser conferidos antes de embasar decisões administrativas.

---

## ✨ Funcionalidades

### Conciliação e classificação

- **Conciliação por dotação:** relaciona `QDD.dotacao_id` com `Listagem.Dotação`, utilizando a identificação normalizada prevista pela aplicação.
- **Seis classificações:** Sincronizado, Atraso leve, Atraso moderado, Atraso crítico, Apenas na Listagem e Apenas no QDD.
- **Comparação de três métricas:** Lei + Créditos, Empenhado e Saldo, com valores do QDD, da Listagem e suas diferenças.
- **Indicador Delay:** evidencia a diferença entre os saldos das duas fontes.
- **Indicadores agregados:** totais, ações divergentes e quantidade de divergências críticas.
- **Comparativo por grupo macro de fonte:** consolida diferenças por agrupamentos de fontes orçamentárias.

### Escopo automático por Unidade Orçamentária

Quando o QDD contém dados de uma única UO, a aplicação pode restringir a comparação às dotações daquela unidade, reduzindo falsos registros de “Apenas na Listagem”. O escopo detectado é apresentado na interface e pode ser ajustado conforme as opções disponíveis.

### Fonte, subfonte e região

A aplicação decodifica os códigos reconhecidos pelo catálogo incorporado ao arquivo, exibindo informações como:

- Código e descrição da fonte;
- Subfonte;
- Grupo macro da fonte;
- Região de planejamento, quando identificada.

O catálogo incorporado é baseado em informações do SIOF de 2026. A identificação depende dos códigos presentes nos dados e da cobertura desse catálogo.

### Despesa Não Programada (DNP)

- Registro por **dotação** ou por **ação**;
- Valor positivo representa suplemento; valor negativo representa déficit orçamentário;
- Edição diretamente na tabela ou no painel de detalhamento da ação;
- Consolidação dos registros nos indicadores e nos cálculos de projeção.

### Gasto Pretendido (GP) e projeção

- Registro do gasto total pretendido até 31 de dezembro;
- Valor padrão calculado a partir da autorização do QDD, descontando o saldo das dotações marcadas como não utilizadas;
- Identificação das dotações não utilizadas;
- Projeção recalculada conforme os valores de DNP e GP;
- Indicador agregado da projeção para acompanhamento da meta de encerramento.

### Pesquisa, filtros e navegação

- Pesquisa global por ação, dotação, UO, natureza da despesa, fonte e região;
- Filtros por classificação;
- Ordenação por diferentes critérios;
- Seleção de colunas visíveis;
- Painel lateral com detalhamento da ação e das dotações;
- Edição de valores nas células compatíveis;
- Tooltips explicativos para indicadores e métricas;
- Documentação integrada à interface;
- Atalhos de teclado para navegação e fechamento de painéis.

---

## 🚀 Como usar

### Pré-requisitos

- Navegador moderno: Chrome, Edge, Firefox ou Safari;
- Conexão com a internet para carregar as bibliotecas JavaScript utilizadas na leitura e exportação de arquivos;
- Arquivo QDD exportado do SIOF;
- Arquivo CSV da Listagem Lei + Créditos do SPG.

### 1. Obter o QDD no SIOF

A extração é manual:

1. Abra o [SIOF — Consulta de Execução](https://planejamento.seplag.ce.gov.br/siofconsulta/Paginas/frm_consulta_execucao.aspx).
2. Aplique os filtros desejados de ano, mês, secretaria, órgão e Unidade Orçamentária.
3. Escolha um relatório que apresente dotação e natureza da despesa por linha.
4. Em **Tipo de Exibição**, selecione **Planilha Formatada (XLS)**.
5. Clique em **Visualizar** e baixe o arquivo.
6. Na aplicação, envie o arquivo na área **QDD**.

### 2. Obter a Listagem Lei + Créditos

Exporte a Listagem do SPG em formato CSV, observando o período e o escopo que serão comparados com o QDD. Envie o arquivo na área **Listagem**.

### 3. Analisar os resultados

Após carregar os dois arquivos, a aplicação processa os dados e apresenta os indicadores e a tabela de conciliação. Use a pesquisa, os filtros e a ordenação para localizar divergências. Se necessário, abra uma ação para examinar as dotações, revisar DNP, ajustar Gasto Pretendido e consultar os comparativos.

### 4. Registrar e preservar os ajustes

Os valores de DNP, GP e as marcações de dotações não utilizadas são salvos automaticamente no armazenamento local do navegador. Use a função de backup para exportar os dados em JSON antes de trocar de computador, limpar os dados do navegador ou realizar operações que possam apagar o armazenamento local.

---

## 📄 Formatos de entrada

| Arquivo | Formatos aceitos | Origem / finalidade |
|---|---|---|
| QDD | `.xls`, `.xlsx` | Quadro de Detalhamento da Despesa exportado do SIOF |
| Listagem | `.csv` | Dados de Lei + Créditos do SPG |
| Backup | `.json` | Importação e restauração dos registros locais de DNP, GP e dotações não utilizadas |

Os arquivos precisam conter colunas e identificadores compatíveis com a estrutura esperada pela aplicação. A comparação só é confiável quando os arquivos correspondem a escopos e períodos coerentes.

---

## 📐 Indicadores e cálculos

### Delay

O Delay de saldo representa a diferença entre o saldo da Listagem e o saldo do QDD:

```text
Delay = Saldo SPG − Saldo QDD
```

Conforme os conceitos utilizados pela aplicação:

```text
Saldo QDD = Autorizada QDD − Empenhado QDD
Saldo SPG = Lei + Créditos − Parcelas
```

Valor positivo indica que o saldo da Listagem é superior ao saldo calculado a partir do QDD; valor negativo indica o contrário. O Delay é um indicador de diferença entre fontes, não uma comprovação isolada de erro ou de atraso administrativo.

### Classificação da divergência

| Classificação | Critério apresentado pela aplicação |
|---|---|
| **Sincronizado** | Os valores comparados coincidem |
| **Atraso leve** | Divergência inferior a 1% |
| **Atraso moderado** | Divergência entre 1% e 5% |
| **Atraso crítico** | Divergência igual ou superior a 5% |
| **Apenas na Listagem** | Dotação encontrada somente na Listagem |
| **Apenas no QDD** | Dotação encontrada somente no QDD |

Os percentuais são critérios de classificação da ferramenta. Para interpretar um caso concreto, confira os valores de origem, o escopo e a regra aplicada ao registro.

### Despesa Não Programada (DNP)

- **DNP positiva:** valor adicional a considerar como suplemento;
- **DNP negativa:** valor a considerar como déficit orçamentário.

A DNP pode ser registrada por dotação ou por ação e integra a projeção.

### Gasto Pretendido (GP) e projeção

O Gasto Pretendido representa a despesa total que se pretende empenhar até 31 de dezembro. Por padrão, a aplicação calcula esse valor a partir da autorização do QDD, descontando o saldo das dotações marcadas como não utilizadas.

```text
Projeção = Autorizada QDD + DNP − Gasto Pretendido
```

A meta de referência é **R$ 0,00** ao final do exercício. A projeção é uma estimativa baseada nos valores informados e não uma previsão garantida da execução.

---

## 📤 Exportações

| Exportação | Conteúdo / finalidade |
|---|---|
| **Excel completo** | Ações incluídas na visualização filtrada, consolidadas em uma planilha |
| **Excel desta ação** | Relatório detalhado da ação aberta, com indicadores, comparativos por fonte, dotações e legenda |
| **RLTS (Excel)** | Relatório simples, mais enxuto, com foco no Delay total |
| **CSV desta ação** | Dados da ação, com uma linha por dotação |
| **Backup JSON** | Registros locais de DNP, Gasto Pretendido e dotações não utilizadas para portabilidade e restauração |

As exportações de análise respeitam o escopo correspondente à opção selecionada. O Excel completo considera os filtros ativos; o relatório por ação se limita à ação aberta.

---

## 🔐 Privacidade

- O processamento dos arquivos ocorre no navegador;
- A aplicação não possui backend próprio, banco de dados remoto, autenticação ou mecanismo de telemetria implementado no arquivo;
- Os arquivos selecionados são lidos localmente para análise e não são enviados a um servidor da aplicação;
- Os registros editáveis são persistidos no `localStorage` do navegador;
- As bibliotecas de terceiros são carregadas por CDN, portanto a primeira utilização exige conexão com a internet.

**Atenção:** `localStorage` é específico do navegador e do perfil utilizado. Ele não substitui um backup. Em computadores compartilhados, considere quem tem acesso ao mesmo perfil do navegador.

---

## 🧱 Arquitetura

- **Aplicação:** arquivo único `HTML`, com CSS e JavaScript integrados;
- **Execução:** client-side, sem servidor de aplicação;
- **Leitura de planilhas e CSV:** SheetJS (`xlsx`), carregado via CDN;
- **Geração de arquivos Excel:** ExcelJS, carregado via CDN;
- **Persistência local:** `localStorage`;
- **Backup e restauração:** JSON;
- **Build:** não exige etapa de compilação ou instalação de dependências locais.

A aplicação pode ser executada abrindo o arquivo HTML em um navegador moderno, desde que as bibliotecas externas estejam acessíveis.

---

## ⚠️ Limitações e responsabilidade de uso

- A aplicação não extrai automaticamente o QDD do SIOF: o download é manual.
- A ferramenta não substitui os sistemas oficiais nem valida, por conta própria, a correção dos lançamentos orçamentários.
- Diferenças podem decorrer de datas de extração, filtros, escopos, critérios de cálculo ou atualizações entre as fontes.
- O resultado deve ser interpretado à luz dos arquivos efetivamente carregados e conferido nos sistemas de origem antes de uso em auditoria, prestação de contas ou decisão administrativa.
- A persistência local pode ser perdida se os dados do navegador forem apagados; mantenha backups quando os ajustes forem relevantes.

---

## 📌 Versão

**Versão atual do arquivo:** `1.6.0`

Consulte o código-fonte e as demais informações do projeto no [GitHub de Wendell Moura](https://github.com/wendellmoura?tab=repositories).

---

<div align="center">

**QDD × Lei + Créditos** · Conciliação orçamentária, análise de divergências e projeção de encerramento.

</div>

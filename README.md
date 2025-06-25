# 📊 Análise de Risco de Crédito com Modelagem Preditiva

Este projeto tem como objetivo desenvolver um pipeline de ciência de dados para prever inadimplência de clientes com base em informações comportamentais e financeiras. A modelagem utiliza dados reais disponibilizados em uma competição pública da plataforma Kaggle.

---

## 📁 Estrutura do Projeto

```bash
risco_de_credito/
├── data/
│   ├── 1_raw/            # Dados brutos (Kaggle)
│   ├── 2_trusted/        # Dados tratados (ETL)
│   └── 3_refined/        # Base final para modelagem + dicionario de dados
├── relatorio_executivo/  # Relatório de achados e sugestões de ação
└── notebook.ipynb        # Notebook principal da análise
```

---

## 🔍 Etapas Desenvolvidas

### 1. Extração e Carga
Foram utilizados 3 arquivos principais da base original (cerca de 3GB), selecionados para garantir simplicidade e interpretabilidade:

- `train_base.csv`
- `train_static_0_0.csv`
- `train_static_cb_0.csv`

Esses arquivos foram integrados via `case_id` e processados até gerar a base `refined.csv`.

### 2. Transformação e Pré-processamento
- Remoção de colunas com baixa completude ou variância nula
- Conversão de datas, codificação de categorias e tratamento de outliers
- Aplicação de `log1p` em variáveis com caudas longas
- Seleção de variáveis numéricas mais correlacionadas com a inadimplência

### 3. Análise Exploratória (EDA)
- Análise da distribuição do target (`inadimplente`: ~3%)
- Estudo de correlação entre variáveis numéricas e categóricas com `target`
- Diagnóstico de completude e tipos de variáveis

### 4. Modelagem Preditiva
Modelos treinados com validação hold-out:
- **Regressão Logística** (baseline): AUC ≈ 0.70
- **LightGBM** (modelo principal): AUC ≈ 0.73 | Recall da classe 1 ≈ 62%

### 5. Interpretação e Insights
As variáveis mais importantes se relacionam com:
- Atrasos recentes em parcelas
- Frequência de rejeições de crédito
- Tipo de transação inicial e origem do crédito

---

## ✅ Resultados

- AUC: **0.7304**
- Modelo com boa capacidade de identificar inadimplentes, mesmo com dataset desbalanceado
- Conjunto `refined` com variáveis transformadas e prontas para aplicação + dicionario de dados

---

## 🧠 Relatório Executivo

- [Relatório Executivo](/relatorio_executivo/teste.txt) com achados e sugestões de ações

---

## 📌 Requisitos

- Python 3.8+
- Bibliotecas:
  - pandas, numpy, matplotlib, seaborn
  - scikit-learn, lightgbm

Para instalar todas:

```bash
pip install -r requirements.txt
```

---

## 🤖 Próximos Passos

- Ajuste de hiperparâmetros e tuning
- Uso de técnicas de balanceamento supervisionado (SMOTE, etc.)
- Avaliação com outras métricas de negócio (ex: custo real da inadimplência)

---

## 👨‍💻 Autor

Felipe Reis • [LinkedIn](https://www.linkedin.com/in/felipecsr) • Contato: felipecsr@gmail.com

> Projeto com fins educacionais. Inspirado em desafios reais de risco de crédito.

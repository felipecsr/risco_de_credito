# 📊 Análise de Risco de Crédito com Modelagem Preditiva

Este projeto tem como objetivo desenvolver um pipeline de ciência de dados para prever inadimplência de clientes com base em informações comportamentais e financeiras. A modelagem utiliza dados reais disponibilizados em uma competição pública da plataforma Kaggle.

---

## 📁 Estrutura do Projeto

```bash
risco_de_credito/
├── data/
│   ├── 1_raw/            # Dados brutos (Kaggle)
│   ├── 2_trusted/        # Dados tratados (vazios e tipos)
│   └── 3_refined/        # Base final para modelagem + dicionario de dados
├── notebook/             # Notebook principal da análise
└── relatorio_executivo/  # Relatório executivo com relato de etapas e achados
 
```

---

##  🔗 Dados do projeto

- Dados obtidos da [competição pública do Kaggle](https://www.kaggle.com/competitions/home-credit-credit-risk-model-stability)


```bash
kaggle competitions download -c home-credit-credit-risk-model-stability
```

> Comando para terminal, após criação da conta na plataforma e solicitação de API key (json local)

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
- Análise da distribuição do target (`inadimplente`: ~3%) (forte desbalanceamento)
- Diagnóstico de completude e tipos de variáveis
- Estudo de correlação entre variáveis numéricas e categóricas com `target`


### 4. Modelagem Preditiva
Modelos treinados com validação hold-out:
- **Regressão Logística** (baseline): AUC ≈ 0.70
- **LightGBM** (modelo principal): AUC ≈ 0.73
> O modelo LightGBM identificou cerca de 62% dos inadimplentes (recall da classe 1), mesmo em um cenário com forte desbalanceamento.

### 5. Interpretação e Insights
As variáveis mais importantes se relacionam com:
- Atrasos recentes em parcelas
- Frequência de rejeições de crédito
- Tipo de transação inicial e origem do crédito

---

## ✅ Resultados

- AUC: **0.7304** | F1-score: **0.12**
- O modelo demonstrou boa capacidade de distinguir inadimplentes, mesmo com forte desbalanceamento de classes.
- A base refined.csv contém variáveis tratadas e selecionadas, acompanhada de um dicionário de dados para referência.

---

## 🧠 Relatório Executivo

- [Relatório Executivo](/relatorio_executivo/relatorio_executivo.pdf) com etapas do projeto e achados.

---

## 📌 Requisitos

- Python (pandas, numpy, matplotlib, seaborn, scikit-learn, lightgbm)
- Jupyter Notebook

```bash
pip install -r requirements.txt
```

---

## 🤖 Próximos Passos

- Ajuste de hiperparâmetros e tuning
- Uso de técnicas de balanceamento supervisionado (SMOTE, etc.)
- Avaliação com outras métricas de negócio (ex: custo real da inadimplência)
- Adição, cruzamento e verificação de correlação de outras variáveis disponíveis em `raw data` 

---

## 👨‍💻 Autor

Felipe Reis • [LinkedIn](https://www.linkedin.com/in/felipecsr) • Contato: felipecsr@gmail.com

> *Projeto com fins educacionais. Inspirado em desafios reais de risco de crédito.*

---

## 📄 Licença

Este projeto está licenciado sob os termos da **[GNU General Public License v3.0 (GPL-3.0)](https://www.gnu.org/licenses/gpl-3.0.html)**.  
Você é livre para usar, modificar e distribuir este código, desde que mantenha a mesma licença e os créditos de autoria.

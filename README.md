# Mitigação de Vieses em Modelos de Machine Learning: Evasão Escolar

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white) ![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white) ![UFF](https://img.shields.io/badge/UFF-MESC-blue)

Este projeto foi desenvolvido como parte da disciplina de **Inteligência Artificial** do Mestrado em Engenharia de Sistemas e Computação (MESC) da **Universidade Federal Fluminense (UFF)**.

O objetivo principal é treinar um modelo de redes neurais para prever a evasão escolar e aplicar técnicas de **Fairness (Equidade)** para identificar e mitigar vieses algorítmicos relacionados a atributos sensíveis, como raça e nível socioeconômico, utilizando a biblioteca **AIF360** e a técnica de **Adversarial Debiasing**.

## 👥 Integrantes
*   Matheus Monclai
*   Guilherme Barrucho
*   **Professor:** Dr. Leonard Barreto Moreira

---

## 📖 Contexto e Dados

A base de dados utilizada é um dataset sintético de **Evasão Escolar**, obtido no [Kaggle](https://www.kaggle.com/datasets/danilonaves/evaso-escolar-sintetico). Ela contém 1000 registros de alunos com 37 colunas, incluindo:
*   **Atributos Sensíveis:** Sexo, Raça/Cor, Nível Socioeconômico.
*   **Atributos Acadêmicos:** Notas médias, Frequência escolar, Repetência.
*   **Target:** `evasao_confirmada` (Sim/Não).

---

## 🛠️ Tecnologias Utilizadas

*   **Linguagem:** Python
*   **Manipulação e Viz:** Pandas, Numpy, Seaborn, Matplotlib.
*   **Machine Learning:** Scikit-Learn, Imbalanced-learn (SMOTE).
*   **Deep Learning:** TensorFlow/Keras.
*   **Fairness/Equidade:** [AI Fairness 360 (AIF360)](https://aif360.mybluemix.net/).
*   **Explicabilidade:** SHAP (SHapley Additive exPlanations).

---

## 🚀 Fluxo de Trabalho

1.  **Análise Exploratória (EDA):** Identificação de correlações (Frequência e Notas são os maiores preditores) e desbalanceamento de classes (70% não evadidos / 30% evadidos).
2.  **Pré-processamento:** Tratamento de variáveis categóricas com One-Hot Encoding e normalização com StandardScaler.
3.  **Balanceamento:** Aplicação de **SMOTE** no conjunto de treino para equalizar as classes.
4.  **Modelo Baseline:** Construção de uma Rede Neural Multicamadas (MLP) com Dropout e Regularização L2.
5.  **Auditoria de Viés:** Implementação de um relatório automatizado para calcular o **Recall por subgrupo**. Identificou-se que alunos de raça Indígena e nível socioeconômico N6 possuíam recall significativamente menor que a média global.
6.  **Mitigação (Adversarial Debiasing):** Uso de uma rede adversária para remover informações sobre o atributo sensível (`raca_cor_Indigena`) das representações latentes do classificador.
7.  **Interpretabilidade:** Uso de **SHAP Values** para entender como o modelo toma decisões antes e depois da mitigação.

---

## 📊 Principais Resultados

*   **Frequência Escolar:** Identificada como o fator de maior impacto na retenção do aluno.
*   **Recall Global:** O modelo baseline atingiu cerca de 0.47 de recall para a classe de evasão, mas com disparidades gritantes entre grupos.
*   **Adversarial Debiasing:** O modelo mitigado buscou equilibrar as métricas de equidade (*Statistical Parity Difference* e *Disparate Impact*). O SHAP revelou que, mesmo com a mitigação, atributos sensíveis com pouquíssima representação (como a raça Indígena) ainda oferecem desafios para a rede adversária.

---

## ⚙️ Como Executar

1.  Clone o repositório:
    ```bash
    git clone https://github.com/seu-usuario/evasao-escolar-bias-mitigation.git
    ```
2.  Instale as dependências:
    ```bash
    pip install aif360 tensorflow shap scikit-learn pandas matplotlib seaborn imblearn
    ```
3.  Abra o notebook `evasão_escolar.ipynb` no Jupyter ou Google Colab.
4.  Certifique-se de carregar o arquivo `dataset_evasao_sintetico.csv` no mesmo diretório.

---

## ⚖️ Licença

Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

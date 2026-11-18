# 📦 Supply Chain Analytics: Previsão de Riscos e Atrasos Logísticos

## 🎯 1. Visão Geral do Projeto
Este projeto de **Data Mining e Machine Learning** tem como objetivo analisar a cadeia de suprimentos da base **DataCo Smart Supply Chain**, aplicando técnicas estatísticas e preditivas em Python para antecipar riscos de atrasos em entregas e otimizar processos logísticos e operacionais.

---

## 🛠️ 2. Stack Tecnológica
* **Linguagem:** Python 3
* **Ambiente:** Google Colab / Jupyter Notebook
* **Bibliotecas Principais:** `pandas`, `NumPy`, `scikit-learn`, `Matplotlib`, `Seaborn`, `mlxtend`
* **Visualização de Resultados:** Microsoft Power BI

---

## 📈 3. Ingestão e Inspeção Inicial dos Dados
A base de dados utilizada contém **180.519 registros e 53 variáveis** estruturadas cobrindo transações comerciais, datas de envio real vs agendado e status de entrega.

![Ingestão de Dados](images/01_ingestao_dados.png)

---

## 📊 4. Análise Exploratória de Dados (EDA)

A análise da variável alvo (`Late_delivery_risk`) revelou um cenário crítico de ineficiência operacional na cadeia de suprimentos:

* **Desequilíbrio Operacional:** **54,83%** dos pedidos (98.977 registros) apresentam risco real de atraso, contra **45,17%** (81.542 registros) entregues dentro do prazo.
* **Gargalo nos Fretes Expressos:** Ao cruzar o risco com a modalidade de envio (`Shipping Mode`), identificou-se que a categoria **First Class** concentra uma taxa de risco de **95,32%**, evidenciando falhas severas no cumprimento de SLAs prioritários. Em contrapartida, a modalidade **Standard Class** apresenta a maior previsibilidade, com **61,93%** das entregas sem risco.

![Análise Exploratória - Risco de Atraso](images/02_eda_risco_atraso.png)

---

## 🧹 5. Limpeza de Dados e Engenharia de Features

Para garantir a integridade estatística do modelo preditivo e evitar *Data Leakage* (vazamento de informações futuras que não existem no momento do despacho), a base passou por um rigoroso processo de higienização, reduzindo a dimensionalidade de **53 para 28 variáveis** sem perda de registros (180.519 linhas mantidas e 0 valores nulos):

* **Prevenção de Data Leakage:** Remoção de variáveis conhecidas apenas após o envio ou entrega (`Days for shipping (real)`, `Delivery Status`, `Order Status`, `shipping date`).
* **Tratamento de Nulos e Privacidade (LGPD):** Descarte de colunas inviáveis (`Product Description` com 100% de nulos e `Order Zipcode` com 86,2% de nulos) e remoção de dados pessoais sensíveis (e-mails, senhas, endereços exatos) e identificadores únicos (IDs).
* **Eliminação de Redundâncias:** Remoção de colunas financeiras espelhadas para evitar multicolinearidade.
* **Engenharia de Features Temporais:** Extração de `Order_Month` (mês), `Order_DayOfWeek` (dia da semana) e `Order_Hour` (hora do pedido) a partir do timestamp original para capturar gargalos operacionais de virada de turno e fins de semana.
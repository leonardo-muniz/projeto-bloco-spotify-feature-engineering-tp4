# Teste de Performance 4: Feature Engineering com K-Means para Otimizar Classificadores

Este repositório documenta o quarto Teste de Performance (TP) do bloco de Machine Learning. O projeto explora uma técnica avançada de engenharia de features, utilizando o algoritmo de clusterização não supervisionado K-Médias para criar uma nova feature e melhorar o desempenho de modelos de classificação supervisionados (SVM e Random Forest).

### Objetivo

O objetivo central deste projeto é investigar se a adição de uma feature baseada na estrutura de clusters dos dados (distância ao centroide) pode aumentar a performance preditiva de modelos de classificação em um dataset de músicas do Spotify.

### Base de Dados

O dataset utilizado é o **"Spotify Tracks Dataset"**, disponível no Kaggle.
* **Contexto:** Contém mais de 100.000 músicas com diversos atributos de áudio calculados pelo Spotify, como `danceability`, `energy`, `acousticness`, `liveness`, etc.
* **Tarefa de Classificação:** Para este projeto, o desafio foi construir um modelo de classificação binária para prever o gênero de uma música, distinguindo entre as categorias "Pop" e "Classical" com base em seus atributos de áudio.
* **Fonte:** O dataset pode ser encontrado no [Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset/data).

### Metodologia e Etapas

O projeto foi estruturado como um experimento comparativo, seguindo as etapas abaixo:

1.  **Análise e Preparação dos Dados:**
    * Carregamento do dataset e seleção dos atributos numéricos relevantes.
    * Análise exploratória para entender a distribuição dos dados.
    * Padronização das features (`StandardScaler`) para prepará-las para os algoritmos de K-Médias e SVM.

2.  **Clusterização com K-Médias (Aprendizado Não Supervisionado):**
    * Aplicação do algoritmo K-Médias para identificar agrupamentos naturais (clusters) entre as músicas.
    * Utilização do **Método do Cotovelo (Elbow Method)** e do **Índice de Silhueta (Silhouette Score)** para determinar o número ótimo de clusters (*k*).

3.  **Engenharia de Features via Clusterização:**
    * Criação de uma nova feature chamada `distancia_cluster`.
    * Para cada música no dataset, foi calculada a sua distância euclidiana ao centroide do cluster ao qual ela pertence. Essa distância foi adicionada como uma nova coluna, enriquecendo o conjunto de dados.

4.  **Treinamento e Avaliação Comparativa dos Modelos:**
    Foram treinados e avaliados dois conjuntos de modelos para comparar os resultados:
    * **Cenário 1 (Baseline):** Modelos SVM (com kernels `linear`, `poly`, `rbf`) e Random Forest treinados **apenas com as features originais**.
    * **Cenário 2 (Com Feature de Cluster):** Os mesmos modelos treinados com as **features originais + a nova feature `distancia_cluster`**.
    * A otimização de hiperparâmetros foi considerada em ambos os cenários.

5.  **Resultados e Análise Comparativa:**
    * A performance de todos os modelos foi medida com métricas como Acurácia, Precisão, Recall, F1-Score e AUC-ROC.
    * Foi realizada uma análise comparativa, com o auxílio de gráficos, para determinar se a adição da feature de clusterização resultou em uma melhoria estatisticamente significativa no desempenho dos classificadores.

# Exercícios de comparação de modelos de predição

## Problema 1 — compra de produto

Utilize a base `dados_predicao_modelos.csv`, incluída nesta pasta.

Variáveis de entrada:

- `Idade`;
- `Renda_Anual_K`;
- `Score_Credito`;
- `Pontuacao_Engajamento`.

Variável alvo: `Compro_Produto`, em que 0 representa não comprou e 1 representa
comprou.

## Problema 2 — risco de internação

Utilize a base `dados_saude_predicao.csv`, incluída nesta pasta.

## Execução

Todos os arquivos necessários estão nesta pasta. Para preparar um ambiente local,
execute:

```bash
python -m pip install -r requirements.txt
jupyter lab
```

Depois, abra `solucao_exercicios.ipynb` e execute as células em ordem. Não é
necessário clonar ou acessar o restante do repositório.

Variáveis de entrada:

- `Idade`;
- `Pressao_Arterial`;
- `Colesterol_Total`;
- `Frequencia_Cardiaca_Max`.

Variável alvo: `Risco_Internacao`, em que 0 representa baixo risco/sem internação
e 1 representa alto risco/necessidade de internação.

## Atividades

Para cada problema:

1. Treinar e comparar Regressão Logística, Árvore de Decisão, Random Forest,
   KNN, Naive Bayes, SVM e Gradient Boosting.
2. Analisar as matrizes de confusão.
3. Calcular, explicar e comparar acurácia e F1-Score.
4. Comparar desempenho de treino e teste e usar validação cruzada para investigar
   overfitting.
5. Justificar se os dados foram adequados para o treinamento e se algum modelo
   poderia ser utilizado em produção.

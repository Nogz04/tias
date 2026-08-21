# TIAS - Semana 4

## DecisionTreeClassifier - Scikit-learn (sklearn).

> O DecisionTreeClassifier é um algoritmo de Machine Learning para classificação disponível no scikit-learn (sklearn). Ele implementa uma Árvore de Decisão (Decision Tree).
>
> Ele trabalha digamos que usando uma sequência de perguntas: Imagine que queremos classificar se uma pessoa possui alto ou baixo risco de uma doença, usando algumas informações:

  ```txt
    Idade
    Pressão arterial
    Glicose
    Colesterol
  ```

> A árvore aprende regras parecidas como:

```txt
                 Glicose > 125?
                  /          \
               SIM            NÃO
                |              |
          Idade > 60?      Baixo risco
           /      \
         SIM      NÃO
          |         |
      Alto risco  Pressão alta?
                   /       \
                 SIM       NÃO
                  |         |
              Alto risco  Baixo risco
```

> O importante é que o usuário não escreve essas regras manualmente. O algoritmo analisa os dados de treinamento e aprende quais perguntas/divisões são mais úteis para separar as classes.
>
> **Exemplo usando Sklearn:**

```python
from sklearn.tree import DecisionTreeClassifier

modelo = DecisionTreeClassifier()

modelo.fit(X_treino, y_treino)

resultado = modelo.predict(X_teste)
```

> -> **DecisionTreeClassifier()** → cria o modelo de árvore de decisão.
> 
> -> **.fit()** → treina a árvore usando exemplos conhecidos.
> 
> -> **.predict()** → utiliza o que foi aprendido para classificar novos dados.

## Pipeline de Machine Learning aplicado aos dados de glicose do repositório do zamberlan 

> Tecnicamente nesse código é usado os dois primeiros princípios de ETL:

```txt
EXTRACT (E)
   ↓
pd.read_csv(url)
   ↓
Extrai/carrega os dados do CSV

==============================

TRANSFORM (T)
   ↓
Seleciona features
Separa X e y
train_test_split()
StandardScaler()
   ↓
Prepara e transforma os dados

==============================

LOAD
   ↓
Não foi aplicado:

-> O Load clássico não aparece claramente. Em um ETL tradicional, os dados transformados seriam carregados em algum destino,
por exemplo: df_transformado.to_sql(...) ou df_transformado.to_csv(...)


```

```python
# ============================================================
# COMPARAÇÃO ENTRE MODELOS DE CLASSIFICAÇÃO - BASE DE GLICOSE
# ============================================================

# pandas:
# Biblioteca usada para ler, organizar e manipular dados em formato de tabela.
# Aqui será usada principalmente para carregar o arquivo CSV.
import pandas as pd


# train_test_split:
# Divide a base de dados em duas partes:
# - dados para TREINAMENTO do modelo
# - dados para TESTE do modelo
from sklearn.model_selection import train_test_split


# StandardScaler:
# Padroniza os valores das variáveis para uma escala semelhante.
#
# Exemplo:
# KCAL pode ter valores como 2000
# SONO pode ter valores como 8
#
# Essa diferença de escala pode prejudicar alguns algoritmos,
# principalmente KNN e SVM.
from sklearn.preprocessing import StandardScaler


# Métricas usadas para verificar o desempenho dos modelos:
from sklearn.metrics import (
    accuracy_score,        # calcula a porcentagem geral de acertos
    classification_report, # mostra precision, recall, F1-score e support
    confusion_matrix,      # mostra os acertos e erros entre cada classe
    f1_score               # calcula o equilíbrio entre precision e recall
)


# ============================================================
# MODELOS DE MACHINE LEARNING
# ============================================================

# Regressão Logística:
# modelo de classificação baseado em probabilidades.
from sklearn.linear_model import LogisticRegression


# Árvore de Decisão:
# cria uma sequência de regras/perguntas para separar as classes.
from sklearn.tree import DecisionTreeClassifier


# Random Forest:
# utiliza várias árvores de decisão e combina seus resultados.
#
# Gradient Boosting:
# cria vários modelos em sequência, onde cada novo modelo
# tenta corrigir os erros do anterior.
from sklearn.ensemble import (
    RandomForestClassifier,
    GradientBoostingClassifier
)


# Naive Bayes:
# modelo baseado em probabilidades e no Teorema de Bayes.
from sklearn.naive_bayes import GaussianNB


# KNN:
# classifica um exemplo observando os seus vizinhos mais próximos.
from sklearn.neighbors import KNeighborsClassifier


# SVM:
# tenta encontrar uma fronteira que melhor separe as classes.
from sklearn.svm import SVC


# ============================================================
# 1. CARREGAR A BASE DE DADOS
# ============================================================

url = 'https://raw.githubusercontent.com/alexandrezamberlan/tias/refs/heads/main/predicao_previsao_codigos_exemplos/glicose_data.csv'

# read_csv():
# lê um arquivo CSV e transforma seu conteúdo em um DataFrame.
#
# DataFrame = estrutura do pandas semelhante a uma tabela.
df = pd.read_csv(url)


# ============================================================
# 2. DEFINIR FEATURES E TARGET
# ============================================================

# Features:
# são as informações que serão entregues aos modelos
# para tentar realizar a classificação.
features = ['INSULINA', 'KCAL', 'CARB', 'SONO', 'padel']


# Target:
# é aquilo que queremos que o modelo aprenda a classificar.
target = 'GLICEMIA'


# X recebe somente as colunas usadas como entrada.
#
# Exemplo:
# INSULINA | KCAL | CARB | SONO | padel
X = df[features]


# y recebe a resposta correta que queremos prever/classificar.
#
# Nesse caso:
# GLICEMIA
y = df[target]


# Podemos pensar assim:
#
# INSULINA
# KCAL
# CARB
# SONO
# PADEL
#    ↓
#  MODELO
#    ↓
# GLICEMIA


# ============================================================
# 3. DIVIDIR A BASE EM TREINAMENTO E TESTE
# ============================================================

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,

    # test_size=0.3:
    # 30% dos dados serão usados para TESTE.
    # Os outros 70% serão usados para TREINAMENTO.
    test_size=0.3,

    # random_state:
    # define uma "semente" para a divisão aleatória.
    #
    # Isso faz com que, ao executar novamente o código,
    # a divisão seja sempre a mesma.
    random_state=42,

    # stratify=y:
    # tenta manter a mesma proporção das classes
    # tanto no treinamento quanto no teste.
    #
    # Exemplo:
    # Base original:
    # 70% classe A
    # 20% classe B
    # 10% classe C
    #
    # O treino e o teste tentarão manter essas proporções.
    stratify=y
)


# Resultado da divisão:
#
# X_train = dados de entrada para treinamento
# y_train = respostas corretas do treinamento
#
# X_test  = dados usados para testar o modelo
# y_test  = respostas corretas usadas para comparar o resultado


# ============================================================
# 4. PADRONIZAÇÃO DOS DADOS
# ============================================================

# Cria o objeto responsável pela padronização.
scaler = StandardScaler()


# fit_transform():
#
# FIT:
# aprende a média e o desvio padrão dos dados de treinamento.
#
# TRANSFORM:
# utiliza esses valores para transformar os dados.
#
# Depois da padronização, as variáveis ficam aproximadamente:
# média = 0
# desvio padrão = 1
X_train = scaler.fit_transform(X_train)


# transform():
#
# No conjunto de teste NÃO usamos fit novamente.
#
# Apenas aplicamos a mesma transformação que foi aprendida
# utilizando os dados de treinamento.
#
# Isso evita que informações dos dados de teste sejam usadas
# durante o treinamento (data leakage).
X_test = scaler.transform(X_test)


# ============================================================
# 5. CRIAR OS MODELOS
# ============================================================

# Criamos um dicionário:
#
# "nome do modelo" : objeto do modelo
#
# Isso facilita percorrer todos os modelos usando um único for.
modelos = {

    # max_iter=1000:
    # permite até 1000 iterações para o algoritmo tentar
    # encontrar uma solução durante o treinamento.
    'Logistic Regression': LogisticRegression(max_iter=1000),

    # Cria regras em formato de árvore.
    # Pode sofrer overfitting se crescer demais.
    'Decision Tree': DecisionTreeClassifier(),

    # Utiliza várias árvores e combina suas classificações.
    'Random Forest': RandomForestClassifier(),

    # Observa os exemplos mais próximos para definir a classe.
    'KNN': KNeighborsClassifier(),

    # Calcula probabilidades para decidir a classe mais provável.
    'Naive Bayes': GaussianNB(),

    # Procura uma fronteira que separe as diferentes classes.
    'SVM': SVC(),

    # Cria modelos sequencialmente tentando corrigir erros anteriores.
    'Gradient Boosting': GradientBoostingClassifier()
}


# ============================================================
# 6. CRIAR UMA LISTA PARA GUARDAR OS RESULTADOS
# ============================================================

# A lista começa vazia.
#
# Posteriormente será armazenado:
#
# (nome_modelo, acurácia, f1_score)
resultados = []


print("Avaliação dos Modelos:\n")


# ============================================================
# 7. TREINAR E TESTAR TODOS OS MODELOS
# ============================================================

# modelos.items():
#
# percorre a chave e o valor do dicionário.
#
# Exemplo:
#
# nome   = "Decision Tree"
# modelo = DecisionTreeClassifier()
for nome, modelo in modelos.items():

    # --------------------------------------------------------
    # TREINAMENTO
    # --------------------------------------------------------

    # fit():
    # treina o modelo.
    #
    # X_train = características dos dados
    # y_train = respostas corretas
    #
    # O algoritmo tenta aprender relações entre X e y.
    modelo.fit(X_train, y_train)


    # --------------------------------------------------------
    # PREDIÇÃO
    # --------------------------------------------------------

    # predict():
    # utiliza o modelo já treinado para classificar dados
    # que não foram utilizados durante o treinamento.
    #
    # y_pred = respostas previstas pelo modelo.
    y_pred = modelo.predict(X_test)


    # --------------------------------------------------------
    # ACURÁCIA
    # --------------------------------------------------------

    # accuracy_score():
    # compara a resposta verdadeira (y_test)
    # com a resposta prevista (y_pred).
    #
    # Fórmula simplificada:
    #
    #              acertos
    # acurácia = -----------
    #               total
    #
    # Exemplo:
    # 90 acertos em 100 exemplos = 0.90 = 90%
    acc = accuracy_score(y_test, y_pred)


    # --------------------------------------------------------
    # F1-SCORE
    # --------------------------------------------------------

    # f1_score():
    # combina Precision e Recall em uma única métrica.
    #
    # Precision:
    # "Dos que o modelo disse que eram dessa classe,
    # quantos realmente eram?"
    #
    # Recall:
    # "De todos que realmente eram dessa classe,
    # quantos o modelo encontrou?"
    #
    # average='macro':
    # calcula o F1 de cada classe separadamente
    # e depois tira uma média simples.
    #
    # Assim todas as classes possuem o mesmo peso.
    #
    # zero_division=0:
    # caso alguma divisão não possa ser calculada,
    # retorna 0 em vez de gerar erro/aviso.
    f1 = f1_score(
        y_test,
        y_pred,
        average='macro',
        zero_division=0
    )


    # --------------------------------------------------------
    # GUARDAR RESULTADOS
    # --------------------------------------------------------

    # append():
    # adiciona um novo elemento na lista.
    #
    # Exemplo:
    # ("Random Forest", 0.92, 0.91)
    resultados.append((nome, acc, f1))


    # --------------------------------------------------------
    # MOSTRAR RESULTADOS DO MODELO
    # --------------------------------------------------------

    print(f"Modelo: {nome}")
    print(f"Acurácia: {acc:.4f}")
    print(f"F1-Score (Macro): {f1:.4f}")


    # classification_report():
    #
    # apresenta métricas para cada classe:
    #
    # precision = precisão
    # recall    = capacidade de encontrar exemplos da classe
    # f1-score  = equilíbrio entre precision e recall
    # support   = quantidade real de exemplos daquela classe
    print("Relatório de Classificação:")
    print(
        classification_report(
            y_test,
            y_pred,
            zero_division=0
        )
    )


    # confusion_matrix():
    #
    # cria uma matriz mostrando quais classes o modelo
    # acertou e quais ele confundiu.
    #
    # Exemplo:
    #
    #              PREVISTO
    #             A       B
    #
    # REAL A     40       5
    #      B      3      22
    #
    # 40 = classe A classificada corretamente
    # 5  = classe A confundida com B
    # 3  = classe B confundida com A
    # 22 = classe B classificada corretamente
    print("Matriz de Confusão:")
    print(confusion_matrix(y_test, y_pred))

    print("-" * 60)


# ============================================================
# 8. CRIAR O RANKING DOS MODELOS
# ============================================================

# Cada elemento da lista possui:
#
# (nome, acurácia, f1)
#    0       1      2
#
# lambda x: x[2]
# significa que queremos utilizar o índice 2,
# ou seja, o F1-Score, para ordenar.
#
# reverse=True:
# ordena do MAIOR F1 para o MENOR F1.
resultados.sort(
    key=lambda x: x[2],
    reverse=True
)


# ============================================================
# 9. MOSTRAR O RANKING FINAL
# ============================================================

print("\nRanking Final dos Modelos:")

print(
    f"{'Modelo':<25} "
    f"{'Acurácia':<10} "
    f"{'F1-Score (Macro)':<15}"
)

print("-" * 50)


# Percorre os resultados já ordenados pelo F1-Score.
for nome, acc, f1 in resultados:

    # .4f:
    # mostra o número com 4 casas decimais.
    #
    # Exemplo:
    # 0.913327 → 0.9133
    print(
        f"{nome:<25} "
        f"{acc:<10.4f} "
        f"{f1:<15.4f}"
    )
```

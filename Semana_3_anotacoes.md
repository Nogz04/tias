# TIAS - Semana 3 

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

## ETL aplicado aos dados disponibilizados pelo zamberlan

> - Scaler = StandardScaler() para padronizar

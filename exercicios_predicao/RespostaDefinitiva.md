# Apresentação

Este documento reúne as perguntas do enunciado, as respostas obtidas com os
modelos, as tabelas de resultados para a apresentação.

## 1. Termos utilizados nas respostas e tabelas

### Modelo

É um método matemático que aprende padrões nos dados para produzir uma resposta.
Neste trabalho, cada modelo tenta classificar um cliente ou paciente na classe 0
ou 1.

Os modelos mostrados nas tabelas são:

- **Regressão Logística:** calcula a probabilidade de cada classe;
- **Árvore de Decisão:** aprende uma sequência de perguntas e decisões;
- **Random Forest:** combina várias árvores de decisão;
- **KNN:** observa os registros mais parecidos para escolher a classe;
- **Naive Bayes:** realiza a classificação utilizando probabilidades;
- **SVM:** procura uma fronteira que separe as duas classes;
- **Gradient Boosting:** cria modelos em sequência para que cada novo modelo
  tente corrigir erros dos anteriores.

### Classificação

É a tarefa de escolher uma categoria para cada registro. Neste trabalho, o modelo
escolhe entre as categorias 0 e 1.

### Classe 0 e classe 1

São as duas respostas possíveis de cada problema:

- no problema 1, classe 0 significa “não comprou” e classe 1 significa “comprou”;
- no problema 2, classe 0 significa “baixo risco” e classe 1 significa “alto
  risco de internação”.

### Treino

É a parte dos dados utilizada pelo modelo para aprender. Foram usados 175 dos 250
registros de cada base para treino.

### Teste

É a parte separada para avaliar o modelo depois do treinamento. Esses registros
não são apresentados ao modelo durante o aprendizado. Foram usados 75 dos 250
registros de cada base para teste.

### Divisão estratificada

É uma divisão que tenta manter a mesma proporção das classes no treino e no teste.
Isso evita que quase todos os registros de uma classe fiquem em apenas um dos
conjuntos.

### Acurácia de teste

É a proporção de respostas corretas nos dados de teste. Por exemplo, acurácia de
0,760 significa que o modelo acertou 76% dos registros de teste.

### Precisão

Entre todos os registros classificados pelo modelo como classe 1, a precisão
indica quantos realmente pertenciam à classe 1.

### Recall

Entre todos os registros que realmente pertenciam à classe 1, o recall indica
quantos foram encontrados pelo modelo.

### F1-Score

Uma **métrica** é uma medida numérica usada para avaliar um resultado. O F1-Score
é uma métrica que combina precisão e recall. O resultado varia entre 0 e 1 e
valores mais altos indicam melhor equilíbrio entre essas duas medidas.

### F1 Macro de teste

Primeiro, o F1 é calculado separadamente para as classes 0 e 1. Depois, é feita
uma média simples. Assim, as duas classes possuem a mesma importância. “De teste”
significa que o cálculo foi feito nos 75 registros que o modelo não usou para
aprender.

### Validação cruzada ou CV

CV é a abreviação de *cross-validation*, ou validação cruzada. Nessa técnica, a
base é dividida de diferentes maneiras e o modelo é treinado e avaliado várias
vezes. Foram usadas cinco divisões. Isso reduz a dependência de uma única
separação entre treino e teste.

Cada grupo de registros utilizado em uma avaliação pode ser chamado de
**amostra**.

### F1 Macro médio CV

É a média dos valores de F1 Macro encontrados nas cinco avaliações da validação
cruzada. Neste trabalho, essa foi a principal métrica usada para ordenar os
modelos, pois representa melhor a estabilidade entre diferentes divisões.

**Estabilidade** significa obter resultados semelhantes em diferentes divisões
dos dados.

O **ranking** é a ordenação dos modelos do maior para o menor resultado nessa
métrica.

### Gap F1 treino–teste

*Gap* significa diferença. Ele foi calculado subtraindo o F1 Macro de teste do F1
Macro de treino:

```text
gap = F1 Macro de treino - F1 Macro de teste
```

Um gap positivo e grande mostra que o resultado caiu quando o modelo recebeu
dados não vistos. Isso pode indicar overfitting.

### Matriz de confusão

É uma tabela que mostra os tipos de acerto e erro do modelo:

```text
[[VN, FP],
 [FN, VP]]
```

- **VN — verdadeiro negativo:** era classe 0 e o modelo respondeu 0;
- **FP — falso positivo:** era classe 0, mas o modelo respondeu 1;
- **FN — falso negativo:** era classe 1, mas o modelo respondeu 0;
- **VP — verdadeiro positivo:** era classe 1 e o modelo respondeu 1.

### Overfitting

Overfitting, ou sobreajuste, acontece quando o modelo aprende os dados de treino
em detalhes excessivos, mas não consegue manter o mesmo desempenho em dados
novos. Um resultado quase perfeito no treino acompanhado de uma queda importante
no teste é um sinal de overfitting.

### Classe majoritária e referência

A classe majoritária é a que aparece mais vezes na base. A acurácia de referência
mostra o resultado de uma estratégia simples que sempre escolhe essa classe. Um
modelo deve superar essa referência e também conseguir reconhecer a outra classe.

### Dados sintéticos

São dados criados artificialmente para representar uma situação. Eles são úteis
para exercícios, mas não substituem dados reais na validação de um modelo que será
utilizado em produção.

### Produção

Significa utilizar o modelo em uma situação real, com clientes ou pacientes novos,
para apoiar decisões reais.

### Protótipo

É uma versão inicial usada para estudar e testar uma ideia. Um protótipo ainda não
possui todas as validações necessárias para ser utilizado em produção.

### Dados representativos

São dados que refletem adequadamente a população e as situações reais nas quais o
modelo será utilizado.

## 2. Resultados do problema 1 — compra de produto

A base possui 151 clientes da classe 0 e 99 clientes da classe 1. A acurácia de
referência da classe majoritária é aproximadamente 0,604.

| Modelo | Acurácia de teste | F1 Macro de teste | F1 Macro médio CV | Gap F1 treino–teste |
|---|---:|---:|---:|---:|
| SVM | 0,680 | 0,624 | 0,678 | 0,121 |
| Naive Bayes | 0,653 | 0,610 | 0,662 | 0,085 |
| Regressão Logística | 0,653 | 0,610 | 0,661 | 0,070 |
| Random Forest | 0,653 | 0,610 | 0,657 | 0,390 |
| KNN | 0,653 | 0,624 | 0,646 | 0,137 |
| Gradient Boosting | 0,600 | 0,530 | 0,624 | 0,464 |
| Árvore de Decisão | 0,640 | 0,618 | 0,618 | 0,382 |

### Matriz de confusão da SVM

A SVM apresentou o maior F1 Macro médio na validação cruzada:

| Resultado | Quantidade | Significado |
|---|---:|---|
| VN | 40 | Não comprou e o modelo respondeu “não comprou” |
| FP | 5 | Não comprou, mas o modelo respondeu “comprou” |
| FN | 19 | Comprou, mas o modelo respondeu “não comprou” |
| VP | 11 | Comprou e o modelo respondeu “comprou” |

Havia 30 compradores no teste, mas a SVM encontrou somente 11. Seu recall para
compradores foi 0,367, ou 36,7%.

## 3. Resultados do problema 2 — risco de internação

A base possui 125 pacientes da classe 0 e 125 pacientes da classe 1. Como as
classes estão equilibradas, a acurácia de referência é 0,500.

| Modelo | Acurácia de teste | F1 Macro de teste | F1 Macro médio CV | Gap F1 treino–teste |
|---|---:|---:|---:|---:|
| Regressão Logística | 0,760 | 0,760 | 0,760 | 0,006 |
| Naive Bayes | 0,813 | 0,812 | 0,747 | -0,047 |
| Gradient Boosting | 0,787 | 0,786 | 0,734 | 0,214 |
| Random Forest | 0,760 | 0,760 | 0,733 | 0,240 |
| KNN | 0,693 | 0,692 | 0,727 | 0,107 |
| SVM | 0,747 | 0,747 | 0,721 | 0,070 |
| Árvore de Decisão | 0,760 | 0,760 | 0,665 | 0,240 |

### Matriz de confusão da Regressão Logística

A Regressão Logística apresentou o maior F1 Macro médio na validação cruzada:

| Resultado | Quantidade | Significado |
|---|---:|---|
| VN | 28 | Baixo risco e o modelo respondeu “baixo risco” |
| FP | 10 | Baixo risco, mas o modelo respondeu “alto risco” |
| FN | 8 | Alto risco, mas o modelo respondeu “baixo risco” |
| VP | 29 | Alto risco e o modelo respondeu “alto risco” |

Havia 37 pacientes de alto risco no teste. A Regressão Logística encontrou 29 e
deixou de encontrar 8. Seu recall para alto risco foi 0,784, ou 78,4%.

## 4. Perguntas e respostas do enunciado

### Pergunta 1 — O que a matriz de confusão mostra?

**Resposta:** a matriz de confusão mostra quantos acertos e erros o modelo cometeu
em cada classe. Ela permite separar os erros em falsos positivos e falsos
negativos, o que não aparece quando observamos somente a acurácia.

No problema 1, a matriz da SVM mostrou que 19 dos 30 compradores não foram
identificados. Portanto, mesmo sendo o primeiro modelo do ranking, ela apresentou
dificuldade para encontrar a classe dos compradores.

No problema 2, a matriz da Regressão Logística mostrou 8 falsos negativos. Isso
significa que 8 pacientes de alto risco foram classificados como baixo risco. Em
uma aplicação de saúde, esse erro é especialmente importante.

### Pergunta 2 — A matriz de confusão permite identificar overfitting?

**Resposta:** não sozinha. A matriz mostra os erros de um conjunto avaliado, mas
overfitting é identificado principalmente comparando o resultado de treino com o
resultado de teste e verificando a validação cruzada.

Random Forest, Árvore de Decisão e Gradient Boosting tiveram resultados próximos
de 1 no treino, mas caíram no teste. Os grandes gaps apresentados nas tabelas são
sinais de overfitting.

### Pergunta 3 — Os dados usados no treinamento foram adequados?

**Resposta:** os dados foram adequados para realizar o exercício, comparar os
modelos e demonstrar o processo de treinamento. A divisão estratificada, a
separação entre treino e teste e a validação cruzada permitiram uma avaliação
coerente.

Porém, as bases possuem somente 250 registros e são sintéticas. Portanto, elas não
são suficientes para afirmar que o mesmo desempenho ocorreria em uma situação
real.

### Pergunta 4 — O treinamento surtiu efeito nos modelos?

**Resposta:** sim, mas com intensidades diferentes.

No problema 1, alguns modelos superaram a acurácia de referência de 0,604. Isso
indica que aprenderam algum padrão. Entretanto, o desempenho para encontrar
compradores foi baixo, e alguns modelos apresentaram overfitting.

No problema 2, a Regressão Logística obteve F1 Macro médio de 0,760, bem acima da
referência de 0,500, e manteve resultados semelhantes no treino, teste e validação
cruzada. Nesse caso, o aprendizado foi mais consistente.

### Pergunta 5 — Como interpretar a acurácia e o F1-Score?

**Resposta:** a acurácia informa a proporção total de acertos. O F1-Score combina
precisão e recall. O F1 Macro calcula esse equilíbrio para cada classe e atribui a
mesma importância às duas.

No problema 1, a acurácia da SVM foi 0,680, mas seu recall para compradores foi
somente 0,367. Isso demonstra por que a acurácia não deve ser analisada sozinha.

No problema 2, a Regressão Logística teve acurácia e F1 Macro iguais a 0,760 no
teste. A proximidade dessas métricas indica um desempenho mais equilibrado entre
as classes.

### Pergunta 6 — Qual foi o melhor modelo do problema 1?

**Resposta:** a SVM foi a melhor pelo F1 Macro médio da validação cruzada, com
0,678. Entretanto, ela não pode ser considerada pronta para produção, pois
identificou somente 11 dos 30 compradores no teste e apresentou gap de 0,121.

### Pergunta 7 — Qual foi o melhor modelo do problema 2?

**Resposta:** a resposta depende do critério utilizado. O Naive Bayes teve o maior
resultado em uma única amostra de teste, com acurácia de 0,813 e F1 Macro de
0,812. A Regressão Logística, porém, teve a maior média na validação cruzada e o
menor gap, apresentando maior estabilidade.

Por isso, a Regressão Logística é a escolha mais defensável para continuar como
modelo de estudo do problema 2.

### Pergunta 8 — Algum modelo pode ser utilizado em produção?

**Resposta:** não com as evidências atuais.

No problema 1, o desempenho é insuficiente e existem sinais de overfitting. No
problema 2, a Regressão Logística é uma boa candidata para continuar em um
protótipo, mas ainda cometeu 8 falsos negativos.

Além disso, as bases são pequenas e sintéticas. Antes da produção, seria
necessário testar dados reais e representativos, repetir a validação e analisar o
custo dos diferentes erros. No problema de saúde, também seria necessária uma
avaliação realizada por profissionais da área.

## 5. Sugestão de fala para a apresentação ao professor

### 5.1 Introdução

> Neste trabalho, eu comparei sete modelos de classificação em dois problemas. O
> primeiro tenta identificar se um cliente comprou um produto. O segundo tenta
> identificar o risco de internação de um paciente. Cada base possui 250 registros.
> Eu separei 70% para treino e 30% para teste, mantendo a proporção das classes.
> Também utilizei validação cruzada com cinco divisões para não depender somente
> de uma separação aleatória.

### 5.2 Explicação das métricas

> Eu analisei acurácia, F1 Macro, matriz de confusão e a diferença entre treino e
> teste. A acurácia mostra a proporção total de acertos. O F1 Macro considera o
> equilíbrio entre precisão e recall das duas classes. A matriz de confusão mostra
> quais tipos de erro foram cometidos. A diferença entre treino e teste ajuda a
> identificar overfitting.

### 5.3 Explicação do problema 1

> No problema de compra, a SVM teve o maior F1 Macro médio na validação cruzada,
> com 0,678. Sua acurácia de teste foi 0,680, acima da referência de 0,604. Porém,
> ao analisar a matriz de confusão, percebi que ela encontrou somente 11 dos 30
> compradores e deixou 19 sem identificação. O recall dos compradores foi apenas
> 36,7%. Além disso, Random Forest, Árvore de Decisão e Gradient Boosting tiveram
> resultados quase perfeitos no treino e quedas grandes no teste, indicando
> overfitting. Portanto, nenhum modelo do problema 1 está pronto para produção.

### 5.4 Explicação do problema 2

> No problema de internação, o Naive Bayes teve o melhor resultado na amostra de
> teste, mas a Regressão Logística apresentou o melhor F1 Macro médio na validação
> cruzada, com 0,760, e um gap de apenas 0,006. Isso mostra maior estabilidade. Sua
> matriz teve 28 verdadeiros negativos, 10 falsos positivos, 8 falsos negativos e
> 29 verdadeiros positivos. Os 8 falsos negativos são importantes porque são
> pacientes de alto risco classificados como baixo risco.

### 5.5 Defesa da conclusão

> Minha conclusão é que o treinamento surtiu efeito, principalmente no problema
> 2, mas isso não torna os modelos automaticamente adequados para produção. As
> bases são pequenas e sintéticas. A Regressão Logística é a candidata mais
> estável para continuar em um protótipo do problema 2, enquanto o problema 1
> precisa de mais dados e características melhores. Antes de qualquer uso real,
> seria necessário validar com dados reais e analisar o impacto dos falsos
> positivos e falsos negativos.

## 6. Resumo curto para responder rapidamente

Se o professor pedir uma resposta breve, pode ser dito:

> A matriz de confusão mostrou os acertos e os tipos de erro, mas a análise de
> overfitting exigiu a comparação entre treino, teste e validação cruzada. No
> problema 1, a SVM liderou o ranking, porém perdeu muitos compradores e nenhum
> modelo ficou pronto para produção. No problema 2, a Regressão Logística foi a
> mais estável, mas ainda precisa de validação com dados reais, principalmente
> porque falsos negativos representam pacientes de alto risco não identificados.

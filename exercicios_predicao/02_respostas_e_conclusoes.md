# Respostas e conclusões

Este texto foi escrito para que a análise possa ser entendida mesmo por quem está
começando a estudar Inteligência Artificial e aprendizado de máquina. Primeiro,
serão explicados os termos usados no trabalho. Depois, os resultados dos dois
problemas serão analisados passo a passo.

## 1. Conceitos necessários antes da análise

### 1.1 O que é aprendizado de máquina?

Aprendizado de máquina, ou *Machine Learning*, é uma área da Inteligência
Artificial na qual um programa aprende padrões a partir de exemplos.

Neste exercício, o programa recebe registros que já possuem uma resposta correta.
Ele tenta descobrir uma relação entre as características de cada registro e essa
resposta. Depois do treinamento, pode estimar a resposta de um registro novo.

### 1.2 O que é uma base de dados?

Uma base de dados é um conjunto organizado de informações. Nos arquivos CSV deste
trabalho:

- cada linha representa uma observação, como um cliente ou paciente;
- cada coluna representa uma informação sobre essa observação;
- uma das colunas contém a resposta que queremos prever.

CSV é um formato de texto no qual os valores normalmente são separados por
vírgulas.

### 1.3 O que são características ou *features*?

Características, também chamadas de *features* ou variáveis de entrada, são as
informações que o modelo utiliza para fazer uma predição.

No problema 1, por exemplo, idade, renda, pontuação de crédito e engajamento são
características usadas para tentar descobrir se um cliente comprará um produto.

No código, o conjunto de características recebe tradicionalmente o nome `X`.

### 1.4 O que é variável alvo ou *target*?

A variável alvo, também chamada de *target*, é a resposta que desejamos prever.
Ela recebe tradicionalmente o nome `y` no código.

Neste trabalho:

- `Compro_Produto` é o alvo do problema 1;
- `Risco_Internacao` é o alvo do problema 2.

### 1.5 O que é classificação binária?

Classificação é a tarefa de escolher a qual categoria uma observação pertence.
Ela é binária quando existem somente duas classes possíveis.

Neste exercício, as classes são representadas por 0 e 1:

- no problema 1, 0 significa não comprou e 1 significa comprou;
- no problema 2, 0 significa baixo risco e 1 significa alto risco.

Usar 0 e 1 é apenas uma forma numérica de representar duas categorias. Isso não
significa que a classe 1 seja sempre mais importante, embora em certos problemas
ela possa exigir mais atenção.

### 1.6 O que é um modelo?

Um modelo é o método matemático que aprende padrões nos dados. Foram comparados
sete modelos:

- **Regressão Logística:** calcula a probabilidade de um registro pertencer a uma
  das duas classes. Apesar do nome “regressão”, é muito utilizada para
  classificação;
- **Árvore de Decisão:** cria uma sequência de perguntas e decisões, semelhante a
  regras do tipo “se... então...”;
- **Random Forest:** combina várias árvores de decisão e utiliza o conjunto delas
  para chegar a uma resposta;
- **KNN:** procura os registros mais parecidos, chamados de vizinhos, e considera
  suas classes;
- **Naive Bayes:** utiliza probabilidades e supõe que as características tenham
  certa independência entre si;
- **SVM:** procura uma fronteira que separe as classes da melhor forma possível;
- **Gradient Boosting:** constrói modelos em sequência, fazendo cada novo modelo
  tentar corrigir erros dos anteriores.

### 1.7 O que é treinamento?

Treinamento é a etapa em que o modelo recebe exemplos com respostas conhecidas e
ajusta seus parâmetros para aprender os padrões.

**Parâmetros** são valores internos que o próprio modelo aprende durante o
treinamento. Eles representam matematicamente os padrões encontrados nos dados.

No notebook, o treinamento acontece no comando:

```python
modelo.fit(X_treino, y_treino)
```

O modelo pode aprender somente com os dados de treino. Ele não deve conhecer as
respostas do teste durante essa etapa.

### 1.8 O que são dados de treino e dados de teste?

Os dados foram divididos em dois grupos:

- **treino:** 70% dos registros, usados para o modelo aprender;
- **teste:** 30% dos registros, usados para verificar o desempenho depois do
  aprendizado.

Cada base possui 250 registros. Portanto, foram usados 175 registros para treino
e 75 para teste.

Uma comparação simples é imaginar um aluno estudando para uma prova. Os dados de
treino são os exercícios utilizados para estudar. Os dados de teste são questões
novas da prova. Se o aluno apenas decorou os exercícios antigos, pode ir muito bem
no treino e mal nas questões novas.

### 1.9 O que é estratificação?

Estratificação é o cuidado de manter aproximadamente a mesma proporção das
classes nos conjuntos de treino e teste.

Por exemplo, se 40% da base completa pertence à classe 1, a divisão estratificada
tenta manter perto de 40% da classe 1 tanto no treino quanto no teste. Isso torna
a comparação mais justa.

No código, isso é solicitado com `stratify=y`.

### 1.10 O que é `random_state`?

A separação dos registros possui uma parte aleatória. O `random_state=42` fixa
essa aleatoriedade. Assim, outras pessoas que executarem o notebook obterão a
mesma divisão e poderão reproduzir os resultados.

O número 42 não possui significado estatístico especial; ele funciona apenas
como uma semente fixa.

### 1.11 O que é predição?

Predição é a resposta produzida pelo modelo após o treinamento. Ela é obtida com:

```python
previsao_teste = modelo.predict(X_teste)
```

O modelo recebe somente as características e tenta descobrir a classe de cada
registro.

### 1.12 O que é padronização?

As características podem utilizar escalas muito diferentes. Uma idade pode estar
entre 18 e 65, enquanto uma pontuação de crédito pode chegar a 850.

O `StandardScaler` transforma os valores para que fiquem em uma escala comparável.
Isso é especialmente importante para Regressão Logística, KNN e SVM.

O scaler foi colocado dentro de um *pipeline*, garantindo que ele aprenda a
transformação somente com os dados de treino.

### 1.13 O que é um *pipeline*?

Um *pipeline* organiza várias etapas que precisam ser executadas em sequência.
Neste trabalho, ele primeiro padroniza os dados e depois executa o modelo.

Essa organização reduz erros e garante que a mesma transformação seja aplicada
corretamente no treino e no teste.

### 1.14 O que é vazamento de dados?

Vazamento de dados, ou *data leakage*, ocorre quando uma informação que deveria
estar disponível somente no teste influencia o treinamento.

Isso seria semelhante a um aluno conhecer as respostas da prova antes de fazê-la.
O resultado pareceria excelente, mas não mostraria aprendizado verdadeiro.

Neste trabalho, os pipelines ajudam a impedir vazamento durante a padronização.

### 1.15 O que é acurácia?

Acurácia é a proporção total de previsões corretas:

```text
acurácia = quantidade de acertos / quantidade total de previsões
```

Uma acurácia de 0,760 significa que 76% das previsões estavam corretas.

A acurácia pode enganar quando uma classe aparece muito mais do que a outra. Se
95 de 100 registros fossem da classe 0, um modelo que sempre respondesse 0 teria
95% de acurácia, mesmo sem conseguir reconhecer a classe 1.

### 1.16 O que são precisão e recall?

**Precisão** responde: entre os registros que o modelo marcou como positivos,
quantos realmente eram positivos?

```text
precisão = VP / (VP + FP)
```

**Recall**, também chamado de sensibilidade, responde: entre todos os positivos
reais, quantos o modelo conseguiu encontrar?

```text
recall = VP / (VP + FN)
```

No problema de saúde, recall é muito importante. Um recall baixo significa que
muitos pacientes de alto risco não foram identificados.

### 1.17 O que é F1-Score?

F1-Score combina precisão e recall em uma única medida. Ele utiliza a média
harmônica, que dá uma pontuação baixa quando uma das duas medidas está baixa.

```text
F1 = 2 × (precisão × recall) / (precisão + recall)
```

O valor varia entre 0 e 1. Quanto mais próximo de 1, melhor. Um F1 alto exige um
equilíbrio entre encontrar os positivos e evitar falsos alarmes.

### 1.18 O que significa “Macro” em F1 Macro?

No F1 Macro, o F1 é calculado separadamente para cada classe. Depois, é feita uma
média simples entre os resultados.

Em uma classificação com as classes 0 e 1:

```text
F1 Macro = (F1 da classe 0 + F1 da classe 1) / 2
```

“Macro” significa que cada classe possui o mesmo peso na média, mesmo que uma
delas tenha mais registros. Essa métrica foi escolhida porque segue o padrão dos
exemplos do repositório e evita que a classe mais numerosa domine o resultado.

### 1.19 O que é matriz de confusão?

A matriz de confusão organiza os acertos e erros do modelo. Para as classes 0 e
1, ela possui o formato:

```text
[[VN, FP],
 [FN, VP]]
```

Os termos significam:

- **VN — verdadeiro negativo:** era classe 0 e o modelo respondeu 0;
- **FP — falso positivo:** era classe 0, mas o modelo respondeu 1;
- **FN — falso negativo:** era classe 1, mas o modelo respondeu 0;
- **VP — verdadeiro positivo:** era classe 1 e o modelo respondeu 1.

“Positivo” significa classe 1 e “negativo” significa classe 0. “Verdadeiro” indica
acerto e “falso” indica erro.

### 1.20 O que é validação cruzada?

Uma única divisão entre treino e teste pode produzir um resultado influenciado
pela sorte de quais registros ficaram em cada conjunto.

Uma **amostra** é um grupo de registros retirado da base para uma análise. Neste
caso, cada divisão cria diferentes amostras de treino e validação.

Na validação cruzada, a base é dividida em várias partes. O modelo é treinado e
avaliado várias vezes, trocando a parte utilizada para validação. Neste trabalho,
foram utilizadas cinco partes.

O **F1 Macro médio da validação cruzada** é a média dos cinco resultados. Ele dá
uma visão mais estável do desempenho esperado.

O **desvio** mostra quanto os resultados variaram entre as cinco avaliações. Um
desvio menor indica maior estabilidade.

### 1.21 O que é *overfitting*?

*Overfitting*, ou sobreajuste, acontece quando o modelo aprende os dados de treino
em detalhes excessivos, incluindo ruídos e casos específicos, mas não consegue
generalizar bem para dados novos.

**Ruído** é uma variação aleatória ou informação que não representa um padrão
útil. **Generalizar** significa aplicar o que foi aprendido a registros novos, e
não apenas repetir os exemplos conhecidos.

Um sinal comum é:

- resultado muito alto no treino;
- resultado consideravelmente menor no teste ou na validação cruzada.

Uma Árvore de Decisão com F1 igual a 1 no treino e F1 muito menor no teste pode
ter decorado os exemplos de treino.

### 1.22 O que é gap entre treino e teste?

*Gap* significa diferença. Neste relatório, ele é calculado assim:

```text
gap = F1 Macro de treino - F1 Macro de teste
```

Um gap próximo de zero indica resultados parecidos. Um gap positivo e grande é
um sinal de possível overfitting. Ele não deve ser analisado sozinho; também é
necessário observar a validação cruzada e entender o problema.

Um gap negativo pequeno pode acontecer quando, por acaso, o conjunto de teste é
um pouco mais fácil que o conjunto de treino.

### 1.23 O que é uma classe majoritária?

Classe majoritária é a classe que possui mais registros na base. Um classificador
ingênuo poderia sempre escolher essa classe sem aprender qualquer padrão.

O resultado desse classificador serve como referência inicial, ou *baseline*. Um
modelo útil deve fazer mais do que simplesmente repetir a classe mais frequente.

### 1.24 O que são hiperparâmetros?

Hiperparâmetros são configurações escolhidas antes do treinamento. Exemplos são a
quantidade de árvores de uma Random Forest e a quantidade de vizinhos do KNN.

Ajustar hiperparâmetros significa testar configurações de maneira controlada para
encontrar uma combinação adequada, sempre evitando utilizar o teste para escolher
a melhor opção.

### 1.25 O que significa colocar um modelo em produção?

Colocar em produção significa utilizar o modelo em uma situação real, com novos
clientes ou pacientes, e permitir que suas respostas apoiem decisões.

Um bom resultado em uma base de exercício não é suficiente. Antes da produção,
é necessário testar dados reais, medir riscos, verificar possíveis injustiças,
monitorar o desempenho e definir quem será responsável pelas decisões.

### 1.26 Outros conceitos usados na conclusão

- **Protótipo:** versão inicial usada para estudar a viabilidade de uma ideia;
- **validação externa:** teste realizado em outra base, que não participou do
  desenvolvimento;
- **limiar:** valor de probabilidade a partir do qual o modelo decide pela classe
  1. O valor comum é 0,5, mas ele pode ser ajustado conforme o custo dos erros;
- **calibração:** verificação de que as probabilidades produzidas correspondem à
  frequência observada na realidade;
- **viés:** padrão de erro que pode prejudicar injustamente determinados grupos;
- **governança:** regras que definem uso, responsabilidade, segurança e auditoria
  do modelo;
- **monitoramento:** acompanhamento contínuo do modelo depois que ele começa a ser
  utilizado;
- **estabilidade:** capacidade de manter resultados parecidos em diferentes
  divisões ou amostras;
- **dados sintéticos:** dados criados artificialmente para imitar uma situação;
- **dados clínicos:** dados reais relacionados ao atendimento e à saúde de
  pacientes.

## 2. Como o experimento foi realizado

As duas bases possuem 250 registros. O notebook realizou os seguintes passos:

1. carregou os arquivos CSV;
2. conferiu as primeiras linhas e os valores ausentes;
3. separou as características `X` e a variável alvo `y`;
4. dividiu os registros de forma estratificada em 70% para treino e 30% para
   teste;
5. criou os sete modelos;
6. treinou cada modelo somente com os 175 registros de treino;
7. fez predições nos dados de treino e nos 75 registros de teste;
8. calculou acurácia e F1 Macro;
9. executou validação cruzada estratificada com cinco partes;
10. gerou os relatórios e as matrizes de confusão.

Os modelos que precisam de padronização receberam `StandardScaler` dentro de um
pipeline. A semente `random_state=42` foi mantida para permitir a reprodução dos
resultados.

## 3. Problema 1 — compra de produto

### 3.1 Entendendo a base

A variável `Compro_Produto` informa se o cliente comprou:

- classe 0 — não comprou: 151 clientes;
- classe 1 — comprou: 99 clientes.

A classe 0 é a majoritária. Um modelo que sempre respondesse “não comprou” teria
acurácia de aproximadamente 0,604, pois acertaria 151 dos 250 registros. Contudo,
ele não encontraria comprador algum. Por isso, não podemos olhar somente para a
acurácia.

### 3.2 Resultados

| Modelo | Acurácia teste | F1 Macro teste | F1 Macro médio CV | Gap F1 treino–teste |
|---|---:|---:|---:|---:|
| SVM | 0,680 | 0,624 | 0,678 | 0,121 |
| Naive Bayes | 0,653 | 0,610 | 0,662 | 0,085 |
| Regressão Logística | 0,653 | 0,610 | 0,661 | 0,070 |
| Random Forest | 0,653 | 0,610 | 0,657 | 0,390 |
| KNN | 0,653 | 0,624 | 0,646 | 0,137 |
| Gradient Boosting | 0,600 | 0,530 | 0,624 | 0,464 |
| Árvore de Decisão | 0,640 | 0,618 | 0,618 | 0,382 |

Os modelos estão ordenados pelo F1 Macro médio da validação cruzada. A SVM ficou
em primeiro lugar, com 0,678. Isso significa que, considerando igualmente as duas
classes e repetindo a avaliação em cinco divisões, ela apresentou a melhor média.

Entretanto, “melhor entre os modelos testados” não significa necessariamente
“bom o suficiente para uso real”. É preciso analisar os erros.

### 3.3 Leitura da matriz de confusão da SVM

A matriz da SVM no teste foi:

```text
[[40,  5],
 [19, 11]]
```

Lendo cada número:

- 40 clientes não compraram e foram classificados corretamente como não
  compradores;
- 5 clientes não compraram, mas foram classificados como compradores;
- 19 clientes compraram, mas foram classificados como não compradores;
- 11 clientes compraram e foram identificados corretamente.

Havia 30 compradores no teste. A SVM encontrou somente 11 deles:

```text
recall dos compradores = 11 / (11 + 19) = 0,367
```

Portanto, aproximadamente 36,7% dos compradores foram encontrados e 63,3% foram
perdidos. Esse desempenho é fraco caso o objetivo seja identificar clientes com
potencial de compra.

### 3.4 Houve overfitting?

Os sinais variam entre os modelos:

- Random Forest teve gap de 0,390;
- Árvore de Decisão teve gap de 0,382;
- Gradient Boosting teve gap de 0,464.

Esses modelos chegaram perto de F1 Macro igual a 1 no treino, mas tiveram
resultado muito inferior no teste. Isso é um sinal forte de overfitting.

A SVM teve gap de 0,121. O gap é menor que o dos modelos anteriores, mas ainda
mostra uma queda perceptível. A validação cruzada ajuda a confirmar que seu
desempenho é apenas moderado.

Naive Bayes e Regressão Logística apresentaram gaps menores, porém suas métricas
também não foram altas. Um modelo não deixa de ser fraco apenas porque não sofreu
overfitting: ele pode simplesmente não ter aprendido padrões suficientes.

### 3.5 Resposta e conclusão do problema 1

Os dados permitiram que alguns modelos aprendessem algum padrão, pois a SVM
superou a acurácia de referência de 0,604. Porém, o aprendizado não foi suficiente
para uma aplicação real.

A SVM foi a melhor na validação cruzada, mas encontrou somente 11 dos 30
compradores presentes no teste. Os modelos baseados em árvores apresentaram sinais
fortes de overfitting. Além disso, a base é pequena e sintética.

**Conclusão:** nenhum dos sete modelos deve ser colocado em produção com esses
resultados. A SVM pode ser mantida como referência para novos testes, mas seriam
necessários mais registros, características mais informativas, ajuste de
hiperparâmetros e validação em dados reais.

## 4. Problema 2 — risco de internação

### 4.1 Entendendo a base

A variável `Risco_Internacao` representa:

- classe 0 — baixo risco: 125 pacientes;
- classe 1 — alto risco: 125 pacientes.

A base está perfeitamente equilibrada. Um classificador que escolhesse sempre uma
das classes teria acurácia de 0,500. Esse valor é a referência inicial.

### 4.2 Resultados

| Modelo | Acurácia teste | F1 Macro teste | F1 Macro médio CV | Gap F1 treino–teste |
|---|---:|---:|---:|---:|
| Regressão Logística | 0,760 | 0,760 | 0,760 | 0,006 |
| Naive Bayes | 0,813 | 0,812 | 0,747 | -0,047 |
| Gradient Boosting | 0,787 | 0,786 | 0,734 | 0,214 |
| Random Forest | 0,760 | 0,760 | 0,733 | 0,240 |
| KNN | 0,693 | 0,692 | 0,727 | 0,107 |
| SVM | 0,747 | 0,747 | 0,721 | 0,070 |
| Árvore de Decisão | 0,760 | 0,760 | 0,665 | 0,240 |

O Naive Bayes teve o maior resultado no conjunto de teste: acurácia de 0,813 e F1
Macro de 0,812. Porém, a Regressão Logística teve o maior F1 Macro médio na
validação cruzada: 0,760 contra 0,747 do Naive Bayes.

Isso indica que o excelente resultado do Naive Bayes nessa divisão específica
pode ter sido influenciado pelos registros que ficaram no teste. A Regressão
Logística apresentou resultado mais estável ao longo das cinco divisões.

### 4.3 Leitura da matriz da Regressão Logística

A matriz no teste foi:

```text
[[28, 10],
 [ 8, 29]]
```

Lendo cada valor:

- 28 pacientes de baixo risco foram classificados corretamente;
- 10 pacientes de baixo risco foram classificados como alto risco;
- 8 pacientes de alto risco foram classificados como baixo risco;
- 29 pacientes de alto risco foram identificados corretamente.

Os 8 falsos negativos merecem atenção especial. Eles representam pacientes de
alto risco que o modelo considerou de baixo risco. Em uma situação real, esse erro
poderia atrasar cuidados importantes.

O recall da classe de alto risco foi:

```text
recall do alto risco = 29 / (29 + 8) = 0,784
```

Assim, o modelo encontrou aproximadamente 78,4% dos pacientes de alto risco, mas
deixou de encontrar cerca de 21,6% deles.

### 4.4 Houve overfitting?

A Regressão Logística teve:

- F1 Macro de treino próximo de 0,766;
- F1 Macro de teste igual a 0,760;
- gap igual a 0,006;
- F1 Macro médio da validação cruzada igual a 0,760.

Os três resultados são muito parecidos. Portanto, não há sinal importante de
overfitting nesse modelo.

Random Forest e Árvore de Decisão tiveram gap de 0,240, enquanto Gradient Boosting
teve gap de 0,214. Eles alcançaram F1 Macro igual a 1 no treino e tiveram queda no
teste. Isso indica overfitting.

O gap do Naive Bayes foi negativo porque seu resultado no teste foi melhor do que
no treino. Isso pode acontecer por variação da amostra e não significa que o
modelo seja perfeito. Sua validação cruzada foi mais variável que a da Regressão
Logística.

### 4.5 Qual modelo foi melhor?

A resposta depende do critério:

- se olharmos somente para esta amostra de teste, o Naive Bayes foi o melhor;
- se buscarmos estabilidade em diferentes divisões, a Regressão Logística foi a
  escolha mais consistente;
- se o custo dos falsos negativos for muito alto, poderá ser necessário ajustar o
  limiar ou escolher o modelo com base principalmente no recall da classe 1.

Para este trabalho, a Regressão Logística é a candidata mais defensável porque
teve o melhor F1 Macro médio na validação cruzada e praticamente não apresentou
gap entre treino e teste.

### 4.6 Resposta e conclusão do problema 2

Os resultados mostram que houve aprendizado real: os modelos ficaram acima da
referência de 0,500 e a Regressão Logística manteve desempenho parecido no treino,
teste e validação cruzada.

**Conclusão:** a Regressão Logística pode seguir para a próxima etapa de um
protótipo. Isso não significa que esteja pronta para uso clínico. A base possui
somente 250 registros e é sintética. Antes de qualquer uso real, seriam
necessários dados clínicos representativos, validação externa, análise de viés,
calibração, escolha cuidadosa do limiar e supervisão de profissionais da saúde.

## 5. Conclusão geral

A análise não deve escolher um modelo apenas porque ele possui o maior número em
uma única métrica. É necessário observar:

1. se ele supera uma referência simples;
2. se acurácia e F1 Macro são adequados;
3. quais tipos de erro aparecem na matriz de confusão;
4. se treino e teste possuem resultados próximos;
5. se a validação cruzada mostra estabilidade;
6. qual é o custo real dos falsos positivos e falsos negativos.

No problema 1, os modelos apresentaram desempenho limitado e alguns sofreram
forte overfitting. Nenhum está pronto para produção.

No problema 2, a Regressão Logística apresentou o aprendizado mais consistente.
Mesmo assim, ela deve ser considerada somente um protótipo, pois bons resultados
em uma base sintética e pequena não garantem segurança em pacientes reais.

Por fim, a matriz de confusão sozinha não consegue provar se existe overfitting.
Ela mostra os tipos de acerto e erro em um conjunto. Para analisar overfitting, é
necessário comparar o desempenho de treino com teste e validação cruzada.

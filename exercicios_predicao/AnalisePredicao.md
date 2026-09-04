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

Havia 30 compradores no teste, mas a SVM encontrou somente 11. Seu recall para compradores foi 0,367, ou 36,7%.

### Análise profissional da base de compras

Para fins profissionais, a base de compras não pode ser considerada suficientemente boa para sustentar um modelo de previsão de compra em produção.

O primeiro problema é o tamanho da base. São somente 250 registros, dos quais 175 foram utilizados para treinamento e 75 para teste. Essa quantidade é pequena para representar adequadamente diferentes perfis de consumidores e torna os resultados mais sensíveis à divisão dos dados. A validação cruzada reduz a dependência de uma única divisão, mas não cria novas informações nem resolve a limitação de uma base pequena.

O segundo problema é a quantidade limitada de variáveis. A previsão de compra é feita com apenas idade, renda anual, score de crédito e pontuação de engajamento. Essas características podem conter algum sinal relacionado à compra, mas não representam muitos dos fatores que normalmente influenciam o comportamento de consumo, como histórico de compras, frequência de compras, preço, descontos, campanhas, produtos visualizados, carrinhos abandonados, canal de venda e comportamento anterior. Portanto, mesmo um algoritmo sofisticado fica limitado pela informação disponível na base.

O terceiro problema aparece diretamente nos resultados. A SVM foi a melhor entre os modelos avaliados segundo o F1 Macro médio da validação cruzada, com 0,678, mas identificou somente 11 dos 30 compradores no conjunto de teste. Isso significa que 19 compradores não foram identificados, produzindo recall de apenas 36,7% para a classe de interesse. Portanto, a acurácia de 68,0% não deve ser interpretada como se o modelo conseguisse identificar 68% dos compradores.

Outro ponto importante são os sinais de overfitting. Random Forest, Gradient Boosting e Árvore de Decisão apresentaram gaps F1 treino–teste de 0,390, 0,464 e 0,382, respectivamente. Esses valores indicam uma queda considerável do desempenho quando o modelo passa dos dados de treinamento para dados não vistos. Para uso profissional, esse comportamento é um alerta de baixa capacidade de generalização.

Além disso, a própria natureza da base limita a conclusão. Os dados são sintéticos, ou seja, foram criados artificialmente para representar uma situação. Isso é adequado para demonstrar técnicas de Machine Learning, mas não é suficiente para provar que os padrões aprendidos correspondem ao comportamento real de consumidores.

### Avaliação profissional do problema 1

**A base é boa para aprendizado e demonstração de Machine Learning, mas é inadequada para um sistema profissional de previsão de compras.**

Se fosse necessário colocar um modelo em produção, eu não utilizaria essa base como única fonte de treinamento. Seria necessário aumentar significativamente a quantidade de dados, utilizar dados reais e representativos e incluir variáveis comportamentais e de contexto mais diretamente relacionadas à compra.

Também seria necessário definir previamente qual erro possui maior custo para o negócio. Se o objetivo principal for encontrar compradores potenciais, o recall da classe “comprou” pode ser mais importante do que a acurácia geral. Nesse contexto, o desempenho de 36,7% de recall apresentado pela SVM é insuficiente.

---

## 3. Resultados do problema 2 — risco de internação

A base possui 125 pacientes da classe 0 e 125 pacientes da classe 1. Como as classes estão equilibradas, a acurácia de referência é 0,500.

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

Havia 37 pacientes de alto risco no teste. A Regressão Logística encontrou 29 e deixou de encontrar 8. Seu recall para alto risco foi 0,784, ou 78,4%.

### Análise profissional da base de saúde

Para fins profissionais, a base de saúde também não pode ser considerada suficiente para colocar um modelo de previsão de risco de internação em produção, apesar de apresentar resultados mais consistentes do que a base de compras.

A primeira diferença positiva é que as classes estão perfeitamente equilibradas, com 125 pacientes de baixo risco e 125 de alto risco. Isso evita que o resultado seja favorecido simplesmente pela predominância de uma classe.

Outro ponto positivo é o comportamento da Regressão Logística. Ela apresentou F1 Macro médio de 0,760 na validação cruzada e gap de apenas 0,006 entre treino e teste. Isso mostra uma diferença muito pequena entre o desempenho observado nos dados de treinamento e nos dados não vistos, sendo um sinal de maior estabilidade no experimento.

Mesmo assim, o tamanho da base continua sendo uma limitação: são apenas 250 pacientes. Em um cenário profissional, esse conjunto seria pequeno para representar adequadamente a diversidade clínica de uma população e para sustentar conclusões fortes sobre generalização.

A segunda limitação importante é a quantidade de variáveis. A base utiliza idade, pressão arterial, colesterol total e frequência cardíaca máxima para prever risco de internação. Essas variáveis podem ter relação com o problema, mas são insuficientes para representar toda a complexidade clínica associada ao risco de internação. A ausência de outros fatores clínicos e históricos reduz a capacidade do modelo de representar adequadamente situações reais.

Existe ainda uma questão fundamental: a base é sintética e o arquivo não apresenta como o rótulo `Risco_Internacao` foi determinado. Sem conhecer a origem e a metodologia de definição do target, não é possível garantir que a classe “alto risco” corresponda a um desfecho clínico real e confiável. Assim, um modelo pode estar aprendendo os padrões utilizados para gerar artificialmente o rótulo, em vez de aprender relações que se mantenham em pacientes reais.

A matriz de confusão também merece atenção. No teste, a Regressão Logística apresentou 8 falsos negativos: pacientes que eram de alto risco, mas foram classificados como baixo risco. Entre os 37 pacientes de alto risco do conjunto de teste, isso corresponde a aproximadamente 21,6% não identificados. Em uma aplicação de saúde, esse tipo de erro pode ser muito mais relevante do que uma pequena diferença na acurácia, pois representa a possibilidade de não sinalizar um paciente que realmente apresenta alto risco.

Por isso, mesmo com F1 de 0,760 e gap pequeno, não seria correto afirmar que o modelo possui “76% de precisão em pacientes reais”. Esse resultado vale para o conjunto de dados e para a metodologia utilizada no experimento. Antes de qualquer uso profissional, seria necessária validação em dados reais, independentes e representativos.

### Avaliação profissional do problema 2

**A base de saúde é melhor para o experimento acadêmico do que a base de compras, mas continua inadequada para uso clínico profissional.**

A Regressão Logística é a candidata mais consistente entre os modelos avaliados, porque apresentou a maior média de F1 na validação cruzada e o menor gap entre treino e teste. Entretanto, isso significa somente que ela foi a opção mais estável dentro desse experimento; não significa que esteja pronta para produção.

Para transformar esse estudo em um sistema profissional, seria necessário trabalhar com uma base maior e real, definir claramente a origem do target, incluir mais informações clínicas relevantes e realizar validação externa com pacientes que não participaram da construção do modelo. Também seria necessário avaliar explicitamente o custo de falsos positivos e falsos negativos e estabelecer um limiar de decisão compatível com o risco clínico.

---

## 4. Análise geral da qualidade das duas bases para uso profissional

### As bases são boas ou ruins?

A resposta depende do objetivo.

| Objetivo | Compra | Saúde |
|---|---|---|
| Aprender Machine Learning | Boa | Excelente |
| Trabalho acadêmico | Boa | Boa |
| Comparar algoritmos | Boa | Boa |
| Fazer protótipo | Limitada | Limitada |
| Pesquisa mais séria | Limitada | Limitada |
| Uso em produção | Inadequada | Inadequada |
| Tomada de decisão real | Inadequada | Inadequada |

As duas bases são adequadas para estudar classificação, porque possuem um target binário e quantidade suficiente para demonstrar treino, teste, validação cruzada, matriz de confusão e comparação entre modelos. Porém, esses resultados devem ser interpretados como resultados de um experimento didático, e não como evidência de desempenho em produção.

### Por que não são suficientes para uso profissional?

Os principais fatores são:

1. **Poucos registros:** cada base possui somente 250 exemplos.
2. **Dados sintéticos:** não há garantia de que os padrões artificiais representem adequadamente situações reais.
3. **Poucas variáveis:** os atributos disponíveis não capturam toda a complexidade dos problemas.
4. **Representatividade desconhecida:** não há evidência de que os registros representem adequadamente a população real.
5. **Validação externa ausente:** os resultados foram avaliados dentro do próprio conjunto de dados, sem demonstração de desempenho em uma base externa independente.
6. **Erros relevantes:** no problema de compras, o recall dos compradores foi somente 36,7%; no problema de saúde, houve 8 falsos negativos de alto risco no teste.
7. **Overfitting em alguns modelos:** principalmente no problema de compras, alguns algoritmos tiveram grande diferença entre treino e teste.
8. **Target sem contextualização suficiente:** especialmente no problema de saúde, não está documentado no arquivo como o rótulo de risco foi produzido.

### Sobre a precisão dos modelos

Não é correto afirmar simplesmente que os modelos possuem “muita precisão” com base nesses resultados.

No problema 1, a SVM teve acurácia de 68,0%, mas isso não significa que encontrou 68% dos compradores. Seu recall para compradores foi de apenas 36,7%.

No problema 2, a Regressão Logística alcançou F1 Macro médio de 0,760 e apresentou maior estabilidade, mas ainda deixou de detectar 8 pacientes de alto risco no conjunto de teste. Além disso, esse desempenho não foi demonstrado em pacientes reais independentes.

Portanto, as métricas demonstram desempenho **dentro dessas bases**, e não “precisão garantida” em ambiente profissional.

### O que seria necessário para torná-las adequadas?

Para a base de compras, seria necessário aumentar a quantidade de clientes e incorporar histórico de compras, comportamento de navegação, interações com campanhas, preços, descontos e outras características relacionadas ao processo de compra. Também seria importante avaliar o modelo em períodos posteriores, com clientes que não fizeram parte do treinamento, para verificar se o comportamento se mantém.

Para a base de saúde, seriam necessários dados clínicos reais, maior quantidade de pacientes, definição confiável do desfecho de internação, mais características clínicas relevantes e validação externa. Em uma aplicação clínica, também seria necessário analisar o impacto de cada tipo de erro e envolver profissionais da saúde na avaliação do sistema.

### Conclusão profissional

As duas bases são úteis e adequadas para demonstrar o processo de Machine Learning, mas **não são bases suficientemente boas para sustentar um modelo profissional de produção**.

A base de compras apresenta limitações mais evidentes no próprio resultado: embora a SVM seja a melhor entre os modelos avaliados, ela identificou somente 36,7% dos compradores no teste e alguns modelos apresentaram forte overfitting.

A base de saúde apresentou um cenário mais promissor: a Regressão Logística obteve F1 Macro médio de 0,760 e gap de apenas 0,006. Mesmo assim, os dados são pequenos e sintéticos, existem poucas variáveis clínicas e houve falsos negativos relevantes. Portanto, ela pode ser uma boa candidata para continuar um **protótipo acadêmico**, mas não para uso clínico real.

A conclusão profissional correta é: **os modelos aprenderam padrões presentes nessas bases, mas as bases não fornecem evidência suficiente para afirmar que esses modelos terão alta precisão, segurança ou generalização no mundo real.**

---

## 5. Sugestão de fala para a apresentação ao professor

### 5.1 Introdução

> Neste trabalho, eu comparei sete modelos de classificação em dois problemas. O primeiro tenta identificar se um cliente comprou um produto. O segundo tenta identificar o risco de internação de um paciente. Cada base possui 250 registros. Eu separei 70% para treino e 30% para teste, mantendo a proporção das classes, e também utilizei validação cruzada com cinco divisões.

### 5.2 Explicação das métricas

> Eu analisei acurácia, F1 Macro, matriz de confusão e a diferença entre treino e teste. A acurácia mostra a proporção total de acertos. O F1 Macro considera o equilíbrio entre precisão e recall das duas classes. A matriz de confusão mostra quais tipos de erro foram cometidos. A diferença entre treino e teste ajuda a identificar overfitting.

### 5.3 Explicação do problema 1

> No problema de compra, a SVM teve o maior F1 Macro médio na validação cruzada, com 0,678. Sua acurácia de teste foi 0,680, acima da referência de 0,604. Porém, quando analisei a matriz de confusão, percebi que ela encontrou somente 11 dos 30 compradores e deixou 19 sem identificação. O recall dos compradores foi de apenas 36,7%. Além disso, Random Forest, Árvore de Decisão e Gradient Boosting apresentaram gaps muito grandes entre treino e teste, indicando overfitting.

> Profissionalmente, eu não consideraria essa base suficiente para produção. Ela possui somente 250 registros, é sintética e tem poucas variáveis para representar o comportamento de compra. Portanto, o modelo conseguiu aprender alguns padrões, mas não há evidência suficiente de que esses padrões se manteriam em clientes reais.

### 5.4 Explicação do problema 2

> No problema de internação, a Regressão Logística foi a opção mais estável, com F1 Macro médio de 0,760 na validação cruzada e gap de somente 0,006. Isso indica uma diferença pequena entre o desempenho de treino e teste. Porém, a base continua sendo pequena e sintética e possui apenas quatro variáveis explicativas.

> A matriz de confusão mostrou 8 falsos negativos, ou seja, 8 pacientes de alto risco foram classificados como baixo risco. Em uma aplicação de saúde, esse erro é importante. Por isso, apesar do resultado ser melhor que no problema de compra, eu não utilizaria esse modelo em produção sem uma base real, maior e independente.

### 5.5 Defesa da conclusão

> Minha conclusão é que as bases são boas para aprendizado e para demonstrar técnicas de Machine Learning, mas não são suficientemente boas para uso profissional. Na base de compras, o principal problema é a dificuldade de identificar os compradores e os sinais de overfitting. Na base de saúde, a Regressão Logística apresentou resultados mais estáveis, mas ainda existem limitações importantes relacionadas ao tamanho, à natureza sintética dos dados, à quantidade de variáveis e aos falsos negativos.

> Portanto, os resultados mostram que os modelos aprenderam padrões presentes nas bases, mas não permitem afirmar que eles terão alta precisão ou serão confiáveis em produção. Antes de qualquer uso real, seria necessário utilizar dados reais e representativos, aumentar a quantidade e qualidade das informações, realizar validação externa e analisar o impacto dos diferentes tipos de erro.

---

## 6. Resumo curto para responder rapidamente

> As duas bases são boas para aprender e demonstrar Machine Learning, mas não são adequadas para uso profissional. A base de compras tem somente 250 registros, poucas variáveis e apresentou baixo recall para compradores: a SVM encontrou apenas 11 dos 30 compradores. Já a base de saúde apresentou resultados mais estáveis, principalmente com a Regressão Logística, que teve F1 médio de 0,760 e gap de 0,006. Mesmo assim, ela também é pequena e sintética, possui poucas variáveis clínicas e teve 8 falsos negativos de alto risco no teste. Portanto, os resultados mostram aprendizado dentro das bases, mas não garantem alta precisão ou generalização em dados reais.

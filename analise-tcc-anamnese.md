# Tecnologias Inteligentes Aplicadas à Saúde

## Identificação do trabalho

- **Título:** Anamnese Intuitiva Orientada por IA
- **Curso:** Ciência da Computação — Universidade Franciscana (UFN)
- **Aluno:** Rian Beskow Friedrich
- **Orientador:** Sylvio André Garcia Vieira
- **Link do trabalho:** *https://tfgonline.lapinf.ufn.edu.br/media/midias/anamnese_GA4moZU.pdf*

---

## Descrição básica do trabalho

O trabalho apresenta o desenvolvimento de uma aplicação Web para realização de **anamnese orientada por Inteligência Artificial**, com foco no apoio ao **pré-diagnóstico de doenças cardíacas**.

**Anamnese** é a etapa da consulta em que o profissional de saúde coleta informações sobre o paciente, como sintomas, histórico de doenças, hábitos, medicamentos utilizados e histórico familiar. No sistema, essa coleta é realizada por meio de um formulário.

O sistema coleta informações como idade, pressão arterial, IMC, tabagismo, consumo de álcool, diabetes, histórico familiar e outros fatores clínicos. Esses dados são organizados e comparados com o conjunto de dados **Heart Disease**.

**Heart Disease** significa, em tradução direta, **doença cardíaca**. No TCC, esse nome identifica um *dataset* voltado à análise de doenças cardiovasculares, contendo mais de 10 mil registros de pacientes e 21 atributos clínicos.

Um **dataset** é um conjunto organizado de dados utilizado para análise ou treinamento de modelos de Inteligência Artificial.

A Inteligência Artificial utilizada no protótipo é baseada em **Aprendizado de Máquina supervisionado**, por meio do algoritmo **Decision Tree Classifier**.

**Aprendizado de Máquina supervisionado** é uma técnica na qual o algoritmo aprende a partir de exemplos que já possuem uma resposta conhecida. Neste caso, os dados de treinamento indicam se há ou não presença de doença cardíaca.

O **Decision Tree Classifier**, ou **Classificador por Árvore de Decisão**, é um algoritmo que toma decisões por meio de uma estrutura semelhante a uma árvore, realizando sucessivas divisões com base nas características dos dados até chegar a uma classificação.

Após o treinamento, o modelo analisa os dados da anamnese e calcula uma **probabilidade percentual de o paciente apresentar uma condição cardíaca**. O resultado é apresentado ao profissional de saúde como um indicativo de pré-diagnóstico, servindo como apoio à decisão clínica e não como substituição ao julgamento médico.

**Pré-diagnóstico** é uma indicação inicial de uma possível condição de saúde. Ele não substitui o diagnóstico realizado por um profissional habilitado.

---

## Área da Saúde

A principal área da saúde relacionada ao trabalho é a **Medicina**, especialmente no contexto de:

- anamnese;
- avaliação de fatores de risco cardiovascular;
- apoio ao pré-diagnóstico;
- apoio à decisão do profissional de saúde.

---

## Técnicas de Inteligência Artificial relacionadas ao trabalho

### Aprendizado de Máquina

Esta é a principal técnica de IA implementada no trabalho. **Machine Learning (Aprendizado de Máquina)** é a área da IA em que algoritmos aprendem padrões a partir de dados para realizar classificações ou predições.

O sistema utiliza **Aprendizado de Máquina supervisionado**, treinando um modelo `DecisionTreeClassifier` com dados previamente classificados quanto à presença ou ausência de doença cardíaca.

O modelo aprende relações entre atributos clínicos e o resultado esperado, possibilitando posteriormente classificar novos pacientes.

### Reconhecimento de padrões

O sistema realiza **reconhecimento de padrões**, isto é, identifica combinações e relações que se repetem nos dados clínicos dos pacientes e que podem estar associadas a determinado resultado.

A árvore de decisão procura relações e correlações entre características como:

- idade;
- pressão sanguínea;
- colesterol;
- IMC;
- diabetes;
- tabagismo;
- consumo de álcool;
- histórico familiar;
- níveis de glicemia;
- triglicerídeos;
- outros fatores relacionados à saúde cardiovascular.

Esses padrões são utilizados para estimar a probabilidade de doença cardíaca.

### Base de amostras para treinamento

O treinamento utiliza o dataset **Heart Disease**, contendo aproximadamente **10.000 registros de pacientes e 21 atributos**.

Essa base funciona como um conjunto de amostras conhecidas que permite ao algoritmo aprender padrões associados à presença ou ausência de doença cardíaca.

Além disso, o sistema permite incorporar novos dados de pacientes e realizar novamente o treinamento do modelo.

### Raciocínio automatizado

O trabalho possui um processo automatizado de **inferência**, ou seja, a etapa em que um modelo já treinado recebe novos dados e produz uma resposta. Nesse caso, o modelo recebe os dados do paciente e percorre a estrutura da árvore de decisão para chegar a uma classificação probabilística.

Entretanto, não se trata de um sistema clássico de raciocínio baseado em uma base explícita de regras médicas. O raciocínio realizado decorre principalmente do modelo de **Aprendizado de Máquina** treinado a partir dos dados.

### Processamento da Língua Natural

Conceitos relacionados a **Processamento de Linguagem Natural (PLN)**, LLMs, RAG, LangChain, Ollama e Whisper aparecem na fundamentação teórica do trabalho.

De forma resumida:

- **PLN (Processamento de Linguagem Natural):** área da IA voltada para compreender, interpretar ou gerar linguagem humana.
- **LLM (Large Language Model):** modelo de linguagem treinado com grande quantidade de textos, capaz de compreender e gerar linguagem.
- **RAG (Retrieval-Augmented Generation):** técnica que combina um modelo de linguagem com busca em fontes externas para produzir respostas mais contextualizadas.
- **LangChain:** framework usado para integrar modelos de linguagem a bancos de dados, APIs e outras ferramentas.
- **Ollama:** ferramenta que permite executar modelos de linguagem localmente.
- **Whisper:** modelo de reconhecimento de fala que converte áudio em texto.

Porém, essas técnicas **não foram implementadas no protótipo atual**. Elas são apresentadas como possibilidades de evolução futura, por exemplo, para interpretar relatos falados ou escritos pelos pacientes.

### Redes Neurais

O protótipo não utiliza redes neurais.

A técnica implementada é uma **Árvore de Decisão (`DecisionTreeClassifier`)**, pertencente ao campo de Aprendizado de Máquina supervisionado.

### Sistemas Multiagentes

O trabalho não utiliza Sistemas Multiagentes.

---

## Rotinas da Saúde trabalhadas

### 1. Diagnóstico

**Aplicável ao trabalho: Sim, como pré-diagnóstico e apoio ao diagnóstico.**

O sistema recebe os dados da anamnese e utiliza o modelo treinado para identificar padrões associados à presença de doença cardíaca.

Como resultado, apresenta ao profissional de saúde um indicativo de **pré-diagnóstico**, acompanhado de uma probabilidade percentual.

Portanto, o sistema não realiza um diagnóstico médico definitivo. Ele atua como uma ferramenta de apoio ao profissional.

**Relação com o conteúdo da disciplina:**

> reconhecer padrões → utilizar um volume de dados → aplicar algoritmos de Aprendizado de Máquina.

Esse fluxo corresponde diretamente ao funcionamento do TCC.

---

### 2. Monitoramento / Sensoriamento e atuação

**Aplicável ao trabalho: Não diretamente.**

O sistema não realiza monitoramento contínuo do paciente e não utiliza sensores, dispositivos vestíveis, equipamentos médicos ou coleta automática de sinais em tempo real.

Os dados são fornecidos durante o preenchimento da anamnese.

Assim, apesar de armazenar informações clínicas, o trabalho não caracteriza uma rotina de monitoramento ou sensoriamento contínuo.

---

### 3. Predição

**Aplicável ao trabalho: Sim.**

Esta é uma das principais operações inteligentes do sistema.

A partir dos dados da anamnese, o modelo calcula a probabilidade de o paciente pertencer à classe associada à presença de doença cardíaca.

Exemplo conceitual:

```text
Dados do paciente
        ↓
Pré-processamento
        ↓
Decision Tree Classifier
        ↓
Reconhecimento de padrões
        ↓
Probabilidade de doença cardíaca
        ↓
Pré-diagnóstico apresentado ao profissional
```

O sistema utiliza, portanto, dados conhecidos para **predizer uma classe ou probabilidade para um novo paciente**.

---

### 4. Previsão

**Aplicável ao trabalho: Não como operação principal.**

Apesar de os termos *predição* e *previsão* serem utilizados de forma semelhante em alguns contextos, neste trabalho o termo mais adequado é **predição**.

A aplicação não procura estimar como a condição do paciente irá evoluir ao longo do tempo, nem prevê valores futuros em uma série temporal.

Ela utiliza características atuais do paciente para estimar a probabilidade de uma condição cardíaca.

Assim:

- **Predição:** estima um resultado desconhecido a partir de características disponíveis.
- **Previsão:** normalmente está relacionada à estimativa de um acontecimento ou valor futuro, frequentemente considerando uma dimensão temporal.

Nesse TCC ocorre principalmente **predição**.

---

### 5. Recomendação

**Aplicável ao trabalho: Parcialmente, como apoio à decisão, mas não como sistema de recomendação.**

O sistema não recomenda diretamente:

- medicamentos;
- tratamentos;
- procedimentos;
- exames;
- mudanças de conduta.

Ele fornece uma informação preditiva ao profissional de saúde, que pode utilizá-la como apoio para sua própria decisão.

Por isso, o trabalho está mais próximo de um **Sistema de Apoio à Decisão Clínica** do que de um Sistema de Recomendação.

---

## Sistema de Apoio à Decisão x Sistema de Recomendação

### Sistema de Apoio à Decisão

Um Sistema de Apoio à Decisão fornece informações, análises, classificações ou estimativas para auxiliar um profissional na tomada de decisão.

No TCC, a IA apresenta ao profissional:

- dados da anamnese;
- probabilidade percentual de doença cardíaca;
- classificação de risco;
- indicativo de pré-diagnóstico.

A decisão final continua sendo responsabilidade do profissional de saúde.

Portanto, o trabalho pode ser classificado principalmente como um **Sistema de Apoio à Decisão Clínica**.

### Sistema de Recomendação

Um Sistema de Recomendação procura indicar uma ação, item ou alternativa considerada adequada para determinado contexto.

Na área da saúde, por exemplo, poderia recomendar:

- um exame;
- um tratamento;
- uma conduta clínica;
- um medicamento;
- uma intervenção.

O protótipo apresentado no TCC **não realiza diretamente esse tipo de recomendação**.

---

## Predição x Previsão

| Conceito | Definição | Relação com o TCC |
|---|---|---|
| **Predição** | Estima uma classe, resultado ou probabilidade desconhecida utilizando dados disponíveis. | **Sim.** O sistema estima a probabilidade de doença cardíaca com base nos dados da anamnese. |
| **Previsão** | Estima um acontecimento ou valor futuro, geralmente considerando comportamento ao longo do tempo. | **Não diretamente.** O sistema não trabalha com séries temporais ou evolução futura da condição clínica. |

---

## Relação geral entre os conteúdos da disciplina e o TCC

O fluxo principal do trabalho pode ser relacionado aos conteúdos estudados da seguinte forma:

```text
ANAMNESE DO PACIENTE
        ↓
Coleta de dados clínicos
        ↓
BASE DE AMOSTRAS
Heart Disease Dataset
10.000+ registros
        ↓
APRENDIZADO DE MÁQUINA
Decision Tree Classifier
        ↓
RECONHECIMENTO DE PADRÕES
        ↓
PREDIÇÃO
Probabilidade de doença cardíaca
        ↓
PRÉ-DIAGNÓSTICO
        ↓
SISTEMA DE APOIO À DECISÃO
        ↓
PROFISSIONAL DE SAÚDE
Decisão clínica final
```

---

## Síntese da classificação do trabalho

| Item estudado | Presente no TCC? | Como aparece |
|---|---|---|
| Medicina | **Sim** | Anamnese e avaliação de doença cardíaca |
| Diagnóstico | **Sim** | Indicativo de pré-diagnóstico |
| Monitoramento / Sensoriamento | **Não** | Não existe coleta contínua ou sensores |
| Predição | **Sim** | Probabilidade de presença de doença cardíaca |
| Previsão | **Não diretamente** | Não estima evolução futura no tempo |
| Recomendação | **Parcialmente** | Fornece apoio à decisão, mas não recomenda tratamentos |
| Aprendizado de Máquina | **Sim** | Decision Tree Classifier |
| Reconhecimento de padrões | **Sim** | Correlação entre atributos clínicos e doença cardíaca |
| Base de amostras para treinamento | **Sim** | Heart Disease Dataset |
| Redes Neurais | **Não** | Não implementadas |
| Processamento de Linguagem Natural | **Somente teórico/futuro** | LLM, RAG, Whisper etc. não foram implementados |
| Sistemas Multiagentes | **Não** | Não implementados |
| Sistema de Apoio à Decisão | **Sim** | Probabilidade e pré-diagnóstico para auxiliar o profissional |
| Sistema de Recomendação | **Não diretamente** | Não indica tratamento, medicamento ou procedimento |

---



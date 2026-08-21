# Tecnologias Inteligentes Aplicadas à Saúde - Anotações da Semana 1

## 1. Predição vs. Previsão

**Predição** e **Previsão** parecerem a mesma coisa, mas dentro da área de IA elas representam objetivos diferentes.

### Predição

A **predição** busca determinar ou classificar um resultado a partir dos dados disponíveis.

Normalmente temos informações de entrada sobre um paciente e queremos que um modelo identifique a qual classe ou situação aquele paciente pertence.

**Exemplo na saúde:**

Um sistema recebe informações de um exame de um tumor e tenta classificá-lo como:

* **Benigno**
* **Maligno**

Nesse caso, o objetivo principal não é descobrir **quando** alguma coisa acontecerá, mas identificar uma condição a partir dos dados disponíveis.

Do ponto de vista da Ciência da Computação, isso pode ser realizado através de técnicas de **Machine Learning**, especialmente algoritmos de classificação.

Exemplo simplificado:

```text
Dados do paciente/exame
        ↓
Modelo de Machine Learning
        ↓
Classificação
        ↓
Benigno ou Maligno
```

Outros exemplos:

* Predizer se um paciente possui determinada doença.
* Classificar um paciente como baixo, médio ou alto risco.
* Identificar se uma imagem contém sinais de uma determinada patologia.
* Predizer a possibilidade de reinternação de um paciente.

---

### Previsão

A **previsão** está relacionada principalmente com a estimativa de algo que acontecerá **no futuro**, portanto existe uma relação importante com o **tempo**.

Exemplo:

> Quantos leitos de UTI provavelmente serão necessários na próxima semana?

Nesse caso, podem ser utilizados dados históricos:

```text
Semana 1 → 70 leitos utilizados
Semana 2 → 74 leitos utilizados
Semana 3 → 81 leitos utilizados
Semana 4 → 85 leitos utilizados
                ↓
        Modelo de previsão
                ↓
Semana 5 → aproximadamente 90 leitos
```

Esse tipo de problema pode envolver **séries temporais**, em que dados coletados ao longo do tempo são utilizados para estimar valores futuros.

Outros exemplos:

* Prever número de internações no próximo mês.
* Prever demanda de medicamentos.
* Prever evolução de casos de determinada doença.
* Prever demanda hospitalar durante determinado período.

### Diferença principal

Podemos resumir da seguinte maneira:

**Predição → "O que é / qual é a classe ou resultado?"**

**Previsão → "O que provavelmente acontecerá no futuro?"**

---

# 2. Reconhecimento de Padrões

O **Reconhecimento de Padrões** é uma área muito importante da Inteligência Artificial.

A ideia consiste em utilizar dados para identificar **características, relações ou comportamentos que se repetem**.

Na saúde existe uma grande quantidade de dados que pode ser utilizada para isso, como:

* idade;
* peso;
* pressão arterial;
* frequência cardíaca;
* resultados de exames;
* histórico de doenças;
* medicamentos utilizados;
* internações anteriores;
* informações presentes em prontuários.

Um algoritmo pode analisar essas informações e encontrar relações que seriam difíceis de perceber manualmente quando existe uma quantidade muito grande de pacientes.

### Exemplo

Imagine uma base contendo milhares de pacientes:

```text
Paciente | Idade | Pressão | Glicose | Histórico | Diagnóstico
---------------------------------------------------------------
A        | 65    | Alta    | Alta    | Sim       | Doença X
B        | 25    | Normal  | Normal  | Não       | Saudável
C        | 70    | Alta    | Alta    | Sim       | Doença X
...
```

Um algoritmo pode identificar que determinadas combinações de características aparecem frequentemente em pacientes que desenvolveram determinada doença.

Isso permite construir modelos capazes de reconhecer esses padrões em novos pacientes.

---

## Dados estruturados

**Dados estruturados** são informações organizadas seguindo uma estrutura definida, normalmente representadas através de tabelas, campos ou registros.

Por exemplo:

```text
Paciente
├── nome
├── idade
├── peso
├── pressão arterial
├── glicemia
└── diagnóstico
```

Um banco de dados SQL é um exemplo clássico de armazenamento de dados estruturados.

Na saúde, podem existir dados estruturados em:

* Prontuários Eletrônicos de Saúde;
* históricos de pacientes;
* resultados laboratoriais;
* registros de internações;
* informações sobre medicamentos;
* sinais vitais armazenados em sistemas.

A Inteligência Artificial pode utilizar essas bases para encontrar padrões e posteriormente realizar **classificações, predições ou previsões**.

---

# 3. Sistema de Recomendação vs. Sistema de Apoio à Decisão

Os dois tipos de sistemas utilizam informações para ajudar o usuário, mas possuem objetivos diferentes.

## Sistema de Recomendação

Um **Sistema de Recomendação** tenta sugerir algo que seja relevante para determinado usuário.

Um exemplo conhecido é a **Netflix**, que analisa informações como histórico de visualizações e preferências para recomendar filmes e séries.

De maneira simplificada:

```text
Perfil do usuário
        +
Histórico/comportamento
        ↓
Sistema de Recomendação
        ↓
Sugestões personalizadas
```

Na saúde, um sistema desse tipo poderia recomendar:

* hábitos mais saudáveis;
* exercícios;
* conteúdos educativos;
* trilhas de cuidado;
* ações de prevenção.

Por exemplo, dependendo das informações de uma pessoa, o sistema poderia recomendar atividades relacionadas à melhoria da qualidade de vida.

É importante que recomendações relacionadas à saúde sejam tratadas com cuidado, pois uma recomendação computacional não deve automaticamente substituir a avaliação de um profissional.

---

# 4. Sistema de Apoio à Decisão

Um **Sistema de Apoio à Decisão** não necessariamente toma a decisão pelo profissional.

Seu objetivo é fornecer **informações, análises ou alertas que auxiliem na tomada de decisão**.

Na área médica isso é particularmente importante porque a decisão final pode continuar sendo responsabilidade do profissional de saúde.

### Exemplo

Imagine que um médico tente prescrever dois medicamentos.

O sistema identifica que existe uma interação conhecida entre eles:

```text
Médico prescreve:
Medicamento A
      +
Medicamento B
      ↓
Sistema analisa a combinação
      ↓
⚠ Possível interação medicamentosa
      ↓
Informação apresentada ao médico
      ↓
Médico avalia e toma a decisão
```

O sistema está **apoiando a decisão**, e não necessariamente decidindo pelo médico.

Outros exemplos:

* alertas sobre alergias;
* identificação de possíveis interações medicamentosas;
* apresentação de fatores de risco;
* auxílio na interpretação de exames;
* indicação de informações relevantes do histórico do paciente.

---

# 5. Principais Áreas de Atuação das Tecnologias Inteligentes na Saúde

As tecnologias inteligentes podem ser aplicadas em diferentes áreas dentro da saúde.

## 5.1 Recomendação

Utilização de sistemas inteligentes para sugerir ações ou conteúdos personalizados.

Exemplos:

* hábitos saudáveis;
* exercícios;
* conteúdos de bem-estar;
* trilhas de cuidados;
* acompanhamento personalizado.

A recomendação pode considerar características e histórico do usuário para produzir sugestões mais adequadas ao seu perfil.

---

## 5.2 Predição e Previsão

### Predição

Busca identificar um resultado ou risco com base nos dados disponíveis.

Exemplo:

```text
Dados clínicos
     ↓
Modelo
     ↓
Risco de doença
```

### Previsão

Busca estimar acontecimentos futuros considerando também uma dimensão temporal.

Exemplo:

```text
Histórico de internações
        ↓
Modelo de previsão
        ↓
Estimativa de internações
para o próximo mês
```

Essas técnicas podem ser utilizadas tanto para pacientes individuais quanto para planejamento hospitalar e epidemiológico.

---

# 6. Diagnóstico

A Inteligência Artificial também pode ser utilizada como ferramenta de **auxílio ao diagnóstico**.

Um exemplo importante é a análise de imagens médicas.

Podem ser analisadas imagens provenientes de:

* Raio-X;
* tomografia;
* ressonância magnética;
* ultrassonografia;
* outras modalidades de exames.

Algoritmos de Inteligência Artificial, principalmente técnicas de **Machine Learning e Deep Learning**, podem aprender padrões presentes nessas imagens.

Exemplo:

```text
Imagem de Raio-X
       ↓
Modelo de IA
       ↓
Reconhecimento de padrões
       ↓
Possível alteração detectada
       ↓
Profissional avalia o resultado
```

A IA pode funcionar como uma ferramenta adicional para auxiliar o profissional na identificação de alterações.

---

# 7. Monitoramento e Sensoriamento

Outra aplicação importante é o acompanhamento contínuo das condições de um paciente.

Isso pode ser feito através de **sensores e dispositivos wearables**.

### Wearables

*Wearable* significa basicamente uma tecnologia que pode ser **vestida ou utilizada junto ao corpo**.

Exemplos:

* smartwatch;
* pulseiras inteligentes;
* sensores cardíacos;
* sensores de glicose;
* dispositivos de monitoramento médico.

Esses dispositivos podem coletar informações como:

```text
Paciente
   ↓
Sensores / Wearable
   ↓
Frequência cardíaca
Oxigenação
Temperatura
Movimentação
etc.
   ↓
Sistema
   ↓
Análise dos dados
   ↓
Possível alerta
```

Por exemplo, caso um dispositivo detecte uma alteração significativa na frequência cardíaca, essa informação pode ser enviada para um sistema responsável pelo acompanhamento.

---

## IoT na saúde

Nesse contexto também aparece o conceito de **IoT — Internet of Things (Internet das Coisas)**.

IoT consiste na utilização de dispositivos físicos conectados capazes de **coletar e trocar informações através de uma rede**.

Na saúde, podemos ter:

```text
Sensor
   ↓
Coleta dados do paciente
   ↓
Internet/Rede
   ↓
Servidor / Sistema
   ↓
Processamento dos dados
   ↓
Profissional de saúde
```

Isso possibilita o **monitoramento remoto de pacientes**, evitando que toda coleta de informações precise acontecer presencialmente.

---

# Para lembrar/revisar rapidamente

* **Predição:** identificar ou classificar um resultado a partir dos dados.
* **Previsão:** estimar acontecimentos futuros, normalmente considerando uma dimensão temporal.
* **Reconhecimento de padrões:** encontrar relações e características recorrentes em grandes conjuntos de dados.
* **Dados estruturados:** informações organizadas em campos e registros, como dados armazenados em bancos relacionais.
* **Sistema de recomendação:** sugere opções ou ações de acordo com informações do usuário.
* **Sistema de apoio à decisão:** fornece informações e análises para auxiliar um profissional na tomada de decisão.
* **Diagnóstico:** IA pode auxiliar na identificação de doenças e alterações, inclusive através da análise de imagens médicas.
* **Monitoramento e sensoriamento:** sensores, IoT e dispositivos wearables permitem acompanhar continuamente informações sobre o paciente.


A ideia principal é que a tecnologia pode ser utilizada não apenas para armazenar informações médicas, mas também para **analisar dados, reconhecer padrões, gerar alertas, realizar estimativas e fornecer informações que auxiliem profissionais da saúde**.

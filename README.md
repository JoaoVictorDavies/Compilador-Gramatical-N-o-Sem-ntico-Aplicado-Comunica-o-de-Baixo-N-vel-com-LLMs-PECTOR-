# Pector

**Pector** é um projeto experimental de engenharia de linguagem, métodos formais e interação com Modelos de Linguagem.

Ele pode ser definido como um **protocolo/compilador gramatical não semântico aplicado à comunicação com LLMs**.

A proposta do Pector não é criar uma nova inteligência artificial, nem substituir modelos como GPT, Claude, Gemini ou Llama. O objetivo é criar uma camada intermediária, determinística e de escopo fechado entre a linguagem humana e sistemas que interpretam, transformam ou executam instruções.

Em termos simples:

```txt
linguagem humana → Pector → protocolo formal → LLM / automação / análise posterior
```

O Pector tenta estruturar formalmente uma instrução antes que ela seja enviada para uma LLM.

---

## Status atual

O Pector está em fase de MVP experimental.

Atualmente, ele roda localmente como um sistema modular em Python. A ativação do motor principal é feita pelo arquivo `main.py`, normalmente executado em ambiente de desenvolvimento local.

O sistema processa uma entrada em linguagem natural, aplica uma lógica própria de slots gramaticais e gera automaticamente um arquivo `.pec` nas pastas locais do projeto.

O uso atual ainda é manual:

```txt
1. escrevo ou colo uma instrução em linguagem natural
2. rodo o motor via main.py
3. o Pector gera um arquivo .pec
4. copio a saída
5. uso essa saída como camada intermediária em uma LLM
```

O projeto ainda não possui integração automática com LLMs, API pública ou interface final.

---

## Por que o Pector existe

O Pector nasceu de um incômodo prático: muitas vezes, uma LLM responde bem, mas não preserva completamente a estrutura do que foi dito.

Em instruções humanas complexas, partes importantes podem se perder:

* uma negação;
* uma exceção;
* uma condição;
* uma adversativa;
* uma restrição;
* uma mudança de escopo;
* uma tensão entre dois pedidos;
* uma ordem específica de execução.

Isso é especialmente importante em tarefas de software, automação e análise de requisitos, onde retrabalho custa tempo e dinheiro.

O Pector foi criado a partir da seguinte hipótese:

> antes da interpretação probabilística de uma LLM, pode existir uma etapa determinística de estruturação gramatical da instrução humana.

A intenção não é fazer a IA “entender melhor” por mágica.

A intenção é entregar para a IA uma estrutura mais explícita do que foi pedido.

---

## O que o Pector é

O Pector é uma camada de pré-processamento formal para instruções naturais.

Ele recebe uma entrada humana em linguagem natural e gera uma representação intermediária estruturada.

Essa representação pode marcar elementos como:

* núcleos verbais;
* termos nominais;
* operadores negativos;
* operadores adversativos;
* blocos contextuais;
* relações de oposição;
* relações de dependência;
* sequência formal do enunciado.

Exemplo conceitual:

```xml
<modo_enunciativo_exec>
  <nucleo_verbal>crie</nucleo_verbal>
  <termo_nominal>sistema</termo_nominal>

  <operador_adversativo>mas</operador_adversativo>

  <operador_negativo>não</operador_negativo>
  <nucleo_verbal>vire</nucleo_verbal>
  <termo_nominal>ERP</termo_nominal>
</modo_enunciativo_exec>
```

Essa saída não é a resposta final.

Ela é um protocolo intermediário.

---

## O que o Pector não é

O Pector não é uma LLM.

O Pector não é um chatbot.

O Pector não é um agente autônomo.

O Pector não é uma ferramenta comum de prompt engineering.

O Pector não interpreta livremente o significado completo de uma instrução.

O Pector não decide sozinho qual é a melhor solução técnica para um problema.

O Pector não executa comandos críticos.

O Pector não garante segurança por si só.

O Pector não substitui revisão humana, testes, análise técnica ou validação de domínio.

O projeto ainda não deve ser tratado como uma solução madura ou pronta para produção.

Ele é, neste momento, uma pesquisa aplicada em forma de protótipo funcional.

---

## Por que “não semântico”?

O Pector é chamado de **não semântico** porque sua camada inicial não tenta interpretar livremente o significado profundo do texto.

Ele não tenta adivinhar intenção psicológica, contexto externo ou solução ideal.

Ele atua sobre a forma da instrução.

O foco está em elementos como:

* posição;
* verbo;
* alvo;
* negação;
* contraste;
* condição;
* escopo;
* sequência;
* operador;
* slot.

Por exemplo, na frase:

```txt
Não quero usar React, mas posso considerar se facilitar o offline.
```

O Pector não precisa decidir se React é uma boa escolha técnica.

Ele precisa preservar a estrutura formal:

```xml
<operador_negativo>Não</operador_negativo>
<nucleo_verbal>quero usar</nucleo_verbal>
<termo_nominal>React</termo_nominal>

<operador_adversativo>mas</operador_adversativo>

<nucleo_verbal>posso considerar</nucleo_verbal>
<contexto_nominal>se facilitar o offline</contexto_nominal>
```

A decisão técnica pode ficar para uma etapa posterior.

O Pector preserva a forma da instrução.

---

## Lógica de slots

O núcleo do Pector é uma lógica de slots.

A implementação atual usa Python e spaCy, mas a ideia central não depende exclusivamente dessas ferramentas.

A tecnologia automatiza o processo.

A lógica, porém, é formal o suficiente para ser descrita independentemente da implementação.

Uma instrução pode ser observada como uma sequência de relações entre ações, alvos, operadores e contextos:

```txt
operador → núcleo verbal → termo nominal → contexto → restrição → condição
```

Exemplo:

```txt
criar sistema
controlar estoque
gerar relatório
não apagar vendas
```

Pode ser representado como:

```xml
<modo_enunciativo_exec>
  <nucleo_verbal>criar</nucleo_verbal>
  <termo_nominal>sistema</termo_nominal>

  <nucleo_verbal>controlar</nucleo_verbal>
  <termo_nominal>estoque</termo_nominal>

  <nucleo_verbal>gerar</nucleo_verbal>
  <termo_nominal>relatório</termo_nominal>

  <operador_negativo>não</operador_negativo>
  <nucleo_verbal>apagar</nucleo_verbal>
  <termo_nominal>vendas</termo_nominal>
</modo_enunciativo_exec>
```

---

## Modo enunciativo executivo

O modo principal do MVP atual é o `modo_enunciativo_exec`.

Esse modo é usado para instruções em que existe intenção de execução, criação, transformação, organização ou solicitação prática.

A estrutura básica do modo é:

```xml
<modo_enunciativo_exec>
  <nucleo_verbal></nucleo_verbal>
  <termo_nominal></termo_nominal>

  <nucleo_verbal></nucleo_verbal>
  <termo_nominal></termo_nominal>

  <nucleo_verbal></nucleo_verbal>
  <termo_nominal></termo_nominal>
</modo_enunciativo_exec>
```

Essa forma permite representar uma instrução como uma cadeia de relações entre ações e objetos.

A estrutura pode ser enriquecida com negações, adversativas, contextos e condições.

---

## Arquivo `.pec`

A saída atual do Pector é um arquivo `.pec`.

Esse arquivo funciona como um protocolo intermediário.

Ele pode conter:

* versão do protocolo;
* data de geração;
* tipo macro utilizado;
* entrada original;
* estrutura formal gerada;
* marcações aplicadas.

Exemplo de cabeçalho:

```txt
# PECTOR PROTOCOL FILE v1.9
# GENERATED_AT: 2026-05-31 19:14:34
# MACRO_TYPE: MODO_ENUNCIATIVO_EXEC
# INPUT_ORIGINAL: "..."
```

O formato `.pec` ainda está em evolução.

A saída atual é XML-like, mas o formato visual não é o ponto central do projeto.

A mesma lógica poderia ser emitida em outros formatos, como JSON, XML, texto estruturado ou `.pack`.

O ponto central é a estrutura formal gerada.

---

## Motores e versões

O Pector possui versões internas chamadas de motores.

As primeiras versões eram mais monolíticas. Com a evolução do projeto, o sistema passou a ser modular.

A versão modular separa o comportamento em etapas internas, permitindo que cada parte do processo evolua de forma mais controlada.

De forma conceitual, o fluxo pode ser entendido assim:

```txt
entrada natural → análise formal → emissão do protocolo .pec
```

O versionamento é importante porque o projeto está em desenvolvimento experimental.

Cada motor representa uma etapa de amadurecimento da lógica, das regras e da forma de emissão do protocolo.

---

## Arquitetura atual

A arquitetura atual do Pector pode ser resumida assim:

```txt
[Entrada humana]
      ↓
[main.py]
      ↓
[Motor Pector]
      ↓
[Biblioteca de termos]
      ↓
[Lógica de slots]
      ↓
[Emissão do protocolo]
      ↓
[Arquivo .pec salvo localmente]
      ↓
[Uso manual com LLMs]
```

O projeto é modular e pode evoluir para novos formatos, novos modos de análise e integrações futuras.

---

## Tecnologias usadas

A versão atual utiliza:

* Python;
* spaCy;
* lógica própria de slots;
* biblioteca interna de termos;
* regras formais de marcação;
* geração automática de arquivos `.pec`.

O spaCy é usado como apoio ao processamento linguístico.

A lógica central do Pector está na estrutura formal criada sobre a instrução.

---

## Como rodar localmente

O projeto é executado localmente via `main.py`.

Durante o desenvolvimento, o fluxo principal é:

```txt
abrir o projeto no PyCharm
executar main.py
aguardar a geração automática do arquivo .pec
usar a saída gerada conforme necessário
```

Execução via terminal:

```bash
python main.py
```

Dependências básicas:

```bash
pip install -r requirements.txt
python -m spacy download pt_core_news_sm
```

Os comandos podem ser ajustados conforme a organização final do repositório.

---

## O que o MVP faz hoje

O MVP atual consegue:

* rodar localmente;
* processar instruções em português;
* usar apoio linguístico com spaCy;
* aplicar uma biblioteca interna de termos;
* marcar núcleos verbais;
* marcar termos nominais;
* marcar operadores negativos;
* marcar operadores adversativos;
* preservar a sequência do enunciado;
* gerar arquivo `.pec` automaticamente;
* permitir uso manual da saída em LLMs.

---

## O que o MVP ainda não faz

O MVP atual ainda não faz:

* integração automática com LLMs;
* execução de automações;
* interface gráfica final;
* API pública;
* empacotamento como biblioteca Python;
* validação formal completa;
* testes quantitativos robustos;
* suporte maduro a múltiplos idiomas;
* resolução semântica de conflitos;
* tomada de decisão técnica automática;
* garantia de segurança operacional.

Essas limitações são parte do estágio atual do projeto.

---

## Relação com LLMs

O Pector pode ser usado como uma camada anterior à LLM.

Em vez de enviar apenas o texto original, é possível enviar a instrução acompanhada de uma estrutura formal intermediária.

Exemplo de uso:

```txt
Entrada original:
[texto humano]

Protocolo Pector:
[arquivo .pec]

Tarefa da LLM:
responder respeitando os núcleos verbais, termos nominais, negações,
adversativas, condições e restrições preservadas no protocolo.
```

A hipótese é que isso pode ajudar em:

* preservação de restrições;
* redução de omissões;
* controle de escopo;
* rastreabilidade;
* comparação entre entrada e resposta;
* segurança em interação com LLMs;
* redução de retrabalho em tarefas operacionais.

---

## Interação segura com LLMs

O Pector também é uma investigação prática sobre interação segura com LLMs.

Uma camada formal anterior pode ajudar a explicitar:

* o que foi pedido;
* o que foi negado;
* o que foi condicionado;
* o que foi colocado como exceção;
* quais operadores relacionam partes do pedido;
* quais trechos precisam ser preservados pela etapa posterior.

Isso não torna uma LLM automaticamente segura.

Mas pode funcionar como uma peça dentro de uma arquitetura maior de controle, validação e auditoria.

---

## Diferença entre Pector e prompt engineering

Prompt engineering geralmente tenta escrever uma instrução melhor para uma IA.

O Pector tenta criar uma etapa anterior à instrução final.

```txt
Prompt engineering:
melhorar a frase para a IA.

Pector:
estruturar formalmente a frase antes da IA.
```

O Pector não é apenas uma forma de escrever prompts melhores.

Ele é uma tentativa de criar um protocolo intermediário entre linguagem humana e sistemas probabilísticos.

---

## Diferença entre Pector e uma LLM

Uma LLM interpreta, infere, completa e gera.

O Pector marca, organiza, separa e emite.

```txt
LLM:
interpretação probabilística e geração.

Pector:
estruturação formal e emissão de protocolo.
```

Eles não são concorrentes.

O Pector pode ser usado antes de uma LLM.

---

## Limitações conhecidas

O Pector ainda é um MVP experimental.

Limitações atuais:

* a execução ainda é local;
* o uso com LLMs ainda é manual;
* a saída `.pec` ainda pode mudar;
* a biblioteca de termos ainda está em evolução;
* o versionamento dos motores ainda precisa ser melhor documentado;
* a lógica de slots ainda precisa de mais testes;
* alguns termos compostos podem ser marcados de forma imprecisa;
* alguns contextos podem precisar de revisão humana;
* ainda não há avaliação quantitativa ampla;
* ainda não há integração automática com ferramentas externas.

Essas limitações são importantes.

O projeto não é apresentado como uma solução final, mas como uma pesquisa aplicada em andamento.

---

## Roadmap

Próximos passos possíveis:

* organizar melhor o repositório;
* documentar os motores e versões;
* documentar a biblioteca interna de termos;
* melhorar a especificação do `.pec`;
* adicionar exemplos controlados;
* criar testes simples para entradas conhecidas;
* comparar respostas de LLMs com e sem Pector;
* melhorar reconhecimento de termos compostos;
* separar melhor ação, alvo, contexto, restrição e condição;
* criar uma interface simples de entrada e saída;
* estudar exportação para JSON ou `.pack`;
* investigar uso em fluxos de interação segura com LLMs.

---

## Perguntas de pesquisa

O Pector tenta investigar perguntas como:

* É possível criar uma camada determinística entre linguagem humana e LLMs?
* Até onde uma instrução natural pode ser estruturada sem interpretação semântica aberta?
* Como preservar negações, exceções e adversativas antes da resposta da IA?
* Como reduzir retrabalho em tarefas mediadas por LLMs?
* Como tornar instruções humanas mais auditáveis?
* Como separar estrutura, interpretação e execução?
* Como usar LLMs de forma mais segura em fluxos operacionais?

---

## Possíveis aplicações

O Pector pode ser explorado em:

* preparação de instruções para LLMs;
* análise de requisitos;
* estruturação de briefings;
* documentação de escopo;
* automação assistida por IA;
* estudo de segurança em agentes;
* comparação de respostas com e sem protocolo;
* pipelines de validação;
* pesquisa em interação humano-LLM.

---

## Uso não recomendado

O Pector ainda não deve ser usado sozinho para:

* executar comandos críticos;
* controlar infraestrutura real sem validação;
* tomar decisões jurídicas;
* tomar decisões médicas;
* tomar decisões financeiras;
* substituir revisão humana;
* garantir segurança de agentes;
* substituir testes de software;
* substituir análise técnica completa.

---

## Origem do nome

O nome Pector nasce de uma referência indireta à Clarice Lispector e à ideia da palavra como isca da ideia.

A palavra, nesse sentido, não é apenas uma superfície. Ela pode ser uma isca para capturar uma estrutura mais profunda do pensamento.

O Pector parte dessa intuição:

```txt
a instrução humana é a isca;
o protocolo tenta revelar a estrutura formal que ela carrega.
```

O projeto não possui relação oficial com Clarice Lispector.

A referência é conceitual.

---

## Objetivo de longo prazo

O objetivo de longo prazo do Pector é amadurecer como uma camada formal intermediária para comunicação entre humanos e sistemas baseados em IA.

A ambição não é criar uma IA mais inteligente.

A ambição é criar uma forma mais controlada de preparar a linguagem humana antes que ela seja entregue a sistemas inteligentes.

```txt
menos improviso na entrada,
mais estrutura antes da geração.
```

---

## Autor

Desenvolvido por **João Davies**.

Projeto experimental de engenharia de linguagem, métodos formais e interação segura com LLMs.

LinkedIn: [ https://www.linkedin.com/in/joaodavies-/ ]

---

## Nota final

O Pector é um projeto em construção.

Ele não é uma promessa de solução universal.

Ele é uma investigação prática sobre uma hipótese:

> talvez parte do problema da comunicação com LLMs não esteja apenas no modelo, mas na ausência de uma camada formal antes do modelo.

O Pector nasce nesse espaço.

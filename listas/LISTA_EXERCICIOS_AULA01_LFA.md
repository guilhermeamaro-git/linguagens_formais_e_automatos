# Lista de Exercícios — Aula 01

## Linguagens Formais e Autômatos

**Tema:** sintaxe, semântica e análise de código  
**Professor:** __________________________________________  
**Aluno(a):** Guilherme Amaro de Castro 
**Turma:** ENGCDM3B-MDC078-20262 **Data:** 09/08/2026

---

## Objetivos

Ao concluir esta lista, você deverá ser capaz de:

- diferenciar sintaxe e semântica;
- reconhecer problemas de escrita, concordância e ordenação;
- classificar erros básicos em trechos de código;
- explicar como o contexto altera o significado;
- distinguir um erro detectado pelo compilador de um erro lógico;
- ordenar as etapas iniciais do processamento realizado por um compilador.

## Orientações

1. Leia cada enunciado com atenção.
2. Não apresente apenas a classificação: escreva uma justificativa curta.
3. Nos exemplos de programação, considere a seguinte pseudolinguagem:
   - `inteiro`, `real` e `lógico` representam tipos;
   - `:=` é o operador de atribuição;
   - variáveis precisam ser declaradas antes do uso;
   - a forma condicional é `se condição então comando`.
4. Quando mais de uma classificação for defensável, indique o critério utilizado.

> **Nota conceitual:** na língua natural, um problema como “vou corre” é mais precisamente um erro gramatical ou de forma verbal. Na análise de compiladores, **erro léxico** possui um sentido técnico: ocorre quando uma sequência de caracteres não pode ser reconhecida como um token válido.

---

## Exercício 1 — Classificação em linguagem natural

Classifique cada sentença utilizando uma das categorias:

- **A — Adequada:** construção sintaticamente adequada no português usual;
- **B — Problema sintático:** problema de ordem, concordância ou estrutura;
- **C — Problema de formação/escrita:** palavra escrita ou flexionada de forma inadequada para o contexto.

| Item | Sentença | Classificação | Justificativa |
|---:|---|:---:|---|
| 1 | “As flores são belas.” | A | A frase obedece perfeitamente às regras gramaticais e de concordância do português. |
| 2 | “As flores é bela.” | B | O sujeito no plural exige exige o verbo e adjetivo no plural. Diante disso, houve um problema de concordância sintática. |
| 3 | “Vou corre hoje no parque.” | C | A palavra corre está flexionada incorretamente, o correto seria o infinitivo "correr". |
| 4 | “Água bebeu José.” | A | Embora a ordem seja indireta (Objeto-Verbo-Sujeito), é uma construção sintaticamente permitida e compreensível. |
| 5 | “O aluno acabou a prova.” | A | Estrutura padrão (Sujeito-Verbo-Objeto) perfeitamente adequada. |

### Questões complementares

1. A sentença do item 4 é impossível em português ou apenas incomum na ordem mais frequente? Explique.

   **Resposta:**  
   É apenas incomum. A língua portuguesa permite flexibilidade na ordem dos elementos da frase. A ordem direta padrão é Sujeito-Verbo-Objeto ("José bebeu água"), mas a ordem Objeto-Verbo-Sujeito ("Água bebeu José") é perfeitamente válida e compreensível.

2. Reescreva todas as sentenças problemáticas de maneira adequada ao português usual.

   **Resposta:**  
   Item 2: "As flores são belas."
   Item 3: "Vou correr hoje no parque."
   Item 4 (passando para a ordem mais usual, embora não estivesse "errada"): "José bebeu água."

---

## Exercício 2 — Sintaxe e semântica na programação

Analise os trechos abaixo. Classifique o problema predominante como:

- **S — Sintático:** a estrutura não segue a gramática da pseudolinguagem;
- **M — Semântico:** a estrutura pode ser reconhecida, mas seus elementos não são válidos ou compatíveis;
- **V — Válido:** não há erro considerando apenas as regras fornecidas.

> Alguns compiladores podem classificar determinadas situações em fases diferentes. Considere as regras da pseudolinguagem apresentadas no início da lista.

### Item 1

```text
45 := a;
```

Classificação: S

Justificativa:  
Na maioria das gramáticas de programação, a regra de atribuição exige que o lado esquerdo seja um identificador válido (variável) capaz de receber um valor, e não uma constante. O formato inverteu a regra estrutural.

### Item 2

```text
então (a < 10) se;
```

Classificação: S

Justificativa:  
A estrutura condicional fornecida nas instruções exige o formato "se condição então comando". As palavras-chave estão fora de ordem, violando as regras gramaticais (sintaxe) da linguagem.

### Item 3

```text
inteiro soma;
soma := 4.5;
```

Classificação: M

Justificativa:  
A estrutura sintática de declaração e atribuição está correta, mas há uma incompatibilidade de tipos no contexto (tentativa de atribuir um valor real a uma variável definida como inteira).

### Item 4

```text
media := 10.0;
```

Considere que `media` não foi declarada anteriormente.

Classificação: M

Justificativa:  
O comando possui a forma correta (<id> := <expressão>), mas falha na análise de contexto (semântica estática). A regra determina que variáveis precisam ser declaradas antes do uso; ao consultar a tabela de símbolos, o compilador não encontrará media.

### Item 5

```text
real media;
media := 10.0;
```

Classificação: V

Justificativa:  
A variável foi declarada, o tipo de dado (real) é compatível com o valor atribuído (10.0) e a sintaxe está correta.
### Item 6

```text
se a < 10 então
    a := a + 1;
```

Considere que `a` foi declarada como inteira.

Classificação: V

Justificativa:  
A estrutura condicional foi respeitada, as variáveis estão declaradas e as operações matemáticas fazem sentido para o tipo inteiro.

---

## Exercício 3 — Ambiguidade e contexto

Explique a classe gramatical e o significado da palavra destacada em cada frase.

### Caso A — “caminho”

1. “Eu **caminho** todos os dias.”
2. “O **caminho** é longo.”

**Explicação:**  
1. Em "Eu caminho", trata-se de um verbo conjugado na 1ª pessoa do singular
2. Em "O caminho", trata-se de um substantivo. A classe muda dependendo dos elementos vizinhos.

### Caso B — “colher”

1. “Vou **colher** flores.”
2. “A **colher** caiu no chão.”

**Explicação:**  
1. A classe muda dependendo dos elementos vizinhos.
2. Em "O caminho", trata-se de um substantivo. A classe muda dependendo dos elementos vizinhos.

### Caso C — programação

Observe os trechos:

```text
inteiro soma;
soma := 10;
```

```text
função soma(inteiro a, inteiro b)
    retorne a + b;
fim
```

1. O que o nome `soma` representa em cada trecho?
2. Que informações o compilador precisa consultar para interpretar corretamente esse nome?

**Resposta:**  
1. No primeiro trecho, "soma" representa uma variável. No segundo, representa o nome (identificador) de uma função.
2. 2. O compilador precisa consultar a tabela de símbolos. É lá que ele armazena o nome do identificador e seus atributos.

### Debate

Por que um compilador precisa considerar declarações, tipos e escopos para decidir se um código está correto?

**Anotações:**  
Um compilador precisa do contexto porque a estrutura de um código não é suficiente para garantir sua viabilidade. Apenas saber que o código possui o formato (A := B + C) não garante que a operação é possível — é preciso saber se A, B e C existem, se estão acessíveis naquele escopo e se seus tipos permitem a adição e atribuição. Isso evita que o programa realize operações absurdas na memória durante a execução.

---

## Exercício 4 — Validade e erros lógicos

Um aluno desenvolveu um programa para conceder **10% de aumento** ao salário de um funcionário. O código deveria multiplicar o salário por `1.1`, mas foi escrito assim:

```text
real salario;
real novoSalario;

novoSalario := salario * 11;
```

O programa é aceito pelo compilador e executado normalmente.

Responda:

1. O trecho está sintaticamente correto? Justifique.

   **Resposta:**  
   Sim. Ele obedece à gramática da linguagem: as declarações de variáveis possuem o formato <tipo> <id>; e a atribuição tem a estrutura <id> := <expressão>;.

2. Há incompatibilidade de tipos ou uso de variável não declarada no trecho apresentado?

   **Resposta:**  
   Não. As variáveis foram declaradas previamente como reais. A operação matemática envolve variáveis reais e o valor 11.

3. O programa realiza o objetivo proposto? Justifique.

   **Resposta:**  
   Não. O objetivo era dar 10% de aumento. Ao multiplicar por 11, o salário está sofrendo um aumento de 1000%.

4. Classifique o problema como erro sintático, erro semântico estático ou erro lógico.

   **Resposta:**  
   Erro Lógico. O compilador não acusa nenhum problema, mas a matemática aplicada pelo programador não corresponde à regra de negócio desejada.

5. Corrija a linha responsável pelo problema.

```text
novoSalario := salario * 1.1;

```

---

## Exercício 5 — Ordem de processamento

Organize as etapas abaixo na ordem didática mais comum de um compilador:

- análise semântica;
- análise léxica (*scanner*);
- análise sintática (*parser*).

### Parte A — Lista numerada

1. Análise léxica (scanner)
2. Análise sintática (parser)
3. Análise semântica

### Parte B — O que cada etapa recebe e produz?

| Etapa | O que analisa? | Exemplo de problema detectado |
|---|---|---|
| Análise léxica | O agrupamento dos caracteres em unidades válidas(tokens). | Uso de caracteres ilegais ou nomes inválidos (ex: 2var como variável). |
| Análise sintática | A estrutura e ordem dos tokens formados na etapa anterior. | Falta de um ponto e vírgula, parênteses desbalanceados. |
| Análise semântica | O significado/contexto das estruturas (tipos, escopo, declarações). | Uso de variável não declarada, incompatibilidade de tipos. |

### Parte C — Fluxograma

Desenhe um fluxo contendo os seguintes elementos:

```text
Código-fonte → Análise léxica → tokens → Análise sintática → estrutura sintática
            → Análise semântica → código validado para as próximas etapas
```

### Questão de reflexão

Por que a análise semântica normalmente depende dos resultados das análises léxica e sintática?

**Resposta:**  
A análise semântica depende da estrutura construída pelas etapas anteriores. Não é possível verificar se os tipos de uma atribuição batem (semântica) sem antes saber que existe um comando de atribuição ali (sintaxe) e quais são as palavras e símbolos que formam esse comando (léxica). Cada fase abstrai o código em um nível mais alto de compreensão.

---

## Desafio opcional — Crie seus próprios exemplos

Crie três pequenos exemplos:

1. uma frase ou código com problema de escrita/tokenização; 
2. uma construção com erro sintático;
3. um programa sintaticamente válido, mas com erro lógico.

Para cada exemplo, apresente a classificação e a justificativa.

---

## Síntese

Complete:

- **Léxico** está relacionado a identificar e classificar palavras ou símbolos individuais como válidos (formação de tokens).
- **Sintaxe** está relacionada a avaliar a estrutura gramatical e a ordem em que esses tokens foram organizados.
- **Semântica** está relacionada a analisar o significado e a coerência do código usando o contexto (regras de escopo e compatibilidade de tipos).
- **Erro lógico** ocorre quando o código é totalmente válido para o compilador, mas a lógica humana aplicada produz resultados divergentes do objetivo.


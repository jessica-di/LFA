# Lista de Exercícios — Autômatos Finitos Determinísticos (AFD)

> **Disciplina:** Teoria das Linguagens e Autômatos  
> **Tema:** Autômatos Finitos Determinísticos  
> **Modalidade:** Atividade prática em grupo  
> **Objetivo:** identificar, interpretar, construir e testar AFDs.

---

## Identificação do grupo

| Campo | Preenchimento |
|---|---|
| Turma | N1 |
| Data |01/09/2026 |
| Integrante 1 |Jéssica Soares Dias |


## Orientações

- Registre o raciocínio utilizado em cada resposta.
- Nos exercícios com cadeias, apresente o caminho percorrido estado por estado.
- Nos exercícios de construção, entregue a quíntupla, a tabela de transição e o diagrama.
- Use `ε` para representar a cadeia vazia.
- Quando solicitado, implemente e teste o autômato no JFLAP.

---

# Parte 1 — Fundamentos

## Exercício 1 — Entendendo um autômato finito

Uma lâmpada controlada por um interruptor possui os estados `Desligado` e `Ligado`. Sempre que o botão é pressionado, ocorre a mudança:

```text
Desligado --pressionar--> Ligado
Ligado    --pressionar--> Desligado
```

Responda:

1. Quantos estados existem? 2 , ligado e desligado 
2. Qual é o estado inicial, considerando que a lâmpada começa apagada? Desligado 
3. Qual entrada provoca uma transição? Quando o interruptor é pressionado 
4. Partindo de `Desligado`, qual será o estado após um acionamento?   Desligado - pressionar - Ligado 
5. Partindo de `Desligado`, qual será o estado após dois acionamentos?  Desligado - pressionar - Ligado - pressionar - Desligado 
6. Explique o funcionamento do sistema com suas palavras.  O primeiro estado é o desligado , ao pressionar o interruptor , ocorre a transição para ligado 

## Exercício 2 — Porta automática

Uma porta automática possui os estados `Fechado` e `Aberto`. O sensor identifica `pessoa_detectada` ou `nenhuma_pessoa`. Quando uma pessoa é detectada, a porta deve ficar aberta; quando ninguém é detectado, deve ficar fechada.

Complete a tabela:

| Estado atual | Entrada | Próximo estado |
|---|---|---|
| Fechado | pessoa_detectada | Aberto |
| Fechado | nenhuma_pessoa | Fechado|
| Aberto | pessoa_detectada | Aberto |
| Aberto | nenhuma_pessoa | Fechado |

Depois, desenhe o diagrama de estados correspondente e indique o estado inicial.

DIAGRAMA 

Fechado - pessoa detectada - Aberta 
Fechado - nenhuma pessoa   - Fechado 

Aberto - pessoa detectada  - Aberto 
Aberto - nenhuma pessoa    - Fechado


---

# Parte 2 — Anatomia e definição formal

## Exercício 3 — Identificando os elementos

Considere um AFD com `Σ = {0,1}`, `Q = {q0,q1}`, estado inicial `q0`, estado final `q1` e as transições abaixo:

| δ | 0 | 1 |
|---|---|---|
| q0 | q0 | q1 |
| q1 | q0 | q1 |

Identifique e explique:

1. o alfabeto `Σ`; {0,1}  - São os símbolos que o autômato pode utilizar 
2. o conjunto de estados `Q`; {q0,q1} -  São os estados que o autômato pode variar 
3. o estado inicial; -  Q0 
4. o conjunto de estados finais `F`;  - {q1}
5. os símbolos que podem ser lidos; - 0 e 1 
6. o significado do círculo duplo em um diagrama; - Significa que ele chegou ao seu estado final 
7. o significado da seta sem origem apontando para um estado. - Significa que o autômato está em seu estado inicial 

## Exercício 4 — A quíntupla do AFD

Um AFD é formalmente representado por:

```text
M = (Σ, Q, δ, q0, F)
```

Complete:

| Elemento | Significado |
|---|---|
| `Σ` | Alfabeto  | 
| `Q` | Quantidade de estados |
| `δ` | Transição  |
| `q0` | Estado inicial |
| `F` | Estado final |

Explique por que esses cinco elementos são suficientes para definir o funcionamento de um AFD.
Porque eles determinam:

-quais símbolos podem ser recebidos;   
-quais estados existem;  
-onde o processamento começa;  
-para qual estado o autômato vai após cada símbolo;  
-quais estados representam aceitação.  
-Assim, é possível determinar o comportamento do autômato para qualquer cadeia de entrada.  

---

# Parte 3 — Tabela de transições e cadeias

## Exercício 5 — Interpretando uma tabela

Considere `Σ = {0,1}`, `Q = {q0,q1,q2}`, estado inicial `q0`, `F = {q1}` e:

| δ | 0 | 1 |
|---|---|---|
| q0 | q0 | q1 |
| q1 | q2 | q1 |
| q2 | q1 | q1 |

Responda:

1. Qual é o resultado de `δ(q0,0)`? Q0
2. Qual é o resultado de `δ(q0,1)`? Q1
3. Qual é o resultado de `δ(q1,0)`? Q2
4. Qual é o resultado de `δ(q2,1)`? Q1
5. Qual é o estado de aceitação? Q1
6. Desenhe o diagrama correspondente à tabela.
   
  → q0  
├──0──> q0  
└──1──> ((q1))  

((q1))  
├──0──> q2  
└──1──> ((q1))  
  
q2  
├──0──> ((q1))  
└──1──> ((q1))  

Q1 é o estado final   
8. Justifique por que o autômato é determinístico.   
Porque para cada combinação de estado + símbolo de entrada existe exatamente uma única transição possível.


## Exercício 6 — Aceita ou rejeita?

Utilize o AFD do Exercício 5. Determine se cada cadeia é aceita ou rejeitada:

```text
a) 1
b) 0011001
c) 010010
d) 1101
e) 000011010
```

Para cada cadeia, registre todas as transições. Exemplo:

```text
Cadeia: 01
q0 --0--> q0
q0 --1--> q1
Estado final: q1
Resultado: ACEITA
```

| Cadeia | Caminho percorrido | Estado final | Resultado |
|---|---|---|---|
| `1` |q0 → q1 |q1 |Aceita|
| `0011001` |q0 → q0 → q0 → q1 → q1 → q2 → q1 | q1| Aceita |
| `010010` |q0 → q0 → q1 → q2 → q1 → q1 → q2 | q2| Rejeitada|
| `1101` |q0 → q1 → q1 → q2 → q1 |q1 | Aceita |
| `000011010` |q0 → q0 → q0 → q0 → q0 → q1 → q1 → q2 → q1 → q2 | q2| Rejeitada|

---

# Parte 4 — Construção de AFDs

## Exercício 7 — Cadeias que terminam em `1`

Construa um AFD sobre `Σ = {0,1}` que reconheça todas as cadeias que terminam em `1`.

- Devem ser aceitas: `1`, `01`, `101`, `0001`, `1101`.
- Devem ser rejeitadas: `ε`, `0`, `10`, `100`, `1110`.

Entregue: conjunto de estados, alfabeto, estado inicial, estados finais, tabela, diagrama e teste de pelo menos cinco cadeias.

*Definição formal*  

M = (Σ,Q,δ,q0,F)  

Σ = {0,1}  
Q = {q0,q1}  
q0 = q0  
F = {q1}  
  
*Tabela de transições*   
| δ  | 0 | 1 |
|---|---|---|
| q0 | q0 | q1|
| q1 | q0| q1 | 

*Diagrama*   

→ q0 --1--> ((q1))    
  q0 --0--> q0   
  q1 --0--> q0   
  q1 --1--> q1   
  
*Testes*
Cadeia ε   
Nenhum símbolo é processado.   

Estado final: q0     
Resultado: REJEITA   

Cadeia 1   
q0 --1--> q1   
Resultado: ACEITA   

Cadeia 01   
q0 --0--> q0   
q0 --1--> q1   
Resultado: ACEITA   

Cadeia 100   
q0 --1--> q1   
q1 --0--> q0    
q0 --0--> q0    
Resultado: REJEITA   

Cadeia 1101   
q0 --1--> q1   
q1 --1--> q1    
q1 --0--> q0   
q0 --1--> q1    
Resultado: ACEITA   

## Exercício 8 — Número par de símbolos `1`

Construa um AFD sobre `Σ = {0,1}` que reconheça cadeias com quantidade par de símbolos `1`.

Analise: `ε`, `0`, `1`, `11`, `101`, `1100` e `10101`.

Apresente a definição formal `M = (Σ, Q, δ, q0, F)`, a tabela, o diagrama e o processamento das cadeias. Lembre-se de que basta controlar duas situações: quantidade par ou ímpar de símbolos `1`.

*Estados*    
qP: quantidade par de símbolos 1;   
qI: quantidade ímpar de símbolos 1.  

*Definição formal*  

M = (Σ,Q,δ,qP,F)   

Σ = {0,1}      
Q = {qP,qI}   
q0 = qP   
F = {qP}   

*Tabela de transições*    
| δ  | 0 | 1 |
|---|---|---|
| qP | qP | qI|
| qI | qI| qP |     

O símbolo 0 não altera a quantidade de símbolos 1.   
O símbolo 1 alterna entre quantidade par e ímpar.   

*Diagrama*    

→ ((qP)) --1--> qI   
     ^           |   
     |-----1-----|   

qP --0--> qP    
qI --0--> qI    

*Processamento das cadeias*    
ε   
Estado inicial: qP   
Resultado: ACEITA   
   
0   
qP --0--> qP   
Resultado: ACEITA   
   
1     
qP --1--> qI     
Resultado: REJEITA    

11    
qP --1--> qI   
qI --1--> qP   
Resultado: ACEITA   

101    
qP --1--> qI   
qI --0--> qI   
qI --1--> qP    
Resultado: ACEITA 

1100   
qP --1--> qI   
qI --1--> qP   
qP --0--> qP   
qP --0--> qP   
Resultado: ACEITA   

10101   
qP --1--> qI   
qI --0--> qI   
qI --1--> qP   
qP --0--> qP   
qP --1--> qI    
Resultado: REJEITA   


## Exercício 9 — Pelo menos dois zeros consecutivos

Construa um AFD para:

```text
L(M) = {w ∈ {0,1}* | w possui pelo menos dois 0s consecutivos}
```

- Devem ser aceitas: `00`, `001`, `100`, `1001`, `110011`, `0000`.
- Devem ser rejeitadas: `ε`, `0`, `1`, `01`, `10`, `10101`.

Responda antes de construir:

1. O que o estado inicial representa? - Representa que ainda não encontramos 00 e que não existe um zero pendente imediatamente anterior.
2. O que ocorre quando aparece o primeiro `0`? - O autômato vai para q1, indicando que um 0 foi encontrado.
3. O que ocorre quando outro `0` aparece imediatamente depois? - O autômato encontra 00 e vai para o estado final q2.
4. Depois de encontrar `00`, a cadeia pode deixar de ser aceita? - Não. Depois que 00 aparece, a cadeia continuará contendo dois zeros consecutivos, independentemente dos símbolos seguintes.
5. Quantos estados são necessários? - São necessários 3 estados.

Apresente a quíntupla, a tabela, o diagrama e os testes.

*Definição formal*   
   
M = (Σ,Q,δ,q0,F)   

Σ = {0,1}    
Q = {q0,q1,q2}   
q0 = q0    
F = {q2}    
   
*Tabela de transições*  
  
| δ  | 0 | 1 |
|---|---|---|
| q0 | q1| q0 |
| q1 | q2| q0 |  
| q2 | q2| q2 |   
   
   
*Diagrama*    
    
→ q0 --0--> q1 --0--> ((q2))   
  q0 --1--> q0   
  q1 --1--> q0   
  q2 --0--> q2   
  q2 --1--> q2   
   
*Testes*      
  
00    
q0 --0--> q1   
q1 --0--> q2   
Resultado: Aceita.    
   
001   
q0 --0--> q1   
q1 --0--> q2   
q2 --1--> q2    
Resultado: Aceita.   
    
100    
q0 --1--> q0    
q0 --0--> q1    
q1 --0--> q2     
Resultado: Aceita.    
   
1001    
q0 --1--> q0    
q0 --0--> q1    
q1 --0--> q2    
q2 --1--> q2     
Resultado: Aceita.     
   
110011     
q0 --1--> q0    
q0 --1--> q0    
q0 --0--> q1    
q1 --0--> q2    
q2 --1--> q2    
q2 --1--> q2    
Resultado: Aceita.   
   
0000    
q0 --0--> q1    
q1 --0--> q2    
q2 --0--> q2    
q2 --0--> q2     
Resultado: Aceita.     
  
ε     
Estado final: q0   
Resultado: Rejeita.   
    
0    
q0 --0--> q1    
Resultado: Rejeita.    
    
1    
q0 --1--> q0    
Resultado: Rejeita.    
    
01    
q0 --0--> q1   
q1 --1--> q0    
Resultado: Rejeita.    
    
10    
q0 --1--> q0    
q0 --0--> q1      
Resultado: Rejeita.     
    
10101    
q0 --1--> q0    
q0 --0--> q1     
q1 --1--> q0     
q0 --0--> q1    
q1 --1--> q0    
Resultado: Rejeita.    

---

# Parte 5 — Desafios de modelagem

## Exercício 10 — Semáforo

Modele um semáforo com os estados `Verde`, `Amarelo` e `Vermelho`. Use a entrada `tempo` e represente o ciclo:

```text
Verde → Amarelo → Vermelho → Verde
```

Entregue o diagrama, a tabela de transições, a definição formal e uma explicação do funcionamento. Discuta se há sentido em definir estados de aceitação nesse modelo e justifique a escolha adotada.

*Estados:*       
    
Verde    
Amarelo    
Vermelho    
Entrada:   
     
*tempo*    
Ciclo:    
Verde → Amarelo → Vermelho → Verde

*Tabela de transições*        
| Estado Atual | Entrada | Próximo Estado |
|---|---|---|
| Verde | tempo | Amarelo |
| Amarelo | tempo| Vermelho|
| Vermelho | tempo | Verde |


*Diagrama*    
   
→ Verde --tempo--> Amarelo --tempo--> Vermelho    
     ^                                      |   
     |--------------- tempo ----------------|   
     
*Definição formal*    
     
M = (Σ,Q,δ,q0,F)     

Σ = {tempo}    
Q = {Verde, Amarelo, Vermelho}    
q0 = Verde    
F = {Verde, Amarelo, Vermelho}    

*Transições:*     
    
δ(Verde,tempo) = Amarelo     
δ(Amarelo,tempo) = Vermelho     
δ(Vermelho,tempo) = Verde     

*Funcionamento*       
Cada vez que ocorre a entrada tempo, o semáforo passa para o próximo estado do ciclo.     

*Estados de aceitação*       
Nesse modelo, estados de aceitação não possuem a mesma importância de um AFD usado para reconhecer uma linguagem, pois o objetivo é modelar o funcionamento do semáforo.     

Uma escolha possível é considerar todos os estados como finais:     

F = {Verde, Amarelo, Vermelho}      
Isso ocorre porque, após qualquer quantidade de entradas tempo, o semáforo permanece em um estado válido     

## Exercício 11 — Sistema de login

Modele um sistema com as entradas `senha_correta` e `senha_incorreta`. Uma senha correta autentica o usuário; após três tentativas incorretas, o sistema fica bloqueado.

Determine:

1. todos os estados necessários para contar as tentativas;
2. o alfabeto de entrada;
3. o estado inicial;
4. os estados finais;
5. todas as transições;
6. o comportamento após a autenticação e após o bloqueio.

Responda: apenas os estados `Aguardando`, `Autenticado` e `Bloqueado` são suficientes para controlar três tentativas? Justifique e construa o AFD completo.

O sistema possui as entradas:     
   
senha_correta    
senha_incorreta    
Após três tentativas incorretas, o sistema deve ficar bloqueado.         

*Estados*      
q0: nenhuma tentativa incorreta;    
q1: uma tentativa incorreta;    
q2: duas tentativas incorretas;    
qA: autenticado;    
qB: bloqueado.    

*Alfabeto*     
Σ = {senha_correta, senha_incorreta}    
Estado inicial    
q0    
Estado final    
F = {qA}    

*Tabela de transições*    
| Estado  | Senha_Correta | Senha_Incorreta|
|---|---|---|
| q0 | qA | q1 |
| q1 | qA| q2|
| q2 | qA | qB |
| qA | qA | qA |
| qB | qB | qB |

Diagrama      
→ q0 --senha_incorreta--> q1 --senha_incorreta--> q2 --senha_incorreta--> qB    
  |                         |                         |        
  | senha_correta           | senha_correta           | senha_correta    
  |                         |                         |    
  +-----------------------> ((qA)) <-----------------+           
Após autenticação:   
    
qA --senha_correta--> qA    
qA --senha_incorreta--> qA    
Após bloqueio:    

qB --senha_correta--> qB    
qB --senha_incorreta--> qB    
Definição formal   
M = (Σ,Q,δ,q0,F)    
   
Σ = {senha_correta, senha_incorreta}    
Q = {q0,q1,q2,qA,qB}    
q0 = q0    
F = {qA}     
Apenas Aguardando, Autenticado e Bloqueado são suficientes?    
Não.             
O sistema precisa distinguir entre:            
zero tentativas incorretas;         
uma tentativa incorreta;               
duas tentativas incorretas.     
Somente assim é possível identificar exatamente quando ocorre a terceira tentativa incorreta e bloquear o usuário.       

---

# Parte 6 — Prática no JFLAP

## Exercício 12 — Implementação e testes

Escolha um dos AFDs dos exercícios 7, 8 ou 9 e implemente-o no JFLAP.

1. Crie os estados.
2. Defina o estado inicial e os estados finais.
3. Crie todas as transições.
4. Teste três cadeias que devem ser aceitas.
5. Teste três cadeias que devem ser rejeitadas.
6. Compare os resultados esperados e obtidos.

Inclua um print do AFD, a tabela de testes e uma breve explicação.

Estados    
q0    
q1   
q2    
    
Configuração:    

q0 como estado inicial;    
q2 como estado final.   
    
Transições    
q0 --0--> q1 -- 0 --> q2      
q0 --1--> q0    
q1 --1--> q0   
q2 --0--> q2   
q2 --1--> q2      

Tabela de testes   
| Cadeia | Resultado esperado | Resultado no JFLAP | Conferência |
|---|---|---|---|
|00 |Aceita |Aceita |Correto |
|001 |Aceita |Aceita |Correto |
|100 |Aceita |Aceita |Correto |
|ε |Rejeita |Rejeita |Correto |
|1 |Rejeita |Rejeita |Correto |
|01 |Rejeita |Rejeita |Correto |

---

# Desafio final

## Exercício 13 — Crie seu próprio problema

Escolha uma situação real representável por estados, como elevador, máquina de vendas, controle de acesso, estacionamento, pedido de delivery, semáforo, porta eletrônica ou protocolo de comunicação.

O grupo deverá:

1. descrever o problema e suas regras;
2. identificar as entradas e os estados;
3. definir o estado inicial e os estados finais;
4. criar a tabela de transições;
5. desenhar o AFD;
6. apresentar `M = (Σ, Q, δ, q0, F)`;
7. testar pelo menos cinco sequências de entrada;
8. explicar por que o modelo é determinístico;
9. apresentar uma conclusão sobre o que foi aprendido.

---

# Entregável

O grupo deverá entregar um único arquivo `README.md`, contendo:

- identificação do grupo;
- respostas dos exercícios indicados pela professora;
- diagramas e tabelas de transição;
- processamento estado por estado das cadeias;
- evidência dos testes no JFLAP;
- conclusão do grupo.

## Modelo para o desafio final

```markdown
## Desafio final

### Problema escolhido

### Estados e significado

### Alfabeto

### Estado inicial e estados finais

### Tabela de transições

### Diagrama

### Definição formal
M = (Σ, Q, δ, q0, F)

### Testes realizados
| Entrada | Resultado esperado | Resultado obtido |
|---|---|---|
| | | |

### Evidência no JFLAP

### Conclusão
```

> **Importante:** não basta apresentar o diagrama. Demonstre como o AFD processa cada cadeia, estado por estado, até decidir pela aceitação ou rejeição.

---

**Profa. Kadidja Valéria**

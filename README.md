[Programação Concorrente](https://www.dcc.fc.up.pt/~edrdo/aulas/pc), CC3037, DCC/FCUP

_Eduardo R. B. Marques, DCC/FCUP_


# Exemplos de deadlocks

## 1. Deadlocks "simples" &rarr; `SimpleDeadlocks.java`


Método |Razão para deadlock|Execução|
-------|---------|--------|
`deadlock1()`|não libertação de um lock.|`java SimpleDeadlocks 1`|
`deadlock2()`|espera mútua por término de execução|`java SimpleDeadlocks 2`|
`deadlock3()`|espera mútua por aquisição de lock|`java SimpleDeadlocks 3`|

## 2. Jantar dos filósofos &rarr; `DiningPhilosophers.java`

Execute `java DiningPhilosophers n` onde `n > 2` é o número de "filósofos" / threads.

Pode descomentar a linha com a chamada a `pause(1000)` para reproduzir mais facilmente a situação de deadlock.

## 3. Contagem decrescente &rarr; `[Test]CountDownLatch.java`

`n` &rarr; valor inicial de contagem decrescente (`3` por omissão)

O programa de teste lança `n` threads que chamam `await()` e outras `n` que chamam `countDown()`. 

Classe |Descrição|Teste|
-------|---------|--------|
`CountDownLatch`|Classe com implementação correcta.|`java TestCountDownLatch 0 n`|
`CountDownLatch_Bug1`|Deadlock resultante do uso de `notify()` em vez de `notifyAll()` em `countDown()`.|`java TestCountDownLatch 1 n`|
`CountDownLatch_Bug2`|Deadlock resultante de violação de atomicidade e condição de corrida associada em `countDown()`.|`java TestCountDownLatch 2 n`|
`CountDownLatch_Bug3`|Deadlock resultante de violação de atomicidade e condição de corrida associada em `await()`.|`java TestCountDownLatch 3 n`|
`CountDownLatch_Bug4`|Deadlock resultante de violação de atomicidade dada a "sincronização em dois passos" em `await()`.|`java TestCountDownLatch 4 n`|

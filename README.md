# 💻 MiniCPU - Torneio de Processadores

**Disciplina:** Infraestrutura de Hardware  
**Equipe:** Grupo 12 (Contagem de Pares)  
**Linguagem:** Python   

## 🎯 Sobre o Projeto
Este projeto consiste na implementação de um simulador de uma **MiniCPU** capaz de executar o ciclo clássico de processamento: **FETCH → DECODE → EXECUTE**. 

O simulador possui uma memória de 256 bytes, 4 registradores de propósito geral (R0 a R3), um Program Counter (PC) e uma Zero Flag (ZF). O conjunto de instruções (ISA) é composto por 10 operações básicas (LOAD, STORE, ADD, SUB, MOV, CMP, JMP, JZ, JNZ, HALT).

## 🧩 O Desafio: Contagem de Pares
O objetivo específico da nossa equipe foi resolver o problema de **Contagem de Pares**. 
* **Entrada:** Um array de 8 valores pré-carregados nos endereços `0x10` a `0x17` da memória.
* **Processamento:** O programa deve iterar sobre o array, verificar quais números são pares e contabilizá-los.
* **Saída:** O total de números pares encontrados deve ser salvo no endereço de memória `0x20`.
* **Validação:** Para os dados de teste `[4, 7, 2, 9, 6, 1, 8, 3]`, o resultado esperado em `0x20` é **4**.

## 🚀 Como Resolvemos (A Lógica)

Como a nossa MiniCPU possui um conjunto de instruções bastante reduzido (não possui divisão/módulo e nem endereçamento indireto de memória), utilizamos duas estratégias avançadas de arquitetura para solucionar o desafio:

1. **Checagem de Paridade via Subtração:** Para descobrir se um número é par, o programa carrega o valor e subtrai `2` sucessivamente. Se o valor chegar a `0` (Zero Flag ativada), o número é par e o contador (R3) é incrementado. Se chegar a `1`, é ímpar e o laço é quebrado.

2. **Iteração de Array via Self-Modifying Code (Código Automodificável):**
   Como não temos ponteiros dinâmicos (ex: `LOAD R0, [R1]`), transformamos o endereço de memória `0x20` em uma variável de estado. Lemos a própria instrução de `LOAD`, somamos 1 ao operando de endereço, e salvamos de volta na memória. Assim, o código "reescreve" a si mesmo durante a execução para avançar de `0x10` até `0x17`. Ao final da execução, sobrescrevemos esse ponteiro temporário em `0x20` com o resultado final da contagem!

## 🛠️ Como Executar o Simulador

Certifique-se de ter o Python 3.x instalado em sua máquina.

1. Clone este repositório:
   ```bash
   git clone [https://github.com/biagalindoo/Desafio-FDE.git](https://github.com/biagalindoo/Desafio-FDE.git)

   ## 👥 Autores
* Beatriz Galindo
* Breno Santiago
* Leonardo de Queiroz
* Matheos Guerra
* Victor Paes

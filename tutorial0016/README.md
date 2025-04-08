# 🌟 Tutorial #16 🌟

Neste tutorial, vamos aprender sobre duas estruturas de dados muito importantes: **pilha** e **fila**. Veremos seus conceitos, funcionamento e implementações básicas em **C** e **Python**.

---

## 🧱 Pilha (Stack)

A pilha é uma estrutura do tipo **LIFO (Last In, First Out)**. O último elemento inserido é o primeiro a ser removido.

### 📌 Operações básicas
- `push(x)`: insere um elemento no topo da pilha
- `pop()`: remove e retorna o elemento do topo
- `peek()`: visualiza o topo sem remover

### ✅ Exemplo em Python
```python
pilha = []

# Inserindo elementos
pilha.append(10)
pilha.append(20)
pilha.append(30)

# Removendo elementos
print(pilha.pop())  # 30
print(pilha[-1])    # 20 (peek)
```

### ✅ Exemplo em C
```c
#include <stdio.h>
#define MAX 100

int stack[MAX];
int topo = -1;

void push(int x) {
    if (topo < MAX - 1)
        stack[++topo] = x;
}

int pop() {
    if (topo >= 0)
        return stack[topo--];
    return -1; // pilha vazia
}

int peek() {
    if (topo >= 0)
        return stack[topo];
    return -1;
}
```

---

## 🚦 Fila (Queue)

A fila é uma estrutura **FIFO (First In, First Out)**. O primeiro elemento inserido é o primeiro a sair.

### 📌 Operações básicas
- `enqueue(x)`: insere um elemento no final da fila
- `dequeue()`: remove o elemento da frente

### ✅ Exemplo em Python
```python
from collections import deque

fila = deque()
fila.append(10)
fila.append(20)
fila.append(30)

print(fila.popleft())  # 10
print(fila[0])         # 20
```

### ✅ Exemplo em C com lista encadeada
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct No {
    int valor;
    struct No* prox;
} No;

typedef struct {
    No* inicio;
    No* fim;
} Fila;

void inicializar(Fila* f) {
    f->inicio = f->fim = NULL;
}

void enqueue(Fila* f, int x) {
    No* novo = malloc(sizeof(No));
    novo->valor = x;
    novo->prox = NULL;
    if (f->fim != NULL) {
        f->fim->prox = novo;
    } else {
        f->inicio = novo;
    }
    f->fim = novo;
}

int dequeue(Fila* f) {
    if (f->inicio == NULL) return -1;
    No* temp = f->inicio;
    int val = temp->valor;
    f->inicio = f->inicio->prox;
    if (f->inicio == NULL) f->fim = NULL;
    free(temp);
    return val;
}
```

---


Problemas que podemos usar filas ou pilhas:

- https://judge.beecrowd.com/pt/problems/view/1062
- https://judge.beecrowd.com/pt/problems/view/1340
- https://judge.beecrowd.com/pt/problems/view/1451
- https://judge.beecrowd.com/pt/problems/view/1068
- https://judge.beecrowd.com/pt/problems/view/1077
---

Essas estruturas são fundamentais para a construção de algoritmos eficientes em programação competitiva e no mundo real!

Fiquem ligados para os próximos tutoriais! 💻📚


# 🌟 Tutorial #11 🌟

## 📌 **Listas Encadeadas: Conceito e Implementação**  

### 🔹 **O que é uma Lista Encadeada?**  

Uma **Lista Encadeada** é uma estrutura de dados linear onde os elementos (**nós**) estão conectados por ponteiros. Diferente dos **arrays**, onde os elementos ocupam posições contíguas na memória, em listas encadeadas cada elemento aponta para o próximo, permitindo maior flexibilidade na alocação de memória.  

![](./C_language_linked_list.png)

📌 **Vantagens**:  
✅ Inserções e remoções são mais eficientes, sem necessidade de deslocar elementos.
✅ Uso dinâmico de memória, evitando desperdício.

⚠️ **Desvantagens**:
❌ Acesso mais lento do que arrays, pois precisa percorrer os elementos um por um.

---

## 🔹 **Estrutura de uma Lista Encadeada**  

Cada **nó** contém dois elementos principais:  
- **Dado** (o valor armazenado).  
- **Ponteiro** para o próximo nó.  

📌 **Exemplo de uma Lista Encadeada Simples**:  
```
[10|*] → [20|*] → [30|NULL]
```
Onde `*` representa o ponteiro para o próximo nó e `NULL` indica o fim da lista.

---

## 🔹 **Operações Essenciais**
Agora, vamos cobrir as operações básicas em uma lista encadeada:  

 * **Inserção**: Adicionar um novo nó no início, no final ou em uma posição específica.
 * **Remoção**: Excluir um nó específico.
 * **Busca**: Encontrar um valor dentro da lista.
 * **Contagem de Elementos**:
   - **Maneira Lenta**: Percorrendo toda a lista sempre que precisar.  
   - **Maneira Otimizada**: Mantendo um contador atualizado.  

---

# 💻 **Implementação em C**  

### 📌 **Definição da Estrutura**
```c
#include <stdio.h>
#include <stdlib.h>

// Definição do nó da lista
typedef struct No {
    int dado;
    struct No* proximo;
} No;
```

---

### **Inserindo no Início**
```c
No* inserirInicio(No* cabeca, int valor) {
    No* novoNo = (No*)malloc(sizeof(No));
    novoNo->dado = valor;
    novoNo->proximo = cabeca;
    return novoNo; // O novo nó vira a cabeça da lista
}
```

---

### **Inserindo no Final**
```c
No* inserirFim(No* cabeca, int valor) {
    No* novoNo = (No*)malloc(sizeof(No));
    novoNo->dado = valor;
    novoNo->proximo = NULL;

    if (cabeca == NULL) return novoNo;

    No* atual = cabeca;
    while (atual->proximo != NULL) {
        atual = atual->proximo;
    }
    atual->proximo = novoNo;
    return cabeca;
}
```

---

### **Removendo um Nó**
```c
No* remover(No* cabeca, int valor) {
    if (cabeca == NULL) return NULL;

    if (cabeca->dado == valor) {
        No* temp = cabeca;
        cabeca = cabeca->proximo;
        free(temp);
        return cabeca;
    }

    No* atual = cabeca;
    while (atual->proximo != NULL && atual->proximo->dado != valor) {
        atual = atual->proximo;
    }

    if (atual->proximo != NULL) {
        No* temp = atual->proximo;
        atual->proximo = temp->proximo;
        free(temp);
    }
    return cabeca;
}
```

---

### 🔍 **Buscando um Elemento**
```c
int buscar(No* cabeca, int valor) {
    No* atual = cabeca;
    while (atual != NULL) {
        if (atual->dado == valor) return 1;
        atual = atual->proximo;
    }
    return 0;
}
```

---

### 📊 **Contando Elementos**
#### Método Lento:
```c
int contarElementos(No* cabeca) {
    int contador = 0;
    No* atual = cabeca;
    while (atual != NULL) {
        contador++;
        atual = atual->proximo;
    }
    return contador;
}
```
#### Método Otimizado:
```c
typedef struct Lista {
    No* cabeca;
    int tamanho;
} Lista;

Lista* criarLista() {
    Lista* lista = (Lista*)malloc(sizeof(Lista));
    lista->cabeca = NULL;
    lista->tamanho = 0;
    return lista;
}

void inserirOtimizado(Lista* lista, int valor) {
    No* novoNo = (No*)malloc(sizeof(No));
    novoNo->dado = valor;
    novoNo->proximo = lista->cabeca;
    lista->cabeca = novoNo;
    lista->tamanho++;  // Mantém a contagem atualizada
}

int contarOtimizado(Lista* lista) {
    return lista->tamanho;
}
```
---
Não esqueça de ao final de usar a lista, é necessário liberar sua memória:
```c
void liberaLista(Lista* l){
    No* no = l->cabeca;
    while(no != NULL){
        No* next = no->proximo;
        free(no)
        no = next;
    }
    free(l);
}
```

---

# 🐍 **Implementação em Python**
Em Python, podemos definir listas encadeadas de forma mais simples usando classes.  

---

### 📌 **Definição da Estrutura**
```python
class No:
    def __init__(self, dado):
        self.dado = dado
        self.proximo = None

class ListaEncadeada:
    def __init__(self):
        self.cabeca = None
        self.tamanho = 0  # Para otimizar a contagem de elementos
```

---

### ✅ **Inserindo no Início**
```python
def inserir_inicio(self, valor):
    novo_no = No(valor)
    novo_no.proximo = self.cabeca
    self.cabeca = novo_no
    self.tamanho += 1
```

---

### ✅ **Inserindo no Final**
```python
def inserir_fim(self, valor):
    novo_no = No(valor)
    if self.cabeca is None:
        self.cabeca = novo_no
    else:
        atual = self.cabeca
        while atual.proximo:
            atual = atual.proximo
        atual.proximo = novo_no
    self.tamanho += 1
```

---

### ❌ **Removendo um Nó**
```python
def remover(self, valor):
    if self.cabeca is None:
        return
    
    if self.cabeca.dado == valor:
        self.cabeca = self.cabeca.proximo
        self.tamanho -= 1
        return
    
    atual = self.cabeca
    while atual.proximo and atual.proximo.dado != valor:
        atual = atual.proximo

    if atual.proximo:
        atual.proximo = atual.proximo.proximo
        self.tamanho -= 1
```

---

### 🔍 **Buscando um Elemento**
```python
def buscar(self, valor):
    atual = self.cabeca
    while atual:
        if atual.dado == valor:
            return True
        atual = atual.proximo
    return False
```

---

### 📊 **Contando Elementos**
#### Método Lento:
```python
def contar_elementos(self):
    contador = 0
    atual = self.cabeca
    while atual:
        contador += 1
        atual = atual.proximo
    return contador
```
#### Método Otimizado:
```python
def contar_otimizado(self):
    return self.tamanho
```
---

Em python, diferente de `C`, não é necessário liberar a memória quando ela não é mais usada. 

---

## Variações de listas encadeadas

### Lista circular

Essa variação ao invez do ultimo elemento da lista apontar para `NULL` ele aponta para o primeiro elemento. Isso pode ser bom quando precisamos dar a volta na lista por algum motivo. 

Em relação ao algoritmo, a unica mudança é que ao invez de realizar a comparação com `NULL` para achar o fim da lista, comparamos com o primeiro elemento, ou seja, quando acharmos um nó que o `proximo` é igual ao primeiro elemento, então achamos o ultimo nó.

### Lista duplamente encadeada

Essa lista adicionar mais uma variavel `anterior` em cada nó que aponta para o nó anterior. Isso facilita para podermos navegar na lista na direção inversa. 

---

Agora que você entende o funcionamento, que tal **praticar implementando suas próprias listas encadeadas?** 💡💻
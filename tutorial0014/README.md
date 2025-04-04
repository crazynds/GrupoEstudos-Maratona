# 🌟 Tutorial #14 🌟

A ordenação e a busca são operações fundamentais em programação. Neste tutorial, vamos explorar como ordenar um array utilizando as funções padrão das linguagens **C** e **Python**, e depois entender o funcionamento da **busca binária**.

---

## 🔹 Ordenação de Arrays

### 📌 Ordenando em Python 🐍
Python fornece a função `sorted()` e o método `.sort()` para ordenar listas:

```python
# Usando sorted() (retorna uma nova lista ordenada)
numeros = [5, 2, 9, 1, 5, 6]
numeros_ordenados = sorted(numeros)
print(numeros_ordenados)  # [1, 2, 5, 5, 6, 9]

# Usando sort() (modifica a lista original)
numeros.sort()
print(numeros)  # [1, 2, 5, 5, 6, 9]

# Ordenação em ordem reversa
numeros.sort(reverse=True)
print(numeros)  # [9, 6, 5, 5, 2, 1]
```

📌 **Dica:** Ambos suportam **parâmetros extras** como `reverse=True` para ordenar em ordem decrescente.

📌 **Complexidade**: Tanto `sorted()` quanto `.sort()` utilizam o algoritmo Timsort, que possui complexidade O(n log n).

---

### 📌 Ordenando em C 💻
Em C, utilizamos a função `qsort()` da biblioteca **stdlib.h**:

```c
#include <stdio.h>
#include <stdlib.h>

// Função de comparação para qsort()
int comparar(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

// Função de comparação reversa
int comparar_reverso(const void *a, const void *b) {
    return (*(int*)b - *(int*)a);
}

int main() {
    int numeros[] = {5, 2, 9, 1, 5, 6};
    int tamanho = 6;
    
    // Ordenação normal
    qsort(numeros, tamanho, sizeof(int), comparar);
    printf("Ordem crescente: ");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");

    // Ordenação reversa
    qsort(numeros, tamanho, sizeof(int), comparar_reverso);
    printf("Ordem decrescente: ");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", numeros[i]);
    }
    printf("\n");

    return 0;
}
```

📌 **Dica:** `qsort()` pode ordenar qualquer tipo de dado, basta alterar a função de comparação.

📌 **Complexidade**: `qsort()` usa QuickSort, que tem complexidade média O(n log n).

---

## 🔹 Busca Binária 🔍
A **busca binária** é um algoritmo eficiente para encontrar elementos **em um array ordenado**. Ela divide repetidamente a lista ao meio, reduzindo o espaço de busca.

📌 **Importante:** A **busca binária só funciona se o array estiver ordenado**. Se o array estiver desordenado, a busca pode falhar ou produzir resultados incorretos.

📌 **Funcionamento:**
1. Comparar o elemento buscado com o valor central do array.
2. Se for igual, retorna a posição.
3. Se for menor, busca na metade esquerda.
4. Se for maior, busca na metade direita.
5. Repete até encontrar ou concluir que o elemento não está presente.

📌 **Vantagem sobre a busca linear**: A busca linear percorre cada elemento um por um, tendo complexidade O(n), enquanto a busca binária reduz a quantidade de verificações pela metade a cada iteração, alcançando O(log n), tornando-a muito mais eficiente para grandes conjuntos de dados.


### 📌 Implementação em Python 🐍

```python
def busca_binaria(arr, alvo):
    esquerda, direita = 0, len(arr) - 1
    while esquerda <= direita:
        meio = (esquerda + direita) // 2
        if arr[meio] == alvo:
            return meio  # Retorna o índice
        elif arr[meio] < alvo:
            esquerda = meio + 1
        else:
            direita = meio - 1
    return -1  # Elemento não encontrado

# Exemplo de uso:
numeros = [1, 2, 3, 5, 6, 9]
print(busca_binaria(numeros, 5))  # Retorna o índice do 5
```

### 📌 Implementação em C 💻

```c
#include <stdio.h>

int busca_binaria(int arr[], int tamanho, int alvo) {
    int esquerda = 0, direita = tamanho - 1;
    while (esquerda <= direita) {
        int meio = esquerda + (direita - esquerda) / 2;
        if (arr[meio] == alvo)
            return meio; // Retorna a posição
        else if (arr[meio] < alvo)
            esquerda = meio + 1;
        else
            direita = meio - 1;
    }
    return -1; // Elemento não encontrado
}

int main() {
    int numeros[] = {1, 2, 5, 5, 6, 9};
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);
    int alvo = 5;
    int resultado = busca_binaria(numeros, tamanho, alvo);
    
    if (resultado != -1)
        printf("Elemento encontrado na posição %d\n", resultado);
    else
        printf("Elemento não encontrado\n");
    
    return 0;
}
```

--- 

Problemas que podemos usar busca linear:

- https://judge.beecrowd.com/pt/problems/view/1912
- https://judge.beecrowd.com/pt/problems/view/2715
- https://judge.beecrowd.com/pt/problems/view/2448

Se divirta com os problemas acima!

---

Agora você pode aplicar essas técnicas para otimizar seus programas! 🚀🔥


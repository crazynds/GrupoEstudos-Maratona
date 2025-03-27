
# 🌟 Tutorial #08 🌟

## 📌 Manipulação de Strings e Alocação Dinâmica em C

### Manipulação de Strings em C

Em C, as strings são representadas como **arrays de caracteres** terminados com o caractere nulo (`\0`).

```c
#include <stdio.h>

int main() {
    char nome[50];
    printf("Digite seu nome: ");
    scanf("%49s", nome); // Lê uma palavra
    printf("Olá, %s!\n", nome);
    return 0;
}
```

Se quisermos ler **uma linha inteira**, podemos usar `fgets()`:

```c
#include <stdio.h>

int main() {
    char nome[50];
    printf("Digite seu nome completo: ");
    fgets(nome, 50, stdin); // Lê uma linha
    printf("Olá, %s", nome);
    return 0;
}
```

### Alocação Dinâmica de Memória

A alocação dinâmica permite criar variáveis e vetores de tamanho flexível usando `malloc`, `calloc` e `realloc`.

#### 🔹 Alocação Dinâmica para um Único Inteiro

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int *)malloc(sizeof(int));
    if (ptr == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }
    *ptr = 10;
    printf("Valor: %d\n", *ptr);
    free(ptr);
    return 0;
}
```

#### 🔹 Alocação Dinâmica para Vetores

##### Vetor de `int`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 5;
    int *vetor = (int *)malloc(n * sizeof(int));
    if (vetor == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    // Inicializando valores
    for (int i = 0; i < n; i++) {
        vetor[i] = i * 2;
    }

    // Exibindo valores
    for (int i = 0; i < n; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    free(vetor);
    return 0;
}
```

##### Vetor de `float`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 3;
    float *valores = (float *)malloc(n * sizeof(float));
    if (valores == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    valores[0] = 1.5;
    valores[1] = 2.75;
    valores[2] = 3.9;

    for (int i = 0; i < n; i++) {
        printf("%.2f ", valores[i]);
    }
    printf("\n");

    free(valores);
    return 0;
}
```

#### 🔹 Redimensionamento com `realloc`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 3;
    int *valores = (int *)malloc(n * sizeof(int));
    if (valores == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        valores[i] = i + 1;
    }

    // Redimensionando para 6 elementos
    n = 6;
    valores = (int *)realloc(valores, n * sizeof(int));
    if (valores == NULL) {
        printf("Erro na realocação de memória!\n");
        return 1;
    }

    for (int i = 3; i < n; i++) {
        valores[i] = i + 1;
    }

    for (int i = 0; i < n; i++) {
        printf("%d ", valores[i]);
    }
    printf("\n");

    free(valores);
    return 0;
}
```

---

## 📌 Manipulação de Strings e Listas Dinâmicas em Python

### Manipulação de Strings

Strings em Python são **imutáveis**, ou seja, não podemos alterá-las diretamente.

```python
s = "Python"
print(s[0])  # P
print(s[-1]) # n
print(s[1:4]) # yth
```

#### Concatenar Strings

```python
nome = "João"
sobrenome = "Silva"
nome_completo = nome + " " + sobrenome
print(nome_completo)  # João Silva
```

#### Dividir Strings

```python
frase = "Isso é um exemplo"
palavras = frase.split(" ")
print(palavras)  # ['Isso', 'é', 'um', 'exemplo']
```

### Listas Dinâmicas em Python

Diferente de C, onde precisamos alocar manualmente a memória, em Python as **listas são dinâmicas**.

```python
lista = []  # Lista vazia
lista.append(10)  # Adiciona um elemento
lista.append(20)
lista.append(30)
print(lista)  # [10, 20, 30]
```

#### Removendo Elementos

```python
lista =[10,20,30]
lista.remove(20)  # Remove o primeiro 20 encontrado
print(lista)  # [10, 30]
```

#### Redimensionando Listas

Em Python, listas podem ser redimensionadas automaticamente:

```python

lista = [1, 2, 3]
lista.extend([4, 5, 6])  # Adiciona múltiplos elementos
print(lista)  # [1, 2, 3, 4, 5, 6]
```

---


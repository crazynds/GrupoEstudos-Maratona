# 🌟 Tutorial #12 🌟

## ✨ Introdução
Ao projetar algoritmos e estruturas de dados, é essencial entender a **complexidade de tempo**, que descreve o crescimento do tempo de execução em relação ao tamanho da entrada. A **notação Big-O (O)** nos ajuda a avaliar a eficiência de algoritmos de maneira independente do hardware e da implementação específica.

## 🚀 **Entendendo a Notação O (Big O)**

A **notação O (Big O)** expressa a complexidade assintótica, ou seja, o comportamento do algoritmo quando a entrada cresce indefinidamente. Vamos ver alguns exemplos comuns:

### 🔹 **O(1) - Tempo Constante**

O tempo de execução **não depende do tamanho da entrada**.

```c
int acessar_primeiro_elemento(int vetor[]) {
    return vetor[0]; // Sempre retorna o primeiro elemento, independente do tamanho do vetor.
}
```

**Exemplo real**: Acessar um elemento específico em um array (índice fixo) é O(1).

### 🔹 **O(n) - Tempo Linear**

O tempo de execução **cresce proporcionalmente** ao tamanho da entrada.

```c
void imprimir_todos_elementos(int vetor[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", vetor[i]);
    }
}
```

Se `n = 10`, o loop roda 10 vezes. Se `n = 1.000.000`, roda um milhão de vezes.

**Exemplo real**: Somar todos os elementos de um array.

### 🔹 **O(n²) - Tempo Quadrático**

Para cada elemento, percorremos todos os outros elementos.

```c
void imprimir_pares(int vetor[], int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("(%d, %d)\n", vetor[i], vetor[j]);
        }
    }
}
```

Se `n = 10`, temos `10 × 10 = 100` operações. Se `n = 1.000`, teremos **1.000.000 operações!**

**Exemplo real**: Algoritmos de ordenação ineficientes, como **Bubble Sort** ou **Insertion Sort**.

### 🔹 **O(log n) - Tempo Logarítmico**

A entrada é reduzida pela metade a cada passo.

```c
int busca_binaria(int vetor[], int inicio, int fim, int chave) {
    while (inicio <= fim) {
        int meio = (inicio + fim) / 2;
        if (vetor[meio] == chave) return meio;
        if (vetor[meio] < chave) inicio = meio + 1;
        else fim = meio - 1;
    }
    return -1;
}
```

A **busca binária** é um ótimo exemplo de O(log n), pois corta o espaço de busca pela metade a cada passo.

**Dica:** Faça uma busca pela internet sobre o funcionamento da busca binária, ela é bastante util e pode reduzir drasticamente o tempo de execução de um processo se usada de maneira correta.

---

O grafico abaixo ajuda bastante a entender o crescimento de tempo em relação ao tamanho da entrada de cada um dos algoritmos:

![](./1_5ZLci3SuR0zM_QlZOADv8Q.jpg)

---

# 🌐 Vetores Dinâmicos em C

Vetores dinâmicos são arrays cujo tamanho pode crescer ou diminuir conforme necessário. No entanto, realocar memória constantemente pode ser ineficiente.

## 🛠️ Implementação com Inserção O(n)
Inicialmente, podemos implementar um vetor dinâmico que aumenta de tamanho **linearmente**, alocando um novo array toda vez que precisamos adicionar um elemento.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int *dados;
    int tamanho;
} VetorDinamico;

VetorDinamico* criarVetor() {
    VetorDinamico *vetor = (VetorDinamico*) malloc(sizeof(VetorDinamico));
    vetor->dados = NULL;
    vetor->tamanho = 0;
    return vetor;
}

void inserir(VetorDinamico *vetor, int valor) {
    vetor->tamanho++;
    vetor->dados = (int*) realloc(vetor->dados, vetor->tamanho * sizeof(int));
    vetor->dados[vetor->tamanho - 1] = valor;
}

void removerUltimo(VetorDinamico *vetor) {  
    if (vetor->tamanho > 0) {
        vetor->tamanho--;
        vetor->dados = (int*) realloc(vetor->dados, vetor->tamanho * sizeof(int));
    }
}

void imprimir(VetorDinamico *vetor) {
    for (int i = 0; i < vetor->tamanho; i++) {
        printf("%d ", vetor->dados[i]);
    }
    printf("\n");
}

int main() {
    VetorDinamico *vetor = criarVetor();
    inserir(vetor, 10);
    inserir(vetor, 20);
    inserir(vetor, 30);
    imprimir(vetor);
    
    removerUltimo(vetor);
    imprimir(vetor);
    
    free(vetor->dados);
    free(vetor);
    return 0;
}
```

Note que para remover qualquer valor diferente do ultimo, é necessario mover todos os dados que estão após ele uma casa a frente. 

### ⚠️ Problema: Ineficiência na Inserção
Cada vez que chamamos `realloc`, um novo bloco de memória é alocado e todos os elementos anteriores são copiados para o novo espaço. Isso resulta em um custo **O(n)** para cada inserção.

---

## ✨ Otimizando para Inserção O(1) Amortizado
Para evitar realocações frequentes, podemos dobrar a capacidade sempre que precisar expandir o array. Isso resulta em um custo **amortizado O(1)** por inserção.

Esse video pode ser consultado com uma explicação mais detalhada: https://www.youtube.com/watch?v=MTl8djZFWE0

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int *dados;
    int tamanho;
    int capacidade;
} VetorDinamico;

VetorDinamico* criarVetor() {
    VetorDinamico *vetor = (VetorDinamico*) malloc(sizeof(VetorDinamico));
    vetor->tamanho = 0;
    vetor->capacidade = 2; // Começamos com capacidade 2
    vetor->dados = (int*) malloc(vetor->capacidade * sizeof(int));
    return vetor;
}

void redimensionar(VetorDinamico *vetor) {
    vetor->capacidade *= 2;
    vetor->dados = (int*) realloc(vetor->dados, vetor->capacidade * sizeof(int));
}

void inserir(VetorDinamico *vetor, int valor) {
    if (vetor->tamanho == vetor->capacidade) {
        redimensionar(vetor);
    }
    vetor->dados[vetor->tamanho++] = valor;
}

void removerUltimo(VetorDinamico *vetor) {
    if (vetor->tamanho > 0) {
        vetor->tamanho--;
    }
}

void imprimir(VetorDinamico *vetor) {
    for (int i = 0; i < vetor->tamanho; i++) {
        printf("%d ", vetor->dados[i]);
    }
    printf("\n");
}

int main() {
    VetorDinamico *vetor = criarVetor();
    inserir(vetor, 10);
    inserir(vetor, 20);
    inserir(vetor, 30);
    inserir(vetor, 40);
    imprimir(vetor);
    
    removerUltimo(vetor);
    imprimir(vetor);
    
    free(vetor->dados);
    free(vetor);
    return 0;
}
```

### ✅ **Por que isso melhora a complexidade?**

- A maioria das inserções será **O(1)**, pois apenas adicionamos o elemento.
- Somente ocasionalmente ocorre **uma realocação O(n)**, mas ao dobrar a capacidade, **essas realocações se tornam raras**.
- **Custo Amortizado**: Se um vetor cresce de 1 para 2, depois para 4, 8, 16..., a cada `n` inserções só precisamos **O(log n) realocações**, resultando em **O(1) por operação em média**.

Note também que a função de remover o ultimo elemento foi simplificado de forma que apenas diminuimos o inteiro que salva o tamanho do vetor, salvando mais operações de `realloc` e deixando espaço caso queiramos reusar a memória futuramente.

---

### Python

Em python o interpretador já faz isso para você com as listas por trás dos panos, então nenhuma ação precisa ser feita. 

---

Agora você pode aplicar esse conceito para melhorar a eficiência dos seus programas! ✨

--- 

### Lista de Exercícios

Vou deixar uma lista de exercícios e dificuldades para que possam treinar o que aprendeu e saber seu nível:


**Fácil**
- https://judge.beecrowd.com/pt/problems/view/1164
- https://judge.beecrowd.com/pt/problems/view/1160
- https://judge.beecrowd.com/pt/problems/view/1176
- https://judge.beecrowd.com/pt/problems/view/2028

**Iniciante**
- https://judge.beecrowd.com/pt/problems/view/1471
- https://judge.beecrowd.com/pt/problems/view/1467
- https://judge.beecrowd.com/pt/problems/view/1437
- https://judge.beecrowd.com/pt/problems/view/3407

**Médio** 
- https://judge.beecrowd.com/pt/problems/view/2667
- https://judge.beecrowd.com/pt/problems/view/3428
- https://judge.beecrowd.com/pt/problems/view/2986
- https://judge.beecrowd.com/pt/problems/view/1029

**Difícil**
- https://judge.beecrowd.com/pt/problems/view/3433
- https://judge.beecrowd.com/pt/problems/view/3444
- https://judge.beecrowd.com/pt/problems/view/3429
- https://judge.beecrowd.com/pt/problems/view/3002


## Desafio Secreto: Balão Extra

Quem leu esse tutorial e quiser ganhar um balão extra, envie um print de cada problema na sessão **Médio** para mim no privado para garantir esse balão. 
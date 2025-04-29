# 🌟 Tutorial #19 🌟

## Introdução

Um **dicionário** é uma estrutura de dados que **mapeia chaves a valores**. Ele permite **armazenar, buscar, inserir e remover** dados com base em uma chave, em tempo constante **(O(1))** na média, isso torna o dicionário extremamente úteis por serem rápidos e ao mesmo tempo abstrair muito toda a complexidade do armazenamento.

### Acessos e Complexidade

| Operação       | Complexidade Média | Complexidade Pior Caso |
|----------------|--------------------|-------------------------|
| Inserção       | O(1)               | O(n)                    |
| Busca (get)    | O(1)               | O(n)                    |
| Remoção (del)  | O(1)               | O(n)                    |

> O pior caso ocorre em caso de **colisões mal resolvidas** ao fazer o hash da chave, mas em geral, dicionários bem implementados oferecem acesso extremamente rápido.


---

## Conceito de dicionário

Um dicionário simples é implementado usando um vetor de listas encadeadas e uma função hash. A chave utilizada é usada na função hash para encontrar qual posição do vetor deve ser colocado aquele valor, se já existir algum item naquela posição do vetor colocamos o novo valor ao final da `lista encadeada` naquela posição.

Vamos supor um exemplo de um dicionário de 4 posições e que nossa função hash é apenas calcular o módulo da chave com o número 4:

```
Estado inicial: [
    0: 
    1: 
    2: 
    3:
]
---
Insere: (3,a) => 3 mod 4 = 3
Resultado: [
    0: 
    1: 
    2: 
    3: (3,a)
]
---
Insere: (8,b) => 8 mod 4 = 0
Resultado: [
    0: (8,b)
    1: 
    2: 
    3: (3,a)
]
---
Insere: (16,c) => 16 mod 4 = 0
Resultado: [
    0: (8,b) -> (16,c)
    1: 
    2: 
    3: (3,a)
]
---
Insere: (7,d) => 7 mod 4 = 3
Resultado: [
    0: (8,b) -> (16,c)
    1: 
    2: 
    3: (3,a) -> (7,d)
]
---
Insere: (3,e) => 7 mod 4 = 3
// Note que se a chave já existe é feito a substituição do seu valor
Resultado: [
    0: (8,b) -> (16,c)
    1: 
    2: 
    3: (3,e) -> (7,d)
]
---
Insere: (11,e) => 11 mod 4 = 3
Resultado: [
    0: (8,b) -> (16,c)
    1: 
    2: 
    3: (3,e) -> (7,d) -> (11,e)
]
// Note que valores podem ser duplicados

```

Com isso podemos ver que caso nossa função hash não seja eficiente e houver muitos conflitos, podemos ter apenas uma posição do vetor com todos as chave-valor, e a nossa busca por uma chave teria que passar por toda a `lista encadeada` naquela posição o que pode ser ineficiente, por conta disso não implementamos um dicionário na manualmente e usamos a implementação padrão da linguagem que usa diversas técnicas de otimização para evitar colisões. 

Algumas técnicas de otimização são:
 - Usar uma função Hash boa o suficiente;
 - Aumentar o tamanho do vetor base (256, 1024, 4096 posições);
 - Usar dicionários multi-níveis, no qual ao invez de ter uma lista encadeada em cada posição, existe um outro dicionário com uma função hash diferente.
 - Entre outras...


## 🐍 Dicionários em Python

O Python tem suporte nativo a dicionários através do tipo `dict`. A chave pode ser de **qualquer tipo imutável**, como `int`, `str`, `tuple`, `float`, etc.

### Exemplo Básico

```python
# Criando um dicionário
meu_dict = {
    "nome": "João",
    "idade": 25,
    "cidade": "São Paulo"
}

# Acessando valores
print(meu_dict["nome"])        # João 

# Adicionando uma nova chave
meu_dict["profissão"] = "Engenheiro"

# Atualizando um valor
meu_dict["idade"] = 26

# Removendo uma chave
del meu_dict["cidade"]

# Iterando sobre as chaves
for chave in meu_dict:
    print(chave, "->", meu_dict[chave])
```

### Funções úteis

```python
# Verifica se uma chave existe
if "nome" in meu_dict:
    print("Existe")

# Obter todas as chaves ou valores em formato de lista
print(meu_dict.keys())
print(meu_dict.values())
```

---

## ⚙️ Dicionário Simples em C

Em C, não existe um tipo nativo de dicionário. Para simular isso, usamos uma **tabela hash com arrays e listas**.

Neste exemplo, implementaremos um dicionário simples com:
- **Chave inteira (`int`)**
- **Valor inteiro (`int`)**
- Tamanho fixo da tabela
- Hash baseada em `key % TAMANHO`

Note que os exemplos abaixo são apenas para demonstração do funcionamento interno do dicionário, mas não é recomendavel o seu uso diretamente em C da forma proposta abaixo.

### Estrutura e funções

```c
#include <stdio.h>
#include <stdlib.h>

#define TAMANHO 10

typedef struct Item {
    int chave;
    int valor;
    struct Item* prox;
} Item;

Item* tabela[TAMANHO];

// Função hash simples: resto da divisão
int hash(int chave) {
    return chave % TAMANHO;
}

// Inserir ou atualizar
void inserir(int chave, int valor) {
    int indice = hash(chave);
    Item* atual = tabela[indice];

    while (atual != NULL) {
        if (atual->chave == chave) {
            atual->valor = valor;
            return;
        }
        atual = atual->prox;
    }

    // Inserção no início da lista
    Item* novo = malloc(sizeof(Item));
    novo->chave = chave;
    novo->valor = valor;
    novo->prox = tabela[indice];
    tabela[indice] = novo;
}

// Buscar valor por chave
int buscar(int chave, int* encontrado) {
    int indice = hash(chave);
    Item* atual = tabela[indice];

    while (atual != NULL) {
        if (atual->chave == chave) {
            *encontrado = 1;
            return atual->valor;
        }
        atual = atual->prox;
    }

    *encontrado = 0;
    return -1;
}

// Remover chave
void remover(int chave) {
    int indice = hash(chave);
    Item* atual = tabela[indice];
    Item* anterior = NULL;

    while (atual != NULL) {
        if (atual->chave == chave) {
            if (anterior == NULL) {
                tabela[indice] = atual->prox;
            } else {
                anterior->prox = atual->prox;
            }
            free(atual);
            return;
        }
        anterior = atual;
        atual = atual->prox;
    }
}

// Mostrar todos os pares
void imprimir_tabela() {
    for (int i = 0; i < TAMANHO; i++) {
        Item* atual = tabela[i];
        printf("[%d]: ", i);
        while (atual != NULL) {
            printf("(%d → %d) ", atual->chave, atual->valor);
            atual = atual->prox;
        }
        printf("\n");
    }
}
```

### Exemplo de uso

```c
int main() {
    inserir(1, 10);
    inserir(11, 20);  // colisão com 1: hash(1) == 1 e hash(11) == 1
    inserir(2, 30);

    imprimir_tabela();

    int ok;
    int valor = buscar(11, &ok);
    if (ok) {
        printf("Valor da chave 11: %d\n", valor);
    }

    remover(1);
    imprimir_tabela();

    return 0;
}
```

## Conclusão

Em geral, nunca impementamos dicionário manualmente, mas usamos o que a linguagem disponibiliza. Algumas linguagens que já possuem implementação de dicionário:
 - C++
 - Java
 - Python
 - Javascript
 - C#
 - E outras que não são C

Note que algumas versões de um dicionário são implementadas usando uma arvore, o que garante que as chaves estajam ser sempre ordenadas ao custo das operações terem complexidade $O(log N)$. Um dicionário usando *tabela hash* não garante que as chaves estejam ordenadas!


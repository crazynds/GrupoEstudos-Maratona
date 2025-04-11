# 🌟 Tutorial #18 🌟

As **structs** (estruturas) são fundamentais na linguagem C para agrupar dados relacionados. Elas permitem criar tipos de dados compostos, ideais para representar entidades do mundo real como pessoas, produtos, carros, etc.

---

## ✨ O que é uma `struct`?
Uma `struct` é uma coleção de variáveis (campos) agrupadas sob um mesmo nome.

### Exemplo básico:
```c
struct Pessoa {
    char nome[100];
    int idade;
    float altura;
};
```

Essa `struct` define um novo tipo chamado `struct Pessoa`, com três campos: `nome`, `idade` e `altura`.

---

## ✅ Declarando variáveis do tipo `struct`

```c
struct Pessoa p1;
```

Também podemos usar `typedef` para simplificar:
```c
// Definição da struct
typedef struct {
    char nome[100];
    int idade;
    float altura;
} Pessoa;

// Declaração da variavel
Pessoa p2;
```
Note que com a declaração `typedef` não precisamos colocar a palavra `struct` na declaração de alguma variavel.

---

## 📂 Acessando os campos

### Usando o operador `.` (ponto):

Quando você tem uma variável comum do tipo `struct`, você acessa os campos com o operador `.`:
```c
p1.idade = 25;
printf("Idade: %d\n", p1.idade);
```

### Usando o operador `->` (seta):
Quando você tem um **ponteiro** para `struct`, você usa o operador `->`:
```c
Pessoa *ptr = &p1;
ptr->idade = 30;
printf("Idade: %d\n", ptr->idade);
```

### Quando você tem um vetor:

```c
// Declaração um vetor de tamanho 10 para a struct pessoa
Pessoa *ptr = malloc(sizeof(Pessoa) * 10); 
// Note que essa sintaxe ainda funciona, porém o acesso é feito apenas na posição 0
ptr->idade = 30;

// O acesso correto é feito da seguinte forma
ptr[0].idade = 30;
printf("Idade: %d\n", ptr[0].idade);
ptr[1].idade = 32;
printf("Idade: %d\n", ptr[1].idade);
```


### Quando usar `.` e `->`
- Use `.` quando você tem a struct diretamente ou quando se tem um vetor.
- Use `->` quando você tem um **ponteiro** para a struct

---

## ✨  Ponteiros e Structs

Structs podem conter ponteiros como membros, ou você pode alocar structs dinamicamente.

### Exemplo com alocação dinâmica:
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char nome[100];
    int idade;
} Pessoa;

int main() {
    Pessoa *p = malloc(sizeof(Pessoa));
    p->idade = 22;
    printf("Idade: %d\n", p->idade);
    free(p);
    return 0;
}
```

---

## 🔹 Struct como parâmetro de função

### Passando por valor (cópia):
```c
void imprimePessoa(Pessoa p) {
    printf("%s tem %d anos.\n", p.nome, p.idade);
}
```
> Neste caso, uma **cópia** da struct é passada. Mudanças dentro da função **não afetam** o original.

Note que nesse caso, todos os dados são copiados para a função, então existe uma perda de desempenho passar structs muito grandes.

### Passando por referência (ponteiro):

```c
void modificaIdade(Pessoa *p) {
    p->idade += 10;
}
```
> Aqui, modificamos diretamente os dados da struct original.

---



# Tutorial: Ponteiros em C 🔧

Os ponteiros são um dos conceitos mais importantes (e também mais temidos) da linguagem C. Entender bem como eles funcionam é essencial para manipular memória de forma eficiente, trabalhar com arrays, strings, funções e estruturas dinâmicas.

---

## 🔹 O que são Ponteiros?
Um **ponteiro** é uma variável que armazena o **endereço de memória** de outra variável.

```c
int x = 10;
int *p = &x;  // p aponta para o endereço de x
```

- `*p` é o **conteúdo** apontado por `p` (ou seja, o valor de `x`).
- `&x` é o **endereço** da variável `x`.

---

## 🔹 Declarando Ponteiros

```c
int *p;        // Ponteiro para int
float *f;      // Ponteiro para float
char *str;     // Ponteiro para char (comum em strings)
```

---

## 🔹 Usando Ponteiros

```c
int x = 20;
int *ptr = &x;

printf("Valor de x: %d\n", x);         // 20
printf("Endereco de x: %p\n", &x);     // endereço (ex: 0x7ffee123)
printf("Valor de ptr: %p\n", ptr);     // mesmo endereço
printf("Valor apontado por ptr: %d\n", *ptr); // 20
```

---

## 🔹 Modificando Valores com Ponteiros

```c
void dobra(int *n) {
    *n = (*n) * 2;
}

int main() {
    int x = 5;
    dobra(&x);
    printf("Valor dobrado: %d\n", x);  // 10
    return 0;
}
```

---

## 🔹 Ponteiros e Arrays
Arrays em C são, na prática, ponteiros para o primeiro elemento.

```c
int v[3] = {10, 20, 30};
int *p = v;

printf("%d\n", p[0]);  // 10
printf("%d\n", *(p + 1)); // 20
printf("%ld\n", p);  // Endereço de v
printf("%ld\n", p + 1); // Endereço de v+4
printf("%ld\n", p + 2); // Endereço de v+8
```

Você pode percorrer um array com ponteiros:

```c
for (int i = 0; i < 3; i++) {
    printf("%d ", *(p + i));
    // O tipo do ponteiro é induzido da declaração, e ao soma +1 ele na verdade soma a quantidade de bytes para acessar a próxima casa do array
    // como se fizesse p + (i * sizeof(typeof p))
}
```

---

## 🔹 Ponteiros e Alocação Dinâmica

Ponteiros são essenciais para alocar memória dinamicamente com `malloc` e `free`:

```c
#include <stdlib.h>

int *vetor = malloc(5 * sizeof(int));
if (vetor == NULL) {
    printf("Erro de alocacao\n");
    return 1;
}

// Usando o vetor
for (int i = 0; i < 5; i++) {
    vetor[i] = i * 10;
}

// Liberando memoria
free(vetor);
```

---

## 🔹 Ponteiros para Ponteiros

Você pode ter ponteiros que apontam para ponteiros:

```c
int x = 42;
int *p = &x;
int **pp = &p;

printf("%d\n", **pp); // 42
```

 - Note que para acessar valores de ponteiros duplos, preciso colocar `**` antes da variave;

---

## 🔹 Ponteiros e Strings

Strings em C são arrays de `char` terminados com `\0`. Com ponteiros, podemos manipulá-las diretamente:

```c
char *s = "Olá";
printf("%c\n", *(s+1)); // 'l'

// Mesma coisa que

char *s = (char*) malloc(4*sizeof(char));
s[0] = 'O';
s[1] = 'l';
s[2] = 'á';
s[3] = '\0';
printf("%c\n", *(s+1)); // 'l'


```

---

## 🔹 Cuidados com Ponteiros ⚠️
- Nunca use ponteiros não inicializados.
- Note que caso não tenha memoria suficiente para reserver, `malloc` pode retornar `NULL`.
- Use `free()` para liberar memória.
- Evite acessar memória fora dos limites do array.

---

🚀 Pratique criando funções que usem ponteiros e manipulando arrays e strings com eles!



# 🌟 Tutorial #17 🌟

Funções são blocos de código que executam uma tarefa específica. Saber como **passar parâmetros** e **retornar valores** corretamente é fundamental para escrever bons programas em C, principalmente quando começamos a lidar com **vetores** e **structs**.

---

## ✋ Como Passar Parâmetros para uma Função

Em C, parâmetros são passados **por valor**, o que significa que uma **cópia da variável** é enviada à função. Para alterar o valor original, usamos **ponteiros**.

### ✅ Exemplo básico: (Parâmetro por valor)

```c
void dobra(int x) {
    x = x * 2;
}

int main() {
    int a = 5;
    dobra(a);
    printf("%d\n", a);  // continua sendo 5!
}
```

### ✅ Passando por referência: (Parâmetro com ponteiros)

```c
void dobra(int *x) {
    *x = *x * 2;
}

int main() {
    int a = 5;
    dobra(&a);
    printf("%d\n", a);  // agora imprime 10!
}
```

---

## 📦 Passando Vetores como Parâmetros

Vetores **sempre são passados por referência** (mesmo sem usar `&`), pois o nome do vetor já é um ponteiro para o primeiro elemento.

```c
void imprime_vetor(int v[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", v[i]);
}
```

Você também pode escrever o parâmetro assim: `int *v`, que é equivalente.

### ⚠️ Cuidado:
Como o vetor é passado por referência, **qualquer alteração feita dentro da função altera o vetor original**.

---

## 🔁 O que uma Função Pode Retornar?

Em C, uma função pode retornar:

- Tipos primitivos (`int`, `float`, `char`, etc)
- Ponteiros (`int*`, `char*`, etc)
- `void` (nada)

```c
int soma(int a, int b) {
    return a + b;
}

char* saudacao() {
    return "Olá!";
}
```

---

## 🧱 Retornando Structs

Você **pode retornar structs** em C, mas isso **não é recomendado**, especialmente se a struct for grande.

### 🚫 Problemas:
- Pode causar cópias desnecessárias. Desempenho ruim.
- Possível uso incorreto de memória em struct complexas.

### ✅ Alternativa:
Prefira **passar um ponteiro para struct** como parâmetro e modificar dentro da função.

```c
typedef struct {
    int x, y;
} Ponto;

void define_origem(Ponto *p) {
    p->x = 0;
    p->y = 0;
}
```

Se ainda quiser retornar, isso é válido tecnicamente:

```c
Ponto cria_ponto() {
    Ponto p = {1, 2};
    return p;
}
```

Mas prefira retornar por ponteiro ou preencher uma struct passada como parâmetro.

---

Se entender esse conteúdo, você já tem uma base muito sólida para funções em C! 💪
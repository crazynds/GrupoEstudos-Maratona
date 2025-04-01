# 🌟 Tutorial #10 🌟

# 📌 **Structs e Objetos**

Neste tutorial, vamos abordar como definir e utilizar **structs** em C e **objetos** em Python. Ambos são usados para armazenar e organizar dados de forma estruturada.

---

## 🖥 **Structs em C**
Em C, **structs** são usadas para agrupar diferentes tipos de variáveis sob um mesmo nome. Elas permitem armazenar múltiplos valores em uma única estrutura.

### 🔹 **Definição de uma Struct**
Para criar uma `struct`, usamos a palavra-chave `struct`:

```c
#include <stdio.h>
#include <string.h>

struct Pessoa {
    char nome[50];
    int idade;
    float altura;
};

int main() {
    struct Pessoa pessoa1;

    strcpy(pessoa1.nome, "Carlos");
    pessoa1.idade = 25;
    pessoa1.altura = 1.75;

    printf("Nome: %s\n", pessoa1.nome);
    printf("Idade: %d\n", pessoa1.idade);
    printf("Altura: %.2f m\n", pessoa1.altura);

    return 0;
}
```

### 🔹 **Usando `typedef` para simplificar**
Podemos usar `typedef` para evitar a necessidade de escrever `struct` toda vez que declaramos uma variável:

```c
typedef struct {
    char nome[50];
    int idade;
    float altura;
} Pessoa;

int main() {
    Pessoa pessoa1;
    
    strcpy(pessoa1.nome, "Ana");
    pessoa1.idade = 30;
    pessoa1.altura = 1.68;

    printf("Nome: %s\n", pessoa1.nome);
    printf("Idade: %d\n", pessoa1.idade);
    printf("Altura: %.2f m\n", pessoa1.altura);

    return 0;
}
```

### 🔹 **Structs com Ponteiros**
Podemos criar ponteiros para `structs`, permitindo a manipulação dinâmica:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char nome[50];
    int idade;
} Pessoa;

int main() {
    Pessoa *p = (Pessoa *)malloc(sizeof(Pessoa));
    
    if (p == NULL) {
        printf("Erro ao alocar memória\n");
        return 1;
    }

    strcpy(p->nome, "João");
    p->idade = 28;

    printf("Nome: %s\n", p->nome);
    printf("Idade: %d\n", p->idade);

    free(p);

    return 0;
}
```

---

## 🐍 **Objetos em Python**
Em Python, um **objeto** é uma instância de uma **classe**. Classes são usadas para estruturar dados de forma organizada.

### 🔹 **Definição de uma Classe**
Criamos uma classe usando a palavra-chave `class`. O método `__init__` é o **construtor**, chamado quando um novo objeto é criado.

```python
class Pessoa:
    def __init__(self, nome, idade, altura):
        self.nome = nome
        self.idade = idade
        self.altura = altura

# Criando objetos
pessoa1 = Pessoa("Carlos", 25, 1.75)

# Acessando atributos
print(f"Nome: {pessoa1.nome}")
print(f"Idade: {pessoa1.idade}")
print(f"Altura: {pessoa1.altura:.2f} m")
```

### 🔹 **Alterando Atributos**
Os atributos podem ser modificados diretamente:

```python
pessoa1.idade = 26
print(f"Nova idade: {pessoa1.idade}")  # 26
```

---
Esse é o básico sobre **structs em C** e **objetos em Python**! 🚀
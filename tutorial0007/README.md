# 🌟 Tutorial #06 🌟

A formatação de saída é essencial para apresentar informações de forma clara e organizada. Neste tutorial, vamos explorar como **formatar decimais e inteiros** ao exibir valores na tela em **Python** e **C**. Além disso, veremos **como ler uma linha inteira em C usando `scanf`**.  

---

## 🔹 Formatação de Print em Python 🐍  

Em Python, podemos formatar a saída usando **f-strings**, `.format()` e `%`.  

### ✅ Usando f-strings (Recomendado)  

A partir do Python 3.6, **f-strings** são a forma mais prática de formatar strings.  

```python
nome = "Lago"
idade = 25
altura = 1.75

print(f"Meu nome é {nome}, tenho {idade} anos e {altura:.2f}m de altura.")
```
📌 **Explicação:**  
- `{idade}` → Insere o valor diretamente.  
- `{altura:.2f}` → Formata `altura` com **2 casas decimais**.  

---

### ✅ Usando `.format()`  

```python
print("Meu nome é {}, tenho {} anos e {:.2f}m de altura.".format(nome, idade, altura))
```
📌 **Aqui, os valores são inseridos na ordem em que aparecem.**  

---

### ✅ Usando `%` (Estilo Antigo)  

```python
print("Meu nome é %s, tenho %d anos e %.2f metros de altura." % (nome, idade, altura))
```
📌 **Tipos mais comuns no `%` em Python:**  
- `%s` → String  
- `%d` → Inteiro  
- `%f` → Decimal (pode ser ajustado como `%.2f` para duas casas)  

---

## 🔹 Formatação de Print em C 💻  

Em C, utilizamos **`printf`** e **especificadores de formato** (`%`).  

```c
#include <stdio.h>

int main() {
    int idade = 25;
    float altura = 1.75;

    printf("Idade: %d anos\n", idade);
    printf("Altura: %.2f metros\n", altura);

    return 0;
}
```
📌 **Explicação:**  
- `%d` → Inteiro  
- `%.2f` → Float com 2 casas decimais  
- `\n` → Nova linha  

---

### ✅ Lista de Especificadores do `printf`  

| Tipo   | Formato  | Exemplo        |
|--------|---------|---------------|
| **Inteiro** | `%d` ou `%i` | `printf("%d", 42);` |
| **Decimal** | `%f` | `printf("%.2f", 3.1415);` |
| **Caractere** | `%c` | `printf("%c", 'A');` |
| **String** | `%s` | `printf("%s", "Texto");` |
| **Hexadecimal** | `%x` ou `%X` | `printf("%x", 255);` (Saída: `ff`) |
| **Octal** | `%o` | `printf("%o", 255);` (Saída: `377`) |

---

## 🔹 Lendo uma Linha Inteira em C  

No `scanf`, quando lemos strings sem um modificador especial, **ele para no primeiro espaço**. Para ler uma linha inteira, devemos usar `scanf(" %[^\n]s", variavel)`, ou a função **`fgets()`**.  

### ✅ Lendo uma Linha Inteira com `scanf`  

```c
#include <stdio.h>

int main() {
    char linha[100];

    printf("Digite uma linha de texto:\n");
    scanf(" %[^\n]s", linha); // Lê até encontrar uma nova linha
    printf("Você digitou: %s\n", linha);

    return 0;
}
```
📌 **Explicação:**  
- `" %[^\n]s"` → Lê até encontrar `\n`, garantindo a captura da linha completa.  

---

### ✅ Usando `fgets()` (Método Seguro)  

```c
#include <stdio.h>

int main() {
    char linha[100];

    printf("Digite uma linha de texto:\n");
    fgets(linha, sizeof(linha), stdin); // Garante segurança e evita estouro de buffer
    printf("Você digitou: %s", linha);

    return 0;
}
```
📌 **`fgets()` é preferível a `scanf`, pois previne problemas de buffer overflow.**  

---

### Exercícios para treinar:

Resolva os seguintes problemas para reforçar o que você aprendeu:

1. https://judge.beecrowd.com/pt/problems/view/1036
2. https://judge.beecrowd.com/pt/problems/view/1040
3. https://judge.beecrowd.com/pt/problems/view/1169
4. https://judge.beecrowd.com/pt/problems/view/1193
5. https://judge.beecrowd.com/pt/problems/view/1198
---

Agora você já pode exibir e formatar informações corretamente nas duas linguagens! 🎯
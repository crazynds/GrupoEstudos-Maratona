# 🌟 Tutorial #13 🌟

A matemática é essencial para a programação competitiva. Neste tutorial, veremos **funções matemáticas da biblioteca padrão**, **MDC e MMC**, **Fibonacci** e **números primos**.

Nos exemplos abaixo é realizado a demonstração do código e seu uso, tente entender seu funcionamento apenas com a leitura do código.

---
## 🔢 1. Funções Matemáticas da Biblioteca Padrão (`math.h`)
A biblioteca `math.h` fornece diversas funções úteis para cálculos matemáticos.

### 📌 Principais Funções:

```c
#include <stdio.h>
#include <math.h>

int main() {
    double x = 9.0;
    printf("Raiz quadrada de %.2lf: %.2lf\n", x, sqrt(x)); // sqrt(x) retorna a raiz quadrada
    
    double base = 2.0, expoente = 3.0;
    printf("%lf elevado a %lf: %lf\n", base, expoente, pow(base, expoente)); // pow(x, y) retorna x^y
    
    double angulo = M_PI / 4; // 45 graus em radianos
    printf("Seno de 45 graus: %lf\n", sin(angulo)); // sin(x) retorna o seno de x em radianos
    
    printf("Logaritmo natural de 10: %lf\n", log(10)); // log(x) retorna logaritmo natural (base e)
    
    printf("Valor absoluto de -5: %d\n", abs(-5)); // abs(x) retorna o valor absoluto de x
    
    return 0;
}
```

Essas funções são úteis para cálculos geométricos, físicos e financeiros.

---
## 🤝 2. Máximo Divisor Comum (MDC) e Mínimo Múltiplo Comum (MMC)

O **MDC** (Máximo Divisor Comum) entre dois números é o maior número que os divide simultaneamente. O **MMC** (Mínimo Múltiplo Comum) é o menor número que é múltiplo de ambos.

### Algoritmo de Euclides para MDC
```c
int mdc(int a, int b) {
    if (b == 0) return a;
    return mdc(b, a % b);
}
```
🔹 **Por que usar?** O algoritmo de Euclides é **O(log n)**, muito mais rápido do que verificar todos os divisores.

### Cálculo do MMC
Sabemos que:
```
MMC(a, b) = (a * b) / MDC(a, b)
```

```c
int mmc(int a, int b) {
    return (a / mdc(a, b)) * b;
}
```
---
## 🌀 3. Fibonacci Eficiente

A sequência de Fibonacci é uma sequência de números onde cada termo é a soma dos dois anteriores, começando por 0 e 1:

### 📌 Exemplo da sequência:
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...

Essa sequência aparece naturalmente em diversos fenômenos, como crescimento populacional, espirais na natureza (conchas, girassóis), algoritmos de otimização e até compressão de dados.

A sequência de Fibonacci é definida por:
```
F(n) = F(n-1) + F(n-2), com F(0) = 0 e F(1) = 1
```

### Implementação Ingênua (Exponencial, Ruim)
```c
long long fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```
❌ **Muito lento**! Complexidade O(2^n).

### Implementação com Programação Dinâmica (O(n))
```c
long long fib_dp(int n) {
    long long f[n+1];
    f[0] = 0;
    f[1] = 1;
    for (int i = 2; i <= n; i++) {
        f[i] = f[i - 1] + f[i - 2];
    }
    return f[n];
}
```
🔹 **Melhor, mas usa O(n) de memória.**

### Fibonacci em O(log n) com Matriz

Existe uma forma de calcular com exponenciação de matrizes com uma complexidade de **O(log n)**, mas não convém para esse tutorial e seria muito complexo de explicar, então deixo na sua mão buscar estudar se um dia precisar usar esse calculo.

---
## 🔍 4. Números Primos

Um número primo é um número natural maior que 1 que só pode ser dividido por 1 e por ele mesmo. Exemplos de números primos são:
2, 3, 5, 7, 11, 13, 17, 19, 23, ...

Os números primos são fundamentais na criptografia, principalmente nos algoritmos de segurança como RSA, onde a dificuldade de fatorar números grandes é usada para proteger informações.

Um número é **primo** se for divisível apenas por `1` e por ele mesmo.

### Teste de Primalidade Ingênuo (O(n))
```c
int eh_primo(int n) {
    if (n <= 1) return 0;
    for (int i = 2; i < n; i++) {
        if (n % i == 0) return 0;
    }
    return 1;
}
```
🔹 **Muito lento para números grandes.**

### Teste de Primalidade Otimizado (O(sqrt(n)))
```c
int eh_primo_otimizado(int n) {
    if (n <= 1) return 0;
    if (n <= 3) return 1;
    if (n % 2 == 0 || n % 3 == 0) return 0;
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) return 0;
    }
    return 1;
}
```
🔹 **Muito mais rápido para números grandes!**

### Crivo de Eratóstenes (Para listar primos até `n` em O(n log log n))
```c
void crivo(int n) {
    int primo[n + 1];
    for (int i = 0; i <= n; i++) primo[i] = 1;
    
    for (int p = 2; p * p <= n; p++) {
        if (primo[p]) {
            for (int i = p * p; i <= n; i += p) {
                primo[i] = 0;
            }
        }
    }
    
    for (int i = 2; i <= n; i++) {
        if (primo[i]) printf("%d ", i);
    }
}
```
🔹 **Muito eficiente para encontrar todos os primos menores que `n`!**

### Miller–Rabin O(log^3(n))

O algoritmo Miller-Rabin extremamente rápido para testar a probabilidade de um número ser primo (100% de certeza para números menores que 2^64) e pode ser usado no lugar de um teste de primalidade comum. 

É um algoritmo complexo então vou deixar para você esse estudo. 

---
Os conceitos e códigos podem ser adaptados para **Python** facilmente! 🐍 Deixo na sua mão esse papel.


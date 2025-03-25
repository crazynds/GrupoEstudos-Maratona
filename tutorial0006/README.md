# 🌟 Tutorial #06 🌟

Funções são blocos de código reutilizáveis que ajudam a organizar melhor um programa. Neste tutorial, veremos como criar funções em **Python** e **C**, como funciona a passagem de parâmetros e, em C, a diferença entre passar variáveis normais, vetores e ponteiros.  

---

##  Python 🐍  

### Criando e Chamando Funções  

Em Python, usamos `def` para definir funções. Elas podem receber **parâmetros** e **retornar valores**.

```python
def saudacao(nome):
    return f"Olá, {nome}!"

print(saudacao("Lago"))  # Chama a função e imprime "Olá, Lago!"
```

### Função com Parâmetros Opcionais  
Podemos definir valores padrão para os parâmetros.  

```python
def saudacao(nome="Mundo"):
    return f"Olá, {nome}!"

print(saudacao())  # "Olá, Mundo!"
print(saudacao("Python"))  # "Olá, Python!"
```

### Função com Múltiplos Parâmetros  
```python
def soma(a, b):
    return a + b

print(soma(10, 5))  # Retorna 15
print(soma('Ola ', 'mundo'))  # Retorna Ola mundo
print(soma(10,'mundo')) # Possivelmente um erro pq não é possivel somar inteiro com string
```

### Funções sem Retorno (`None`)  
```python
def exibir_mensagem():
    print("Isso é uma função sem retorno!")

exibir_mensagem()
```

É possivel verificar se a função retornou comparando com o tipo `None`, conforme exemplo abaixo:
```python
def checaAlgo(num)
    if num < 10:
        return num*num

if checaAlgo(10) == None:
    print('não retornou nada')
else:
    print('retornou algo')
```

---

## 🔹 Funções em C 💻  

### Criando e Chamando Funções  
Em C, devemos **declarar** a função e seu tipo de retorno antes de usá-la. 

```c
#include <stdio.h>

// Declaração da função
int soma(int a, int b);

int main() {
    int resultado = soma(10, 5);
    printf("Soma: %d\n", resultado);
    return 0;
}

// Definição da função
int soma(int a, int b) {
    return a + b;
}
```

Podemos fazer sua definição sem a declaração também da seguinte forma:

```c
#include <stdio.h>

// Definição da função
int soma(int a, int b) {
    return a + b;
}
int main() {
    int resultado = soma(10, 5);
    printf("Soma: %d\n", resultado);
    return 0;
}
```
Note que a função sempre deve ser definida antes do local onde ela foi chamada.

### Função sem Retorno (`void`)  
```c
void mensagem() {
    printf("Isso é uma função sem retorno!\n");
}

int main() {
    mensagem();
    return 0;
}
```

### Função com Múltiplos Parâmetros  
```c
void imprimir_soma(int a, int b) {
    printf("Soma: %d\n", a + b);
}

int main() {
    imprimir_soma(3, 7);
    return 0;
}
```

---

## 📌 Diferença na Passagem de Parâmetros em C  

Em C, podemos passar variáveis de **três formas principais**: **por valor, por referência (ponteiros) e vetores**.  

### 🔹 Passagem por Valor  
Quando passamos um valor comum, **ele é copiado** para a função, ou seja, **qualquer alteração feita dentro da função não afeta a variável original**.  

```c
#include <stdio.h>

void dobrar(int x) {
    x = x * 2;
    printf("Dentro da função: %d\n", x);
}

int main() {
    int numero = 10;
    dobrar(numero);
    printf("Fora da função: %d\n", numero); // Continua 10, pois foi passada uma cópia
    return 0;
}
```

### 🔹 Passagem por Referência (Ponteiros)  
Se passarmos um **ponteiro**, podemos modificar diretamente a variável original. Note que ao trabalhar com o valor da variavel, temos que adicionar o `*` na frente dela. 

Perceba também que ao passar o parâmetro para a variavel, adicionamos `&` antes da variavel.

```c
#include <stdio.h>

void dobrar(int *x) {
    *x = *x * 2;
}

int main() {
    int numero = 10;
    dobrar(&numero);
    printf("Fora da função: %d\n", numero); // Agora será 20
    return 0;
}
```
📌 **Por que usar ponteiros?** Para permitir que a função altere valores originais e evitar a cópia de grandes quantidades de dados.

Em resumo, o funcionamento dos ponteiros é da seguinte forma:
 - O `&` pega o endereço de memória da variavel e manda esse endereço como número.
 - O `int *` entende que aquele número é um endereço de uma variavel do tipo int.
 - Ao acessar a variavel diretamente (sem asterisco na frente), estamos lendo o número do endereço.
 - Ao acessar a variavel com o asterisco, estamos lendo a posição na memória daquele endereço.


### 🔹 Passagem de Arrays  
Quando passamos um **array**, ele é tratado como um ponteiro para seu primeiro elemento, então **qualquer alteração afeta o array original**.  

```c
#include <stdio.h>

void modificarArray(int *arr, int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        arr[i] *= 2;
    }
}

int main() {
    int numeros[] = {1, 2, 3, 4, 5};
    int tamanho = sizeof(numeros) / sizeof(numeros[0]);

    modificarArray(numeros, tamanho);

    for (int i = 0; i < tamanho; i++) {
        printf("%d ", numeros[i]); // Agora todos os valores estão dobrados
    }

    return 0;
}
```

📌 **Observação:** Não precisamos usar `&` para passar um array, pois ele já é tratado como um ponteiro.

---

Dominar funções e a passagem de parâmetros melhora a estrutura do código e facilita a reutilização! 🚀


# 🌟 Tutorial #05 🌟

Arrays e strings são estruturas fundamentais na programação. Neste tutorial, veremos como manipular esses elementos em **Python** e **C**, além de cuidados essenciais ao lidar com strings em C.  

---

## 🧮 Arrays  

### Python 🐍 – **Lists**  

Em Python, **listas** (`list`) são usadas como arrays e podem armazenar qualquer tipo de dado.

**Criando e acessando listas:**  
```python
numeros = [10, 20, 30, 40, 50]  # Criando uma lista
print(numeros[0])  # Acessando o primeiro elemento (índice 0)
print(numeros[1])  # Acessando o segundo elemento
print(numeros[-1])  # Acessando o último elemento
print(numeros[-2])  # Acessando o penultimo elemento
```

**Percorrendo uma lista:**  
```python
for num in numeros:
    print(num)

# Ou acessando pelos indices
for i in range(len(numeros)):
    print(numeros[i])
```

**Alterando elementos:**  
```python
numeros[2] = 100  # Modifica o terceiro elemento
print(numeros)
```

**Adicionando e removendo elementos:**  
```python
numeros.append(60)  # Adiciona um elemento ao final
numeros.remove(20)  # Remove o elemento 20
print(numeros)
```

---

### C 💻 – **Arrays**  
Em C, arrays são fixos e devem ter o tamanho definido.  

**Declarando e acessando um array:**  
```c
#include <stdio.h>

int main() {
    int numeros[5] = {10, 20, 30, 40, 50};  // Criando um array com valores pre-definidos
    int numeros2[5] = {}    // Cria um array com valores zeros
    int numeros3[5];        // Cria um array com valores aleatórios (Lixo de memória)

    printf("%d\n", numeros[0]);  // Acessando o primeiro elemento
    printf("%d\n", numeros[4]);  // Acessando o último elemento
    // Diferente de python, numeros[-1] não é valido e vai resultar em erro
    return 0;
}
```

**Percorrendo um array:**  
```c
for (int i = 0; i < 5; i++) {   // O tamanho deve ser salvo previamente
    printf("%d ", numeros[i]);
}
```

**Modificando um valor:**  
```c
numeros[2] = 100;  // Alterando o terceiro elemento
```

**Criando um vetor de tamanho dinamico:**  
```c

int n;
scanf("%d",&n); // Le um N
int vetor[n];   // Declara um vetor de int de tamanho n
for(int x=0;x<n;x++){
    scanf("%d",&vetor[i]);  // Le um inteiro e coloca na posição i do vetor
}
```

---

## 📝 Strings  

### Python 🐍 – **Manipulação de Strings**  
Em Python, strings são objetos imutáveis, ou seja, possuem tamanho fixo, mas podem ser manipuladas de diversas formas. Ao concatenar duas strings, python cria uma nova string com o tamanho de ambas somadas.

**Criando e acessando strings:**  
```python
texto = "Olá, mundo!"
print(texto[0])  # Primeiro caractere
print(texto[-1])  # Último caractere
# Acesso parecido com listas
```

**Concatenação e repetição:**  
```python
nova_string = texto + " Como vai?"  # Concatenação
print(nova_string)

repetida = "Python! " * 3  # Repetição
print(repetida) # Python! Python! Python!
```

**Fatiamento (slicing):**  
```python
print(texto[0:5])  # "Olá, "
print(texto[::-1])  # Inverte a string
```

*Obs:* isso funciona com listas também.

**Convertendo tipos:**  
```python
numero = "123"
print(int(numero) + 1)  # Converte string para inteiro
```

**Tamanho da string:**
```python
palavra2 = "Teste"
tamanho = len(palavra2)
```

---

### C 💻 – **Strings e Cuidados**  
Em C, strings são arrays de caracteres **terminados por `\0` (null-terminator)**. Se esquecermos de colocar o null terminator no final da string, vamos acessar memória inválida. (Pode crashar o programa)

**Criando e acessando strings:**  
```c
#include <stdio.h>

int main() {
    char texto[] = "Olá, mundo!";  // String como array de caracteres
    // Note que strings como a acima, o compilador adiciona sozinho o \0

    char texto2[10];
    texto2[0] = 'O';
    texto2[1] = 'l';
    texto2[2] = 'á';
    texto2[3] = '\0';   // Criando a string manualmente, devemos colocar o \0


    printf("%c\n", texto[0]);  // Primeiro caractere
    printf("%s\n", texto);  // Imprime a string completa

    return 0;
}
```

⚠️ **Cuidado:** Strings em C precisam ter espaço suficiente, pois não se ajustam automaticamente como em Python. Se um overflow acontecer teremos erros imprevisíveis. 

**Leitura segura de strings:**  
```c
char nome[50];  // String de até 50 caracteres
printf("Digite seu nome: ");
scanf("%49s", nome);  // Limita a leitura a 49 caracteres para evitar overflow, note que ele não le mais de uma palavra.
printf("Olá, %s!\n", nome);
```

**Concatenando strings em C:**  
```c
#include <stdio.h>
#include <string.h>

int main() {
    char parte1[50] = "Olá, ";
    char parte2[] = "mundo!";
    
    strcat(parte1, parte2);  // Concatena parte2 em parte1 (Deve ter espaço suficiente em parte 1)
    printf("%s\n", parte1);

    return 0;
}
```

**Comparando strings:**  
```c
#include <stdio.h>
#include <string.h>

int main() {
    char palavra1[] = "teste";
    char palavra2[] = "Teste";

    if (strcmp(palavra1, palavra2) == 0) {
        printf("As strings são iguais.\n");
    } else {
        printf("As strings são diferentes.\n");
    }

    return 0;
}
```

**Tamanho da string:**

```c
char palavra2[] = "Teste";
int tamanho = strlen(palavra2);

```

---

### Exercícios para treinar:

Cadastre-se no site do beecrowd usando sua conta Git e resolva os seguintes problemas para reforçar o que você aprendeu:

1. https://judge.beecrowd.com/pt/problems/view/1162
2. https://judge.beecrowd.com/pt/problems/view/1259
3. https://judge.beecrowd.com/pt/problems/view/1069
4. https://judge.beecrowd.com/pt/problems/view/1234
5. https://judge.beecrowd.com/pt/problems/view/1273


---

Entender bem esses conceitos ajuda a evitar erros e melhorar a eficiência do código! 🚀
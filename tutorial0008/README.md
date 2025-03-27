
# 🌟 Tutorial #08 🌟

## 📌 Manipulação de Strings e Alocação Dinâmica em C

### Manipulação de Strings em C

Em C, as strings são representadas como arrays de caracteres terminados por um caractere especial `\0` (null character). Além disso, a biblioteca padrão de C fornece várias funções para manipulação de strings. Vamos conhecer algumas das principais funções para manipulação de strings:

### Funções Comuns para Manipulação de Strings

1. **`strlen()`**: Retorna o comprimento de uma string (excluindo o caractere nulo `\0`).

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str[] = "Hello, World!";
       printf("Tamanho da string: %lu\n", strlen(str));  // 13
       return 0;
   }
   ```

2. **`strcat()`**: Concatena (anexa) uma string no final de outra string.

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str1[20] = "Hello";
       char str2[] = " World!";
       strcat(str1, str2);  // Concatena str2 em str1
       printf("String concatenada: %s\n", str1);  // "Hello World!"
       return 0;
   }
   ```

3. **`strcmp()`**: Compara duas strings lexicograficamente. Retorna:

   - 0 se as strings forem iguais.
   - Valor negativo se a primeira string for menor.
   - Valor positivo se a primeira string for maior.

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str1[] = "Hello";
       char str2[] = "Hello";
       if (strcmp(str1, str2) == 0) {
           printf("As strings são iguais.\n");
       } else {
           printf("As strings são diferentes.\n");
       }
       return 0;
   }
   ```

4. **`strcpy()`**: Copia o conteúdo de uma string para outra.

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str1[20];
       char str2[] = "Hello, World!";
       strcpy(str1, str2);  // Copia str2 para str1
       printf("String copiada: %s\n", str1);  // "Hello, World!"
       return 0;
   }
   ```

5. **`strchr()`**: Procura a primeira ocorrência de um caractere em uma string.

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str[] = "Hello, World!";
       char *ptr = strchr(str, 'o');  // Procura o primeiro 'o'
       if (ptr) {
           printf("Caractere encontrado: %c\n", *ptr);
       } else {
           printf("Caractere não encontrado.\n");
       }
       return 0;
   }
   ```

6. **`strtok()`**: Divide uma string em tokens (partes menores), usando delimitadores.

   ```c
   #include <stdio.h>
   #include <string.h>

   int main() {
       char str[] = "Hello,World,How,Are,You";
       char *token = strtok(str, ",");  // Divide pela vírgula
       while (token != NULL) {
           printf("%s\n", token);
           token = strtok(NULL, ",");
       }
       return 0;
   }
   ```

---

### Alocação Dinâmica de Memória

A alocação dinâmica permite criar variáveis e vetores de tamanho flexível usando `malloc`, `calloc` e `realloc`.

#### 🔹 Alocação Dinâmica para um Único Inteiro

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *ptr = (int *)malloc(sizeof(int));
    if (ptr == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }
    *ptr = 10;
    printf("Valor: %d\n", *ptr);
    free(ptr);
    return 0;
}
```

#### 🔹 Alocação Dinâmica para Vetores

##### Vetor de `int`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 5;
    int *vetor = (int *)malloc(n * sizeof(int));
    if (vetor == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    // Inicializando valores
    for (int i = 0; i < n; i++) {
        vetor[i] = i * 2;
    }

    // Exibindo valores
    for (int i = 0; i < n; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    free(vetor);
    return 0;
}
```

##### Vetor de `float`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 3;
    float *valores = (float *)malloc(n * sizeof(float));
    if (valores == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    valores[0] = 1.5;
    valores[1] = 2.75;
    valores[2] = 3.9;

    for (int i = 0; i < n; i++) {
        printf("%.2f ", valores[i]);
    }
    printf("\n");

    free(valores);
    return 0;
}
```

#### 🔹 Redimensionamento com `realloc`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 3;
    int *valores = (int *)malloc(n * sizeof(int));
    if (valores == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        valores[i] = i + 1;
    }

    // Redimensionando para 6 elementos
    n = 6;
    valores = (int *)realloc(valores, n * sizeof(int));
    if (valores == NULL) {
        printf("Erro na realocação de memória!\n");
        return 1;
    }

    for (int i = 3; i < n; i++) {
        valores[i] = i + 1;
    }

    for (int i = 0; i < n; i++) {
        printf("%d ", valores[i]);
    }
    printf("\n");

    free(valores);
    return 0;
}
```

---

## 📌 Manipulação de Strings e Listas Dinâmicas em Python

### Manipulação de Strings

Em Python, as strings são objetos imutáveis, ou seja, você não pode alterar o conteúdo de uma string diretamente. Porém, existem diversas funções e métodos úteis para manipular strings de maneira eficiente.

```python
s = "Python"
print(s[0])  # P
print(s[-1]) # n
print(s[1:4]) # yth
s[0] = 'C' # ERRO - Strings em python não podem ser modificadas diretamente
```

### Funções Comuns para Manipulação de Strings

1. **`len()`**: Retorna o comprimento de uma string.

   ```python
   str = "Hello, World!"
   print(len(str))  # 13
   ```

2. **`+`**\*\* (Concatenação)\*\*: Você pode concatenar strings com o operador `+`.

   ```python
   str1 = "Hello"
   str2 = "World"
   result = str1 + " " + str2
   print(result)  # "Hello World"
   ```

3. **`str.upper()`**: Converte todos os caracteres da string para maiúsculas.

   ```python
   str = "hello"
   print(str.upper())  # "HELLO"
   ```

4. **`str.lower()`**: Converte todos os caracteres da string para minúsculas.

   ```python
   str = "HELLO"
   print(str.lower())  # "hello"
   ```

5. **`str.strip()`**: Remove espaços em branco no início e no final da string.

   ```python
   str = "   Hello   "
   print(str.strip())  # "Hello"
   ```

6. **`str.find()`**: Encontra a posição de uma substring dentro de uma string. Retorna `-1` se não encontrar.

   ```python
   str = "Hello, World!"
   print(str.find("World"))  # 7
   ```

7. **`str.replace()`**: Substitui uma parte da string por outra.

   ```python
   str = "Hello, World!"
   print(str.replace("World", "Python"))  # "Hello, Python!"
   ```

8. **`str.split()`**: Divide a string em uma lista de substrings com base em um delimitador.

   ```python
   str = "apple,banana,cherry"
   fruits = str.split(",")
   print(fruits)  # ['apple', 'banana', 'cherry']
   ```

9. **`str.startswith()`**: Verifica se a string começa com um determinado prefixo.

   ```python
   str = "Hello, World!"
   print(str.startswith("Hello"))  # True
   ```

10. **`str.endswith()`**: Verifica se a string termina com um determinado sufixo.

```python
str = "Hello, World!"
print(str.endswith("World!"))  # True
```

---


### Listas Dinâmicas em Python

Diferente de C, onde precisamos alocar manualmente a memória, em Python as **listas são dinâmicas**.

```python
lista = []  # Lista vazia
lista.append(10)  # Adiciona um elemento
lista.append(20)
lista.append(30)
print(lista)  # [10, 20, 30]
```

#### Removendo Elementos

```python
lista =[10,20,30]
lista.remove(20)  # Remove o primeiro 20 encontrado
print(lista)  # [10, 30]
```

#### Redimensionando Listas

Em Python, listas podem ser redimensionadas automaticamente:

```python

lista = [1, 2, 3]
lista.extend([4, 5, 6])  # Adiciona múltiplos elementos
print(lista)  # [1, 2, 3, 4, 5, 6]
```

---


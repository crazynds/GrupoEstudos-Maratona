# Tutorial: Laços de Repetição (while e for) em Python e C  

Os laços de repetição são fundamentais para executar blocos de código várias vezes sem precisar repetir manualmente as mesmas instruções. Hoje, vamos ver como funcionam os laços **while** e **for** em Python e C.

---

## 🔁 While  

### Python 🐍  
O laço **while** executa um bloco de código **enquanto** a condição especificada for verdadeira.

```python
contador = 0  # Inicializando uma variável
while contador < 5:  # Enquanto 'contador' for menor que 5, o laço continua
    print("Valor do contador:", contador)
    contador += 1  # Incremento para evitar loop infinito

print("Loop finalizado!")
```

**Explicação**:
- O código começa com `contador = 0`.
- O **while** verifica se `contador < 5`. Se for verdadeiro, executa o bloco.
- A cada iteração, `contador` aumenta em 1.
- Quando `contador` chega a 5, a condição `contador < 5` se torna falsa, e o laço termina.

### C 💻  
Em C, o funcionamento do **while** é semelhante.

```c
#include <stdio.h>

int main() {
    int contador = 0;  // Inicializando variável
    while (contador < 5) {  // Enquanto contador for menor que 5, executa o bloco
        printf("Valor do contador: %d\n", contador);
        contador++;  // Incremento para evitar loop infinito
    }
    
    printf("Loop finalizado!\n");
    return 0;
}
```

**Destaques**:
- A condição dentro do `while` é sempre verificada antes de executar o bloco.
- O `contador++` garante que o laço eventualmente termine.
- O `printf` exibe o valor do contador a cada iteração.

---

## 🔄 For  

### Python 🐍  
O **for** em Python é usado para percorrer sequências (como listas e intervalos).

```python
for i in range(5):  # range(5) gera os números de 0 a 4
    print("Valor de i:", i)

print("Loop finalizado!")
```

**Explicação**:
- `range(5)` cria uma sequência de números de **0 a 4**.
- A cada iteração, `i` recebe um novo valor dessa sequência.
- O laço termina quando `i` chega ao último valor de `range(5)`.

Podemos também especificar um início e um passo:

```python
for i in range(1, 10, 2):  # Começa em 1, vai até 9, incrementando de 2 em 2
    print(i)
```

### C 💻  
O **for** em C segue a estrutura:

```c
for (inicialização; condição; incremento) {
    // Código a ser executado
}
```

Exemplo:

```c
#include <stdio.h>

int main() {
    for (int i = 0; i < 5; i++) {  // Começa em 0, roda enquanto i < 5, e incrementa 1 a cada iteração
        printf("Valor de i: %d\n", i);
    }

    printf("Loop finalizado!\n");
    return 0;
}
```

**Explicação**:
- `int i = 0;` → Declara e inicializa `i`.
- `i < 5;` → Enquanto `i` for menor que 5, o laço continua.
- `i++` → A cada iteração, incrementa `i` em 1.

Exemplo com passo diferente:

```c
#include <stdio.h>

int main() {
    for (int i = 1; i < 10; i += 2) {  // Começa em 1 e soma 2 a cada repetição
        printf("%d\n", i);
    }
    return 0;
}
```

---

## 🚀 Conclusão  
- **while**: repete **enquanto** a condição for verdadeira.
- **for**:
  - Em Python, percorre elementos de uma sequência.
  - Em C, tem estrutura fixa com inicialização, condição e incremento.

Ambos os laços são essenciais para automatizar repetições e tornar o código mais eficiente. 🚀
# 🌟 Tutorial #02 🌟
No tutorial de hoje vou mostrar a vocês como fazer o primeiro programa de vocês! Vamos entender a estrutura de cada linguagem e como executar o programa. Podem abrir os editores de texto de vocês e mãos a obra!

## Python 🐍

### Estrutura de um Arquivo Python

Arquivos Python possuem a extensão `.py`. Python não tem uma estrutura fixa obrigatória para execução, ou seja, até um arquivo vazio é válido.

#### Variáveis
Em Python, não é necessário declarar o tipo das variáveis antes de usá-las. Basta inicializar e utilizar.

```python
# Comentários são iniciados com '#' e são ignorados na execução
var1 = 10  # Variável recebe o valor 10
var2 = 20  # Variável recebe o valor 20
nome = 'Texto qualquer'  # Textos devem estar entre aspas simples ou duplas
outro_nome = "Texto"  # Nomes de variáveis não podem conter espaços
var3 = var1 * var2  # Multiplica var1 por var2
```

#### Saída no Console
Para exibir valores no terminal, utilizamos a função `print()`.

```python
print('Olá, Mundo!')  # Exibe o texto
print(var3)  # Exibe o valor da variável var3
print(var1 + var2)  # Exibe a soma de var1 com var2
```

### Como Executar um Arquivo Python
1. Salve o seguinte código em um arquivo `meu_script.py`:

```python
v1 = 'Olá'
v2 = ', '
v3 = 'Mundo!'
print(v1 + v2 + v3)
```

2. Abra o terminal (CMD, PowerShell ou terminal do VSCode) e navegue até a pasta onde o arquivo foi salvo:
   ```sh
   cd C:\caminho\para\meu\script
   ```
3. Execute o comando:
   ```sh
   python meu_script.py
   ```
4. Se tudo estiver correto, a saída será:
   ```sh
   Olá, Mundo!
   ```

---

## C 💻

### Estrutura de um Arquivo C

Arquivos C possuem a extensão `.c` e precisam ser compilados antes de serem executados.

#### Variáveis
Diferente de Python, em C é necessário declarar o tipo da variável antes de usá-la.

```c
#include <stdio.h>

int main() {
    // Comentários em C são iniciados com '//'
    int var1 = 10;  // Declaração e inicialização de uma variável inteira
    int var2 = 20;
    int var3 = var1 * var2;
    
    printf("Olá, Mundo!\n");  // Exibe "Olá, Mundo!"
    return 0;
}
```

### Como Compilar e Executar um Arquivo C
1. Salve o seguinte código em um arquivo `meu_programa.c`.

2. Abra o terminal (CMD, PowerShell ou terminal do VSCode) e navegue até a pasta onde o arquivo foi salvo:
   ```sh
   cd C:\caminho\para\meu\programa
   ```
3. Compile o programa com o GCC:
   ```sh
   gcc meu_programa.c -o meu_programa.exe
   ```
4. Execute o programa gerado:
   ```sh
   meu_programa.exe
   ```
5. Se tudo estiver correto, a saída será:
   ```sh
   Olá, Mundo!
   ```


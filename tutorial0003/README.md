# 🌟 Tutorial #03 🌟

No tutorial de hoje vamos ver como fazer a leitura de dados do terminal, usar esse dados e entender o funcionamento de estrutura condicionais.

## Python 🐍  

### 📥 Como Ler Dados no Terminal  

Em Python, usamos a função `input()` para capturar informações do usuário. Essa função sempre retorna uma **string**, então precisamos converter os dados caso desejemos outro tipo, como `int` ou `float`.  

#### Exemplo de Leitura de Dados:  
```python
nome = input()  # Lê uma string
idade = int(input())  # Converte para inteiro
altura = float(input())  # Converte para float (número com casas decimais)

# Cada parametro do print será impresso separadamente
print("Nome:", nome)
print("Idade:", idade)
print("Altura:", altura)
```  

💡 **Dica:** O `input()` sempre lê a linha inteira como string até a próxima quebra de linha. (Um enter ou \n)

---

### 🔀 Estruturas Condicionais  

O `if` e `else` em Python são usados para tomar decisões no código.  

#### Exemplo:  
```python
idade = int(input("Digite sua idade: "))

if idade >= 18:
    print("Você é maior de idade.")
else:
    print("Você é menor de idade.")
```

⚡ **Observações:**  
- Em Python, usamos **dois pontos `:`** no final do `if` e `else`.  
- Os blocos de código são **indentados** com espaços ou tabulações. Busque sempre usar o mesmo padrão de identação dentro dos escopos.

---

## C 💻  

### 📥 Como Ler Dados no Terminal  

Em C, utilizamos a função `scanf()` para capturar informações do usuário. Precisamos informar **o tipo da variável** e usar o **& (e comercial)** para passar o endereço de memória da variável.  

O funcionamento do `scanf` é relativamente simples, na string passada no primeiro parametro você informa o que você quer buscar, e o `scanf`
 vai fazer tentar encontrar o tipo informado e colocar dentro do valor da variavel.

#### Exemplo de Leitura de Dados:  
```c
#include <stdio.h>

int main() {
    int idade;
    float altura;

    printf("Digite sua idade: ");
    scanf("%d", &idade);  // %d para inteiros, & para passar o endereço da variável

    printf("Digite sua altura em metros: ");
    scanf("%f", &altura);  // %f para floats

    printf("Idade: %d\n", idade);
    printf("Altura: %.2f metros\n", altura);

    return 0;
}
```

⚠️ **Importante:**  
- `%d` → Lê um número inteiro (`int`).  
- `%f` → Lê um número decimal (`float`).  
- `%s` → Lê uma palavra/string (não aceita espaços).  
- O `&` é necessário para passar o **endereço da variável**.  

Note que os tipos para leitura são os mesmo tipos que usamos para imprimir valores no `printf`. A única diferença é que no `printf` não passamos o parametro por referência (Com o `&`).

---

### 🔀 Estruturas Condicionais  

Em C, usamos `if` e `else` da seguinte forma:  

```c
#include <stdio.h>

int main() {
    int idade;
    printf("Digite sua idade: ");
    scanf("%d", &idade);

    if (idade >= 18) {
        printf("Você é maior de idade.\n");
    } else {
        printf("Você é menor de idade.\n");
    }

    return 0;
}
```

⚡ **Observações:**  
- O `if` e `else` devem estar dentro de `{ }`.  
- O `;` no final de cada linha é obrigatório.  
- Comparações de igualdade devem sempre serem feitas usando `==` pois o `=` único é reservado para atribuições de valores do lado direito para o esquerdo!

---

### Exercícios para treinar:

Cadastre-se no site do beecrowd usando sua conta Git e resolva os seguintes problemas para reforçar o que você aprendeu:

1. https://judge.beecrowd.com/pt/problems/view/1004
2. https://judge.beecrowd.com/pt/problems/view/1036
3. https://judge.beecrowd.com/pt/problems/view/1037
4. https://judge.beecrowd.com/pt/problems/view/1065

--- 

🚀 Agora você já sabe como ler entradas no terminal e usar condicionais em Python e C! Se tiver dúvidas, manda aí! 😃

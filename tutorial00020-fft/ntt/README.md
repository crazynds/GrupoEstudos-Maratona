# Multiplicação Eficiente de Polinômios: De $O(n^2)$ à NTT $(n log n)$

Multiplicar dois polinômios parece uma tarefa simples de álgebra escolar, mas quando lidamos com graus na casa dos milhões (comum em criptografia e processamento de sinais), a abordagem tradicional se torna um gargalo intransponível.

## 1. O Problema da Abordagem Direta

A forma clássica de multiplicar polinômios é o que chamamos de **convolução ingênua**. Se temos dois polinômios de grau $D$:

$$P(x) = a_0 + a_1x + \dots + a_Dx^D$$

$$Q(x) = b_0 + b_1x + \dots + b_Dx^D$$

Para encontrar o produto $R(x) = P(x)Q(x)$, cada termo de $P$ deve multiplicar todos os termos de $Q$. Se ambos têm $N$ termos, realizaremos exatas $N^2$ multiplicações. Na notação computacional, dizemos que o custo é **$O(N^2)$**. Para um polinômio de grau 100.000, isso significa 10 bilhões de operações — algo proibitivo para sistemas em tempo real.

---

## 2. A Mudança de Paradigma: Coeficientes vs. Valores

A grande sacada para otimizar esse processo é perceber que existem duas formas de representar o mesmo polinômio:

1. **Representação por Coeficientes:** A lista $$a_0, a_1, \dots, a_D$$. É ótima para somar, mas terrível para multiplicar.
2. **Representação por Valores (Pontos):** Um polinômio de grau $D$ é unicamente definido por **$D+1$ pontos** distintos $(x, y)$.

> **O Insight Fundamental:** Multiplicar polinômios através de seus coeficientes é difícil, mas multiplicar seus valores em pontos específicos é trivial.

Se eu sei que $P(2) = 5$ e $Q(2) = 3$, então o produto $R(x) = P(x)Q(x)$ obrigatoriamente terá $R(2) = 15$. Se fizermos essa conta para pontos suficientes, poderemos reconstruir o polinômio resultante.

---

## 3. A Estratégia "Dividir para Conquistar"

O plano de ataque para uma multiplicação ultraveloz segue três etapas:

* **Avaliação:** Transformamos $P$ e $Q$ da forma de coeficientes para a forma de pontos.
* **Multiplicação Escalar:** Multiplicamos os valores ponto a ponto — isso custa apenas $O(N)$.
* **Interpolação:** Transformamos o resultado de volta para a forma de coeficientes.

O problema é que avaliar um polinômio em $N$ pontos de forma comum ainda levaria $O(N^2)$. Para quebrar essa barreira, precisamos de pontos "mágicos" que possuam simetria.

### FFT (Fast Fourier Transform)

A FFT resolve a etapa de avaliação e interpolação em **$O(N \log N)$**. Ela utiliza as **raízes complexas da unidade** (pontos no círculo unitário do plano complexo). Graças às propriedades de simetria desses números ($x^2$ de um ponto é igual ao de outro, mas com sinal oposto), conseguimos reaproveitar cálculos recursivamente.

* **Uso ideal:** Processamento de áudio, sinais de rádio e engenharia.
* **O Ponto Fraco:** Como utiliza números complexos (`double`/`float`), a FFT sofre com erros de precisão decimal e arredondamento, o que é inaceitável em contextos que exigem exatidão absoluta.

---

## 4. NTT: A Evolução para o valores exatos Inteiros

Quando entramos no terreno da **Programação Competitiva, Criptografia ou Teoria dos Números**, não podemos aceitar um erro de $0.000001$. Precisamos de números inteiros exatos sob um módulo $M$.

A **NTT (Number Theoretic Transform)** é a versão "exata" da FFT. Em vez de usar o círculo unitário complexo, ela utiliza a **aritmética modular**.

| Característica | FFT | NTT |
| --- | --- | --- |
| **Domínio** | Números Complexos ($\mathbb{C}$) | Inteiros Módulo $M$ ($\mathbb{Z}_m$) |
| **Raiz da Unidade** | $e^{i\frac{2\pi}{n}}$ | Raiz primitiva $g$ tal que $g^n \equiv 1 \pmod M$ |
| **Precisão** | Sujeita a ruído de arredondamento | **Exatidão absoluta** |
| **Aplicação** | Engenharia e Física | Criptografia (RSA/Lattice) e Maratona de Programação |

Para a NTT funcionar, o módulo (M) geralmente precisa ser um "Primo de FFT" (como (998244353)), que possui propriedades específicas para permitir que a divisão recursiva do algoritmo ocorra perfeitamente.

Um detalhe muito importante no uso da NTT é que o resultado vem sempre em módulo do primo usado:

$$
R(x) = P(x)Q(x) \mod p
$$

e isso pode afetar o resultado do polinômio encontrado. Existem algumas formas de lidar com isso:

* **Aplicar um primo (p) tal que ele seja maior que qualquer possível coeficiente do resultado.**

  Se sabemos que os coeficientes de (P) e (Q) são limitados, podemos estimar um limite superior para os coeficientes do produto.

  Se:

  $$
  |a_i| \le A, \quad |b_i| \le B
  $$

  e cada polinômio tem no máximo (n) coeficientes, então um coeficiente do resultado pode ser limitado por algo como:

  $$
  |c_k| \le n \cdot A \cdot B
  $$

  Se escolhermos um primo (p) maior que esse valor máximo, então nenhuma redução modular realmente "altera" o resultado — o valor já está dentro do intervalo ($0, p$). Assim, o resultado obtido pela NTT coincide com o resultado inteiro exato.

---

* **Utilizar múltiplos primos e reconstruir o resultado com o Teorema Chinês do Resto (CRT).**

  Quando os coeficientes podem crescer muito (por exemplo, em multiplicação de inteiros gigantes), um único primo pode não ser suficiente.

  Nesse caso, podemos:

  1. Executar a NTT módulo (p_1)
  2. Executar novamente módulo (p_2)
  3. Repetir para (p_3, p_4, ...)

  Obtemos o resultado módulo cada primo, e então reconstruímos o valor inteiro original usando o Teorema Chinês do Resto.

  Se o produto dos primos escolhidos for maior que o maior coeficiente possível do resultado, a reconstrução será exata.

---

* **Escolher uma base menor na representação (no caso de multiplicação de inteiros).**

  Quando usamos NTT para multiplicar números grandes, normalmente representamos o número em uma base (B):

  $$
  N = \sum d_i B^i
  $$

  Se escolhermos (B) pequeno o suficiente (por exemplo (2^{15}) ou (10^3)), os coeficientes intermediários não crescem demais, o que facilita escolher um primo adequado.


---


# [Sessão de Códigos](https://cp-algorithms.com/algebra/fft.html#application-of-the-dft-fast-multiplication-of-polynomials)


## FFT

```c++
using cd = complex<double>;
const double PI = acos(-1);

void fft(vector<cd> & a, bool invert) {
    int n = a.size();

    for (int i = 1, j = 0; i < n; i++) {
        int bit = n >> 1;
        for (; j & bit; bit >>= 1)
            j ^= bit;
        j ^= bit;

        if (i < j)
            swap(a[i], a[j]);
    }

    for (int len = 2; len <= n; len <<= 1) {
        double ang = 2 * PI / len * (invert ? -1 : 1);
        cd wlen(cos(ang), sin(ang));
        for (int i = 0; i < n; i += len) {
            cd w(1);
            for (int j = 0; j < len / 2; j++) {
                cd u = a[i+j], v = a[i+j+len/2] * w;
                a[i+j] = u + v;
                a[i+j+len/2] = u - v;
                w *= wlen;
            }
        }
    }

    if (invert) {
        for (cd & x : a)
            x /= n;
    }
}
```


## NTT

```c++
const int mod = 7340033;
const int root = 5;
const int root_1 = 4404020;
const int root_pw = 1 << 20;

int power(int a, int b) {
    long long res = 1;
    while (b) {
        if (b & 1)
            res = res * a % mod;
        a = 1LL * a * a % mod;
        b >>= 1;
    }
    return (int)res;
}

int inverse(int a, int m) {
    // Fermat: a^(m-2) mod m
    return power(a, m - 2);
}


void fft(vector<int> & a, bool invert) {
    int n = a.size();

    for (int i = 1, j = 0; i < n; i++) {
        int bit = n >> 1;
        for (; j & bit; bit >>= 1)
            j ^= bit;
        j ^= bit;

        if (i < j)
            swap(a[i], a[j]);
    }

    for (int len = 2; len <= n; len <<= 1) {
        int wlen = invert ? root_1 : root;
        for (int i = len; i < root_pw; i <<= 1)
            wlen = (int)(1LL * wlen * wlen % mod);

        for (int i = 0; i < n; i += len) {
            int w = 1;
            for (int j = 0; j < len / 2; j++) {
                int u = a[i+j], v = (int)(1LL * a[i+j+len/2] * w % mod);
                a[i+j] = u + v < mod ? u + v : u + v - mod;
                a[i+j+len/2] = u - v >= 0 ? u - v : u - v + mod;
                w = (int)(1LL * w * wlen % mod);
            }
        }
    }

    if (invert) {
        int n_1 = inverse(n, mod);
        for (int & x : a)
            x = (int)(1LL * x * n_1 % mod);
    }
}
```


# Aplicações


## Multiplicacão de polinômios (FFT)


```c++
#include <bits/stdc++.h>
using namespace std;

// code for fft...

int main() {
    // Polinômios exemplo:
    // P(x) = 1 + 2x + 3x^2
    // Q(x) = 4 + 5x + 6x^2
    vector<int> P = {1, 2, 3};
    vector<int> Q = {4, 5, 6};

    int n = 1;
    int needed = P.size() + Q.size() - 1;

    while (n < needed)
        n <<= 1;

    vector<cd> fa(P.begin(), P.end());
    vector<cd> fb(Q.begin(), Q.end());

    fa.resize(n);
    fb.resize(n);

    // FFT
    fft(fa, false);
    fft(fb, false);

    // Multiplicação ponto a ponto
    for (int i = 0; i < n; i++)
        fa[i] *= fb[i];

    // FFT inversa
    fft(fa, true);

    // Resultado final (arredondando)
    vector<long long> R(needed);
    for (int i = 0; i < needed; i++)
        R[i] = llround(fa[i].real());

    // Imprimir resultado
    cout << "Coeficientes de R(x):\n";
    for (int i = 0; i < R.size(); i++)
        cout << R[i] << " ";
    cout << "\n";

    return 0;
}
```

## Multiplicacão de polinômios (NTT)


```c++
#include <bits/stdc++.h>
using namespace std;

// code for ntt...

int main() {
    // Exemplo:
    // P(x) = 1 + 2x + 3x^2
    // Q(x) = 4 + 5x + 6x^2

    vector<int> P = {1, 2, 3};
    vector<int> Q = {4, 5, 6};

    int n = 1;
    int needed = P.size() + Q.size() - 1;

    while (n < needed)
        n <<= 1;

    vector<int> fa(P.begin(), P.end());
    vector<int> fb(Q.begin(), Q.end());

    fa.resize(n);
    fb.resize(n);

    // NTT
    fft(fa, false);
    fft(fb, false);

    // Multiplicação ponto a ponto
    for (int i = 0; i < n; i++)
        fa[i] = ((int64_t) fa[i] * fb[i]) % mod;

    // NTT inversa
    fft(fa, true);

    // Resultado final (módulo mod)
    vector<int> R(needed);
    for (int i = 0; i < needed; i++)
        R[i] = fa[i];

    cout << "Coeficientes de R(x) modulo " << mod << ":\n";
    for (int x : R)
        cout << x << " ";
    cout << "\n";

    return 0;
}
```

### [All possible sums](https://cp-algorithms.com/algebra/fft.html#all-possible-sums)

We are given two arrays  
$a[]$  and  
$b[]$ . We have to find all possible sums  
$a[i] + b[j]$ , and for each sum count how often it appears.

For example for  
$a = [1,~ 2,~ 3]$  and  
$b = [2,~ 4]$  we get: then sum  
$3$  can be obtained in  
$1$  way, the sum  
$4$  also in  
$1$  way,  
$5$  in  
$2$ ,  
$6$  in  
$1$ ,  
$7$  in  
$1$ .

We construct for the arrays  
$a$  and  
$b$  two polynomials  
$A$  and  
$B$ . The numbers of the array will act as the exponents in the polynomial ( 
$a[i] \Rightarrow x^{a[i]}$ ); and the coefficients of this term will be how often the number appears in the array.

Then, by multiplying these two polynomials in  
$O(n \log n)$  time, we get a polynomial  
$C$ , where the exponents will tell us which sums can be obtained, and the coefficients tell us how often. To demonstrate this on the example:

 
$$(1 x^1 + 1 x^2 + 1 x^3) (1 x^2 + 1 x^4) = 1 x^3 + 1 x^4 + 2 x^5 + 1 x^6 + 1 x^7$$ 



# Exercícios:

- https://www.spoj.com/problems/POLYMUL/
- https://open.kattis.com/problems/aplusb
- https://www.codechef.com/SEPT19A/problems/PSUM

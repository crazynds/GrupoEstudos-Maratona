# 🌟 **Tutorial #0001** 🌟

E aí, pessoal! Vamos começar a preparar o nosso ambiente de programação? 💻🎯

Hoje, o tutorial vai ser sobre como montar o nosso setup de programação. Vamos lá? 🚀

## **1. Requisitos mínimos para começar:**
Antes de mais nada, vamos separar o básico que precisamos:

_Dispositivo com tela_:
Pode ser um notebook, tablet, PC ou até uma TV Smart (sim, dá para programar até na TV! 😄). Se tiver uma torradeira com monitor, também dá super certo! O ideal, para a maioria do curso, é um notebook.

_Teclado_:
Qualquer teclado serve. Se você estiver programando no tablet ou na TV Smart, me manda uma DM que eu te ajudo a configurar o ambiente. Para quem tem notebook ou PC, o teclado já deve estar junto e pode seguir com esse tutorial normalmente.

_Sistema operacional_:
Pode ser Windows, Linux ou Mac. Hoje, vou focar na configuração para Windows, mas o conceito vale para outros sistemas também.

## **2. Escolhendo um editor de texto!** 📝
Agora vamos falar sobre os editores de texto. O que usar para programar? 🤔

_CodeBlocks:_
Essa é a opção mais comum! Já vem com compilador para C/C++, o que facilita bastante no começo. Porém, tem um "detalhe"… depois de usar, é meio difícil sair do CodeBlocks. 🛑

_VSCode:_
O queridinho de muitos programadores! 🌟 Tem várias extensões incríveis e uma comunidade enorme por trás. A única coisa é que vocês vão precisar usar o terminal para rodar os programas, mas isso não é um problema, pois teremos um tutorial futuramente para aprender a usar o terminal. ⌨️

_Bloco de Notas:_
Quem diria, né? O simples Bloco de Notas também serve como editor de texto! É super básico, já vem instalado no sistema e dá para quebrar um galho no início. 😅

_Minha recomendação:_
No começo, instale CodeBlocks e VSCode. O Pozzer geralmente pede os trabalhos no CodeBlocks (então usem para os trabalhos dele 📚), e, ao mesmo tempo, podem se familiarizar com o VSCode para resolver os problemas de maratona. 💡


## 🔧**Instalando os Programas Necessários**!🔧

Agora que já temos os editores instalados, vamos preparar o ambiente para as linguagens que vamos usar no curso! 🚀

Neste grupo de estudos, vamos priorizar C, C++ e Python. Fiquem à vontade para escolher uma, ou até mesmo as 3, para praticar. 💡 Durante o curso CC, vocês vão usar mais o C, e aqui no grupo de estudos, vou focar um pouco mais em Python, então recomendo usarem ambas! 😉

### **Python** 🐍
Se você está no Windows, pode instalar o Python pela Microsoft Store.
👉 Instalem a versão 3.13 ou superior, se possível!

Para testar se deu tudo certo, abra o terminal (digite CMD na barra de busca do Windows) e digite: ```python --version```
Se não aparecer o erro de "programa não encontrado", significa que o Python foi instalado com sucesso! 🎉

### **C/C++** 💻
Instalar o GCC (Compilador de C/C++) no Windows pode ser um pouco mais complicado, mas não se preocupem! Sigam esse passo a passo:

- Baixem o arquivo .7z da última versão dos binários do MinGW aqui: https://github.com/niXman/mingw-builds-binaries/releases
- Dentro do arquivo ZIP, existe uma pasta chamada mingw64. Copiem essa pasta para o disco C do PC de vocês. O caminho final deve ser: `C:\mingw64`

Agora, precisamos adicionar o path ao ambiente do Windows. Para fazer isso:

- Digitem path na barra de busca do Windows e abram o programa Editar as Variáveis de Ambiente do Sistema.
- Cliquem em Variáveis de Ambiente.
- Na parte de cima, cliquem duas vezes na variável Path.
- Cliquem em Novo e colem o seguinte caminho: `C:\mingw64\bin`

Para testar se o GCC foi instalado corretamente, abram o terminal (digitem CMD na barra de busca do Windows) e digitem: ```gcc --version```
Se não der o erro de "programa não encontrado", então o compilador C/C++ foi instalado com sucesso! 🚀🎉
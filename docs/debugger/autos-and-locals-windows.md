---
title: Inspecionar variáveis - janelas Autos e locais | Microsoft Docs
ms.custom: seodec18
ms.date: 10/18/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 584704471f9346611f240a3a24e0d45cf2eec364
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068348"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>Inspecionar variáveis nas janelas Autos e locais

O **automóveis** e **Locals** windows mostram valores de variáveis durante a depuração. Os windows estão disponíveis somente durante uma sessão de depuração. O **automóveis** janela mostra as variáveis usadas em torno do ponto de interrupção atual. O **Locals** janela mostra as variáveis definidas no escopo local, que geralmente é o método ou a função atual. Se essa for a primeira vez que você tentou depurar o código, você talvez queira ler [corrigir bugs, escrevendo melhor C# código](../debugger/write-better-code-with-visual-studio.md) e [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes de prosseguir com este artigo.

 O **automóveis** janela está disponível para C#, código do Visual Basic, C++ e Python, mas não para JavaScript ou F#.
  
Para abrir o **automóveis** janela, durante a depuração, selecione **Debug** > **Windows** > **Autos**, ou pressione **Ctrl**+**Alt**+**V** > **um**.  

Para abrir o **Locals** janela, durante a depuração, selecione **Debug** > **Windows** > **Locals**, ou pressione **Alt**+**4**.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, consulte [visualizações de dados no Visual Studio para Mac](/visualstudio/mac/data-visualizations).

## <a name="use-the-autos-and-locals-windows"></a>Usar as janelas Autos e locais

Matrizes e objetos mostram na **automóveis** e **locais** windows como controles de árvore. Selecione a seta à esquerda de um nome de variável para expandir a exibição para mostrar os campos e propriedades. Aqui está um exemplo de uma <xref:System.IO.FileStream?displayProperty=fullName> do objeto na **Locals** janela:

![FileStream Locals](../debugger/media/locals-filestream.png "FileStream Locals")

Um valor de vermelho na **Locals** ou **Autos** janela significa que o valor foi alterado desde a última avaliação. A alteração pode ser proveniente de uma sessão de depuração anterior, ou porque você alterou o valor na janela.

O formato numérico de padrão nas janelas do depurador é decimal. Para alterá-la em hexadecimal, clique com botão direito no **Locals** ou **Autos** janela e selecione **exibição Hexadecimal**. Essa alteração afeta todas as janelas do depurador.

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>Editar valores de variáveis na janela Autos ou locais

Para editar os valores da maioria das variáveis na **automóveis** ou **Locals** windows, clique duas vezes o valor e digite o novo valor.

Você pode inserir uma expressão para um valor, por exemplo `a + b`. O depurador aceita expressões de linguagem mais válidas.

No código C++ nativo, talvez você precise qualificar o contexto de um nome de variável. Para obter mais informações, consulte [operador de contexto (C++)](../debugger/context-operator-cpp.md).

>[!CAUTION]
>Certifique-se de que compreender as consequências antes de alterar valores e expressões. Alguns problemas possíveis são:
>
>-   Avaliar algumas expressões pode alterar o valor de uma variável ou, de outra forma, afetar o estado do programa. Por exemplo, avaliando `var1 = ++var2` altera o valor de ambos `var1` e `var2`. Essas expressões são consideradas como tendo [efeitos colaterais](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Efeitos colaterais podem causar resultados inesperados se você não estiver ciente deles.
>
>-   Editar valores de ponto flutuante pode resultar em imprecisões secundárias devido à conversão decimal-binária de componentes fracionários. Até mesmo uma edição aparentemente inofensiva pode resultar em alterações para alguns dos bits na variável de ponto flutuante.

## <a name="change-the-context-for-the-autos-or-locals-window"></a>Alterar o contexto para a janela Autos ou locais

Você pode usar o **local de depuração** barra de ferramentas para selecionar uma função desejada, thread ou processo, que altera o contexto para o **Autos** e **locais** windows.

Para habilitar o **local de depuração** barra de ferramentas, clique em uma parte vazia da área da barra de ferramentas e selecione **local de depuração** da lista suspensa ou selecione **exibição**  >   **Barras de ferramentas** > **local de depuração**.

Definir um ponto de interrupção e iniciar a depuração. Quando o ponto de interrupção é atingido, as pausas de execução e você pode ver o local na **local de depuração** barra de ferramentas.

![Barra de ferramentas local de depuração](../debugger/media/debuglocationtoolbar.png "barra de ferramentas Depurar local")

## <a name="bkmk_whatvariables"></a> As variáveis na janela Autos (C#, C++, Visual Basic, Python)

 Linguagens de código diferentes exibem variáveis diferentes nos **automóveis** janela.

 - No C# e Visual Basic, o **Autos** janela exibirá qualquer variável usada na linha atual ou anterior. Por exemplo, em C# ou Visual Basic de código, declare as quatro variáveis a seguir:

   ```csharp
       public static void Main()
       {
          int a, b, c, d;
          a = 1;
          b = 2;
          c = 3;
          d = 4;
       }
   ```

   Defina um ponto de interrupção na linha `c = 3;`, e inicie o depurador. Quando a execução pausa, o **automóveis** janela será exibida:

   ![Autos-CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")

   O valor de `c` é 0, porque a linha `c = 3` ainda não foi executada.

 - No C++, o **automóveis** janela exibe as variáveis usadas em pelo menos três linhas antes da linha atual em que a execução está em pausa. Por exemplo, no código C++, declare seis variáveis:

   ```C++
       void main() {
           int a, b, c, d, e, f;
           a = 1;
           b = 2;
           c = 3;
           d = 4;
           e = 5;
           f = 6;
       }
   ```

    Defina um ponto de interrupção na linha `e = 5;` e executar o depurador. Quando a execução for interrompida, o **automóveis** janela será exibida:

    ![C++ Autos](../debugger/media/autos-cplus.png "Autos-c + +")

    A variável `e` não foi inicializada, porque a linha `e = 5` ainda não foi executada.

##  <a name="bkmk_returnValue"></a> Modo de exibição de valores de retorno de chamadas de método
 No código .NET e C++, você pode examinar os valores de retorno na **automóveis** janela ao passar sobre ou fora de uma chamada de método. Chamada de método exibindo retornam valores podem ser úteis quando eles não são armazenados em variáveis locais. Um método pode ser usado como um parâmetro, ou como o valor retornado de outro método.

 Por exemplo, a seguinte C# código adiciona os valores de retorno das duas funções:

```csharp
static void Main(string[] args)
{
    int a, b, c, d;
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    int x = sumVars(a, b) + subtractVars(c, d);
}

private static int sumVars(int i, int j)
{
    return i + j;
}

private static int subtractVars(int i, int j)
{
    return j - i;
}
```

Para ver os valores de retorno de `sumVars()` e `subtractVars()` chamadas de método na janela Autos:

1. Defina um ponto de interrupção a `int x = sumVars(a, b) + subtractVars(c, d);` linha.  
   
1. Iniciar a depuração e quando a execução pausa no ponto de interrupção, selecione **Step Over** ou pressione **F10**. Você deve ver os seguintes valores de retornados na **automóveis** janela:  
   
  ![Valor de retorno de Autos C# ](../debugger/media/autosreturnvaluecsharp2.png "Autos retornam valorC#")  
  
## <a name="see-also"></a>Consulte também  
 [O que é depuração?](../debugger/what-is-debugging.md)  
 [Corrigir bugs escrevendo um melhor código C#](../debugger/write-better-code-with-visual-studio.md)  
 [Introdução à depuração](../debugger/debugger-feature-tour.md) [janelas do depurador](../debugger/debugger-windows.md)

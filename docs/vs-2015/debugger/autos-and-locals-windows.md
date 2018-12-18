---
title: Autos e locais Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 51e62df0fb98a9c7b04b09b3e58fb52828e1bd5a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782473"
---
# <a name="autos-and-locals-windows"></a>Autos e locais Windows
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **Autos** janela (durante a depuração, **CTRL + ALT + V, A**, ou **depurar / Windows / automóveis**) e o **Locals** janela (durante a depuração,  **CTRL + ALT + V, L**, ou **depurar / Windows / locais**) são muito úteis quando você deseja ver valores de variáveis durante a depuração. O **Locals** janela exibe as variáveis que são definidas no escopo local, que geralmente é a função ou método que está sendo executado. O **automóveis** janela exibe as variáveis usadas ao redor da linha atual (o local em que o depurador é interrompido). Exatamente quais variáveis exibido é diferente em diferentes idiomas. Veja o que as variáveis que aparecem na janela Autos? abaixo.  
  
 Se você precisar de mais informações sobre depuração básica, consulte [Introdução ao depurador](../debugger/getting-started-with-the-debugger.md).  
  
## <a name="looking-at-objects-in-the-autos-and-locals-windows"></a>Examinando objetos nas janelas Autos e locais  
 Matrizes e objetos são exibidos nas janelas Autos e locais, como controles de árvore. Clique na seta à esquerda do nome da variável para expandir a exibição para mostrar os campos e propriedades. Aqui está um exemplo de uma <xref:System.IO.FileStream> do objeto na **Locals** janela:  
  
 ![Locals&#45;FileStream](../debugger/media/locals-filestream.png "Locals-FileStream")  
  
## <a name="what-variables-appear-in-the-autos-window"></a>Quais variáveis são exibidos na janela Autos?  
 Você pode usar o **automóveis** janela no código c#, Visual Basic e C++. O **automóveis** não tem suporte para JavaScript ou F#.  
  
 Em c# e Visual Basic, o **automóveis** janela exibirá qualquer variável usada na linha atual ou anterior. Por exemplo, se você declara quatro variáveis e defini-los da seguinte maneira:  
  
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
  
 Se você definir um ponto de interrupção na linha `c = 3`; e execute o depurador quando a execução para o **Autos** janela terá esta aparência:  
  
 ![Autos&#45;CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")  
  
 Observe que o valor de `c` é 0, porque a linha `c = 3` ainda não foi executada.  
  
 Em C++ a **automóveis** janela exibe as variáveis usadas pelo menos três linhas antes da linha atual (a linha em que a execução é interrompida). Se você declarar seis variáveis:  
  
```cpp  
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
  
 Se você definir um ponto de interrupção na linha `e = 5;` e executar o depurador, quando a execução para o **Autos** janela terá esta aparência:  
  
 ![Autos&#45;Cplus](../debugger/media/autos-cplus.png "Autos-Cplus")  
  
 Observe que a variável e não foi inicializada porque o código na linha `e = 5;` ainda não foi executada.  
  
 Você também pode ver os valores de retorno de funções e métodos em determinadas circunstâncias. Ver [valores de retorno de modo de exibição de chamadas de método](#bkmk_returnValue) abaixo.  
  
##  <a name="bkmk_returnValue"></a> Modo de exibição de valores de retorno de chamadas de método  
 No código .NET e C++, você pode examinar valores de retorno ao passar sobre ou fora de uma chamada de método. Essa funcionalidade é útil quando o resultado de uma chamada de método não é armazenado em uma variável local, por exemplo, quando um método é usado como um parâmetro ou como um valor de retorno de outro método.  
  
 O código c# a seguir adiciona os valores de retorno das duas funções:  
  
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
  
 Defina um ponto de interrupção de int `x = sumVars(a, b) + subtractVars(c, d);` linha.  
  
 Iniciar a depuração e quando a execução é interrompida no primeiro ponto de interrupção, pressione **F10 (Step Over)**. Você deve ver o seguinte a **Autos** janela:  
  
 ![AutosReturnValueCSharp2](../debugger/media/autosreturnvaluecsharp2.png "AutosReturnValueCSharp2")  
  
## <a name="why-are-variable-values-sometimes-red-in-locals-and-autos-windows"></a>Por que são valores de variáveis, às vezes, vermelho no windows locais e Autos?  
 Você pode perceber que o valor de uma variável, às vezes, é vermelho na **Locals** e **Autos** windows. Esses são valores de variáveis que foram alterados desde a última avaliação. A alteração pode ser proveniente de uma sessão de depuração anterior, ou porque o valor foi alterado na janela.  
  
## <a name="changing-the-numeric-format-of-a-variable-window"></a>Alterando o formato numérico de uma janela variável  
 Formato numérico padrão é decimal, mas você pode alterá-lo em hexadecimal. Clique com botão direito dentro de um **Locals** ou **Autos** janela e selecione **exibição Hexadecimal**. A alteração afeta todas as janelas do depurador.  
  
## <a name="editing-a-value-in-a-variable-window"></a>Edição de um valor em uma janela variável  
 Você pode editar os valores da maioria das variáveis que aparecem na **Autos**, **Locals**, **Assista**, e **QuickWatch** windows. Para obter informações sobre **Watch** e **QuickWatch** windows, consulte [inspeção e QuickWatch Windows](../debugger/watch-and-quickwatch-windows.md). Clicar duas vezes o valor que você deseja alterar e adicionar o novo o valor.  
  
 Você pode inserir uma expressão para um valor, por exemplo `a + b`. O depurador aceita expressões de linguagem mais válidas.  
  
 No código C++ nativo, talvez você precise qualificar o contexto de um nome de variável. Para obter mais informações, consulte [operador de contexto (C++)](../debugger/context-operator-cpp.md).  
  
 No entanto, você deve ter cuidado ao alterar valores. Estes são alguns problemas possíveis:  
  
-   Avaliar algumas expressões pode alterar o valor de uma variável ou, de outra forma, afetar o estado do programa. Por exemplo, avaliando `var1 = ++var2` altera o valor da `var1` e `var2`.  
  
     Expressões que alteram os dados são consideradas como tendo [efeitos colaterais](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)), que pode produzir resultados inesperados se você não estiver ciente deles. Verifique se que você entende as consequências de tal alteração antes de você fazê-lo.  
  
-   Editar valores de ponto flutuante pode resultar em imprecisões secundárias devido à conversão decimal-binária de componentes fracionários. Mesmo uma edição aparentemente inofensiva pode resultar em alterações em alguns bits menos significativos na variável de ponto flutuante.  
  
## <a name="debug-location-toolbar"></a>Depurar barra de ferramentas de local  
 Você pode usar o **local de depuração** barra de ferramentas para selecionar a função desejada, thread ou processo. Defina um ponto de interrupção e iniciar a depuração. (Se você não vir essa barra de ferramentas, você pode habilitá-lo clicando em uma parte vazia da área de barra de ferramentas. Você deve ver uma lista das barras de ferramentas; Selecione **local de depuração**). Quando o ponto de interrupção é atingido, a execução é interrompida e você pode ver a barra de ferramentas do local de depuração, que é a linha inferior do gráfico a seguir:  
  
 ![DebugLocationToolbar](../debugger/media/debuglocationtoolbar.png "DebugLocationToolbar")  
  
 Você também pode alterar o contexto de processos, threads ou chamadas de função diferente clicando duas vezes o elemento na **pilha de chamadas** janela, o **Threads** janela, ou o **processos** janela.  
  
## <a name="see-also"></a>Consulte também  
 [Janelas do depurador](../debugger/debugger-windows.md)






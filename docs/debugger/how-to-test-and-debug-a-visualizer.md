---
title: Como testar e depurar um visualizador | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- visualizers, testing
- visualizers, debugging
- debugging [Visual Studio], visualizers
ms.assetid: 5cc12ce8-c819-48e4-b487-98d403001b28
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1a81a8d094999585620ab6ab412c3b0610caf517
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348893"
---
# <a name="how-to-test-and-debug-a-visualizer"></a>Como testar e depurar um visualizador
Quando você tiver gravado um visualizador, precisará depurá-lo e testá-lo.

Uma maneira de testar um visualizador é instalando-o no Visual Studio e chamando-o de uma janela do depurador. (Consulte [como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md).) Se fizer isso, você precisará usar uma segunda instância do Visual Studio para anexar e depurar o visualizador, que está em execução na primeira instância do depurador.

Uma maneira mais fácil de depurar um visualizador é executar o visualizador de um driver de teste. As APIs do visualizador facilitam a criação desse driver, que é chamado de *host de desenvolvimento do visualizador*.

### <a name="to-create-a-visualizer-development-host"></a>Para criar um host de desenvolvimento do visualizador

1. Em sua classe do lado do depurador, inclua um método estático que cria um objeto <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerDevelopmentHost> e chama seu método de apresentação:

    ```csharp
    public static void TestShowVisualizer(object objectToVisualize)
    {
        VisualizerDevelopmentHost myHost = new VisualizerDevelopmentHost(objectToVisualize, typeof(DebuggerSide));
        myHost.ShowVisualizer();
    }
    ```

    Os parâmetros usados para criar o host são o objeto de dados que será exibido no visualizador (`objectToVisualize`) e o tipo de classe do lado do depurador.

2. Adicione a seguinte instrução para chamar `TestShowVisualizer`. Se você criou o visualizador em uma biblioteca de classe, precisará criar um executável para chamar a biblioteca de classes e colocar essa instrução em seu executável:

    ```csharp
    DebuggerSide.TestShowVisualizer(myString);
    ```

    Para obter um exemplo mais completo, consulte [Walkthrough: escrevendo um visualizador em C#](../debugger/walkthrough-writing-a-visualizer-in-csharp.md).

## <a name="see-also"></a>Veja também
- [Walkthrough: escrevendo um visualizador em C #](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)

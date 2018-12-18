---
title: Depurador de sombreador HLSL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.shaderviewer
ms.assetid: 4ccec541-3c49-42bd-972a-686eb3a88fbc
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e2c79491703ba2e20ae7bbb8c1303cfd5496a686
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760936"
---
# <a name="hlsl-shader-debugger"></a>Depurador de sombreador HLSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O depurador HLSL no analisador de gráficos do Visual Studio ajuda você a entender como o código do sombreador HLSL opera em condições reais do seu aplicativo.  
  
 Este é o depurador HLSL:  
  
 ![Depuração HLSL usando Assista e janelas de pilha de chamada. ](../debugger/media/gfx-diag-demo-hlsl-debugger-orientation.png "gfx_diag_demo_hlsl_debugger_orientation")  
  
## <a name="understanding-the-hlsl-debugger"></a>Noções básicas do depurador HLSL  
 O depurador HLSL pode ajudar você a entender os problemas que ocorrem no código do sombreador. A depuração do código HLSL no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] se parece com a depuração de código que foi escrito em outras linguagem, como no C++, C# ou Visual Basic. Você pode inspecionar o conteúdo das variáveis, definir pontos de interrupção, avançar no código e percorrer até a pilha de chamadas, exatamente como faz ao depurar outras linguagens.  
  
 No entanto, como as GPUs atingem alto desempenho executando código do sombreador em centenas de threads simultaneamente, o depurador HLSL foi projetado para trabalhar junto com as outras ferramentas do analisador de gráficos para apresentar todas essas informações de uma maneira que ajuda você a dar sentido -lo. Analisador de gráficos recria quadros capturados usando informações que foram gravadas no log de gráficos; o depurador HLSL não monitora a execução de GPU em tempo real conforme ele executa o código do sombreador. Como um log de gráficos contém informações suficientes para recriar qualquer parte da saída, e porque a análise de gráficos fornece ferramentas que podem ajudá-lo a identificar o pixel exato e o evento onde ocorre um erro, o depurador HLSL precisa apenas simular o sombreador exato thread que você está interessado. Isso significa que o trabalho do sombreador pode ser simulado na CPU, onde seu funcionamento interno é no modo de exibição completa. Isso é o que proporciona ao depurador HLSL uma experiência de depuração parecida com a de uma CPU.  
  
 No entanto, o depurador HLSL, atualmente, encontra-se limitado por estes motivos:  
  
- O depurador HLSL não dá suporte a editar e continuar, mas você pode fazer alterações em seus sombreadores e, em seguida, gerar novamente o quadro para ver os resultados.  
  
- Não é possível depurar um aplicativo e seu código de sombreador ao mesmo tempo. No entanto, você pode alternar entre eles.  
  
- É possível adicionar variáveis e registros à janela Inspeção, mas expressões não têm suporte.  
  
  Entretanto, o depurador HLSL oferece a melhor experiência de depuração e mais parecida com a de uma CPU, que de outra forma não seria possível.  
  
## <a name="hlsl-shader-edit--apply"></a>Editar e aplicar sombreador HLSL  
 O depurador de sombreador HLSL não oferece suporte para Editar e Continuar da mesma maneira que o depurador de CPU, porque o modelo de execução GPU não permite que o estado do sombreador seja desfeito. Em vez disso, o depurador HLSL oferece suporte a editar e aplicar, o que permite que você edite os arquivos de origem HLSL e escolha **aplicar** para regenerar o quadro para ver o efeito das alterações. Seu código de sombreador modificado é armazenado em um arquivo separado para preservar a integridade dos arquivos de origem HLSL originais do seu projeto, mas quando você estiver satisfeito com as alterações que você pode escolher **copiar para...** Para copiar as alterações em seu projeto. Usando esse recurso, você pode iterar rapidamente no código do sombreador que contém erros e eliminar as etapas caras de recompilação e captura do seu do fluxo de trabalho de depuração do HLSL.  
  
## <a name="hlsl-disassembly"></a>Desmontagem do HLSL  
 O depurador de sombreador HLSL fornece uma lista de assembly de sombreador HLSL à direita da lista de código-fonte do HLSL.  
  
## <a name="debugging-hlsl-code"></a>Depurando código HLSL  
 Você pode acessar o depurador HLSL do windows estágios de Pipeline ou histórico de Pixel.  
  
#### <a name="to-start-the-hlsl-debugger-from-the-graphics-pipeline-stages-window"></a>Para iniciar o depurador HLSL da janela Estágios de Pipeline Gráficos  
  
1.  No **estágios de Pipeline gráficos** janela, localize o estágio de pipeline associado ao sombreador que você deseja depurar.  
  
2.  Abaixo do título do estágio de pipeline, escolha **iniciar depuração**, que aparece como uma pequena seta verde.  
  
    > [!NOTE]
    >  Esse ponto de entrada no depurador HLSL depura apenas o primeiro thread do sombreador para o estágio correspondente, isto é, o primeiro vértice ou pixel que é processado. Você pode usar o histórico de Pixel para acessar outros threads dos estágios desse sombreador.  
  
#### <a name="to-start-the-hlsl-debugger-from-the-graphics-pixel-history"></a>Para iniciar o depurador HLSL do Histórico de Pixel de Gráficos  
  
1. No **histórico de Pixel de gráficos** janela, expanda a chamada de desenho associada ao sombreador que você deseja depurar. Cada chamada de desenho pode corresponder a vários primitivos.  
  
2. Nos detalhes da chamada de desenho, expanda um primitivo cuja contribuição de cor resultante sugira um bug em seu código de sombreador. Se vários primitivos sugerirem um bug, escolha o primeiro primitivo que o sugere, de modo que você possa evitar uma acumulação de erros, o que pode dificultar o diagnóstico do problema.  
  
3. Nos detalhes do primitivos, escolha se deseja depurar o **sombreador de vértice** ou o **sombreador de Pixel**. Depure o sombreador de vértices quando você suspeitar que o sombreador de pixel está correto, mas está gerando uma contribuição de cor incorreta porque o sombreador de vértices está passando constantes incorretas a ele. Caso contrário, depure o sombreador de pixel.  
  
    À direita do sombreador escolhido, escolha **iniciar depuração**, que aparece como uma pequena seta verde.  
  
   > [!NOTE]
   >  Esse ponto de entrada no depurador HLSL depura o thread do sombreador de pixel, que corresponde à chamada de desenho, ao primitivo e ao pixel que você escolheu, ou os threads do sombreador de vértices, cujos resultados são interpolados pela chamada de desenho, pelo primitivo e pelo pixel que você escolheu. No caso de sombreadores de vértices, você ainda pode refinar o ponto de entrada para um vértice específico expandindo os detalhes do sombreador de vértices.  
  
   Para obter exemplos sobre como usar o depurador HLSL para depurar erros do sombreador, consulte [exemplos](../debugger/graphics-diagnostics-examples.md) ou explicações passo a passo vinculadas na seção Consulte também.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Objetos ausentes devido ao sombreamento de vértice](../debugger/walkthrough-missing-objects-due-to-vertex-shading.md)   
 [Passo a passo: Depurando erros devido ao sombreamento de renderização](../debugger/walkthrough-debugging-rendering-errors-due-to-shading.md)   
 [Passo a passo: usando diagnóstico de gráficos para depurar um sombreador de cálculo](../debugger/walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader.md)




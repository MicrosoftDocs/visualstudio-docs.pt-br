---
title: 'Walkthrough: depuração de erros de renderização devido ao sombreamento | Microsoft Docs'
description: Siga uma investigação que encontre um bug de sombreador. Ele mostra o uso do Visual Studio Diagnóstico de Gráficos, incluindo o histórico de pixel de gráficos e o depurador HLSL.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 01875b05-cc7b-4add-afba-f2b776f86974
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 218b263d7e971a0d2bdaa72020bb7cb58c31e000
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387080"
---
# <a name="walkthrough-debugging-rendering-errors-due-to-shading"></a>Passo a passo: Como depurar erros de renderização devido ao sombreamento
Este tutorial demonstra como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] diagnóstico de gráficos para investigar um objeto que está colorido incorretamente devido a um bug de sombreador.

 Este guia passo a passo demonstra como:

- Examine o documento de log de gráficos para identificar os pixels que mostram o problema.

- Use a janela **histórico de pixels de gráficos** para examinar o estado de pixel mais de forma mais próxima.

- Use o **depurador HLSL** para examinar os sombreadores de pixel e vértice.

## <a name="scenario"></a>Cenário
 A coloração incorreta em objetos geralmente ocorre quando um sombreador de vértice passa um sombreador de pixel incorreto ou informações incompletas.

 Nesse cenário, você adicionou recentemente um objeto ao seu aplicativo. Você também adicionou um novo vértice e sombreadores de pixel para transformar o objeto e dar a ele uma aparência exclusiva. Quando você executa o aplicativo durante um teste, o objeto é renderizado em preto sólido. Usando Diagnóstico de Gráficos, você captura o problema em um log de gráficos para que você possa depurar o aplicativo. O problema é semelhante a esta imagem no aplicativo:

 ![O objeto é renderizado com cores incorretas.](media/gfx_diag_demo_render_error_shader_problem.png "gfx_diag_demo_render_error_shader_problem")

## <a name="investigation"></a>Investigação
 Usando as ferramentas de Diagnóstico de Gráficos, você pode carregar o documento de log de gráficos para inspecionar os quadros que foram capturados durante o teste.

#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro em um log de gráficos

1. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , carregue um log de gráficos que tem um quadro que mostra o modelo ausente. Uma janela de documento de novo log gráfico aparece em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Na parte superior dessa janela está a saída de destino de renderização do quadro selecionado. Na parte inferior está a **lista de quadros**, que exibe cada quadro capturado como uma imagem em miniatura.

2. Na **lista de quadros**, selecione um quadro no qual o objeto não tenha a aparência correta. O destino de renderização é atualizado para refletir o quadro selecionado. Nesse cenário, a janela documento de log de gráficos se parece com esta imagem:

    ![O documento de log de gráficos no Visual Studio.](media/gfx_diag_demo_render_error_shader_step_1.png "gfx_diag_demo_render_error_shader_step_1")

   Depois de selecionar um quadro que demonstre o problema, você pode usar a janela de **histórico de pixels de gráficos** para diagnosticar. A janela **histórico de pixels de gráficos** mostra os primitivos que poderiam ter tido um efeito em um pixel específico, seus sombreadores e quais são seus efeitos no destino de renderização, em ordem cronológica.

#### <a name="to-examine-a-pixel"></a>Para examinar um pixel

1. Abra a janela **histórico de pixels de gráficos** . Na barra de ferramentas **diagnóstico de gráficos** , escolha **histórico de pixel**.

2. Selecione um pixel para examinar. Na janela documento de log de gráficos, selecione um dos pixels no objeto que está com a cor incorreta:

    ![Selecionar um pixel exibe informações sobre seu histórico.](media/gfx_diag_demo_render_error_shader_step_2.png "gfx_diag_demo_render_error_shader_step_2")

    A janela **histórico de pixels de gráficos** é atualizada para refletir o pixel selecionado. Nesse cenário, a janela de **histórico de pixels de gráficos** tem a seguinte aparência:

    ![O histórico de pixel mostra um evento DrawIndexed.](media/gfx_diag_demo_render_error_shader_step_3.png "gfx_diag_demo_render_error_shader_step_3")

    Observe que o resultado do sombreador de pixel é preto opaco (0, 0, 0, 1) e que a **mesclagem de saída** combinou esse sombreador de pixel com a cor **anterior** do pixel de forma que o **resultado** também seja preto totalmente opaco.

   Depois de examinar um pixel que está incorretamente colorido e descobrir que a saída do sombreador de pixel não é a cor esperada, você pode usar o depurador HLSL para examinar o sombreador de pixel e descobrir o que aconteceu com a cor do objeto. Você pode usar o depurador HLSL para examinar o estado das variáveis HLSL durante a execução, percorrer o código HLSL e definir pontos de interrupção para ajudá-lo a diagnosticar o problema.

#### <a name="to-examine-the-pixel-shader"></a>Para examinar o sombreador de pixel

1. Inicia a depuração do sombreador de pixel. Na janela **histórico de pixels de gráficos** , na primitiva do objeto, ao lado de **sombreador de pixel**, escolha o botão **Iniciar Depuração** .

2. Nesse cenário, como o sombreador de pixel apenas passa a cor por meio do sombreador de vértice, é fácil observar que o sombreador de pixel não é a origem do problema.

3. Posicione o ponteiro sobre `input.color` . Observe que seu valor é totalmente opaco preto (0, 0, 0, 1).

    ![O membro "Color" de "Input" é preto.](media/gfx_diag_demo_render_error_shader_step_5.png "gfx_diag_demo_render_error_shader_step_5")

    Nesse cenário, o exame revela que a cor incorreta é provavelmente o resultado de um sombreador de vértice que não fornece as informações de cor corretas para o sombreador de pixel operar.

   Depois de determinar que o sombreador de vértice provavelmente não está fornecendo as informações certas para o sombreador de pixel, a próxima etapa é examinar o sombreador de vértice.

#### <a name="to-examine-the-vertex-shader"></a>Para examinar o sombreador de vértice

1. Inicia a depuração do sombreador de vértice. Na janela **histórico de pixels de gráficos** , na primitiva do objeto, ao lado de **sombreador de vértice**, escolha o botão **Iniciar Depuração** .

2. Localize a estrutura de saída do sombreador de vértice — essa é a entrada para o sombreador de pixel. Nesse cenário, o nome dessa estrutura é `output` . Examine o código do sombreador de vértice e observe que o `color` membro da `output` estrutura foi explicitamente definido como preto totalmente opaco, talvez como resultado de esforços de depuração de alguém.

3. Confirme se o membro de cor nunca é copiado da estrutura de entrada. Como o valor de `output.color` é definido como preto totalmente opaco logo antes da `output` estrutura ser retornada, é uma boa ideia certificar-se de que o valor de `output` não foi inicializado corretamente em uma linha anterior. Percorra o código do sombreador de vértice até chegar à linha que define `output.color` como preto enquanto você observa o valor de `output.color` . Observe que o valor de `output.color` não é inicializado até que seja definido como preto. Isso confirma que a linha de código que define `output.color` para preto deve ser modificada, em vez de excluída.

    ![O valor de "output. Color" é preto.](media/gfx_diag_demo_render_error_shader_step_7.png "gfx_diag_demo_render_error_shader_step_7")

   Depois de determinar que a causa do problema de renderização é que o sombreador de vértice não fornece o valor de cor correto para o sombreador de pixel, você pode usar essas informações para corrigir o problema. Nesse cenário, você pode corrigi-lo alterando o seguinte código no sombreador de vértice

```hlsl
output.color = float3(0.0f, 0.0f, 0.0f);
```

 como

```hlsl
output.color = input.color;
```

 Esse código apenas passa a cor do vértice por meio dos vértices do objeto sem modificações – sombreadores de vértice mais complexos podem modificar a cor antes de passá-la. O código do sombreador de vértice corrigido deve ser semelhante ao seguinte:

 ![O código do sombreador do vértice corrigido.](media/gfx_diag_demo_render_error_shader_step_8.png "gfx_diag_demo_render_error_shader_step_8")

 Depois de corrigir o código, recompile-o e execute o aplicativo novamente para descobrir que o problema de renderização foi resolvido.

 ![O objeto é renderizado com as cores corretas.](media/gfx_diag_demo_render_error_shader_resolution.png "gfx_diag_demo_render_error_shader_resolution")

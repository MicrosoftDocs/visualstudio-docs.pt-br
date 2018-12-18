---
title: 'Passo a passo: Objetos ausentes devido ao sombreamento de vértice | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e42b54a0-8092-455c-945b-9ecafb129d93
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ecff22d99eb995f0dbe70e93783460f4343d74f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745932"
---
# <a name="walkthrough-missing-objects-due-to-vertex-shading"></a>Instruções passo a passo: objetos ausentes devido ao sombreamento de vértice
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo demonstra como usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ferramentas de diagnóstico de gráficos para investigar um objeto que está faltando devido a um erro que ocorre durante o estágio de sombreador de vértice.  
  
 Este passo a passo ilustra essas tarefas:  
  
-   Usando o **lista de eventos gráficos** para localizar fontes potenciais do problema.  
  
-   Usando o **estágios de Pipeline gráficos** janela para verificar o efeito do `DrawIndexed` chamadas à API do Direct3D.  
  
-   Usando o **depurador HLSL** para examinar o sombreador de vértices.  
  
-   Usando o **pilha de chamadas do evento de gráficos** para ajudar a localizar a origem de uma constante de HLSL incorreta.  
  
## <a name="scenario"></a>Cenário  
 Uma das causas comuns de um objeto ausente em um aplicativo 3D ocorre quando o sombreador de vértices transforma os vértices do objeto de uma forma incorreta ou inesperada — por exemplo, o objeto pode ser dimensionado para um tamanho muito pequeno ou transformado, de modo que ele seja exibido por trás da câmera , em vez de na frente dele.  
  
 Nesse cenário, quando o aplicativo é executado para testá-lo, o plano de fundo é renderizado conforme o esperado, mas um dos objetos não aparece. Usando o diagnóstico de gráficos, você capturar o problema para um log de gráficos para que você possa depurar o aplicativo. O problema se parece com isso no aplicativo:  
  
 ![O objeto não pode ser visto. ](../debugger/media/gfx-diag-demo-missing-object-shader-problem.png "gfx_diag_demo_missing_object_shader_problem")  
  
## <a name="investigation"></a>Investigação  
 Usando as ferramentas de diagnóstico de gráficos, você pode carregar o arquivo de log de gráficos para inspecionar os quadros que foram capturados durante o teste.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro no log de gráficos  
  
1. No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], carregar um log de gráficos que contém um quadro que exibe o objeto ausente. Uma nova guia do log de gráficos aparece no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Na parte superior dessa guia é a saída de destino de renderização do quadro selecionado. Na parte inferior é parte do **lista de quadros**, que exibe cada quadro capturado como uma imagem em miniatura.  
  
2. No **lista de quadros**, selecione um quadro que demonstra que o objeto não é exibido. O destino de renderização é atualizado para refletir o quadro selecionado. Nesse cenário, os gráficos de log guia semelhante ao seguinte:  
  
    ![Documento de log de gráficos no Visual Studio](../debugger/media/gfx-diag-demo-missing-object-shader-step-1.png "gfx_diag_demo_missing_object_shader_step_1")  
  
   Depois de selecionar um quadro que demonstra o problema, você pode começar a diagnosticá-lo usando o **lista de eventos gráficos**. O **lista de eventos gráficos** contém todas as chamadas de API do Direct3D que foi feita para renderizar o quadro ativo, por exemplo, chamadas de API para configurar o estado do dispositivo, para criar e atualizar os buffers de e para desenhar objetos que aparecem no quadro. Muitos tipos de chamadas são interessantes porque há muitas vezes (mas nem sempre) uma alteração correspondente no destino de renderização quando o aplicativo está funcionando conforme o esperado, por exemplo desenhar, expedição, cópia ou chamadas claras. Chamadas de desenho são particularmente interessantes porque cada um deles representa a geometria que o aplicativo processado (chamadas de expedição também podem renderizar a geometria).  
  
   Porque você sabe que o objeto ausente não é que está sendo desenhado para o destino de renderização (neste caso) — mas que o restante da cena é desenhado conforme esperado — você pode usar o **lista de eventos gráficos** junto com o **Pipeline gráfica Estágios** tool para determinar qual chamada de desenho corresponde à geometria do objeto ausente. O **estágios de Pipeline gráficos** janela mostra a geometria que foi enviada para cada chamada de desenho, independentemente de seu efeito sobre o destino de renderização. Conforme você percorrer as chamadas draw, os estágios de pipeline são atualizados para mostrar a geometria que está associada essa chamada, e a saída de destino de renderização é atualizada para mostrar o estado do destino de renderização depois que a chamada foi concluída.  
  
#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>Para localizar a chamada de desenho para a geometria ausente  
  
1. Abra o **lista de eventos gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **lista de eventos**.  
  
2. Abra o **estágios de Pipeline gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **estágios de Pipeline**.  
  
3. Conforme você percorrer cada chamada de desenho **lista de eventos gráficos** janela, assista a **estágios de Pipeline gráficos** janela para o objeto ausente. Para facilitar essa tarefa, digite "Desenhar" na **pesquisa** caixa no canto superior direito das **lista de eventos gráficos** janela. Isso filtra a lista para que ele contenha somente os eventos que possuam "Desenho" em seus títulos.  
  
    No **estágios de Pipeline gráficos** janela, o **Assembler de entrada** estágio mostra a geometria do objeto antes de transformados e o **sombreador de vértices** estágio mostra a mesma objeto depois que ele é transformado. Nesse cenário, você sabe que você encontrou o objeto ausente quando ele for exibido na **Assembler de entrada** estágio e nada é exibido na **sombreador de vértices** estágio.  
  
   > [!NOTE]
   >  Se outros estágios de geometria — por exemplo, os estágios de sombreador Hull, o sombreador de domínio ou o sombreador de geometria — processar o objeto, eles podem ser a causa do problema. Normalmente, o problema está relacionado ao mais cedo em que o resultado não é exibido ou é exibido de forma inesperada.  
  
4. Pare quando atingir a chamada de desenho que corresponde ao objeto ausente. Nesse cenário, o **estágios de Pipeline gráficos** janela indica que a geometria foi emitida para a GPU (indicada pela miniatura Assembler de entrada), mas não aparecerão no destino de renderização porque algo deu errado durante a estágio de sombreador de vértice (indicado pela miniatura do sombreador de vértices):  
  
    ![Um evento DrawIndexed e seu efeito no pipeline](../debugger/media/gfx-diag-demo-missing-object-shader-step-2.png "gfx_diag_demo_missing_object_shader_step_2")  
  
   Depois de confirmar que o aplicativo emitiu uma chamada de desenho para geometria do objeto ausente e descobrir que o problema ocorre durante o estágio de sombreador de vértice, você pode usar o depurador HLSL para examinar o sombreador de vértices e descobrir o que aconteceu com a geometria do objeto. Você pode usar o depurador HLSL para examinar o estado das variáveis HLSL durante a execução, percorrer o código HLSL e defina pontos de interrupção para ajudá-lo a diagnosticar o problema.  
  
#### <a name="to-examine-the-vertex-shader"></a>Para examinar o sombreador de vértice  
  
1. Inicie o estágio de sombreador de vértice de depuração. No **estágios de Pipeline gráficos** janela, sob o **sombreador de vértice** estágio, escolha o **iniciar depuração** botão.  
  
2. Porque o **Assembler de entrada** estágio é exibido para fornecer dados adequados para o sombreador de vértices e as **sombreador de vértices** estágio é exibida não produzir nenhuma saída, você deseja examinar a saída do sombreador de vértice estrutura, `output`. Conforme você percorre o código HLSL, você examinar parecer quando `output` é modificado.  
  
3. Na primeira vez em que `output` for modificado, o membro `worldPos` é gravado.  
  
    ![O valor "output.worldPos" aparece razoável](../debugger/media/gfx-diag-demo-missing-object-shader-step-4.png "gfx_diag_demo_missing_object_shader_step_4")  
  
    Porque seu valor parece ser razoável, continuar percorrendo o código até a próxima linha modifica `output`.  
  
4. Na próxima vez em que `output` for modificado, o membro `pos` é gravado.  
  
    ![O valor de "output.pos" foi zerado](../debugger/media/gfx-diag-demo-missing-object-shader-step-5.png "gfx_diag_demo_missing_object_shader_step_5")  
  
    Neste momento, o valor da `pos` membro — todos os zeros — parece suspeito. Em seguida, você deseja determinar como `output.pos` passou a ter um valor de todos os zeros.  
  
5. Observe que `output.pos` obtém seu valor de uma variável chamada `temp`. Na linha anterior, você verá que o valor de `temp` é o resultado da multiplicação seu valor anterior por uma constante chamada `projection`. Você suspeita que `temp`do valor suspeita é o resultado dessa multiplicação. Quando você posiciona o ponteiro em `projection`, você notar que seu valor é também todos os zeros.  
  
    ![A matriz de projeção contém uma transformação incorreta](../debugger/media/gfx-diag-demo-missing-object-shader-step-6.png "gfx_diag_demo_missing_object_shader_step_6")  
  
    Nesse cenário, o exame revela que `temp`do valor suspeita provavelmente é causado por seu multiplicação por `projection`e porque `projection` é uma constante que tem que deve conter uma matriz de projeção, você sabe que não deveria contém todos os zeros.  
  
   Depois de determinar que a constante HLSL `projection`— passado para o sombreador pelo seu aplicativo — é a probabilidade de origem do problema, a próxima etapa é encontrar o local no código-fonte do seu aplicativo onde o buffer de constantes é preenchido. Você pode usar o **pilha de chamadas do evento de gráficos** para localizar esse local.  
  
#### <a name="to-find-where-the-constant-is-set-in-your-apps-source-code"></a>Para localizar onde a constante é definida no código-fonte do seu aplicativo  
  
1. Abra o **pilha de chamadas do evento de gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **pilha de chamadas do evento de gráficos**.  
  
2. Navegue até a pilha de chamada no código-fonte do seu aplicativo. No **pilha de chamadas do evento de gráficos** janela, escolha a chamada mais alto para ver se o buffer de constantes estiver sendo preenchido lá. Se não for, continue a pilha de chamadas até encontrar onde ele está sendo preenchido. Nesse cenário, você descobre que o buffer de constantes está sendo preenchido — usando o `UpdateSubresource` API do Direct3D — ainda mais para cima a pilha de chamadas em uma função que é denominada `MarbleMaze::Render`, e que seu valor vem de um objeto de buffer de constantes que é chamado `m_marbleConstantBufferData` :  
  
    ![O código que define o buffer de constantes do objeto](../debugger/media/gfx-diag-demo-missing-object-shader-step-7.png "gfx_diag_demo_missing_object_shader_step_7")  
  
   > [!TIP]
   >  Se estiver depurando seu aplicativo ao mesmo tempo, você pode definir um ponto de interrupção neste local e será atingido quando o próximo quadro é renderizado. Em seguida, você pode inspecionar os membros da `m_marbleConstantBufferData` para confirmar que o valor da `projection` membro está definido como todos os zeros quando o buffer de constantes é preenchido.  
  
   Depois de encontrar o local em que o buffer de constantes estiver sendo preenchido e descobrir que seus valores provenientes de variável `m_marbleConstantBufferData`, a próxima etapa é descobrir onde o `m_marbleConstantBufferData.projection` membro está definido como todos os zeros. Você pode usar **localizar todas as referências** examinar rapidamente para o código que altera o valor de `m_marbleConstantBufferData.projection`.  
  
#### <a name="to-find-where-the-projection-member-is-set-in-your-apps-source-code"></a>Para localizar onde o membro de projeção é definido no código-fonte do seu aplicativo  
  
1. Localizar referências a `m_marbleConstantBufferData.projection`. Abra o menu de atalho para a variável `m_marbleConstantBufferData`e, em seguida, escolha **localizar todas as referências**.  
  
2. Para navegar até o local da linha no código-fonte do seu aplicativo em que o `projection` membro será modificado, escolha a linha em de **Find Symbol Results** janela. Porque o primeiro resultado que modifica o membro de projeção pode não ser a causa do problema, você talvez precise examinar várias áreas do código-fonte do seu aplicativo.  
  
   Depois de localizar o local onde `m_marbleConstantBufferData.projection` estiver definido, você pode examinar o código ao redor do código-fonte para determinar a origem do valor incorreto. Nesse cenário, você descobre que o valor de `m_marbleConstantBufferData.projection` é definido como uma variável local denominada `projection` antes que ela foi inicializada com um valor que é fornecido pelo código `m_camera->GetProjection(&projection);` na próxima linha.  
  
   ![A projeção de mármore é definida antes da inicialização](../debugger/media/gfx-diag-demo-missing-object-shader-step-9.png "gfx_diag_demo_missing_object_shader_step_9")  
  
   Para corrigir o problema, você move a linha de código que define o valor de `m_marbleConstantBufferData.projection` após a linha que inicializa o valor da variável local `projection`.  
  
   ![O C corrigido&#43; &#43; o código-fonte](../debugger/media/gfx-diag-demo-missing-object-shader-step-10.png "gfx_diag_demo_missing_object_shader_step_10")  
  
   Depois de corrigir o código, você pode recriá-lo e executar o aplicativo novamente para descobrir que o problema de renderização é resolvido:  
  
   ![O objeto agora é exibido. ](../debugger/media/gfx-diag-demo-missing-object-shader-resolution.png "gfx_diag_demo_missing_object_shader_resolution")




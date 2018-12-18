---
title: 'Passo a passo: Objetos ausentes devido ao Pipeline configurado incorretamente | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ed8ac02d-b38f-4055-82fb-67757c2ccbb9
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 88e313b7db1306465bce530eea41e875227abc0e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49855177"
---
# <a name="walkthrough-missing-objects-due-to-misconfigured-pipeline"></a>Instruções passo a passo: objetos ausentes devido ao pipeline configurado incorretamente
Este passo a passo demonstra como usar o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ferramentas de diagnóstico de gráficos para investigar um objeto que está faltando devido a um sombreador de pixel não definidas.  
  
 Este passo a passo ilustra essas tarefas:  
  
-   Usando o **lista de eventos gráficos** para localizar fontes potenciais do problema.  
  
-   Usando o **estágios de Pipeline gráficos** janela para examinar o efeito do `DrawIndexed` chamada à API do Direct3D.  
  
-   Inspecionando o contexto de dispositivo para confirmar que um estágio de sombreador não foi definido.  
  
-   Usando o **estágios de Pipeline gráficos** janela junto com o **pilha de chamadas do evento de gráficos** para ajudar a encontrar a fonte do sombreador de pixel não definidas.  
  
## <a name="scenario"></a>Cenário  
 Quando um objeto está ausente em um aplicativo 3D, às vezes, é porque um dos estágios do sombreador não está definido antes que o objeto é renderizado. Em aplicativos que têm necessidades de processamento simples, a origem desse erro é geralmente localizada em algum lugar na pilha de chamadas de chamada de desenho do objeto. No entanto, como uma otimização, alguns objetos de lote juntos de aplicativos que têm programas de sombreador, texturas ou outros dados em comum para minimizar a alteração de estadom sobrecarga. Esses aplicativos, a origem do erro pode ser escondida no sistema de envio em lote, em vez de localizado na pilha de chamadas da chamada de desenho. O cenário neste passo a passo demonstra um aplicativo que tem necessidades de processamento simples e, portanto, a origem do erro pode ser encontrada na pilha de chamadas.  
  
 Nesse cenário, quando o aplicativo é executado para testá-lo, o plano de fundo é renderizado conforme o esperado, mas um dos objetos não for exibido. Usando o diagnóstico de gráficos, você capturar o problema para um log de gráficos para que você possa depurar o aplicativo. O problema se parece com isso no aplicativo:  
  
 ![O objeto não pode ser visto](media/gfx_diag_demo_misconfigured_pipeline_problem.png "gfx_diag_demo_misconfigured_pipeline_problem")  
  
## <a name="investigation"></a>Investigação  
 Usando as ferramentas de diagnóstico de gráficos, você pode carregar o documento de log de gráficos para inspecionar os quadros que foram capturados durante o teste.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro no log de gráficos  
  
1. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar um documento de log de gráficos que contém um quadro que exibe o objeto ausente. Uma nova guia do log de gráficos aparece no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Na parte superior dessa guia é a saída de destino de renderização do quadro selecionado. Na parte inferior é parte do **lista de quadros**, que exibe cada quadro capturado como uma imagem em miniatura.  
  
2. No **lista de quadros**, selecione um quadro que demonstra que o objeto não é exibido. O destino de renderização é atualizado para refletir o quadro selecionado. Nesse cenário, os gráficos de log guia semelhante ao seguinte:  
  
    ![Documento de log de gráficos no Visual Studio](media/gfx_diag_demo_misconfigured_pipeline_step_1.png "gfx_diag_demo_misconfigured_pipeline_step_1")  
  
   Depois de selecionar um quadro que demonstra o problema, você pode começar a diagnosticá-lo usando o **lista de eventos gráficos**. O **lista de eventos gráficos** contém todas as chamadas de API do Direct3D que foi feita para renderizar o quadro ativo — por exemplo, para configurar o estado do dispositivo, para criar e atualizar os buffers de e para desenhar objetos que aparecem no quadro. Muitos tipos de chamadas — por exemplo, desenho, expedição, cópia ou chamadas claras — são interessantes porque há muitas vezes (mas nem sempre) uma alteração correspondente no destino de renderização quando o aplicativo está funcionando conforme o esperado. Chamadas de desenho são particularmente interessantes porque cada um deles representa a geometria que o aplicativo renderizado.  
  
   Porque você sabe que o destino de renderização não contém o campo ausente do objeto, mas também que não parece haver outros erros, você pode usar o **lista de eventos gráficos** junto com o **estágios de Pipeline gráficos**tool para determinar qual chamada de desenho corresponde à geometria do objeto ausente. O **estágios de Pipeline gráficos** janela mostra a geometria que foi enviada para cada chamada de desenho, independentemente de seu efeito sobre o destino de renderização. Conforme você percorrer as chamadas draw, os estágios de pipeline são atualizados para mostrar a geometria que está associada com cada chamada conforme ela flui através de cada estágio habilitado e a saída de destino de renderização é atualizada para mostrar o estado do destino de renderização depois da chamada ser concluída.  
  
#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>Para localizar a chamada de desenho para a geometria ausente  
  
1. Abra o **lista de eventos gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **lista de eventos**.  
  
2. Abra o **estágios de Pipeline gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **estágios de Pipeline**.  
  
3. Conforme você percorrer cada chamada de desenho **lista de eventos gráficos** janela, assista a **estágios de Pipeline gráficos** janela para o objeto ausente. Para facilitar essa tarefa, digite "Desenhar" na **pesquisa** caixa no canto superior direito das **lista de eventos gráficos** janela. Isso filtra a lista para que ele contenha somente os eventos que possuam "Desenho" em seus títulos.  
  
    No **estágios de Pipeline gráficos** janela, o **Assembler de entrada** estágio mostra a geometria do objeto antes que seja transformada e o **sombreador de vértices** estágio mostra a mesma objeto depois que ele é transformado. Nesse cenário, observe que o **estágios de Pipeline gráficos** janela mostra o **Assembler de entrada** e **sombreador de vértices** estágios, mas não o **sombreador de Pixel**  estágio para uma das chamadas de desenho.  
  
   > [!NOTE]
   >  Se outros estágios de pipeline — por exemplo, o sombreador hull, o sombreador de domínio ou estágios de sombreador de geometria — processar o objeto, qualquer um deles pode ser a causa do problema. Normalmente, o problema está relacionado ao mais cedo em que o resultado não é exibido ou é exibido de forma inesperada.  
  
4. Pare quando atingir a chamada de desenho que corresponde ao objeto ausente. Nesse cenário, o **estágios de Pipeline gráficos** janela indica que a geometria foi emitida para a GPU (indicado pela presença da **Assembler de entrada** estágio) e transformados (indicado pelo  **Sombreador de vértice** estágio), mas não aparecerão no destino de renderização porque não parece haver um sombreador de pixel do Active Directory (indicado pela ausência do **sombreador de Pixel** estágio). Nesse cenário, você pode até ver a silhueta do objeto ausente na **fusão de saída** estágio:  
  
    ![Um evento DrawIndexed e seu efeito no pipeline](media/gfx_diag_demo_misconfigured_pipeline_step_2.png "gfx_diag_demo_misconfigured_pipeline_step_2")  
  
   Depois de confirmar que o aplicativo emitiu uma chamada de desenho para geometria do objeto ausente e descobrir que o estágio de sombreador de pixel estava inativo, você pode examinar o estado do dispositivo para confirmar suas descobertas. Você pode usar o **tabela de objetos gráficos** para examinar o contexto de dispositivo e outros dados de objeto do Direct3D.  
  
#### <a name="to-examine-device-context"></a>Para examinar o contexto de dispositivo  
  
1. Abra o **contexto de dispositivo d3d11**. No **estágios de Pipeline gráficos** janela, escolha o **ID3D11DeviceContext** link que faz parte do `DrawIndexed` chamada que é exibida na parte superior da janela.  
  
2. Examinar o estado do dispositivo que é exibido na **contexto de dispositivo d3d11** tab para confirmar que nenhum sombreador de pixel estava ativo durante a chamada de desenho. Nesse cenário, o **informações gerais do sombreador**— exibido sob **estado de sombreador de pixel**— indica que o sombreador é **nulo**:  
  
    ![O contexto do dispositivo D3D 11 mostra o estado do sombreador de pixel](media/gfx_diag_demo_misconfigured_pipeline_step_4.png "gfx_diag_demo_misconfigured_pipeline_step_4")  
  
   Depois de confirmar que o sombreador de pixel foi definido como null por seu aplicativo, a próxima etapa é encontrar o local no código-fonte do seu aplicativo em que o sombreador é definido. Você pode usar o **lista de eventos gráficos** junto com o **pilha de chamadas do evento de gráficos** para localizar esse local.  
  
#### <a name="to-find-where-the-pixel-shader-is-set-in-your-apps-source-code"></a>Para localizar onde o sombreador de pixel é definido no código-fonte do seu aplicativo  
  
1. Encontre o `PSSetShader` chamada que corresponde ao objeto ausente. No **lista de eventos gráficos** janela, insira "desenho; PSSetShader"no **pesquisa** caixa no canto superior direito das **lista de eventos gráficos** janela. Isso filtra a lista para que ele contenha somente os eventos de "PSSetShader" e eventos que possuam "Desenho" em seus títulos. Escolha o primeiro `PSSetShader` chamada que aparece antes da chamada de desenho do objeto ausente.  
  
   > [!NOTE]
   >  `PSSetShader` não será exibida na **lista de eventos gráficos** se ele não foi definido durante esse quadro de janela. Normalmente, isso ocorre somente se o sombreador de pixel apenas um é usado para todos os objetos, ou se o `PSSetShader` chamada acidentalmente foi ignorada durante esse período. Em ambos os casos, é recomendável que você pesquisa o código-fonte do aplicativo para `PSSetShader` chamadas e use tradicional de técnicas de depuração para examinar o comportamento dessas chamadas.  
  
2. Abra o **pilha de chamadas do evento de gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **pilha de chamadas do evento de gráficos**.  
  
3. Use a pilha de chamadas para localizar o `PSSetShader` chamar no código-fonte do seu aplicativo. No **pilha de chamadas do evento de gráficos** janela, escolha a chamada mais alto e examine o valor que está sendo definido como o sombreador de pixel. O sombreador de pixel pode ser definido diretamente como nulo, ou o nulo de valor pode ocorrer devido a um argumento que foi passado para a função ou outro estado. Se ele não é definido diretamente, você poderá localizar a origem do valor nulo em algum lugar para cima a pilha de chamadas. Nesse cenário, você descobre que o sombreador de pixel está sendo definido diretamente para `nullptr` na função principal, que é denominado `CubeRenderer::Render`:  
  
    ![O código que não inicializam o sombreador de pixel](media/gfx_diag_demo_misconfigured_pipeline_step_5.png "gfx_diag_demo_misconfigured_pipeline_step_5")  
  
   > [!NOTE]
   >  Se você não conseguir localizar a origem do valor nulo apenas examinando a pilha de chamadas, é recomendável que você defina um ponto de interrupção condicional no `PSSetShader` chamar, de modo que a execução do programa é interrompida quando o sombreador de pixel será definido como null. Em seguida, reinicie o aplicativo no modo de depuração e usar técnicas de depuração tradicionais para localizar a origem do valor nulo.  
  
   Para corrigir o problema, atribua o sombreador de pixel correto, usando o primeiro parâmetro do `ID3D11DeviceContext::PSSetShader` chamada à API.  
  
   ![O C corrigido&#43; &#43; o código-fonte](media/gfx_diag_demo_misconfigured_pipeline_step_6.png "gfx_diag_demo_misconfigured_pipeline_step_6")  
  
   Depois de corrigir o código, você pode recriá-lo e executar o aplicativo novamente para verificar se o problema de renderização é resolvido:  
  
   ![O objeto agora é exibido](media/gfx_diag_demo_misconfigured_pipeline_resolution.jpg "gfx_diag_demo_misconfigured_pipeline_resolution")
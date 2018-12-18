---
title: 'Passo a passo: Objetos ausentes devido ao estado do dispositivo | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1b0d2bbd-0729-4aa5-8308-70c5bf1468c5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8d1e31063bf5cf24fa5b19b1446b4c41f2dd7bd2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49869753"
---
# <a name="walkthrough-missing-objects-due-to-device-state"></a>Instruções passo a passo: objetos ausentes devido ao estado do dispositivo
Este passo a passo demonstra como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] diagnóstico de gráficos para investigar um objeto que está faltando devido a configurado incorretamente o estado do dispositivo.  
  
 Este passo a passo demonstra como:  
  
-   Use o **lista de eventos gráficos** para localizar fontes potenciais do problema.  
  
-   Use o **estágios de Pipeline gráficos** janela para verificar o efeito do `DrawIndexed` chamadas à API do Direct3D.  
  
-   Use o **histórico de Pixel de gráficos** janela para localizar o problema mais especificamente.  
  
-   Inspecione o estado do dispositivo quanto a possíveis problemas ou configurações incorretas.  
  
## <a name="scenario"></a>Cenário  
 Um dos motivos que os objetos podem não aparecer onde elas são esperadas em um aplicativo 3D é um erro de configuração do dispositivo gráfico que faz com que os objetos a serem excluídos da renderização — por exemplo, quando o giro causa triângulos a ser removido em erro , ou quando a função de teste de profundidade faz com que todos os pixels no objeto a serem rejeitadas.  
  
 No cenário descrito neste passo a passo, você apenas atingiu a primeira etapa no desenvolvimento de seu aplicativo 3D e está pronto para testá-lo pela primeira vez. No entanto, quando você executa o aplicativo, somente a interface do usuário é renderizada na tela. Usando o diagnóstico de gráficos, você capturar o problema para um arquivo de log de gráficos para que você possa depurar o aplicativo. O problema se parece com isso no aplicativo:  
  
 ![O aplicativo antes do problema é corrigido](media/vsg_walkthru1_firstview.png "vsg_walkthru1_firstview")  
  
 Para obter informações sobre como capturar problemas de gráficos no log de gráficos, consulte [capturando informações de gráficos](capturing-graphics-information.md).  
  
## <a name="investigation"></a>Investigação  
 Usando as ferramentas de diagnóstico de gráficos, você pode carregar o arquivo de log de gráficos para inspecionar os quadros que foram capturados durante o teste.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro no log de gráficos  
  
1. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar um log de gráficos que contém um quadro que exibe o modelo ausente. Uma nova guia de diagnóstico de gráficos aparece no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Na parte superior dessa guia é a saída de destino de renderização do quadro selecionado. Na parte inferior é parte do **lista de quadros**, que exibe cada quadro capturado como uma imagem em miniatura.  
  
2. No **lista de quadros**, selecione um quadro que demonstra que o modelo não é exibido. O destino de renderização é atualizado para refletir o quadro selecionado. Nesse cenário, os gráficos de log guia semelhante ao seguinte:  
  
    ![A lista de visualização e quadro de framebuffer do guia. vsglog](media/vsg_walkthru1_experiment.png "vsg_walkthru1_experiment")  
  
   Depois de selecionar um quadro que demonstra o problema, você pode usar o **lista de eventos gráficos** para diagnosticá-lo. O **lista de eventos gráficos** contém todas as chamadas de API do Direct3D que foi feita para renderizar o quadro ativo, por exemplo, chamadas de API para configurar o estado do dispositivo, para criar e atualizar os buffers de e para desenhar objetos que aparecem no quadro. Muitos tipos de chamadas são interessantes porque há muitas vezes (mas nem sempre) uma alteração correspondente no destino de renderização quando o aplicativo está funcionando conforme o esperado, por exemplo desenhar, expedição, cópia ou chamadas claras. Chamadas de desenho são particularmente interessantes porque cada um deles representa a geometria que o aplicativo processado (chamadas de expedição também podem renderizar a geometria).  
  
#### <a name="to-ensure-that-draw-calls-are-being-made"></a>Para garantir que estão sendo feitas chamadas de desenho  
  
1. Abra o **lista de eventos gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **lista de eventos**.  
  
2. Inspecione o **lista de eventos gráficos** para chamadas de desenho. Para facilitar essa tarefa, digite "Desenhar" na **pesquisa** caixa no canto superior direito das **lista de eventos gráficos** janela. Isso filtra a lista para que ele contenha somente os eventos que possuam "Desenho" em seus títulos. Nesse cenário, você descobre que várias chamadas de desenho foram feitas:  
  
    ![Lista de eventos de gráficos mostrando eventos capturados](media/vsg_walkthru1_.png "vsg_walkthru1_")  
  
   Depois de confirmar que estão sendo feitas chamadas de desenho, você pode determinar qual delas corresponde à geometria ausente. Como você sabe que a geometria ausente não é que está sendo desenhada para o destino de renderização (neste caso), você pode usar o **estágios de Pipeline gráficos** janela para determinar qual chamada de desenho corresponde à geometria ausente. O **estágios de Pipeline gráficos** janela mostra a geometria que foi enviada para cada chamada de desenho, independentemente de seu efeito sobre o destino de renderização. Conforme você percorrer as chamadas draw, os estágios de pipeline são atualizados para mostrar a geometria que está associada essa chamada, e a saída de destino de renderização é atualizada para mostrar o estado do destino de renderização depois que a chamada foi concluída.  
  
#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>Para localizar a chamada de desenho para a geometria ausente  
  
1. Abra o **estágios de Pipeline gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **estágios de Pipeline**.  
  
2. Percorrer cada chamada de desenho enquanto assiste a **estágios de Pipeline gráficos** janela para o modelo ausente. O **Assembler de entrada** estágio mostra os dados de modelo bruto. O **sombreador de vértices** estágio mostra os dados de modelo transformado. O **sombreador de Pixel** estágio mostra a saída do sombreador de pixel. O **fusão de saída** estágio mostra o destino de renderização mesclada desta chamada de desenho e todas as chamadas de desenho anterior.  
  
3. Pare quando atingir a chamada de desenho que corresponde ao modelo ausente. Nesse cenário, o **estágios de Pipeline gráficos** janela indica que a geometria foi processada, mas não apareceu no destino de renderização:  
  
    ![Visualizador de pipeline mostrando o objeto ausente](media/vsg_walkthru1_pipeline.png "vsg_walkthru1_pipeline")  
  
   Depois de confirmar que o aplicativo processado a geometria ausente e localizar a chamada de desenho correspondente, você pode selecionar uma parte da saída de destino de renderização que deve mostrar a geometria ausente e, em seguida, usar o **histórico de Pixel de gráficos** janela para descobrir por que os pixels foram excluídos. O histórico de pixel contém uma lista de cada chamada de desenho pode ter tido um efeito em um determinado pixel. Cada desenho chamar o **histórico de Pixel de gráficos** janela é identificada por um número que também é exibido no **lista de eventos gráficos** janela. Isso ajuda você a confirmar que o pixel deve exibir a geometria ausente e para descobrir por que o pixel foi excluído  
  
#### <a name="to-determine-why-the-pixel-was-excluded"></a>Para determinar por que o pixel foi excluído  
  
1. Abra o **histórico de Pixel de gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **histórico de Pixel**.  
  
2. Com base nas **sombreador de Pixel** miniatura, selecione um pixel no framebuffer de saída que deve conter uma parte da geometria ausente. Nesse cenário, a saída do sombreador de pixel deve abranger a maior parte do destino de renderização; Depois que um pixel é selecionado, o **histórico de Pixel de gráficos** janela tem esta aparência:  
  
    ![Chamadas de desenho de janela de histórico de pixel mostrando relacionados](media/vsg_walkthru1_hist1.png "vsg_walkthru1_hist1")  
  
3. Confirme se o pixel do destino de renderização selecionado contém uma parte da geometria correspondendo o número da chamada de desenho que você está analisando (da **lista de eventos gráficos** janela) para uma das chamadas de desenho no **gráficos Histórico de pixel** janela. Se não houver nenhuma das chamadas a **histórico de Pixel de gráficos** correspondência na janela de chamada de desenho que você está analisando, repita essas etapas (exceto a etapa 1) até encontrar uma correspondência. Nesse cenário, a chamada de desenho correspondente tem esta aparência:  
  
    ![Janela de histórico de pixel mostrando informações de fragmento](media/vsg_walkthru1_hist2.png "vsg_walkthru1_hist2")  
  
4. Quando você encontrar uma correspondência, expanda a chamada de desenho correspondente na **histórico de Pixel de gráficos** janela e confirme que o pixel foi excluído. Cada desenho chamar o **histórico de Pixel de gráficos** janela corresponde a um ou mais primitivos geométricos (pontos, linhas ou triângulos) que cruzam daquele pixel como resultado da geometria do objeto correspondente. Cada interseção de tal pode contribuir para a cor final do pixel. Um primitivo que foi excluído porque ele falhou no teste de profundidade é representado por um ícone que mostra a letra Z ao longo de uma seta que se incline para baixo da esquerda para a direita.  
  
5. Expanda um primitivo excluído para examinar melhor o estado que fez com que ele seja excluído. No **fusão de saída** grupo, mova o ponteiro sobre o **resultado**. Uma dica de ferramenta indica por que a primitiva foi excluída. Nesse cenário, o exame revela que o primitivo foi excluído porque ele falhou no teste de profundidade e, portanto, não contribuiu com a cor final do pixel.  
  
   Depois de determinar que a geometria não aparece porque seus primitivos falharam no teste de profundidade, você pode suspeitar que esse problema está relacionado ao estado do dispositivo configurado incorretamente. Estado do dispositivo e outros Direct3D objeto de dados podem ser examinados usando o **tabela de objetos gráficos**.  
  
#### <a name="to-examine-device-state"></a>Para examinar o estado do dispositivo  
  
1. Abra o **tabela de objetos gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **objeto tabela**.  
  
2. Localize o **dispositivo D3D10** do objeto na **tabela de objetos gráficos**e, em seguida, abra o **dispositivo D3D10** objeto. Uma nova **dispositivo d3d10** guia é aberta no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Para facilitar essa tarefa, você pode classificar os **tabela de objetos gráficos** pela **tipo**:  
  
    ![Tabela de objetos gráficos e o estado do dispositivo relacionados](media/vsg_walkthru1_objtable.png "vsg_walkthru1_objtable")  
  
3. Examinar o estado do dispositivo que é exibido na **dispositivo d3d10** guia problemas em potencial. Porque a geometria não aparece porque seus primitivos falharam no teste de profundidade, você pode se concentrar no estado do dispositivo, como o estêncil de profundidade, o que afeta o teste de profundidade. Nesse cenário, o **descrição de estêncil de profundidade** (sob **estado de fusão de saída**) contém um valor incomum para o **função profundidade** membro, `D3D10_COMPARISON_GREATER`:  
  
    ![Janela de dispositivo D3D10 mostrando informações de estêncil de profundidade](media/vsg_walkthru1_devicestate.png "vsg_walkthru1_devicestate")  
  
   Depois de determinar que a causa do problema de renderização pode ser uma função de profundidade configurado incorretamente, você pode usar essas informações junto com seu conhecimento do código para localizar onde a função de profundidade foi definida incorretamente e, em seguida, corrigir o problema. Se você estiver familiarizado com o código, você pode procurar o problema por meio de dicas que você coletou enquanto você estava depurando — por exemplo, com base nas **descrição de estêncil de profundidade** nesse cenário, você pode pesquisar o código para palavras como "camadas" ou "Maior". Depois de corrigir o código, recriá-lo e executar o aplicativo novamente para descobrir que o problema de renderização é resolvido:  
  
   ![Aplicativo depois que o problema é corrigido](media/vsg_walkthru1_finalview.png "vsg_walkthru1_finalview")
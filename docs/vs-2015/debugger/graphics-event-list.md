---
title: Lista de eventos gráficos | Microsoft Docs
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
- vs.graphics.eventlist
ms.assetid: a1252e19-b27d-4dc7-a16b-fdac894c1f0e
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 497ee3fe1c588c84195a544179d0d2955b1932b0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766222"
---
# <a name="graphics-event-list"></a>Lista de eventos do gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use a lista de eventos de gráficos no analisador de gráficos do Visual Studio para explorar os eventos Direct3D registrados durante a renderização de um quadro do seu jogo ou aplicativo.  
  
 Esta é a lista de eventos:  
  
 ![Uma lista de eventos que têm "Index" em seu nome. ](../debugger/media/gfx-diag-demo-event-list-orientation.png "gfx_diag_demo_event_list_orientation")  
  
## <a name="using-the-event-list"></a>Usando a lista de eventos  
 Quando você seleciona um evento no evento de lista, isso se reflete nas informações que são exibidas por outras ferramentas de análise de gráficos; usando a lista de eventos junto com essas outras ferramentas, você pode examinar um problema de renderização em detalhes para determinar sua causa. Para saber mais sobre como você pode resolver problemas de renderização, usando a lista de eventos junto com outras ferramentas de análise de gráficos, consulte [exemplos](../debugger/graphics-diagnostics-examples.md).  
  
 O uso dos recursos da lista de eventos de maneira efetiva é importante para contornar quadros complexos que podem conter milhares de eventos. Para usar a lista de eventos de maneira efetiva, escolha a exibição que funcione melhor para você, use a pesquisa para filtrar a lista de eventos, siga os links para saber mais sobre os objetos Direct3D associados a um evento e use os botões de seta para alternar rapidamente chamadas de desenho.  
  
### <a name="color-coded-events-in-direct3d-12"></a>Eventos codificados por cores no Direct3D 12  
 Direct3D 12 expõe várias filas que correspondem à funcionalidade de um hardware diferente. Para ajudar a identificar a fila que está associado a um evento de gráficos específico no Direct3D 12, os eventos são codificadas por cores na lista de eventos de acordo com suas filas quando você está trabalhando com uma captura de um aplicativo Direct3D 12.  
  
|Direct3D 12 fila|Cor|  
|-----------------------|-----------|  
|Processar a fila|Verde|  
|Fila de computação|Amarelo|  
|Fila de cópia|Laranja|  
  
 Direct3D 11 não expõem várias filas, portanto, os eventos não são codificadas por cores na lista de eventos quando você está trabalhando com uma captura de um aplicativo Direct3D 11.  
  
### <a name="event-list-views"></a>Exibições da lista de eventos  
 A lista de eventos oferece suporte a duas exibições diferentes que organizam eventos de gráficos de maneiras distintas para dar suporte ao fluxo de trabalho e às preferências. A primeira exibição é o *modo de exibição de chamadas de desenho* que organiza eventos e seu estado associado hierarquicamente. A segunda exibição é o *modo de exibição de linha do tempo* que organiza eventos cronologicamente, em uma lista simples.  
  
 O **chamadas Draw** exibição  
 Exibe eventos capturados e seu estado em uma hierarquia. O nível superior da hierarquia é constituído de eventos como chamadas de desenho, limpezas, presentes e os que lidam com exibições. Na lista de eventos, é possível expandir chamadas de desenho para exibir o estado atual do dispositivo no momento da chamada de desenho. E você ainda pode expandir cada tipo de estado para exibir os eventos que definem seus valores. Nesse nível, também é possível ver se um determinado estado foi definido em um quadro anterior ou se ele foi definido mais de uma vez desde a chamada de desenho mais recente.  
  
 O **linha do tempo** exibição  
 Exibe cada evento capturado em ordem cronológica. Essa forma de organizar a lista de eventos é a mesma de versões anteriores do Visual Studio.  
  
##### <a name="to-change-the-event-list-view-mode"></a>Para alterar o modo de exibição da lista de eventos  
  
-   No **lista de eventos gráficos** janela acima da lista de eventos, localize a **exibição** lista suspensa e escolha o **linha do tempo** exibição ou a **dechamadasdedesenho** modo de exibição.  
  
### <a name="filtering-events"></a>Filtrando eventos  
 Você pode usar a caixa de pesquisa — localizado no canto superior direito dos **lista de eventos gráficos** janela — para filtrar a lista de eventos para incluir apenas eventos cujos nomes contenham palavras-chave específicas. Você pode especificar palavras-chave únicas como `Vertex`— conforme mostrado na ilustração anterior — ou várias palavras-chave, usando uma lista delimitada por ponto e vírgula como `Draw;Primitive`— que corresponde a eventos que tenham `Draw` ou `Primitive` em seus nomes. Pesquisas diferenciam espaço em branco — por exemplo, `VSSet` e `VS Set` são pesquisas diferentes — portanto, certifique-se de formar pesquisas com cuidado.  
  
### <a name="moving-between-draw-calls"></a>Alternando entre chamadas de desenho  
 Como o exame `Draw` chamadas é especialmente importante, você pode usar o **ir para a próxima chamada de desenho** e **chamada de desenho de ir para anterior** botões — localizado no canto superior esquerdo do **Lista de eventos gráficos** janela — para encontrar e alternar rapidamente entre chamadas de desenho.  
  
### <a name="links-to-graphics-objects"></a>Links a objetos de gráficos  
 Para entender determinados eventos de gráficos, talvez seja necessário obter informações adicionais sobre o estado atual do Direct3D ou sobre os objetos Direct3D que são referenciados pelo evento. Muitos eventos fornecem links a essas informações, que é possível seguir para obter mais detalhes.  
  
## <a name="kinds-of-events-and-event-markers"></a>Tipos de eventos e marcadores de eventos  
 Os eventos exibidos na lista de eventos são organizados em quatro categorias: eventos gerais, eventos de desenho, grupos de eventos definidos pelo usuário e marcadores de evento definidos pelo usuário. Exceto no caso de eventos em geral, cada evento é exibido com um ícone que indica a categoria a que pertence.  
  
|Ícone|Descrição do evento|  
|----------|-----------------------|  
|(sem ícone)|Evento em geral<br /> Qualquer evento que não seja um evento definido pelo usuário, um grupo de eventos definido pelo usuário ou um evento de desenho.|  
|![O ícone de evento de desenho](../debugger/media/vsg-eventlist-icon-draw.png "vsg_eventlist_icon_draw")|Evento de desenho<br /> Marca um evento de desenho ocorrido durante o quadro capturado.|  
|![O usuário&#45;definido pelo ícone de marcador de evento](../debugger/media/vsg-eventlist-icon-user.png "vsg_eventlist_icon_user")|Grupo de eventos definido pelo usuário<br /> Eventos relacionados a grupos, conforme definido pelo aplicativo.|  
|![O usuário&#45;definido pelo ícone de marcador de evento](../debugger/media/vsg-eventlist-icon-user.png "vsg_eventlist_icon_user")|Marcador de evento definido pelo usuário<br /> Marca um local específico, conforme definido pelo aplicativo.|  
  
## <a name="marking-user-defined-events-in-your-app"></a>Marcando eventos definidos pelo usuário em seu aplicativo  
 Os eventos definidos pelo usuário são específicos do aplicativo. É possível usá-los para correlacionar eventos significativos ocorridos no aplicativo com eventos na Lista de Eventos de Gráficos. Por exemplo, é possível criar grupos de eventos definidos pelo usuário para organizar eventos relacionados, como os que renderizam a interface do usuário, em grupos ou em hierarquias de forma que você possa navegar na lista de eventos mais facilmente ou criar marcadores quando determinados tipos de objetos forem utilizados para encontrar de maneira fácil os eventos de gráficos na lista de eventos.  
  
 Para criar grupos e marcadores no aplicativo, você usa as mesmas APIs fornecidas pelo Direct3D a serem usadas por outras ferramentas de depuração do Direct3D. Essas APIs, às vezes, alterar entre as versões do Direct3D, mas a funcionalidade básica é o mesmo.  
  
### <a name="user-defined-events-in-direct3d-12"></a>Eventos definidos pelo usuário no Direct3D 12  
 Para criar grupos e marcadores no Direct3D 12, use as APIs descritas nesta seção. A tabela a seguir resume as APIs que você pode usar dependendo se você estiver marcando eventos em uma fila de comando ou lista de comando.  
  
|Descrição da API|[ID3D12CommandQueue](https://msdn.microsoft.com/library/dn788627.aspx)|[ID3D12GraphicsCommandList](https://msdn.microsoft.com/library/dn903537.aspx)|  
|---------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|Verificar a disponibilidade de evento definido pelo usuário|[PIXGetStatus](http://msdn.microsoft.com/en-us/f7ebd985-fb5d-46d7-abec-099df4b9be0e)|[PIXGetStatus](http://msdn.microsoft.com/en-us/1046ac43-a0a3-42bf-bae8-14aa72fa7567)|  
|Iniciar um grupo de eventos|[PIXBeginEvent](http://msdn.microsoft.com/en-us/5f51fff7-f313-4558-965b-2a443653cd7b)|[PIXBeginEvent](http://msdn.microsoft.com/en-us/4ddb3311-b9b5-449a-bbfb-7634e0d56e87)|  
|Final de um grupo de eventos|[PIXEndEvent](http://msdn.microsoft.com/en-us/fb526bf2-c17d-4a2a-8665-3b577a0f7fba)|[PIXEndEvent](http://msdn.microsoft.com/en-us/a3cd34a9-9dd9-40e1-ae86-0214b25ff185)|  
|Criar um marcador de evento|[PIXSetMarker](http://msdn.microsoft.com/en-us/0caf49ed-c99d-405e-89f4-0c887b8474ad)|[PIXSetMarker](http://msdn.microsoft.com/en-us/6610e5b9-a0c5-4236-b551-b6eb9fac64c1)|  
  
### <a name="user-defined-events-in-direct3d-11-and-earlier"></a>Eventos definidos pelo usuário no Direct3D 11 e versões anteriores  
 Para criar grupos e marcadores no Direct3D 11 ou anterior, use as APIs descritas nesta seção. A tabela a seguir resume as APIs que você pode usar para versões diferentes do Direct3D 11 e versões anteriores do Direct3D.  
  
|Descrição da API|[ID3D11DeviceContext2](http://msdn.microsoft.com/library/windows/desktop/dn280498.aspx) (Direct3D 11.2)|[ID3DUserDefinedAnnotation](http://go.microsoft.com/fwlink/p/?LinkID=250967) (Direct3D 11.1)|Família de APIs de D3DPerf_ (Direct3D 11.0 e anteriores)|  
|---------------------|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------|  
|Iniciar um grupo de eventos|`BeginEventInt`|`BeginEvent`|`D3DPerf_BeginEvent`|  
|Terminar um grupo de eventos|`EndEventInt`|`EndEvent`|`D3DPerf_EndEvent`|  
|Criar um marcador de evento|`SetMarkerInt`|`SetMarker`|`D3DPerf_SetMarker`|  
  
 É possível usar qualquer uma dessas APIs compatíveis com a versão do Direct3D. Por exemplo, se estiver segmentando a API Direct3D 11.1, você poderá usar `SetMarker` ou `D3DPerf_SetMarker` para criar um marcador de evento, mas não `SetMarkerInt`, porque ele só está disponível no Direct3D 11.2, e não é possível misturar aqueles compatíveis com versões diferentes do Direct3D no mesmo aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: objetos ausentes devido ao estado do dispositivo](../debugger/walkthrough-missing-objects-due-to-device-state.md)




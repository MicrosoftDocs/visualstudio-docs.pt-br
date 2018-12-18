---
title: Visualizando eventos EventSource como marcadores | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a10022a-5c37-48b1-a833-dd35902176b6
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c39f137299c1f229de8c3c6dc8d7329cba6033cb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742553"
---
# <a name="visualizing-eventsource-events-as-markers"></a>Visualizando eventos EventSource como marcadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A Visualização Simultânea pode exibir eventos do EventSource como marcadores e você pode controlar como os marcadores são exibidos. Para exibir os marcadores do EventSource, registre o GUID do provedor ETW usando a caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md). A Visualização Simultânea tem convenções padrão para representar eventos do EventSource como [Marcadores de Sinalizador](../profiling/flag-markers.md), [Marcadores de Período](../profiling/span-markers.md) e [Marcadores de Mensagem](../profiling/message-markers.md). Você pode personalizar como os eventos EventSource são exibidos, adicionando campos personalizados aos eventos. Para obter mais informações sobre marcadores, consulte [Marcadores da Visualização Simultânea](../profiling/concurrency-visualizer-markers.md). Para obter mais informações sobre eventos do EventSource, consulte <xref:System.Diagnostics.Tracing>.  
  
## <a name="default-visualization-of-eventsource-events"></a>Visualização Padrão de Eventos do EventSource  
 Por padrão, a Visualização Simultânea usa as seguintes convenções para representar eventos do EventSource.  
  
### <a name="marker-type"></a>Tipo de marcador  
  
1.  Eventos que tenham [Opcode](http://msdn.microsoft.com/en-us/d97953df-669b-4c55-b1a8-925022b339b7) win:Start ou win:Stop são tratados como o início ou fim de um período, respectivamente.  Períodos aninhados ou sobrepostos não podem ser exibidos. Pares de eventos que começam em um thread e terminam em outro não podem ser exibidos.  
  
2.  Um evento cujo Opcode não é win:Start nem win:Stop é tratado como um sinalizador de marcador, a menos que seu [Nível](http://msdn.microsoft.com/en-us/dfa4e0a9-4d89-4f50-aef9-1dae0dc11726) (campo de EVENT_RECORD.EVENT_HEADER.EVENT_DESCRIPTOR) seja win:Verbose ou superior.  
  
3.  Em todos os outros casos, o evento é tratado como uma mensagem.  
  
### <a name="importance"></a>Importância  
 A tabela a seguir define como o nível do evento mapeia para a importância de marcador.  
  
|Nível ETW|Importância da Visualização Simultânea|  
|---------------|---------------------------------------|  
|win:LogAlways|Normal|  
|win:Critical|Critical|  
|win:Error|Crítico|  
|win:Warning|High|  
|win:Informational|Normal|  
|win:Verbose|Low|  
|Maior que win:verbose|Low|  
  
### <a name="series-name"></a>Nome da Série  
 O nome da tarefa do evento é usado para o nome da série. O nome da série está vazio se nenhuma tarefa tiver sido definida para o evento.  
  
### <a name="category"></a>Categoria  
 Se o nível for win:Critical ou win:Error, a categoria será Alerta (-1). Caso contrário, a categoria será padrão (0).  
  
### <a name="text"></a>Texto  
 Se uma mensagem de texto formatada do tipo printf tiver sido definida para o evento, ela será exibida como a descrição do Marcador. Caso contrário, a descrição será o nome do evento e o valor de cada campo de carga.  
  
## <a name="customizing-visualization-of-eventsource-events"></a>Personalizando a Visualização de Eventos do EventSource  
 Você pode personalizar como os eventos do EventSource são exibidos, adicionando os campos apropriados ao evento, conforme descrito nas seções a seguir.  
  
### <a name="marker-type"></a>Tipo de marcador  
 Use o campo `cvType`, um byte, para controlar o tipo de marcador que é usado para representar o evento. Aqui estão os valores disponíveis para cvType:  
  
|Valor de cvType|Tipo de Marcador Resultante|  
|------------------|---------------------------|  
|0|Mensagem|  
|1|Intervalo Inicial|  
|2|Intervalo final|  
|3|Sinalizador|  
|Todos os outros valores|Mensagem|  
  
### <a name="importance"></a>Importância  
 Você pode usar o campo `cvImportance`, um byte, para controlar a configuração de importância para um evento do EventSource. No entanto, é recomendável que você controle a importância exibida de um evento usando o seu nível.  
  
|Valor de cvImportance|Importância da Visualização Simultânea|  
|------------------------|---------------------------------------|  
|0|Normal|  
|1|Critical|  
|2|High|  
|3|High|  
|4|Normal|  
|5|Baixo|  
|Todos os outros valores|Low|  
  
### <a name="series-name"></a>Nome da Série  
 Use o campo de evento `cvSeries`, uma cadeia de caracteres, para controlar o nome que a Visualização Simultânea dá a um evento do EventSource.  
  
### <a name="category"></a>Categoria  
 Use o campo `cvCategory`, um byte, para controlar a categoria que a Visualização Simultânea dá a um evento do EventSource.  
  
### <a name="text"></a>Texto  
 Use o campo `cvTextW`, uma cadeia de caracteres, para controlar a descrição que a Visualização Simultânea dá a um evento do EventSource.  
  
### <a name="spanid"></a>SpanID  
 Use o campo cvSpanId, int, para fazer a correspondência de pares de eventos. O valor para cada par de eventos de iniciar/parar que representa um intervalo deve ser exclusivo. Normalmente, para código simultâneo, ele requer o uso dos primitivos de sincronização, como <xref:System.Threading.Interlocked.Exchange%2A>, para garantir que a chave (o valor que é usado para CvSpanID) esteja correto.  
  
> [!NOTE]
>  O uso de SpanID para aninhar intervalos, permitir que eles parcialmente sobreponham o mesmo thread ou permitir que eles comecem em um thread e terminem em outro não tem suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Marcadores da Visualização Simultânea](../profiling/concurrency-visualizer-markers.md)




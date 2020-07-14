---
title: Visualizador de eventos | Microsoft Docs
ms.date: 4/30/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, Events Viewer
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 4cba043d8300d47ae5ffba1c175a19fcfa2e65ed
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330339"
---
# <a name="events-viewer"></a>Visualizador de eventos

O Visualizador de eventos genérico mostra a atividade do aplicativo por meio de uma lista de eventos, como carregamento de módulo, início de thread e configuração do sistema. Essa exibição ajuda você a diagnosticar melhor como seu aplicativo está fazendo dentro do criador de perfil do Visual Studio.

## <a name="setup"></a>Instalação

1. Selecione **ALT + F2** para abrir o criador de perfil de desempenho no Visual Studio.

1. Marque a caixa de seleção **Visualizador de eventos** .

   ![A caixa de seleção Visualizador de eventos está marcada](../profiling/media/eventsviewerselected.png "A caixa de seleção Visualizador de eventos está marcada")

1. Selecione o botão **Iniciar** para executar a ferramenta.

1. Depois que a ferramenta começar a ser executada, percorra o cenário para criar o perfil em seu aplicativo. Em seguida, selecione **parar coleta** ou feche seu aplicativo para ver seus dados.

   ![Uma janela mostrando A coleção de parada](../profiling/media/stopcollectioneventsviewer.png "Uma janela mostrando A coleção de parada")

Para obter mais informações sobre como tornar a ferramenta mais eficiente, consulte [otimizando as configurações de criação de perfil](../profiling/optimize-profiler-settings.md).

## <a name="understand-your-data"></a>Entenda seus dados

![Um rastreamento do Visualizador de eventos](../profiling/media/eventviewertrace.png "Um rastreamento do Visualizador de eventos")

|Nome da coluna|Descrição|
|----------|---------------------|
|Nome do Provedor|A origem do evento|
|Nome do Evento|O evento conforme especificado por seu provedor|
|Texto|Descrições do provedor, nome do evento e ID do evento|
|Carimbo de data/hora (MS)|Quando o evento ocorreu|
|GUID do provedor|A ID do provedor de eventos|
|ID do evento|A ID do evento|
|ID do Processo|O processo do qual o evento ocorreu (se conhecido)|
|Nome do Processo|O nome do processo se ele estiver ativamente em execução|
|ID do thread|A ID do thread do qual o evento ocorreu (se conhecido)|

Se alguma coluna estiver ausente por padrão, clique com o botão direito do mouse em um dos cabeçalhos de coluna existentes e selecione a coluna que você deseja adicionar.

![Adicionando colunas ao Visualizador de eventos](../profiling/media/eventvieweraddcolumns.png "Adicionando colunas ao Visualizador de eventos")

Quando você seleciona um evento, a janela **Propriedades adicionais** é exibida. **Propriedades comuns** mostra a lista de propriedades que serão exibidas para qualquer evento. **Propriedades de carga** mostra propriedades específicas para o evento. Para alguns eventos, você também pode exibir **pilhas**.

![O Visualizador de eventos mostrando pilhas](../profiling/media/eventviewerstacks.png "O Visualizador de eventos mostrando pilhas")

## <a name="organize-your-data"></a>Organizar seus dados

Todas as colunas, exceto a coluna de **texto** , são classificável.

![O rastreamento do Visualizador de eventos](../profiling/media/eventviewertrace.png "O rastreamento do Visualizador de eventos")

O Visualizador de eventos exibe até 20.000 eventos de cada vez. Para se concentrar nos eventos de interesse, você pode filtrar a exibição de eventos selecionando o filtro de eventos. Você também pode ver qual porcentagem do número total de eventos ocorreu para cada provedor. Passe o mouse sobre um único filtro de evento para ver uma dica de ferramenta que mostra:

- Nome do evento
- Provedor
- GUID
- Percentual do total de eventos
- Contagem de eventos

![O filtro de eventos do Visualizador de eventos](../profiling/media/eventviewereventfilter.png "O filtro de eventos do Visualizador de eventos")

O filtro do provedor mostra qual porcentagem do número total de eventos ocorreu para cada provedor. Passe o mouse sobre um único provedor para ver uma dica de ferramenta semelhante com o nome do provedor, a porcentagem do total de eventos e a contagem de eventos.

![O filtro do provedor do Visualizador de eventos](../profiling/media/eventviewerproviderfilter.png "O filtro do provedor do Visualizador de eventos")

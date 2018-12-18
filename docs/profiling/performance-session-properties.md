---
title: Propriedades da sessão de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,properties
- property pages,Profiling Tools
- performance tools, performance session properties
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2ce4fb6b9a57db78e3dbb7f3082a87df9ffb7360
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254687"
---
# <a name="performance-session-properties"></a>Propriedades da sessão de desempenho

Um **Sessão de Desempenho** permite definir as configurações que determinam como o aplicativo é analisado. Ele também armazena relatórios que são gerados para a sessão de criação de perfil.

Crie uma **Sessão de Desempenho** executando o **Assistente de Desempenho** ou criando manualmente uma sessão. A **Sessão de Desempenho** é exibida no **Gerenciador de Desempenho** após a **Sessão de Desempenho** ser criada.

Para exibir as propriedades da **Sessão de Desempenho**, selecione o nome da sessão em **Gerenciador de Desempenho**, clique nela com o botão direito do mouse e selecione **Propriedades**.

A sessão de desempenho tem as seguintes páginas de propriedade:

## <a name="general"></a>Geral

Essas configurações permitem que você selecione o método de criação de perfil para adicionar dados de tempo de vida e de coleção de objetos .NET e para especificar o local do relatório padrão e das convenções de nomenclatura.

Para obter mais informações, consulte:

[Como escolher métodos de coleta](../profiling/how-to-choose-collection-methods.md)

[Coletar a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)

 [Como definir opções do nome do arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)

## <a name="launch"></a>Inicializar

Essas configurações permitem selecionar em uma lista de binários e especificar a ordem de inicialização dos binários.

Para obter mais informações, confira [Como especificar o binário a ser iniciado](../profiling/how-to-specify-the-binary-to-start.md)

## <a name="sampling"></a>Amostragem

Essas configurações permitem que você selecione o intervalo de amostragem e do evento quando a amostragem é usada como o método de criação de perfil. Um evento de amostragem é usado para coletar dados de criação de perfil no intervalo especificado. Por exemplo, se o evento de amostragem for ciclos do relógio e o intervalo de amostragem for definido como 10.000.000, então os dados de criação de perfil serão coletados a cada 10 milhões de ciclos do relógio. Os quatro tipos de eventos de amostragem a seguir estão disponíveis:

- Ciclos do relógio – para problemas ligados à CPU
- Falhas de Página – para problemas relacionados à memória
- Chamadas do Sistema – para problemas relacionados a E/S
- Contadores de Desempenho – para problemas de baixo desempenho
- Eventos de amostragem adicionais podem ser especificados com base nos contadores de desempenho disponíveis

Para obter mais informações, confira [Como escolher os eventos de amostragem](../profiling/how-to-choose-sampling-events.md)

## <a name="binary"></a>Binário
Essas configurações permitem que você especifique se deseja realocar o binário instrumentado para outro local. Por exemplo, se você estiver criando o perfil de *My.DLL* e optar por não realocar o binário instrumentado, será criada uma cópia de backup de *My.DLL* denominada *My.Orig.DLL*. Em seguida, *My.DLL* será modificado pela inserção de investigações para coletar dados. Se você decidir realocar o binário instrumentado, o binário original não será renomeado e o binário instrumentado é copiado para o local especificado para uso durante a instrumentação.

Para obter mais informações, confira [Como especificar o binário a ser iniciado](../profiling/how-to-specify-the-binary-to-start.md)

## <a name="tier-interactions"></a>Interações de camada

Para obter mais informações, consulte [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md)

## <a name="instrumentation"></a>Instrumentação

Essas configurações permitem que coletar dados de desempenho de código JScript em páginas da Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e especificar qualquer evento de **Pré-instrumento** e **Pós-instrumento** que você deseja que ocorra antes ou depois do processo de instrumentação.

Para obter mais informações, consulte:

[Como criar perfil de código JavaScript em páginas da Web](../profiling/how-to-profile-javascript-code-in-web-pages.md)

[Como especificar comandos pré e pós-instrumentação](../profiling/how-to-specify-pre-and-post-instrument-commands.md)

## <a name="cpu-counters"></a>Contadores de CPU

Essas configurações permitem que você colete dados sobre contadores de desempenho da CPU quando estiver usando o método de criação de perfil de instrumentação. Contadores de desempenho portáteis estão disponíveis independentemente do design ou fabricante da CPU. Eventos de plataforma são específicos para o design e fabricante da CPU. Para obter mais informações sobre contadores de desempenho on-chip, consulte a documentação específica do processador.

Para obter mais informações, confira [Como coletar dados do contador de CPU](../profiling/how-to-collect-cpu-counter-data.md)

## <a name="windows-events"></a>Eventos do Windows

Durante a criação de perfil, você pode coletar dados de provedores de rastreamento de eventos. Você pode exibir os dados usando a opção `/calltrace` da ferramenta de linha de comando *VSPerfReport.exe*. Para obter mais informações sobre o ETW (Rastreamento de Eventos para Windows), consulte [Sobre o rastreamento de eventos](http://go.microsoft.com/fwlink/?linkid=90752).

Para obter mais informações, consulte:

[Como coletar dados de ETW (Rastreamento de Eventos para Windows)](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)

[VSPerfReport](../profiling/vsperfreport.md).

## <a name="windows-counters"></a>Contadores do Windows

Essa opção permite que você colete dados de contadores do Monitor de Desempenho do Windows. Para coletar esses dados, marque a caixa de seleção rotulada **Coletar contadores de desempenho do Windows**. O intervalo de coleta pode ser definido na caixa **Intervalo de Coleta**. **Categoria do Contador** e **Instância** também podem estar disponíveis. Alguns contadores do Monitor de Desempenho do Windows padrão estão disponíveis.

 Para obter mais informações, confira [Como coletar dados de contadores do Windows](../profiling/how-to-collect-windows-counter-data.md).

## <a name="advanced"></a>Avançado

Essas configurações permitem que você adicione opções ao processo de instrumentação especificando uma ou mais opções da ferramenta de criação de perfil da linha de comando [VSInstr](../profiling/vsinstr.md). Você também pode especificar a versão do Common Runtime para análise quando o aplicativo estiver usando mais de uma versão.

Para obter mais informações, consulte:

[Como especificar o tempo de execução do .NET Framework](../profiling/how-to-specify-the-dotnet-framework-runtime.md)

[Como especificar opções de instrumentação adicionais](../profiling/how-to-specify-additional-instrumentation-options.md)

## <a name="see-also"></a>Consulte também

[Visões gerais](../profiling/overviews-performance-tools.md)  
[Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)  
[Controlar a coleta de dados](../profiling/controlling-data-collection.md)
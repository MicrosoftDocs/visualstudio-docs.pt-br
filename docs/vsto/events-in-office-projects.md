---
title: Eventos em projetos do Office
description: Saiba como cada modelo de projeto do Office gera vários manipuladores de eventos e como esses manipuladores de eventos são ligeiramente diferentes dos manipuladores de eventos para os suplementos do VSTO.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Sheet1_Startup
- ThisDocument_Shutdown
- ThisDocument_Startup
- application-level add-ins [Office development in Visual Studio], events
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- Sheet2_Startup
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio], events
- Sheet2_Shutdown
- Startup event
- Sheet3_Shutdown
- add-ins [Office development in Visual Studio], events
- Shutdown event
- ThisAddIn_Startup
- Sheet3_Startup
- Startup method [Office development in Visual Studio]
- Shutdown method [Office development in Visual Studio]
- Sheet1_Shutdown
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: be1625be3d8c3fce409562be948c83a34d40d7b1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825674"
---
# <a name="events-in-office-projects"></a>Eventos em projetos do Office
  Cada modelo de projeto do Office gera automaticamente vários manipuladores de eventos. Os manipuladores de eventos para personalizações em nível de documento são ligeiramente diferentes dos manipuladores de eventos para os suplementos do VSTO.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="document-level-projects"></a>Projetos de nível de documento
 O Visual Studio fornece código gerado por trás de documentos ou planilhas novos ou existentes em personalizações em nível de documento. Esse código gera dois eventos diferentes: **inicialização** e **desligamento**.

### <a name="startup-event"></a>Evento de inicialização
 O evento **Startup** é gerado para cada um dos itens de host (documento, pasta de trabalho ou planilha) depois que o documento está em execução e todo o código de inicialização no assembly foi executado. É a última coisa a ser executada no construtor da classe em que seu código está sendo executado. Para obter mais informações sobre itens de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

 Quando você cria um projeto de nível de documento, o Visual Studio cria manipuladores de eventos para o evento de **inicialização** nos arquivos de código gerados:

- Para Microsoft Office projetos do Word, o manipulador de eventos é denominado `ThisDocument_Startup` .

- Para Microsoft Office projetos do Excel, os manipuladores de eventos têm os seguintes nomes:

  - `Sheet1_Startup`

  - `Sheet2_Startup`

  - `Sheet3_Startup`

  - `ThisWorkbook_Startup`

### <a name="shutdown-event"></a>Evento de encerramento
 O evento de **desligamento** é gerado para cada um dos itens de host (documento ou planilha) quando o domínio do aplicativo no qual seu código está carregado está prestes a ser descarregado. É a última coisa a ser chamada na classe à medida que ela é descarregada.

 Quando você cria um projeto de nível de documento, o Visual Studio cria manipuladores de eventos para o evento de **desligamento** nos arquivos de código gerados:

- Para Microsoft Office projetos do Word, o manipulador de eventos é denominado `ThisDocument_Shutdown` .

- Para Microsoft Office projetos do Excel, os manipuladores de eventos têm os seguintes nomes:

  - `Sheet1_Shutdown`

  - `Sheet2_Shutdown`

  - `Sheet3_Shutdown`

  - `ThisWorkbook_Shutdown`

> [!NOTE]
> Não remova os controles por meio de programação durante o manipulador de eventos de **desligamento** do documento. Os elementos da interface do usuário do documento não estão mais disponíveis quando o evento de **desligamento** ocorre. Se você quiser remover os controles antes que o aplicativo seja fechado, adicione seu código a outro manipulador de eventos, como **BeforeClose** ou **BeforeSave**.

### <a name="event-handler-method-declarations"></a>Declarações de método do manipulador de eventos
 Cada declaração de método do manipulador de eventos tem os mesmos argumentos passados: *Sender* e *e*. No Excel, o argumento *remetente* refere-se à planilha, como `Sheet1` ou `Sheet2` ; no Word, o argumento *remetente* refere-se ao documento. O argumento *e* refere-se aos argumentos padrão para um evento, que não são usados nesse caso.

 O exemplo de código a seguir mostra os manipuladores de eventos padrão em projetos de nível de documento para o Word.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet121":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet121":::

 O exemplo de código a seguir mostra os manipuladores de eventos padrão em projetos de nível de documento para o Excel.

> [!NOTE]
> O exemplo de código a seguir mostra os manipuladores de eventos na `Sheet1` classe. Os nomes dos manipuladores de eventos em outras classes de item de host correspondem ao nome da classe. Por exemplo, na `Sheet2` classe, o manipulador de eventos de **inicialização** é chamado `Sheet2_Startup` . Na `ThisWorkbook` classe, o manipulador de eventos de **inicialização** é chamado `ThisWorkbook_Startup` .

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet83":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet83":::

### <a name="order-of-events-in-document-level-excel-projects"></a>Ordem de eventos em projetos do Excel em nível de documento
 Os manipuladores de eventos de **inicialização** em projetos do Excel são chamados nesta ordem:

1. `ThisWorkbook_Startup`.

2. `Sheet1_Startup`.

3. `Sheet2_Startup`.

4. `Sheet3_Startup`.

5. Outras planilhas na ordem.

   Os manipuladores de eventos de **desligamento** em uma solução de pasta de trabalho são chamados nesta ordem:

6. `ThisWorkbook_Shutdown`.

7. `Sheet1_Shutdown`.

8. `Sheet2_Shutdown`.

9. `Sheet3_Shutdown`.

10. Outras planilhas na ordem.

    A ordem é determinada quando o projeto é compilado. Se o usuário reorganizar as planilhas em tempo de execução, ele não alterará a ordem em que os eventos são gerados na próxima vez em que a pasta de trabalho for aberta ou fechada.

## <a name="vsto-add-in-projects"></a>Projetos de suplemento do VSTO
 O Visual Studio fornece código gerado em suplementos do VSTO. Esse código gera dois eventos diferentes: <xref:Microsoft.Office.Tools.AddInBase.Startup> e <xref:Microsoft.Office.Tools.AddInBase.Shutdown> .

### <a name="startup-event"></a>Evento de inicialização
 O <xref:Microsoft.Office.Tools.AddIn.Startup> evento é gerado depois que o suplemento do VSTO é carregado e todo o código de inicialização no assembly foi executado. Esse evento é manipulado pelo `ThisAddIn_Startup` método no arquivo de código gerado.

 O código no `ThisAddIn_Startup` manipulador de eventos é o primeiro código de usuário a ser executado, a menos que o suplemento do VSTO substitua o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método. Nesse caso, o `ThisAddIn_Startup` manipulador de eventos é chamado após <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> .

 Não adicione código no `ThisAdd-In_Startup` manipulador de eventos se o código exigir que um documento seja aberto. Em vez disso, adicione esse código a um evento que o aplicativo do Office gera quando um usuário cria ou abre um documento. Para obter mais informações, consulte [acessar um documento quando o aplicativo do Office for iniciado](../vsto/programming-vsto-add-ins.md#AccessingDocuments).

 Para obter mais informações sobre a sequência de inicialização de suplementos do VSTO, consulte [arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md).

### <a name="shutdown-event"></a>Evento de encerramento
 O <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento é gerado quando o domínio do aplicativo no qual seu código está carregado está prestes a ser descarregado. Esse evento é manipulado pelo `ThisAddIn_Shutdown` método no arquivo de código gerado. Esse manipulador de eventos é o último código de usuário a ser executado quando o suplemento do VSTO é descarregado.

#### <a name="shutdown-event-in-outlook-vsto-add-ins"></a>Evento de desligamento nos suplementos do VSTO do Outlook
 O <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento é gerado somente quando o usuário desabilita o suplemento do VSTO usando a caixa de diálogo suplementos de com no Outlook. Ele não é gerado quando o Outlook sai. Se você tiver um código que deve ser executado quando o Outlook sair, manipule um dos seguintes eventos:

- O <xref:Microsoft.Office.Interop.Outlook.ApplicationEvents_11_Event.Quit> evento do <xref:Microsoft.Office.Interop.Outlook.Application> objeto.

- O <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> evento do <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto.

> [!NOTE]
> Você pode forçar o Outlook a gerar o <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento quando ele for encerrado modificando o registro. No entanto, se um administrador reverter essa configuração, qualquer código que você adicionar ao `ThisAddIn_Shutdown` método não será mais executado quando o Outlook sair. Para obter mais informações, consulte [Shutdown Changes for Outlook 2010](/previous-versions/office/developer/office-2010/ee720183(v=office.14)).

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)

---
title: Eventos em projetos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 85cbee61cde596831d06aa83af326cc0a0534f0f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949676"
---
# <a name="events-in-office-projects"></a>Eventos em projetos do Office
  Cada modelo de projeto do Office automaticamente gera vários manipuladores de eventos. Os manipuladores de eventos para personalizações no nível de documento são ligeiramente diferentes de manipuladores de eventos para suplementos do VSTO.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="document-level-projects"></a>Projetos de nível de documento  
 O Visual Studio fornece o código gerado por trás de documentos novos ou existentes ou planilhas personalizações no nível do documento. Esse código aciona dois eventos diferentes: **inicialização** e **desligamento**.  
  
### <a name="startup-event"></a>Evento de inicialização  
 O **inicialização** é gerado para cada um dos itens de host (documento, pasta de trabalho ou planilha) depois que o documento está em execução e todo o código de inicialização no assembly tiver sido executado. É a última coisa a ser executado no construtor da classe que seu código está em execução no. Para obter mais informações sobre itens de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
 Quando você cria um projeto de nível de documento, o Visual Studio cria manipuladores de eventos para o **inicialização** eventos nos arquivos de código gerado:  
  
-   Para projetos do Microsoft Office Word, o manipulador de eventos é chamado de `ThisDocument_Startup`.  
  
-   Para projetos do Microsoft Office Excel, os manipuladores de eventos têm os seguintes nomes:  
  
    -   `Sheet1_Startup`  
  
    -   `Sheet2_Startup`  
  
    -   `Sheet3_Startup`  
  
    -   `ThisWorkbook_Startup`  
  
### <a name="shutdown-event"></a>Evento de encerramento  
 O **desligamento** é gerado para cada um dos itens de host (documento ou planilha) quando o que seu código é carregado no domínio do aplicativo está prestes a ser descarregado. É a última coisa a ser chamado na classe conforme ele descarrega.  
  
 Quando você cria um projeto de nível de documento, o Visual Studio cria manipuladores de eventos para o **desligamento** eventos nos arquivos de código gerado:  
  
-   Para projetos do Microsoft Office Word, o manipulador de eventos é chamado de `ThisDocument_Shutdown`.  
  
-   Para projetos do Microsoft Office Excel, os manipuladores de eventos têm os seguintes nomes:  
  
    -   `Sheet1_Shutdown`  
  
    -   `Sheet2_Shutdown`  
  
    -   `Sheet3_Shutdown`  
  
    -   `ThisWorkbook_Shutdown`  
  
> [!NOTE]  
>  Não remover programaticamente os controles durante o **desligamento** manipulador de eventos do documento. Os elementos de interface do usuário do documento não estão mais disponíveis quando o **desligamento** evento ocorre. Se você quiser remover os controles antes de fecha o aplicativo, adicione seu código para outro manipulador de eventos, como **BeforeClose** ou **BeforeSave**.  
  
### <a name="event-handler-method-declarations"></a>Declarações de método do manipulador de eventos  
 Cada declaração de método do manipulador de eventos tem os mesmos argumentos passados para ele: *remetente* e *e*. No Excel, o *remetente* argumento se refere à planilha, como `Sheet1` ou `Sheet2`; no Word, o *remetente* argumento se refere ao documento. O *eletrônico* argumento refere-se para os argumentos padrão para um evento, que não são usados nesse caso.  
  
 O exemplo de código a seguir mostra os manipuladores de eventos padrão em projetos de nível de documento para Word.  
  
 [!code-vb[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#121)]
 [!code-csharp[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#121)]  
  
 O exemplo de código a seguir mostra os manipuladores de eventos padrão em projetos de nível de documento para Excel.  
  
> [!NOTE]  
>  O exemplo de código a seguir mostra os manipuladores de eventos no `Sheet1` classe. Os nomes dos manipuladores de eventos em outras classes de item de host correspondem ao nome da classe. Por exemplo, nos `Sheet2` classe, o **inicialização** manipulador de eventos é chamado `Sheet2_Startup`. No `ThisWorkbook` classe, o **inicialização** manipulador de eventos é chamado `ThisWorkbook_Startup`.  
  
 [!code-csharp[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#83)]
 [!code-vb[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#83)]  
  
### <a name="order-of-events-in-document-level-excel-projects"></a>Ordem de eventos em projetos de nível de documento do Excel  
 O **inicialização** manipuladores de eventos em projetos do Excel são chamadas nesta ordem:  
  
1. `ThisWorkbook_Startup`.  
  
2. `Sheet1_Startup`.  
  
3. `Sheet2_Startup`.  
  
4. `Sheet3_Startup`.  
  
5. Outras planilhas em ordem.  
  
   O **desligamento** são chamados de manipuladores de eventos em uma solução de pasta de trabalho nesta ordem:  
  
6. `ThisWorkbook_Shutdown`.  
  
7. `Sheet1_Shutdown`.  
  
8. `Sheet2_Shutdown`.  
  
9. `Sheet3_Shutdown`.  
  
10. Outras planilhas em ordem.  
  
    A ordem é determinada quando o projeto é compilado. Se o usuário reorganiza as planilhas em tempo de execução, ele não altera a ordem que os eventos são disparados na próxima vez em que a pasta de trabalho for aberta ou fechada.  
  
## <a name="vsto-add-in-projects"></a>Projetos de suplemento do VSTO  
 O Visual Studio fornece o código gerado nos suplementos do VSTO. Esse código aciona dois eventos diferentes: <xref:Microsoft.Office.Tools.AddInBase.Startup> e <xref:Microsoft.Office.Tools.AddInBase.Shutdown>.  
  
### <a name="startup-event"></a>Evento de inicialização  
 O <xref:Microsoft.Office.Tools.AddIn.Startup> é gerado depois que o suplemento do VSTO é carregado e todo o código de inicialização no assembly foi executado. Esse evento é manipulado pelo `ThisAddIn_Startup` método no arquivo de código gerado.  
  
 O código na `ThisAddIn_Startup` manipulador de eventos é o primeiro código de usuário para ser executado, a menos que o suplemento do VSTO substitui o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método. Nesse caso, o `ThisAddIn_Startup` manipulador de eventos é chamado após <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A>.  
  
 Não adicione o código no `ThisAdd-In_Startup` se um documento a ser aberto exige que o código de manipulador de eventos. Em vez disso, adicione esse código para um evento que o aplicativo do Office emite quando um usuário cria ou abre um documento. Para obter mais informações, consulte [acessa um documento quando inicia o aplicativo do Office](../vsto/programming-vsto-add-ins.md#AccessingDocuments).  
  
 Para obter mais informações sobre a sequência de inicialização de suplementos do VSTO, consulte [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
### <a name="shutdown-event"></a>Evento de encerramento  
 O <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento é gerado quando o que seu código é carregado no domínio do aplicativo está prestes a ser descarregado. Esse evento é manipulado pelo `ThisAddIn_Shutdown` método no arquivo de código gerado. Esse manipulador de eventos é o último código de usuário para ser executado quando o suplemento do VSTO é descarregado.  
  
#### <a name="shutdown-event-in-outlook-vsto-add-ins"></a>Evento de desligamento nos suplementos do VSTO do Outlook  
 O <xref:Microsoft.Office.Tools.AddInBase.Shutdown> é gerado somente quando o usuário desativa o suplemento do VSTO usando a caixa de diálogo Suplementos COM no Outlook. Ele não é disparado quando o Outlook é fechado. Se você tiver o código que deve ser executado quando o Outlook é fechado, lidar com qualquer um dos seguintes eventos:  
  
-   O <xref:Microsoft.Office.Interop.Outlook.ApplicationEvents_11_Event.Quit> eventos do <xref:Microsoft.Office.Interop.Outlook.Application> objeto.  
  
-   O <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> eventos do <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto.  
  
> [!NOTE]  
>  Você pode forçar o Outlook para gerar o <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento quando ele sai modificando o registro. No entanto, se um administrador reverte essa configuração, qualquer código que você adicione o `ThisAddIn_Shutdown` método não é executado quando o Outlook é fechado. Para obter mais informações, consulte [desligamento é alterado para o Outlook 2010](http://go.microsoft.com/fwlink/?LinkID=184614).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)  
  
  
---
title: Visão geral de modelo de objeto do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.OutlookAddin
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], object model overview
- object models [Office development in Visual Studio], Office
- objects [Office development in Visual Studio], Office object models
- object models [Office development in Visual Studio], Outlook
- Office object models
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b6885968385725f4aa7d991309902ca712849c8a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941185"
---
# <a name="outlook-object-model-overview"></a>Visão geral de modelo de objeto do Outlook
  Para desenvolver suplementos do VSTO para Outlook do Microsoft Office, você pode interagir com os objetos que são fornecidos pelo modelo de objeto do Outlook. O modelo de objeto do Outlook fornece interfaces e classes que representam itens na interface do usuário. Por exemplo, o <xref:Microsoft.Office.Interop.Outlook.Application> objeto representa o aplicativo inteiro, o <xref:Microsoft.Office.Interop.Outlook.Folder> objeto representa uma pasta que contém mensagens de email ou outros itens, e o <xref:Microsoft.Office.Interop.Outlook.MailItem> objeto representa uma mensagem de email.  
  
 Este tópico fornece uma visão geral de alguns dos principais objetos no modelo de objeto do Outlook. Para obter recursos onde você pode aprender mais sobre todo o modelo de objeto do Outlook, consulte [Use a documentação do modelo de objeto Outlook](#refdoc).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [How do i: Use o Outlook para criar um relatório de tarefas personalizado?](http://go.microsoft.com/fwlink/?LinkID=130315).  
  
## <a name="access-objects-in-an-outlook-project"></a>Acessar objetos em um projeto do Outlook  
 O Outlook fornece muitos objetos com os quais você pode interagir. Para usar efetivamente o modelo de objeto, você deve estar familiarizado com os seguintes objetos de nível superior:  
  
-   <xref:Microsoft.Office.Interop.Outlook.Application>  
  
-   <xref:Microsoft.Office.Interop.Outlook.Explorer>  
  
-   <xref:Microsoft.Office.Interop.Outlook.Inspector>  
  
-   <xref:Microsoft.Office.Interop.Outlook.Folder>  
  
-   <xref:Microsoft.Office.Interop.Outlook.MailItem>  
  
-   <xref:Microsoft.Office.Interop.Outlook.AppointmentItem>  
  
-   <xref:Microsoft.Office.Interop.Outlook.TaskItem>  
  
-   <xref:Microsoft.Office.Interop.Outlook.ContactItem>  
  
### <a name="application-object"></a>Objeto de aplicativo  
 O <xref:Microsoft.Office.Interop.Outlook.Application> objeto representa o aplicativo Outlook e é o objeto de nível superior no modelo de objeto do Outlook. Alguns dos membros mais importantes desse objeto incluem:  
  
- O [CreateItem](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) método que você pode usar para criar um novo item como uma mensagem de email, uma tarefa ou um compromisso.  
  
- O <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> propriedade, que você pode usar para acessar as janelas que exibem o conteúdo de uma pasta na interface de usuário (IU) do Outlook.  
  
- O <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> propriedade, que você pode usar para acessar as janelas que exibem o conteúdo de um único item, como uma solicitação de reunião ou de mensagem de email.  
  
  Para obter uma instância das <xref:Microsoft.Office.Interop.Outlook.Application> do objeto, use o campo de aplicativo do `ThisAddIn` classe em seu projeto. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
> [!NOTE]  
>  Para evitar avisos de segurança quando você usa propriedades e métodos que estão bloqueados pelo object model guard do Outlook, obtenha objetos do Outlook do campo de aplicativo a `ThisAddIn` classe. Para obter mais informações, consulte [considerações sobre segurança específicas para soluções do Office](../vsto/specific-security-considerations-for-office-solutions.md).  
  
### <a name="explorer-object"></a>Objeto Explorer  
 O <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto representa uma janela que exibe o conteúdo de uma pasta que contém itens como mensagens de email, tarefas ou compromissos. O <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto inclui métodos e propriedades que você pode usar para modificar a janela e eventos que são gerados quando a janela é alterado.  
  
 Para obter um <xref:Microsoft.Office.Interop.Outlook.Explorer> de objeto, faça o seguinte:  
  
-   Use o <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> propriedade do <xref:Microsoft.Office.Interop.Outlook.Application> objeto para acessar todos o <xref:Microsoft.Office.Interop.Outlook.Explorer> objetos no Outlook.  
  
-   Use o <xref:Microsoft.Office.Interop.Outlook._Application.ActiveExplorer%2A> método da <xref:Microsoft.Office.Interop.Outlook.Application> objeto do qual obter o <xref:Microsoft.Office.Interop.Outlook.Explorer> que tem foco no momento.  
  
-   Use o `GetExplorer` método da <xref:Microsoft.Office.Interop.Outlook.Folder> objeto do qual obter o <xref:Microsoft.Office.Interop.Outlook.Explorer> para a pasta atual.  
  
### <a name="inspector-object"></a>Objeto do Inspetor  
 O <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto representa uma janela que exibe um único item, como uma mensagem de email, uma tarefa ou um compromisso. O <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto inclui métodos e propriedades que você pode usar para modificar a janela e eventos que são gerados quando a janela é alterado.  
  
 Para obter um <xref:Microsoft.Office.Interop.Outlook.Inspector> de objeto, faça o seguinte:  
  
-   Use o <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> propriedade do <xref:Microsoft.Office.Interop.Outlook.Application> objeto para acessar todos o <xref:Microsoft.Office.Interop.Outlook.Inspector> objetos no Outlook.  
  
-   Use o <xref:Microsoft.Office.Interop.Outlook._Application.ActiveInspector%2A> método da <xref:Microsoft.Office.Interop.Outlook.Application> objeto do qual obter o <xref:Microsoft.Office.Interop.Outlook.Inspector> que tem foco no momento.  
  
-   Use o `GetInspector` método de um determinado item, tal como uma <xref:Microsoft.Office.Interop.Outlook.MailItem> ou <xref:Microsoft.Office.Interop.Outlook.AppointmentItem>, para recuperar o Inspetor que está associado ele.  
  
### <a name="folder-object"></a>Objeto de pasta  
 O <xref:Microsoft.Office.Interop.Outlook.Folder> objeto representa uma pasta que contém mensagens de email, contatos, tarefas e outros itens. O Outlook fornece o padrão de 16 <xref:Microsoft.Office.Interop.Outlook.Folder> objetos.  
  
 O padrão <xref:Microsoft.Office.Interop.Outlook.Folder> objetos são definidos pelo <xref:Microsoft.Office.Interop.Outlook.OlDefaultFolders> valores de enumeração. Por exemplo,  
  
 Microsoft.Office.Interop.Outlook.OlDefaultFolders.olFolderInbox corresponde do **caixa de entrada** pasta no Outlook.  
  
 Para obter um exemplo que mostra como acessar um padrão <xref:Microsoft.Office.Interop.Outlook.Folder> e crie um novo <xref:Microsoft.Office.Interop.Outlook.Folder>, consulte [como: criar itens de pasta personalizados programaticamente](../vsto/how-to-programmatically-create-custom-folder-items.md).  
  
### <a name="mailitem-object"></a>Objeto MailItem  
 O <xref:Microsoft.Office.Interop.Outlook.MailItem> objeto representa uma mensagem de email. <xref:Microsoft.Office.Interop.Outlook.MailItem> objetos são normalmente em pastas, como **caixa de entrada**, **itens enviados**, e **caixa de saída**. <xref:Microsoft.Office.Interop.Outlook.MailItem> expõe as propriedades e métodos que podem ser usados para criar e enviar mensagens de email.  
  
 Para obter um exemplo que mostra como criar uma mensagem de email, consulte [como: criar programaticamente um item de email](../vsto/how-to-programmatically-create-an-e-mail-item.md).  
  
### <a name="appointmentitem-object"></a>Objeto AppointmentItem  
 O <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> objeto representa uma reunião, um compromisso único ou um compromisso recorrente ou reunião na **calendário** pasta. O <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> objeto inclui métodos que realizam ações como responder a ou encaminhamento de solicitações de reunião e propriedades que especificam os detalhes da reunião, como o local e a hora.  
  
 Para obter um exemplo que mostra como criar um compromisso, consulte [como: criar programaticamente uma solicitação de reunião](../vsto/how-to-programmatically-create-a-meeting-request.md).  
  
### <a name="taskitem-object"></a>Objeto TaskItem  
 O <xref:Microsoft.Office.Interop.Outlook.TaskItem> objeto representa uma tarefa a ser executada em um intervalo de tempo especificado. <xref:Microsoft.Office.Interop.Outlook.TaskItem> os objetos estão localizados na **tarefas** pasta.  
  
 Para criar uma tarefa, use o [CreateItem](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) método o <xref:Microsoft.Office.Interop.Outlook.Application> do objeto e passar o valor <xref:Microsoft.Office.Interop.Outlook.OlItemType.olTaskItem> para o parâmetro.  
  
### <a name="contactitem-object"></a>Objeto ContactItem  
 O <xref:Microsoft.Office.Interop.Outlook.ContactItem>objeto representa um contato a **contatos** pasta. <xref:Microsoft.Office.Interop.Outlook.ContactItem> os objetos contêm uma variedade de informações de contato para as pessoas com quem que eles representam, como endereços, endereços de email e números de telefone.  
  
 Para obter um exemplo que mostra como criar um novo contato, consulte [como: adicionar uma entrada a contatos do Outlook de forma programática](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md). Para obter um exemplo que mostra como pesquisar um contato existente, consulte [como: pesquisar um contato específico de forma programática](../vsto/how-to-programmatically-search-for-a-specific-contact.md).  
  
##  <a name="refdoc"></a> Use a documentação de modelo de objeto do Outlook  
 Para obter informações completas sobre o modelo de objeto do Outlook, você pode consultar para a referência de assembly de interoperabilidade primária (PIA) do Outlook e a referência de modelo de objeto do VBA.  
  
### <a name="primary-interop-assembly-reference"></a>Referência de assembly de interoperabilidade primário  
 A referência de PIA Outlook documenta os tipos em assemblies de interoperabilidade primários para o Outlook 2010. Para obter mais informações, consulte [referência de assembly de interoperabilidade primária do Outlook 2010](http://go.microsoft.com/fwlink/?LinkId=189580).  
  
 Além de fornecer informações para todos os tipos de PIAs, esta documentação também fornece informações adicionais sobre a estrutura dos PIAs e exemplos de código para tarefas comuns de automação do Outlook.  
  
### <a name="vba-object-model-reference"></a>Referência de modelo de objeto do VBA  
 A referência de modelo de objeto VBA documenta o modelo de objeto do Outlook, como ele é exposto ao Visual Basic para código Applications (VBA). Para obter mais informações, consulte [referência de modelo de objeto do Outlook 2010](http://go.microsoft.com/fwlink/?LinkId=199769).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no PIA do Outlook. Por exemplo, o objeto do Inspetor na referência de modelo de objeto do VBA corresponde à <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto no PIA do Outlook. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência para o Visual Basic ou Visual c#, se você quiser usá-los em um projeto de suplemento de VSTO do Outlook que você cria usando Visual Studio.  
  
### <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Trabalhar com itens de contato](../vsto/working-with-contact-items.md)|Fornece tópicos que mostram como executar tarefas com contatos.|  
|[Trabalhar com itens de email](../vsto/working-with-mail-items.md)|Fornece tópicos que mostram como executar tarefas com itens de email.|  
|[Trabalhar com pastas](../vsto/working-with-folders.md)|Fornece tópicos que mostram como executar tarefas de pastas.|  
|[Trabalhar com itens de calendário](../vsto/working-with-calendar-items.md)|Fornece tópicos que mostram como executar tarefas com itens de calendário.|  
|[Como: determinar o item atual do Outlook de forma programática](../vsto/how-to-programmatically-determine-the-current-outlook-item.md)|Mostra como exibir o nome da pasta atual e algumas informações sobre o item selecionado.|  
  
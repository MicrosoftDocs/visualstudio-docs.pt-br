---
title: Personalizações em nível de documento do programa
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- Sheet3
- thisWorkbook
- thisDocument
- Sheet1
- Sheet2
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ThisDocument class
- Sheet3 class
- ThisWorkbook class
- writing code for Office solutions
- programming [Office development in Visual Studio], document-level customizations
- Sheet1 class
- Office applications [Office development in Visual Studio], document-level customizations
- Sheet2 class
- document-level customizations [Office development in Visual Studio], programming
- application development [Office development in Visual Studio], document-level customizations
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d9c7fa658c24caa65b3c955002ffeeaff6573c55
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812225"
---
# <a name="program-document-level-customizations"></a>Personalizações em nível de documento do programa
  Quando você estende o Microsoft Office Word ou Microsoft Office Excel, usando uma personalização no nível de documento, você pode executar as seguintes tarefas:  
  
- Automatize o aplicativo usando seu modelo de objeto.  
  
- Adicione controles para a superfície do documento.  
  
- Chame o Visual Basic para código do VBA no documento do assembly de personalização.  
  
- Chame o código no assembly de personalização do VBA.  
  
- Gerencie determinados aspectos do documento enquanto ele está em um servidor que não tenha o Microsoft Office instalado.  
  
- Personalize a interface do usuário (IU) do aplicativo.  
  
  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
  Alguns aspectos de escrever código em projetos de nível de documento são diferentes de outros tipos de projetos no Visual Studio. Muitas dessas diferenças são causadas pela maneira como o Office modelos de objeto são expostos ao código gerenciado. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).  
  
  Para obter informações gerais sobre as personalizações no nível de documento e outros tipos de soluções que você pode criar usando as ferramentas de desenvolvimento do Office no Visual Studio, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
## <a name="use-the-generated-classes-in-document-level-projects"></a>Use as classes geradas em projetos de nível de documento  
 Quando você cria um projeto de nível de documento, o Visual Studio gera automaticamente uma classe no projeto que você pode usar para começar a escrever seu código. O Visual Studio gera classes diferentes para Word e Excel:  
  
- Em projetos de nível de documento para Word, a classe é chamada `ThisDocument` por padrão.  
  
- Projetos de nível de documento para Excel tem várias classes geradas: um para a pasta de trabalho em si e outro para cada planilha. Por padrão, essas classes têm os seguintes nomes:  
  
  -   `ThisWorkbook`  
  
  -   `Sheet1`  
  
  -   `Sheet2`  
  
  -   `Sheet3`  
  
  A classe gerada inclui manipuladores de eventos que são chamados quando o documento for aberto ou fechado. Para executar código quando o documento for aberto, adicione código para o `Startup` manipulador de eventos. Para executar código antes do documento é fechado, adicione código para o `Shutdown` manipulador de eventos. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="understand-the-design-of-the-generated-classes"></a>Entender o design das classes geradas  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], tipos de item de host no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] são interfaces, portanto, as classes geradas não podem derivar sua implementação deles. Em vez disso, as classes geradas derivam a maioria de seus membros das seguintes classes base:  
  
- `ThisDocument`: deriva <xref:Microsoft.Office.Tools.Word.DocumentBase>.  
  
- `ThisWorkbook`: deriva <xref:Microsoft.Office.Tools.Excel.WorkbookBase>.  
  
- `Sheet` *n*: deriva <xref:Microsoft.Office.Tools.Excel.WorksheetBase>.  
  
  Essas classes base redirecionar todas as chamadas para seus membros para as implementações internas das interfaces de item de host correspondentes no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Por exemplo, se você chamar o <xref:Microsoft.Office.Tools.Word.DocumentBase.Protect%2A> método da `ThisDocument` classe, o <xref:Microsoft.Office.Tools.Word.DocumentBase> classe redireciona essa chamada para a implementação interna do <xref:Microsoft.Office.Tools.Word.Document> interface no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
## <a name="access-the-object-model-of-the-host-application"></a>Acessar o modelo de objeto do aplicativo host  
 Para acessar o modelo de objeto do aplicativo host, use os membros da classe gerada em seu projeto. Cada uma dessas classes corresponde a um objeto no modelo de objeto do Excel ou Word, e eles contêm a maioria das mesmas propriedades, métodos e eventos. Por exemplo, o `ThisDocument` classe em um projeto de nível de documento para Word fornece a maioria dos mesmos membros que o <xref:Microsoft.Office.Interop.Word.Document> objeto no modelo de objeto do Word.  
  
 O exemplo de código a seguir mostra como usar o modelo de objeto do Word para salvar o documento que faz parte de uma personalização no nível de documento para Word. Este exemplo se destina a ser executado a partir de `ThisDocument` classe.  
  
```vb  
Me.Save()  
```  
  
```csharp  
this.Save();  
```  
  
 Para fazer a mesma coisa de fora o `ThisDocument` classe, use o `Globals` do objeto para o acesso a `ThisDocument` classe. Por exemplo, você pode adicionar esse código em um arquivo de código do painel de ações, se você quiser incluir um **salvar** botão no painel de ações da interface do usuário.  
  
```vb  
Globals.ThisDocument.Save()  
```  
  
```csharp  
Globals.ThisDocument.Save();  
```  
  
 Porque o `ThisDocument` classe obtém a maioria de seus membros do <xref:Microsoft.Office.Tools.Word.Document> item de host, o `Save` método que é chamado nesse código é realmente o <xref:Microsoft.Office.Tools.Word.Document.Save%2A> método da <xref:Microsoft.Office.Tools.Word.Document> item de host. Esse método corresponde à <xref:Microsoft.Office.Interop.Word._Document.Save%2A> método da <xref:Microsoft.Office.Interop.Word.Document> objeto no modelo de objeto do Word.  
  
 Para obter mais informações sobre como usar os modelos de objeto do Word e Excel, consulte [visão geral de modelo de objeto do Word](../vsto/word-object-model-overview.md) e [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  
  
 Para obter mais informações sobre o `Globals` do objeto, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
## <a name="add-controls-to-documents"></a>Adicionar controles a documentos  
 Para personalizar a interface do usuário do documento, você pode adicionar controles de formulários do Windows ou *hospedar controles* à superfície do documento. Combinando conjuntos diferentes de controles e escrevendo código, que você pode associar controles a dados, coletar informações do usuário e responder às ações do usuário.  
  
 Controles de host são classes que estendem alguns dos objetos no modelo de objeto do Word e Excel. Por exemplo, o <xref:Microsoft.Office.Tools.Excel.ListObject> controle de host fornece toda a funcionalidade do <xref:Microsoft.Office.Interop.Excel.ListObject> no Excel. No entanto, o <xref:Microsoft.Office.Tools.Excel.ListObject> controle de host também tem eventos adicionais e recursos de ligação de dados.  
  
 Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md) e [controles na visão geral de documentos do Office do Windows forms](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
## <a name="combine-vba-and-document-level-customizations"></a>Combinar o VBA e personalizações no nível de documento  
 Você pode usar o código VBA em um documento que faz parte de uma personalização no nível de documento. Você pode chamar o código do VBA no documento do assembly de personalização, e você também pode configurar seu projeto para habilitar o código do VBA no documento para chamar o código no assembly de personalização.  
  
 Para obter mais informações, consulte [combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md).  
  
## <a name="manage-documents-on-a-server"></a>Gerenciar documentos em um servidor  
 Você pode gerenciar vários aspectos diferentes de personalizações no nível do documento em um servidor que não tenha o Microsoft Office Word ou Microsoft Office Excel instalado. Por exemplo, você pode acessar e modificar dados no cache de dados do documento. Você também pode gerenciar o assembly de personalização que é associado ao documento. Por exemplo, programaticamente você pode remover o assembly do documento, para que o documento não executa o seu código, ou por meio de programação pode anexar um assembly a um documento.  
  
 Para obter mais informações, consulte [gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md).  
  
## <a name="customize-the-user-interface-of-microsoft-office-applications"></a>Personalizar a interface do usuário de aplicativos do Microsoft Office  
 Usando uma personalização no nível de documento, você pode personalizar a interface do usuário do Word e Excel das seguintes maneiras:  
  
- Adicione controles de host ou controles dos Windows Forms à superfície do documento.  
  
   Para obter mais informações, consulte [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md), [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md), e [controles de formulários do Windows de visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
- Adicione um painel de ações para o documento.  
  
   Para obter mais informações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md).  
  
- Adicione guias personalizadas à faixa de opções.  
  
   Para obter mais informações, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
- Adicione grupos personalizados a uma guia interna na faixa de opções.  
  
   Para obter mais informações, consulte [como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md).  
  
  Para obter mais informações sobre como personalizar os aplicativos de interface do usuário do Microsoft Office, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
## <a name="get-extended-objects-from-native-office-objects-in-document-level-customizations"></a>Obter objetos estendidos de objetos nativos do Office em personalizações no nível de documento  
 Vários manipuladores de eventos do Office recebem um objeto nativo do Office que representa a pasta de trabalho, a planilha ou o documento que gerou o evento. Em alguns casos, você talvez queira executar algum código somente se a pasta de trabalho ou o documento em sua personalização no nível de documento disparou o evento. Por exemplo, em uma personalização no nível de documento para Excel, talvez você queira executar algum código quando o usuário ativa uma das planilhas na pasta de trabalho personalizada, mas não quando o usuário ativa uma planilha em alguma outra pasta de trabalho que vem a ser aberto ao mesmo tempo.  
  
 Quando você tiver um objeto nativo do Office, você pode testar se esse objeto foi estendido em uma *item de host* ou *controle de host* em uma personalização no nível de documento. Itens de host e controles de host são tipos fornecidos pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que adiciona funcionalidade a objetos que existem nativamente nos modelos de objeto do Word ou Excel (chamado *objetos nativos do Office*). Coletivamente, itens de host e controles de host também são chamados *objetos estendidos*. Para obter mais informações sobre itens de host e controles de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
## <a name="understand-the-getvstoobject-and-hasvstoobject-methods"></a>Entender os métodos GetVstoObject e HasVstoObject  
 Para testar um objeto nativo do Office, use o `HasVstoObject` e `GetVstoObject` métodos em seu projeto:  
  
- Use o `HasVstoObject` método se você quiser determinar se o objeto nativo do Office tem um objeto estendido em sua personalização. Esse método retornará **verdadeira** se o objeto nativo do Office tem um objeto estendido, e **falso** caso contrário.  
  
- Use o `GetVstoObject` método se você deseja obter o objeto estendido para um objeto nativo do Office. Esse método retorna um <xref:Microsoft.Office.Tools.Excel.ListObject>, <xref:Microsoft.Office.Tools.Excel.Workbook>, <xref:Microsoft.Office.Tools.Excel.Worksheet>, ou <xref:Microsoft.Office.Tools.Word.Document> objeto se o objeto especificado nativo do Office tem um. Caso contrário, `GetVstoObject` retorna **nulo**. Por exemplo, o `GetVstoObject` método retorna um <xref:Microsoft.Office.Tools.Word.Document> se especificado <xref:Microsoft.Office.Interop.Word.Document> é o objeto subjacente para o documento no seu projeto de documento do Word.  
  
  Em projetos de nível de documento, você não pode usar o `GetVstoObject` método para criar um novo <xref:Microsoft.Office.Tools.Excel.Workbook>, <xref:Microsoft.Office.Tools.Excel.Worksheet>, ou <xref:Microsoft.Office.Tools.Word.Document> item de host em tempo de execução. Você pode usar esse método somente para acessar itens de host existentes que são gerados no seu projeto em tempo de design. Se você quiser criar novos itens de host em tempo de execução, você deve desenvolver um projeto de suplemento do VSTO. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md) e [pastas de trabalho do Excel em suplementos do VSTO em tempo de execução e de documentos do Word estender](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="use-the-getvstoobject-and-hasvstoobject-methods"></a>Use os métodos GetVstoObject e HasVstoObject  
 Para chamar o `HasVstoObject` e `GetVstoObject` método, use o `Globals.Factory.GetVstoObject` ou `Globals.Factory.HasVstoObject` método e passar o objeto nativo do Word ou Excel (como um <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Worksheet>) que você deseja testar.  
  
## <a name="see-also"></a>Consulte também  
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md)   
 [Gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)  
  
  
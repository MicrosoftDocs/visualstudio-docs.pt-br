---
title: Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- GetVstoObject method
- application-level add-ins [Office development in Visual Studio], adding controls to documents
- host items [Office development in Visual Studio], creating at run time in add-ins
- application-level add-ins [Office development in Visual Studio], extending Word documents
- application-level add-ins [Office development in Visual Studio], extending Excel workbooks
- controls [Office development in Visual Studio], adding at run time
- HasVstoObject method
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 424b2cf8a6461ed0d60a1c16555c49c0ed8a0136
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49895776"
---
# <a name="extend-word-documents-and-excel-workbooks-in-vsto-add-ins-at-runtime"></a>Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução
  Você pode usar um suplemento do VSTO para personalizar os documentos do Word e pastas de trabalho do Excel das seguintes maneiras:  
  
- Adicione controles gerenciados para qualquer documento aberto ou planilha.  
  
- Converter um objeto de lista existente em uma planilha do Excel em um estendido <xref:Microsoft.Office.Tools.Excel.ListObject> que expõe eventos e pode ser associado a dados usando o modelo de associação de dados de formulários do Windows.  
  
- Eventos de nível de aplicativo de acesso que são expostos pelo Word e Excel para documentos específicos, pastas de trabalho e planilhas.  
  
  Para usar essa funcionalidade, você deve gerar um objeto em tempo de execução que estende o documento ou pasta de trabalho.  
  
  **Aplica-se a:** as informações neste artigo se aplicam a projetos de suplemento do VSTO para os seguintes aplicativos: Excel e Word. Para obter mais informações, consulte [recursos disponíveis por tipo de projeto e aplicativo do Office](../vsto/features-available-by-office-application-and-project-type.md).  
  
## <a name="generate-extended-objects-in-vsto-add-ins"></a>Gerar objetos estendidos nos suplementos do VSTO  
 *Objetos estendidos* são instâncias de tipos fornecidos pelo Visual Studio Tools para Office runtime que adicionam funcionalidade aos objetos que existem nativamente nos modelos de objeto do Word ou Excel (chamado *objetos nativos do Office*). Para gerar um objeto estendido para um objeto do Word ou Excel, use o `GetVstoObject` método. Na primeira vez que você chamar o `GetVstoObject` objeto do método de uma palavra especificada ou o Excel, ele retorna um novo objeto que estende o objeto especificado. Cada vez que você chama o método e especificar o mesmo do Word ou do Excel do objeto, ele retorna o mesmo objeto estendido.  
  
 O tipo de objeto estendido tem o mesmo nome que o tipo do objeto nativo do Office, mas o tipo é definido na <xref:Microsoft.Office.Tools.Excel> ou <xref:Microsoft.Office.Tools.Word> namespace. Por exemplo, se você chamar o `GetVstoObject` método para estender uma <xref:Microsoft.Office.Interop.Word.Document> do objeto, o método retorna um <xref:Microsoft.Office.Tools.Word.Document> objeto.  
  
 O `GetVstoObject` métodos destinam-se a ser usada principalmente em projetos de suplemento do VSTO. Você também pode usar esses métodos em projetos de nível de documento, mas eles se comportam de maneira diferente e têm menos usos.  
  
 Para determinar se um objeto estendido já foi gerado para um determinado objeto nativo do Office, use o `HasVstoObject` método. Para obter mais informações, consulte [determinar se um objeto do Office foi estendido](#HasVstoObject).  
  
### <a name="generate-host-items"></a>Gerar itens de host  
 Quando você usa o `GetVstoObject` para estender um objeto de nível de documento (ou seja, uma <xref:Microsoft.Office.Interop.Excel.Workbook>, <xref:Microsoft.Office.Interop.Excel.Worksheet>, ou <xref:Microsoft.Office.Interop.Word.Document>), o objeto retornado é chamado um *item de host*. Um item de host é um tipo que pode conter outros objetos, incluindo outros controles e objetos estendidos. Ele se parece com o tipo correspondente no Word ou Excel assembly de interoperabilidade primário, mas ele tem recursos adicionais. Para obter mais informações sobre itens de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
 Depois de gerar um item de host, você pode usá-lo para adicionar controles gerenciados para o documento, pasta de trabalho ou planilha. Para obter mais informações, consulte [gerenciados de adicionar controles a documentos e planilhas](#AddControls).  
  
#### <a name="to-generate-a-host-item-for-a-word-document"></a>Para gerar um item de host para um documento do Word  
  
-   O exemplo de código a seguir demonstra como gerar um item de host para o documento ativo.  
  
     [!code-vb[Trin_WordAddInDynamicControls#8](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#8)]
     [!code-csharp[Trin_WordAddInDynamicControls#8](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#8)]  
  
#### <a name="to-generate-a-host-item-for-an-excel-workbook"></a>Para gerar um item de host para uma pasta de trabalho do Excel  
  
-   O exemplo de código a seguir demonstra como gerar um item de host para a pasta de trabalho ativa.  
  
     [!code-vb[Trin_ExcelAddInDynamicControls#2](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#2)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#2](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#2)]  
  
#### <a name="to-generate-a-host-item-for-an-excel-worksheet"></a>Para gerar um item de host para uma planilha do Excel  
  
-   O exemplo de código a seguir demonstra como gerar um item de host para a planilha ativa em um projeto.  
  
     [!code-vb[Trin_ExcelAddInDynamicControls#1](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#1)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#1](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#1)]  
  
### <a name="generate-listobject-host-controls"></a>Gerar controles de host ListObject  
 Quando você usa o `GetVstoObject` método para estender uma <xref:Microsoft.Office.Interop.Excel.ListObject>, o método retorna um <xref:Microsoft.Office.Tools.Excel.ListObject>. O <xref:Microsoft.Office.Tools.Excel.ListObject> tem todos os recursos do original <xref:Microsoft.Office.Interop.Excel.ListObject>. Ele também tem uma funcionalidade adicional e pode ser associado a dados usando o modelo de vinculação de dados do Windows Forms. Para obter mais informações, consulte [controle ListObject](../vsto/listobject-control.md).  
  
#### <a name="to-generate-a-host-control-for-a-listobject"></a>Para gerar um controle de host para um ListObject  
  
-   O exemplo de código a seguir demonstra como gerar uma <xref:Microsoft.Office.Tools.Excel.ListObject> para o primeiro <xref:Microsoft.Office.Interop.Excel.ListObject> na planilha ativa em um projeto.  
  
     [!code-vb[Trin_ExcelAddInDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#3)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#3](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#3)]  
  
###  <a name="AddControls"></a> Adicionar controles gerenciados a documentos e planilhas  
 Depois de gerar uma <xref:Microsoft.Office.Tools.Word.Document> ou <xref:Microsoft.Office.Tools.Excel.Worksheet>, você pode adicionar controles ao documento ou planilha esses estendidos objetos representam. Para adicionar controles, use o `Controls` propriedade do <xref:Microsoft.Office.Tools.Word.Document> ou <xref:Microsoft.Office.Tools.Excel.Worksheet>. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 Você pode adicionar controles de formulários do Windows ou *hospedar controles*. Um controle de host é um controle fornecido pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que encapsula um controle correspondente no assembly de interoperabilidade primário do Word ou Excel. Um controle de host expõe todo o comportamento do objeto nativo subjacente Office. Ele também gera eventos e pode ser associado a dados usando o modelo de associação de dados de formulários do Windows. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
> [!NOTE]  
>  Não é possível adicionar um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle em uma planilha, ou uma <xref:Microsoft.Office.Tools.Word.XMLNode> ou <xref:Microsoft.Office.Tools.Word.XMLNodes> controle a um documento, usando um suplemento do VSTO. Esses controles de host não podem ser adicionados por meio de programação. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).  
  
### <a name="persist-and-remove-controls"></a>Persistir e remover os controles  
 Quando você adiciona controles gerenciados em um documento ou planilha, os controles não são persistidos quando o documento for salvo e, em seguida, fechado. Todos os controles de host são removidos para que somente nativo Office objetos subjacentes são deixados para trás. Por exemplo, uma <xref:Microsoft.Office.Tools.Excel.ListObject> torna-se um <xref:Microsoft.Office.Interop.Excel.ListObject>. Todos os controles de formulários do Windows também são removidos, mas os wrappers de ActiveX para os controles são deixados para trás no documento. Você deve incluir o código no seu suplemento VSTO para limpar os controles, ou para recriar os controles na próxima vez em que o documento é aberto. Para obter mais informações, consulte [persistir controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).  
  
## <a name="access-application-level-events-on-documents-and-workbooks"></a>Eventos de nível de aplicativo de acesso em documentos e pastas de trabalho  
 Alguns eventos de documento, a pasta de trabalho e a planilha em que os modelos de objeto do Word e Excel nativos são acionados apenas no nível do aplicativo. Por exemplo, o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento é gerado quando um documento é aberto no Word, mas esse evento é definido em de <xref:Microsoft.Office.Interop.Word.Application> classe, em vez de <xref:Microsoft.Office.Interop.Word.Document> classe.  
  
 Quando você usa objetos apenas nativos do Office no seu suplemento do VSTO, você deve lidar com esses eventos de nível de aplicativo e, em seguida, escrever código adicional para determinar se o documento que gerou o evento é aquele que você personalizou. Itens de host fornecem esses eventos no nível do documento, para que ele seja mais fácil de manipular os eventos para um documento específico. Você pode gerar um item de host e, em seguida, manipular o evento para aquele item de host.  
  
### <a name="example-that-uses-native-word-objects"></a>Exemplo que usa objetos nativos do Word  
 O exemplo de código a seguir demonstra como manipular um evento de nível de aplicativo para documentos do Word. O `CreateDocument` método cria um novo documento e, em seguida, define um <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> manipulador de eventos que impede que este documento está sendo salvo. O evento é um evento de nível de aplicativo que é gerado para o <xref:Microsoft.Office.Interop.Word.Application> objeto e o manipulador de eventos devem comparar os `Doc` parâmetro com o `document1` objeto para determinar se `document1` representa o documento salvo.  
  
 [!code-vb[Trin_WordAddInDynamicControls #12](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#12)]
 [!code-csharp[Trin_WordAddInDynamicControls#12](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#12)]  
  
### <a name="examples-that-use-a-host-item"></a>Exemplos que usam um item de host  
 Os exemplos de código a seguir simplificam esse processo manipulando o <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> eventos de um <xref:Microsoft.Office.Tools.Word.Document> item de host. O `CreateDocument2` método nesses exemplos gera uma <xref:Microsoft.Office.Tools.Word.Document> que estende o `document2` objeto e, em seguida, ele define uma <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> manipulador de eventos que impede que o documento que está sendo salvo. O manipulador de eventos é chamado somente quando `document2` é salvo e pode cancelar a ação sem fazer nenhum trabalho extra para verificar qual documento foi salvo.  
  
 O exemplo de código a seguir demonstra essa tarefa.  
  
 [!code-vb[Trin_WordAddInDynamicControls #13](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#13)]
 [!code-csharp[Trin_WordAddInDynamicControls#13](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#13)]  
  
##  <a name="HasVstoObject"></a> Determinar se um objeto do Office foi estendido  
 Para determinar se um objeto estendido já foi gerado para um determinado objeto nativo do Office, use o `HasVstoObject` método. Esse método retornará **verdadeira** se um objeto estendido já foi gerado.  
  
 Use o método `Globals.Factory.HasVstoMethod`. Passe o objeto nativo do Word ou Excel, como um <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Worksheet>, que você deseja testar para um objeto estendido.  
  
 O `HasVstoObject` método é útil quando você deseja executar o código somente quando um objeto especificado do Office tem um objeto estendido. Por exemplo, se você tiver um Add-in do VSTO do Word que lida com o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento para remover os controles gerenciados de um documento antes de ser salvo, use o `HasVstoObject` método para determinar se o documento tiver sido estendido. Se o documento não foi estendido, ele não pode ter controles gerenciados e o manipulador de eventos pode retornar sem tentar limpar os controles no documento.  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)  
  
  
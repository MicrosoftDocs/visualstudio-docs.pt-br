---
title: Estenda documentos do Word & pastas de trabalho do Excel em suplementos do VSTO em tempo de execução
description: Saiba que você pode usar um suplemento do VSTO para personalizar documentos do Word e pastas de trabalho do Excel de várias maneiras.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 90dac328f336f7204bc9a70a0dbc543ec996922a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825661"
---
# <a name="extend-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time"></a>Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução
  Você pode usar um suplemento do VSTO para personalizar documentos do Word e pastas de trabalho do Excel das seguintes maneiras:

- Adicione controles gerenciados a qualquer documento ou planilha aberta.

- Converta um objeto de lista existente em uma planilha do Excel em um estendido <xref:Microsoft.Office.Tools.Excel.ListObject> que exponha eventos e possa ser associado a dados usando o modelo de associação de dados Windows Forms.

- Acesse eventos no nível do aplicativo que são expostos pelo Word e pelo Excel para documentos, pastas de trabalho e planilhas específicos.

  Para usar essa funcionalidade, você gera um objeto em tempo de execução que estende o documento ou a pasta de trabalho.

  **Aplica-se a:** As informações neste artigo se aplicam aos projetos de suplemento do VSTO para os seguintes aplicativos: Excel e Word. Para obter mais informações, consulte [recursos disponíveis por aplicativo do Office e tipo de projeto](../vsto/features-available-by-office-application-and-project-type.md).

## <a name="generate-extended-objects-in-vsto-add-ins"></a>Gerar objetos estendidos em suplementos do VSTO
 *Objetos estendidos* são instâncias de tipos fornecidos pelo ferramentas do Visual Studio para o tempo de execução do Office que adicionam funcionalidade a objetos que existem nativamente nos modelos de objeto do Word ou do Excel (chamados de *objetos nativos do Office*). Para gerar um objeto estendido para um objeto do Word ou do Excel, use o `GetVstoObject` método. Na primeira vez que você chamar o `GetVstoObject` método para um objeto do Word ou Excel especificado, ele retornará um novo objeto que estende o objeto especificado. Cada vez que você chama o método e especifica o mesmo objeto Word ou Excel, ele retorna o mesmo objeto estendido.

 O tipo do objeto estendido tem o mesmo nome que o tipo do objeto do Office nativo, mas o tipo é definido no <xref:Microsoft.Office.Tools.Excel> namespace ou <xref:Microsoft.Office.Tools.Word> . Por exemplo, se você chamar o `GetVstoObject` método para estender um <xref:Microsoft.Office.Interop.Word.Document> objeto, o método retornará um <xref:Microsoft.Office.Tools.Word.Document> objeto.

 Os `GetVstoObject` métodos se destinam a serem usados principalmente em projetos de suplemento do VSTO. Você também pode usar esses métodos em projetos de nível de documento, mas eles se comportam de forma diferente e têm menos usos.

 Para determinar se um objeto estendido já foi gerado para um determinado objeto do Office nativo, use o `HasVstoObject` método. Para obter mais informações, consulte [determinar se um objeto do Office foi estendido](#HasVstoObject).

### <a name="generate-host-items"></a>Gerar itens de host
 Quando você usa o `GetVstoObject` para estender um objeto de nível de documento (ou seja, um <xref:Microsoft.Office.Interop.Excel.Workbook> , <xref:Microsoft.Office.Interop.Excel.Worksheet> ou <xref:Microsoft.Office.Interop.Word.Document> ), o objeto retornado é chamado de *item de host*. Um item de host é um tipo que pode conter outros objetos, incluindo outros controles e objetos estendidos. Ele é semelhante ao tipo correspondente no assembly de interoperabilidade primário do Word ou Excel, mas tem recursos adicionais. Para obter mais informações sobre itens de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

 Depois de gerar um item de host, você pode usá-lo para adicionar controles gerenciados ao documento, pasta de trabalho ou planilha. Para obter mais informações, consulte [Adicionar controles gerenciados a documentos e planilhas](#AddControls).

#### <a name="to-generate-a-host-item-for-a-word-document"></a>Para gerar um item de host para um documento do Word

- O exemplo de código a seguir demonstra como gerar um item de host para o documento ativo.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet8":::

#### <a name="to-generate-a-host-item-for-an-excel-workbook"></a>Para gerar um item de host para uma pasta de trabalho do Excel

- O exemplo de código a seguir demonstra como gerar um item de host para a pasta de trabalho ativa.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet2":::

#### <a name="to-generate-a-host-item-for-an-excel-worksheet"></a>Para gerar um item de host para uma planilha do Excel

- O exemplo de código a seguir demonstra como gerar um item de host para a planilha ativa em um projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet1":::

### <a name="generate-listobject-host-controls"></a>Gerar controles de host ListObject
 Quando você usa o `GetVstoObject` método para estender um <xref:Microsoft.Office.Interop.Excel.ListObject> , o método retorna um <xref:Microsoft.Office.Tools.Excel.ListObject> . O <xref:Microsoft.Office.Tools.Excel.ListObject> tem todos os recursos do original <xref:Microsoft.Office.Interop.Excel.ListObject> . Ele também tem funcionalidade adicional e pode ser associado a dados usando o modelo de associação de dados Windows Forms. Para obter mais informações, consulte o [controle ListObject](../vsto/listobject-control.md).

#### <a name="to-generate-a-host-control-for-a-listobject"></a>Para gerar um controle de host para um ListObject

- O exemplo de código a seguir demonstra como gerar um <xref:Microsoft.Office.Tools.Excel.ListObject> para o primeiro <xref:Microsoft.Office.Interop.Excel.ListObject> na planilha ativa em um projeto.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet3":::

### <a name="add-managed-controls-to-documents-and-worksheets"></a><a name="AddControls"></a> Adicionar controles gerenciados a documentos e planilhas
 Depois de gerar um <xref:Microsoft.Office.Tools.Word.Document> ou <xref:Microsoft.Office.Tools.Excel.Worksheet> , você pode adicionar controles ao documento ou à planilha que esses objetos estendidos representam. Para adicionar controles, use a `Controls` Propriedade do <xref:Microsoft.Office.Tools.Word.Document> ou <xref:Microsoft.Office.Tools.Excel.Worksheet> . Para obter mais informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

 Você pode adicionar Windows Forms controles ou *controles de host*. Um controle de host é um controle fornecido pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que encapsula um controle correspondente no assembly de interoperabilidade primário do Word ou do Excel. Um controle de host expõe todo o comportamento do objeto do Office nativo subjacente. Ele também gera eventos e pode ser associado a dados usando o modelo de associação de dados Windows Forms. Para obter mais informações, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

> [!NOTE]
> Você não pode adicionar um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle a uma planilha ou a <xref:Microsoft.Office.Tools.Word.XMLNode> um <xref:Microsoft.Office.Tools.Word.XMLNodes> controle ou a um documento usando um suplemento do VSTO. Esses controles de host não podem ser adicionados programaticamente. Para obter mais informações, consulte [limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md).

### <a name="persist-and-remove-controls"></a>Persistir e remover controles
 Quando você adiciona controles gerenciados a um documento ou planilha, os controles não são persistidos quando o documento é salvo e fechado. Todos os controles de host são removidos para que apenas os objetos nativos do Office subjacentes sejam deixados para trás. Por exemplo, um <xref:Microsoft.Office.Tools.Excel.ListObject> se torna um <xref:Microsoft.Office.Interop.Excel.ListObject> . Todos os controles de Windows Forms também são removidos, mas os wrappers do ActiveX para os controles são deixados para trás no documento. Você deve incluir o código em seu suplemento do VSTO para limpar os controles ou recriar os controles na próxima vez em que o documento for aberto. Para obter mais informações, consulte [manter controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).

## <a name="access-application-level-events-on-documents-and-workbooks"></a>Acessar eventos no nível do aplicativo em documentos e pastas de trabalho
 Alguns eventos de documento, pasta de trabalho e planilha nos modelos de objeto do Word e do Excel nativos são gerados apenas no nível do aplicativo. Por exemplo, o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento é gerado quando um documento é aberto no Word, mas esse evento é definido na <xref:Microsoft.Office.Interop.Word.Application> classe, em vez da <xref:Microsoft.Office.Interop.Word.Document> classe.

 Ao usar somente objetos nativos do Office em seu suplemento do VSTO, você deve lidar com esses eventos no nível do aplicativo e, em seguida, escrever código adicional para determinar se o documento que disparou o evento é personalizado. Os itens de host fornecem esses eventos no nível do documento, para que seja mais fácil manipular os eventos de um documento específico. Você pode gerar um item de host e, em seguida, manipular o evento para esse item de host.

### <a name="example-that-uses-native-word-objects"></a>Exemplo que usa objetos nativos do Word
 O exemplo de código a seguir demonstra como lidar com um evento no nível do aplicativo para documentos do Word. O `CreateDocument` método cria um novo documento e, em seguida, define um <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> manipulador de eventos que impede que este documento seja salvo. O evento é um evento no nível do aplicativo que é gerado para o <xref:Microsoft.Office.Interop.Word.Application> objeto e o manipulador de eventos deve comparar o `Doc` parâmetro com o `document1` objeto para determinar se `document1` representa o documento salvo.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet12":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet12":::

### <a name="examples-that-use-a-host-item"></a>Exemplos que usam um item de host
 Os exemplos de código a seguir simplificam esse processo manipulando o <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> evento de um <xref:Microsoft.Office.Tools.Word.Document> item de host. O `CreateDocument2` método nesses exemplos gera um <xref:Microsoft.Office.Tools.Word.Document> que estende o `document2` objeto e, em seguida, define um <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> manipulador de eventos que impede que o documento seja salvo. O manipulador de eventos é chamado somente quando `document2` é salvo e pode cancelar a ação salvar sem fazer nenhum trabalho extra para verificar qual documento foi salvo.

 O exemplo de código a seguir demonstra essa tarefa.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet13":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet13":::

## <a name="determine-whether-an-office-object-has-been-extended"></a><a name="HasVstoObject"></a> Determinar se um objeto do Office foi estendido
 Para determinar se um objeto estendido já foi gerado para um determinado objeto do Office nativo, use o `HasVstoObject` método. Esse método retornará **true** se um objeto estendido já tiver sido gerado.

 Use o método `Globals.Factory.HasVstoMethod`. Passe o objeto nativo do Word ou do Excel, como um <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Worksheet> , que você deseja testar para um objeto estendido.

 O `HasVstoObject` método é útil quando você deseja executar o código somente quando um objeto do Office especificado tem um objeto estendido. Por exemplo, se você tiver um suplemento do VSTO do Word que manipule o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento para remover os controles gerenciados de um documento antes que ele seja salvo, use o `HasVstoObject` método para determinar se o documento foi estendido. Se o documento não tiver sido estendido, ele não poderá ter controles gerenciados e o manipulador de eventos poderá retornar sem tentar limpar os controles no documento.

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Exemplos e orientações de desenvolvimento do Office](../vsto/office-development-samples-and-walkthroughs.md)

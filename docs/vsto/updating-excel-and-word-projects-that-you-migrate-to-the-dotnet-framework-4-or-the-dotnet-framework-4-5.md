---
title: Atualizar projetos do Excel e Word migrados para o .NET Framework 4 ou o .NET Framework 4.5
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: aeb36f92533992161e2c7fa4f7bbcd3537fd0ebc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919388"
---
# <a name="update-excel-and-word-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>Atualizar projetos do Excel e Word migrados para o .NET Framework 4 ou o .NET Framework 4.5
  Se você tiver um projeto do Excel ou Word que use qualquer um dos recursos a seguir, você deve modificar seu código se a estrutura de destino é alterada para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior:  
  
- [Métodos GetVstoObject e HasVstoObject](#GetVstoObject)  
  
- [Classes geradas em projetos de nível de documento](#generatedclasses)  
  
- [Controles Windows Forms em documentos](#winforms)  
  
- [Eventos de controle de conteúdo do Word](#ccevents)  
  
- [Classes OLEObject e OLEControl](#ole)  
  
- [Propriedade Controls.Item(Object)](#itemproperty)  
  
- [Coleções que derivam de CollectionBase](#collections)  
  
  Você também deve remover o `Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute` e as referências aos `Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy` classe a partir de projetos do Excel que são redirecionadas para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Visual Studio não remove esse atributo ou a referência de classe para você.  
  
## <a name="remove-the-excellocale1033-attribute-from-excel-projects"></a>Remova o atributo de ExcelLocale1033 dos projetos do Excel  
 O `Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute` foi removido da parte do Visual Studio 2010 Tools para Office runtime que é usado para soluções que direcionam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. O common language runtime (CLR) na [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e posteriormente sempre passa localidade 1033 ID para o modelo de objeto do Excel e você não poderá mais usar esse atributo para desabilitar esse comportamento. Para obter mais informações, consulte [globalização e localização de soluções do Excel](../vsto/globalization-and-localization-of-excel-solutions.md).  
  
### <a name="to-remove-the-excellocale1033attribute"></a>Para remover o ExcelLocale1033Attribute  
  
1.  Com o projeto aberto no Visual Studio, abra **Gerenciador de soluções**.  
  
2.  Sob o **propriedades** nó (para c#) ou o **My Project** nó (para Visual Basic), clique duas vezes no arquivo AssemblyInfo código para abri-lo no editor de códigos.  
  
    > [!NOTE]  
    >  Em projetos do Visual Basic, você deve clicar o **Show All Files** botão na **Gerenciador de soluções** para ver o arquivo de código de AssemblyInfo.  
  
3.  Localize o `Microsoft.Office.Tools.Excel.ExcelLocale1033Attribute` e removê-lo a partir do arquivo ou comentá-lo.  
  
    ```vb  
    <Assembly: ExcelLocale1033Proxy(True)>  
    ```  
  
    ```csharp  
    [assembly: ExcelLocale1033Proxy(true)]  
    ```  
  
## <a name="remove-a-reference-to-the-excellocal1033proxy-class"></a>Remover uma referência à classe ExcelLocal1033Proxy  
 Projetos que foram criados usando o Microsoft Visual Studio 2005 Tools para o Microsoft Office System instanciar o Excel <xref:Microsoft.Office.Interop.Excel.Application> objeto usando o `Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy` classe. Essa classe foi removida da parte do Visual Studio 2010 Tools para Office runtime que usou para soluções que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Portanto, você deve remover ou comentar a linha de código que faz referência a essa classe.  
  
### <a name="to-remove-the-reference-to-the-excellocal1033proxy-class"></a>Para remover a referência à classe ExcelLocal1033Proxy  
  
1.  Abra o projeto no Visual Studio e, em seguida, abra **Gerenciador de soluções**.  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho *ThisAddin.cs* (para c#) ou *ThisAddIn. vb* (para Visual Basic) e, em seguida, escolha **Exibir código**.  
  
3.  No Editor de códigos, no `VSTO generated code` região, remova ou comente a linha de código a seguir.  
  
    ```vb  
    Me.Application = CType(Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy.Wrap(GetType(Excel.Application), Me.Application), Excel.Application)  
  
    ```  
  
    ```csharp  
    this.Application = (Excel.Application)Microsoft.Office.Tools.Excel.ExcelLocale1033Proxy.Wrap(typeof(Excel.Application), this.Application);  
  
    ```  
  
##  <a name="GetVstoObject"></a> Atualizar o código que usa os métodos GetVstoObject e HasVstoObject  
 Em projetos direcionados ao .NET Framework 3.5, o `GetVstoObject` ou `HasVstoObject` métodos estão disponíveis como métodos de extensão em um dos seguintes objetos nativos em seu projeto: <xref:Microsoft.Office.Interop.Word.Document>, <xref:Microsoft.Office.Interop.Excel.Workbook>, <xref:Microsoft.Office.Interop.Excel.Worksheet>, ou <xref:Microsoft.Office.Interop.Excel.ListObject>. Quando você chama esses métodos, você não precisa passar um parâmetro. O exemplo de código a seguir demonstra como usar o método GetVstoObject em um Add-in do VSTO do Word que tem como alvo o .NET Framework 3.5.  
  
```vb  
Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _  
    Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject()  
```  
  
```csharp  
Microsoft.Office.Tools.Word.Document vstoDocument =   
    Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject();  
```  
  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve modificar seu código para acessar esses métodos em uma das seguintes maneiras:  
  
- Você ainda pode acessar esses métodos como métodos de extensão em <xref:Microsoft.Office.Interop.Word.Document>, <xref:Microsoft.Office.Interop.Excel.Workbook>, <xref:Microsoft.Office.Interop.Excel.Worksheet>, ou <xref:Microsoft.Office.Interop.Excel.ListObject> objetos. No entanto, agora você deve passar o objeto retornado pelo `Globals.Factory` propriedade para esses métodos.  
  
  ```vb  
  Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _  
      Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject(Globals.Factory)  
  ```  
  
  ```csharp  
  Microsoft.Office.Tools.Word.Document vstoDocument =   
      Globals.ThisAddIn.Application.ActiveDocument.GetVstoObject(Globals.Factory);  
  ```  
  
- Como alternativa, você pode acessar esses métodos no objeto que é retornado pelo `Globals.Factory` propriedade. Quando você acessa esses métodos dessa forma, você deve passar o objeto nativo que você deseja estender para o método.  
  
  ```vb  
  Dim vstoDocument as Microsoft.Office.Tools.Word.Document = _  
      Globals.Factory.GetVstoObject(Globals.ThisAddIn.Application.ActiveDocument)  
  ```  
  
  ```csharp  
  Microsoft.Office.Tools.Word.Document vstoDocument =   
      Globals.Factory.GetVstoObject(Globals.ThisAddIn.Application.ActiveDocument);  
  ```  
  
  Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
##  <a name="generatedclasses"></a> Atualizar o código que usa instâncias das classes geradas em projetos de nível de documento  
 Em projetos de nível de documento que direcionam o .NET Framework 3.5, as classes geradas nos projetos derivam as classes a seguir no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]:  
  
- `ThisDocument`: <xref:Microsoft.Office.Tools.Word.Document>  
  
- `ThisWorkbook`: <xref:Microsoft.Office.Tools.Excel.Workbook>  
  
- `Sheet` *n*: <xref:Microsoft.Office.Tools.Excel.Worksheet>  
  
- `Chart` *n*: <xref:Microsoft.Office.Tools.Excel.ChartSheet>  
  
  Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, os tipos no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] listados acima são interfaces, em vez de classes. Gerado as classes em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior derivam as seguintes novas classes no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]:  
  
- `ThisDocument`: <xref:Microsoft.Office.Tools.Word.DocumentBase>  
  
- `ThisWorkbook`: <xref:Microsoft.Office.Tools.Excel.WorkbookBase>  
  
- `Sheet` *n*: <xref:Microsoft.Office.Tools.Excel.WorksheetBase>  
  
- `Chart` *n*: <xref:Microsoft.Office.Tools.Excel.ChartSheetBase>  
  
  Se o código em seu projeto se refere a uma instância de uma das classes geradas como a classe base que ela deriva, você deve modificar o código.  
  
  Por exemplo, em um projeto de pasta de trabalho do Excel que tem como alvo o .NET Framework 3.5, você pode ter um método auxiliar que executa algum trabalho em instâncias do gerado `Sheet` *n* classes no seu projeto.  
  
```vb  
Private Sub DoSomethingToSheet(ByVal worksheet As Microsoft.Office.Tools.Excel.Worksheet)  
    ' Do something to the worksheet object.  
End Sub  
```  
  
```csharp  
private void DoSomethingToSheet(Microsoft.Office.Tools.Excel.Worksheet worksheet)  
{  
    // Do something to the worksheet object.  
}  
```  
  
 Se você redirecionar o projeto para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve fazer uma das seguintes alterações em seu código:  
  
-   Modificar qualquer código que chama o `DoSomethingToSheet` método para passar a <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Base%2A> propriedade de um <xref:Microsoft.Office.Tools.Excel.WorksheetBase> objeto em seu projeto. Essa propriedade retorna um <xref:Microsoft.Office.Tools.Excel.Worksheet> objeto.  
  
    ```vb  
    DoSomethingToSheet(Globals.Sheet1.Base)  
    ```  
  
    ```csharp  
    DoSomethingToSheet(Globals.Sheet1.Base);  
    ```  
  
-   Modificar a `DoSomethingToSheet` parâmetro do método para esperar um <xref:Microsoft.Office.Tools.Excel.WorksheetBase> do objeto em vez disso.  
  
    ```vb  
    Private Sub DoSomethingToSheet(ByVal worksheet As Microsoft.Office.Tools.Excel.WorksheetBase)  
        ' Do something to the worksheet object.  
    End Sub  
    ```  
  
    ```csharp  
    private void DoSomethingToSheet (Microsoft.Office.Tools.Excel.WorksheetBase worksheet)  
    {  
        // Do something to the worksheet object.  
    }  
    ```  
  
##  <a name="winforms"></a> Atualizar o código que usa controles Windows Forms em documentos  
 Você deve adicionar uma **usando** (c#) ou **Imports** instrução (Visual Basic) para o <xref:Microsoft.Office.Tools.Excel> ou <xref:Microsoft.Office.Tools.Word> namespace na parte superior de qualquer arquivo de código que usa a propriedade de controles para adicionar formulários do Windows Controla por meio de programação para o documento ou planilha.  
  
 Em projetos direcionados ao .NET Framework 3.5, os métodos que adicionam controles dos Windows Forms (como o `AddButton` método) são definidos na <xref:Microsoft.Office.Tools.Excel.ControlCollection> e <xref:Microsoft.Office.Tools.Word.ControlCollection> classes.  
  
 Em projetos que segmentam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores, esses métodos são métodos de extensão que estão disponíveis na propriedade de controles. Para usar esses métodos de extensão, o arquivo de código em que você pode usar os métodos deve ter uma **usando** ou **Imports** instrução para o <xref:Microsoft.Office.Tools.Excel> ou <xref:Microsoft.Office.Tools.Word> namespace. Essa instrução é gerada automaticamente em novos projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. No entanto, essa instrução não é adicionada automaticamente em projetos que direcionam o .NET Framework 3.5, você deve adicioná-lo ao redirecionar o projeto.  
  
 Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
##  <a name="ccevents"></a> Atualizar o código que trata os eventos de controle de conteúdo do Word  
 Em projetos direcionados ao .NET Framework 3.5, os eventos de controles de conteúdo do Word são identificados por genérica <xref:System.EventHandler%601> delegar. Em projetos que segmentam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores, esses eventos são manipulados por outros delegados.  
  
 A tabela a seguir lista os eventos de controle de conteúdo do Word e os delegados que são associados com eles em projetos direcionados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
|evento|Delegado a ser usado em [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e projetos posteriores|  
|-----------| - |  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Added>|<xref:Microsoft.Office.Tools.Word.ContentControlAddedEventHandler>|  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.ContentUpdating>|<xref:Microsoft.Office.Tools.Word.ContentControlContentUpdatingEventHandler>|  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Deleting>|<xref:Microsoft.Office.Tools.Word.ContentControlDeletingEventHandler>|  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering>|<xref:Microsoft.Office.Tools.Word.ContentControlEnteringEventHandler>|  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Exiting>|<xref:Microsoft.Office.Tools.Word.ContentControlExitingEventHandler>|  
|<xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating>|<xref:Microsoft.Office.Tools.Word.ContentControlStoreUpdatingEventHandler>|  
  
##  <a name="ole"></a> Atualizar o código que usa as classes OLEObject e OLEControl  
 Em projetos direcionados ao .NET Framework 3.5, você pode adicionar controles personalizados (por exemplo, controles de usuário do Windows Forms) para um documento ou planilha usando o `Microsoft.Office.Tools.Excel.OLEObject` e `Microsoft.Office.Tools.Word.OLEControl` classes.  
  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, essas classes foram substituídas pela <xref:Microsoft.Office.Tools.Excel.ControlSite> e <xref:Microsoft.Office.Tools.Word.ControlSite> interfaces. Você deve modificar o código que se refere à `Microsoft.Office.Tools.Excel.OLEObject` e `Microsoft.Office.Tools.Word.OLEControl` para referir-se em vez disso, para <xref:Microsoft.Office.Tools.Excel.ControlSite> e <xref:Microsoft.Office.Tools.Word.ControlSite>. Que não sejam os novos nomes, esses controles se comportam da mesma forma que eles fazem em projetos direcionados ao .NET Framework 3.5.  
  
 Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
##  <a name="itemproperty"></a> Atualizar o código que usa a propriedade Controls.Item(Object)  
 Em projetos direcionados ao .NET Framework 3.5, você pode usar a propriedade Item(Object) da Microsoft.Office.Tools.Word.Document.Controls ou `Microsoft.Office.Tools.Excel.Worksheet.Controls` coleção para determinar se um documento ou a planilha tem um controle especificado.  
  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, a propriedade Item(Object) foi removida dessas coleções. Para determinar se um documento ou planilha contém um controle especificado, use o método Contains(System.Object) a <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> ou <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> coleção em vez disso.  
  
 Para obter mais informações sobre a coleção de controles de documentos e planilhas, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
##  <a name="collections"></a> Atualizar o código que usa coleções que derivam de CollectionBase  
 Em projetos direcionados ao .NET Framework 3.5, coleção de vários tipos na [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] derivam de <xref:System.Collections.CollectionBase> classe, como `Microsoft.Office.Tools.SmartTagCollection`, `Microsoft.Office.Tools.Excel.ControlCollection`, e `Microsoft.Office.Tools.Word.ControlCollection`.  
  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores, esses tipos de coleção agora são interfaces que não derivam de <xref:System.Collections.CollectionBase>. Alguns membros não estão mais disponíveis nesses tipos de coleção, como <xref:System.Collections.CollectionBase.Capacity%2A>, <xref:System.Collections.CollectionBase.List%2A>, e <xref:System.Collections.CollectionBase.InnerList%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Migrar soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [Controles de conteúdo](../vsto/content-controls.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)  
  
  
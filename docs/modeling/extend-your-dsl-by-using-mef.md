---
title: Estender a DSL usando MEF
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04d14b3b17953ef30620d9f616bb471b186e9c9f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547635"
---
# <a name="extend-your-dsl-by-using-mef"></a>Estender a DSL usando MEF

Você pode estender sua DSL (linguagem específica de domínio) usando o Managed Extensibility Framework (MEF). Você ou outros desenvolvedores poderão escrever extensões para a DSL sem alterar a definição de DSL e o código do programa. Essas extensões incluem comandos de menu, manipuladores de arrastar e soltar e validação. Os usuários poderão instalar sua DSL e, opcionalmente, instalar extensões para ela.

Além disso, quando você habilita o MEF em sua DSL, pode ser mais fácil escrever alguns dos recursos de sua DSL, mesmo que eles sejam todos criados com a DSL.

Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).

### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>Para permitir que sua DSL seja estendida pelo MEF

1. Crie uma nova pasta chamada **MefExtension** dentro do projeto **DslPackage** . Adicione os seguintes arquivos a ele:

     Nome do arquivo:`CommandExtensionVSCT.tt`

    > [!IMPORTANT]
    > Defina o GUID nesse arquivo para ser o mesmo que o GUID CommandSetId definido em DslPackage\GeneratedCode\Constants.tt

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#
    // CmdSet Guid must be defined before master template is included
    // This Guid must be kept synchronized with the CommandSetId Guid in Constants.tt
    Guid guidCmdSet = new Guid ("00000000-0000-0000-0000-000000000000");
    string menuidCommandsExtensionBaseId="0x4000";
    #>
    <#@ include file="DslPackage\CommandExtensionVSCT.tt" #>
    ```

    Nome do arquivo:`CommandExtensionRegistrar.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>
    ```

    Nome do arquivo:`ValidationExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>
    ```

    Nome do arquivo:`ValidationExtensionRegistrar.tt`

    Se você adicionar esse arquivo, deverá habilitar a validação em sua DSL usando pelo menos um dos comutadores no **EditorValidation** no Gerenciador de DSL.

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>
    ```

    Nome do arquivo:`PackageExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>
    ```

2. Crie uma nova pasta chamada **MefExtension** dentro do projeto **DSL** . Adicione os seguintes arquivos a ele:

     Nome do arquivo:`DesignerExtensionMetaDataAttribute.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>
    ```

    Nome do arquivo:`GestureExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionEnablement.tt" #>
    ```

    Nome do arquivo:`GestureExtensionController.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionController.tt" #>
    ```

3. Adicione a seguinte linha ao arquivo existente chamado **DslPackage\Commands.vsct**:

    ```xml
    <Include href="MefExtension\CommandExtensionVSCT.vsct"/>
    ```

    Insira a linha após a `<Include>` diretiva existente.

4. Abra *DslDefinition. DSL*.

5. No Gerenciador de DSL, selecione **Editor\Validation**.

6. No janela Propriedades, certifique-se de que pelo menos uma das propriedades nomeadas **usa** seja `true` .

7. Na barra de ferramentas **Gerenciador de soluções** , clique em **transformar todos os modelos**.

     Os arquivos subsidiários aparecem abaixo de cada um dos arquivos que você adicionou.

8. Compile e execute a solução para verificar se ela ainda está funcionando.

Sua DSL agora está habilitada para MEF. Você pode escrever comandos de menu, manipuladores de gestos e restrições de validação como extensões de MEF. Você pode escrever essas extensões em sua solução de DSL junto com outro código personalizado. Além disso, você ou outros desenvolvedores podem escrever extensões do Visual Studio separadas que estendem sua DSL.

## <a name="create-an-extension-for-a-mef-enabled-dsl"></a>Criar uma extensão para uma DSL habilitada para MEF

Se você tiver acesso a um DSL habilitado para MEF criado por você mesmo ou por outra pessoa, você poderá gravar extensões para ele. As extensões podem ser usadas para adicionar comandos de menu, manipuladores de gestos ou restrições de validação. Para criar essas extensões, você usa uma solução de VSIX (Visual Studio Extension). A solução tem duas partes: um projeto de biblioteca de classes que cria o assembly de código e um projeto VSIX que empacota o assembly.

### <a name="to-create-a-dsl-extension-vsix"></a>Para criar um VSIX de extensão de DSL

1. Crie um projeto de **Biblioteca de Classes**.

2. No novo projeto, adicione uma referência ao assembly da DSL.

   - Esse assembly geralmente tem um nome que termina com ".Dsl.dll".

   - Se você tiver acesso ao projeto de DSL, poderá encontrar o arquivo de assembly na pasta de **DSL \\ \\ \* ** do diretório

   - Se você tiver acesso ao arquivo VSIX de DSL, poderá encontrar o assembly alterando a extensão de nome de arquivo do arquivo VSIX para ". zip". Descompacte o arquivo. zip.

3. Adicione referências aos seguintes assemblies .NET:

   - Microsoft.VisualStudio.Modeling.Sdk.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll

   - System.ComponentModel.Composition.dll

   - System.Windows.Forms.dll

4. Crie um novo projeto de **projeto VSIX** .

5. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto VSIX e escolha **definir como projeto de inicialização**.

6. No novo projeto, abra **Source. Extension. vsixmanifest**.

7. Clique em **adicionar conteúdo**. Na caixa de diálogo, defina **tipo de conteúdo** para **componente MEF**e **projeto de origem** para o projeto de biblioteca de classes.

8. Adicione uma referência de VSIX ao DSL.

   1. Em **origem. extensão. vsixmanifest**, clique em **Adicionar referência**

   2. Na caixa de diálogo, clique em **Adicionar carga** e localize o arquivo VSIX da DSL. O arquivo VSIX é criado na solução DSL, no **DslPackage \\ bin \\ \* **.

       Isso permite que os usuários instalem a DSL e sua extensão ao mesmo tempo. Se o usuário já tiver instalado a DSL, somente sua extensão será instalada.

9. Examine e atualize os outros campos de **origem. extensão. vsixmanifest**. Clique em **selecionar edições** e verifique se as edições corretas do Visual Studio estão definidas.

10. Adicione código ao projeto de biblioteca de classes. Use os exemplos na próxima seção como guia.

     Você pode adicionar qualquer número de classes de comando, de gesto e de validação.

11. Para testar a extensão, pressione **F5**. Na instância experimental do Visual Studio, crie ou abra um arquivo de exemplo da DSL.

## <a name="writing-mef-extensions-for-dsls"></a>Gravando extensões de MEF para DSLs

Você pode gravar extensões no projeto de código do assembly de uma solução de extensão de DSL separada. Você também pode usar o MEF em seu projeto DslPackage, como uma maneira conveniente de escrever comandos, gestos e código de validação como parte da DSL.

### <a name="menu-commands"></a>Comandos de menu

Para escrever um comando de menu, defina uma classe que implemente <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> e Prefixe a classe com o atributo que é definido em sua DSL, chamado *YourDsl* `CommandExtension` . Você pode gravar mais de uma classe de comando de menu.

`QueryStatus()`é chamado sempre que o usuário clica com o botão direito do mouse no diagrama. Ele deve inspecionar a seleção atual e definir `command.Enabled` para indicar quando o comando é aplicável.

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl; // My DSL
using Company.MyDsl.ExtensionEnablement; // My DSL
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement; // IVsSelectionContext
using Microsoft.VisualStudio.Modeling.ExtensionEnablement; // ICommandExtension

namespace MyMefExtension
{
  // Defined in Dsl\MefExtension\DesignerExtensionMetaDataAttribute.cs:
  [MyDslCommandExtension]
  public class MyCommandClass : ICommandExtension
  {
    /// <summary>
    /// Provides access to current document and selection.
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Called when the user selects this command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      // Transaction is required if you want to update elements.
      using (Transaction t = SelectionContext.CurrentStore
              .TransactionManager.BeginTransaction("fix names"))
      {
        foreach (ExampleShape shape in SelectionContext.CurrentSelection)
        {
          ExampleElement element = shape.ModelElement as ExampleElement;
          element.Name = element.Name + " !";
        }
        t.Commit();
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines whether the command should appear.
    /// This method should set command.Enabled and command.Visible.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled =
        command.Visible = (SelectionContext.CurrentSelection.OfType<ExampleShape>().Count() > 0);
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines the text of the command in the menu.
    /// </summary>
    public string Text
    {
      get { return "My menu command"; }
    }
  }
}
```

### <a name="gesture-handlers"></a>Manipuladores de gestos

Um manipulador de gestos pode lidar com objetos arrastados para o diagrama de qualquer lugar, dentro ou fora do Visual Studio. O exemplo a seguir permite que o usuário arraste arquivos do Windows Explorer para o diagrama. Ele cria elementos que contêm os nomes de arquivo.

Você pode escrever manipuladores para lidar com arrastar de outros modelos de DSL e modelos UML. Para obter mais informações, consulte [como adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace MefExtension
{
  [MyDslGestureExtension]
  class MyGestureExtension : IGestureExtension
  {
    public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
    {
      System.Windows.Forms.MessageBox.Show("double click!");
    }

    /// <summary>
    /// Called when the user drags anything over the diagram.
    /// Return true if the dragged object can be dropped on the current target.
    /// </summary>
    /// <param name="targetMergeElement">The shape or diagram that the mouse is currently over</param>
    /// <param name="diagramDragEventArgs">Data about the dragged element.</param>
    /// <returns></returns>
    public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      // This handler only allows items to be dropped onto the diagram:
      return targetMergeElement is MefDsl2Diagram &&
      // And only accepts files dragged from Windows Explorer:
        diagramDragEventArgs.Data.GetFormats().Contains("FileNameW");
    }

    /// <summary>
    /// Called when the user drops an item onto the diagram.
    /// </summary>
    /// <param name="targetDropElement"></param>
    /// <param name="diagramDragEventArgs"></param>
    public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      MefDsl2Diagram diagram = targetDropElement as MefDsl2Diagram;
      if (diagram == null) return;

      // This handler only accepts files dragged from Windows Explorer:
      string[] draggedFileNames = diagramDragEventArgs.Data.GetData("FileNameW") as string[];
      if (draggedFileNames == null || draggedFileNames.Length == 0) return;

      using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("file names"))
      {
        // Create an element to represent each file:
        foreach (string fileName in draggedFileNames)
        {
          ExampleElement element = new ExampleElement(diagram.ModelElement.Partition);
          element.Name = fileName;

          // This method of adding the new element allows the position
          // of the shape to be specified:
          ElementGroup group = new ElementGroup(element);
          diagram.ElementOperations.MergeElementGroupPrototype(
            diagram, group.CreatePrototype(), PointD.ToPointF(diagramDragEventArgs.MousePosition));
        }
        t.Commit();
      }
    }
  }
}
```

### <a name="validation-constraints"></a>Restrições de validação

Os métodos de validação são marcados pelo `ValidationExtension` atributo que é gerado pela DSL e também por <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> . O método pode aparecer em qualquer classe que não esteja marcada por um atributo.

Para obter mais informações, consulte [validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md).

```csharp
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.Validation;

namespace MefExtension
{
  class MyValidationExtension // Can be any class.
  {
    // SAMPLE VALIDATION METHOD.
    // All validation methods have the following attributes.

    // Specific to the extended DSL:
    [MyDslValidationExtension]

    // Determines when validation is applied:
    [ValidationMethod(
       ValidationCategories.Save
     | ValidationCategories.Open
     | ValidationCategories.Menu)]

    /// <summary>
    /// When validation is executed, this method is invoked
    /// for every element in the model that is an instance
    /// of the second parameter type.
    /// </summary>
    /// <param name="context">For reporting errors</param>
    /// <param name="elementToValidate"></param>
    private void ValidateClassNames
      (ValidationContext context,
       // Type determines to what elements this will be applied:
       ExampleElement elementToValidate)
    {
      // Write code here to test values and links.
      if (elementToValidate.Name.IndexOf(' ') >= 0)
      {
        // Log any unacceptable values:
        context.LogError(
          // Description:
          "Name must not contain spaces"
          // Error code unique to this type of error:
          , "MyDsl001"
          // Element to highlight when user double-clicks error:
          , elementToValidate);
} } } }
```

## <a name="see-also"></a>Confira também

- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)
- [MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)
- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md)

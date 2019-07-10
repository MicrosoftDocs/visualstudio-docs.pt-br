---
title: Estender a DSL usando MEF
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1b4748cd71416ce4d3e9cce64826f1ec97ceef85
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692976"
---
# <a name="extend-your-dsl-by-using-mef"></a>Estender a DSL usando MEF

Você pode estender sua linguagem específica de domínio (DSL) usando Managed Extensibility Framework (MEF). Você ou outros desenvolvedores poderão escrever extensões para a DSL sem alterar a definição de DSL e o código do programa. Essas extensões incluem comandos de menu, manipuladores de arrastar e soltar e validação. Os usuários poderão instalar a DSL e, opcionalmente, instalar extensões para ele.

Além disso, quando você habilita o MEF na DSL, ele pode ser mais fácil de escrever alguns dos recursos de sua DSL, mesmo se eles são criados junto com a DSL.

Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).

### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>Para habilitar sua DSL seja estendida pelo MEF

1. Criar uma nova pasta chamada **MefExtension** dentro de **DslPackage** projeto. Adicione os seguintes arquivos para ele:

     Nome do arquivo: `CommandExtensionVSCT.tt`

    > [!IMPORTANT]
    > O GUID do conjunto neste arquivo para ser o mesmo que o CommandSetId de GUID que é definido em DslPackage\GeneratedCode\Constants.tt

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

    Nome do arquivo: `CommandExtensionRegistrar.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>
    ```

    Nome do arquivo: `ValidationExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>
    ```

    Nome do arquivo: `ValidationExtensionRegistrar.tt`

    Se você adicionar esse arquivo, você deve habilitar a validação na DSL usando pelo menos uma das opções no **EditorValidation** no Gerenciador de DSL.

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>
    ```

    Nome do arquivo: `PackageExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>
    ```

2. Criar uma nova pasta chamada **MefExtension** dentro de **Dsl** projeto. Adicione os seguintes arquivos para ele:

     Nome do arquivo: `DesignerExtensionMetaDataAttribute.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>
    ```

    Nome do arquivo: `GestureExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionEnablement.tt" #>
    ```

    Nome do arquivo: `GestureExtensionController.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionController.tt" #>
    ```

3. Adicione a seguinte linha ao arquivo existente denominada **Dslpackage\commands.VSCT.** :

    ```xml
    <Include href="MefExtension\CommandExtensionVSCT.vsct"/>
    ```

    Insira a linha depois existente `<Include>` diretiva.

4. Abra *Dsldefinition*.

5. No Gerenciador de DSL, selecione **Editor \ validação**.

6. Na janela Propriedades, certifique-se de que pelo menos uma das propriedades nomeadas **usa** é `true`.

7. No **Gerenciador de soluções** barra de ferramentas, clique em **transformar todos os modelos**.

     Arquivos da subsidiária aparecem abaixo de cada um dos arquivos que você adicionou.

8. Compile e execute a solução para verificar se ele ainda está funcionando.

Sua DSL agora está habilitado para MEF. Você pode gravar comandos de menu, manipuladores de gestos e restrições de validação como extensões MEF. Você pode escrever essas extensões em sua solução DSL, junto com outros códigos personalizados. Além disso, você ou outros desenvolvedores podem escrever extensões do Visual Studio separadas que estendem sua DSL.

## <a name="create-an-extension-for-a-mef-enabled-dsl"></a>Criar uma extensão para uma DSL MEF habilitado

Se você tiver acesso a uma DSL habilitado de MEF, criado por você mesmo ou outra pessoa, você pode escrever extensões para ele. As extensões podem ser usadas para adicionar comandos de menu, manipuladores de gestos ou restrições de validação. Para criar essas extensões, você deve usar uma solução do Visual Studio (VSIX) da extensão. A solução tem duas partes: um projeto de biblioteca de classes que compila o assembly de código e um projeto VSIX que empacota o assembly.

### <a name="to-create-a-dsl-extension-vsix"></a>Para criar uma DSL de extensão VSIX

1. Crie um projeto de **Biblioteca de Classes**.

2. No novo projeto, adicione uma referência ao assembly da DSL.

   - Normalmente, esse assembly tem um nome que termina com ". DSL.dll".

   - Se você tiver acesso ao projeto DSL, você pode encontrar o arquivo do assembly no diretório **Dsl\\bin\\\***

   - Se você tiver acesso ao arquivo VSIX de DSL, você pode encontrar o assembly, alterando a extensão de nome de arquivo do arquivo VSIX para. zip". Descompacte o arquivo. zip.

3. Adicione referências aos assemblies do .NET a seguir:

   - Microsoft.VisualStudio.Modeling.Sdk.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll

   - System.ComponentModel.Composition.dll

   - System.Windows.Forms.dll

4. Criar um novo **projeto VSIX** projeto.

5. Na **Gerenciador de soluções**, clique com botão direito do projeto VSIX e escolha **definir como projeto de inicialização**.

6. No novo projeto, abra **vsixmanifest**.

7. Clique em **adicionar conteúdo**. Na caixa de diálogo, defina **tipo de conteúdo** à **componente MEF**, e **projeto de origem** ao seu projeto de biblioteca de classe.

8. Adicione uma referência VSIX para a DSL.

   1. Na **vsixmanifest**, clique em **adicionar referência**

   2. Na caixa de diálogo, clique em **adicione carga** e, em seguida, localize o arquivo VSIX de DSL. O arquivo VSIX baseia-se na solução de DSL, em **DslPackage\\bin\\\*** .

       Isso permite que os usuários a instalar a DSL e sua extensão ao mesmo tempo. Se o usuário já tiver instalado o DSL, apenas sua extensão será instalada.

9. Revisar e atualizar os outros campos de **vsixmanifest**. Clique em **selecionar edições** e verificar se as edições do Visual Studio corretas estão definidas.

10. Adicione código ao projeto de biblioteca de classes. Use os exemplos na próxima seção como um guia.

     Você pode adicionar qualquer número de comandos, gestos e classes de validação.

11. Para testar a extensão, pressione **F5**. Na instância experimental do Visual Studio, crie ou abra um arquivo de exemplo da DSL.

## <a name="writing-mef-extensions-for-dsls"></a>Gravar extensões de MEF de DSLs

Você pode escrever extensões no projeto de código de assembly de uma solução separada de extensão DSL. Você também pode usar o MEF em seu projeto DslPackage, como uma maneira conveniente de escrever comandos, gestos e código de validação como parte da DSL.

### <a name="menu-commands"></a>Comandos de menu

Para escrever um comando de menu, defina uma classe que implementa <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> e a classe com o atributo que é definido em sua DSL, chamado de prefixo *{1&gt;yourdsl&lt;1*`CommandExtension`. Você pode gravar mais de uma classe de comando de menu.

`QueryStatus()` é chamado sempre que o usuário clica o diagrama. Ele deve inspecionar a seleção atual e definir `command.Enabled` para indicar quando o comando é aplicável.

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

Um manipulador de gesto pode lidar com objetos arrastados para o diagrama em qualquer lugar, dentro ou fora do Visual Studio. O exemplo a seguir permite que o usuário arrastar arquivos do Windows Explorer para o diagrama. Ele cria elementos que contêm os nomes de arquivo.

Você pode escrever manipuladores para lidar com obstáculos de outros modelos DSL e modelos UML. Para obter mais informações, confira [Como: Adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).

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

Métodos de validação são marcados pela `ValidationExtension` atributo que é gerado pela DSL e também pelo <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute>. O método pode aparecer em qualquer classe que não está marcado por um atributo.

Para obter mais informações, consulte [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).

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

## <a name="see-also"></a>Consulte também

- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)
- [MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)
- [Como: Adicionar um manipulador do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)

---
title: Definir restrições de validação para modelos UML | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, validation constraints
ms.assetid: 87b3b0da-122d-4121-9318-200c38ff49d0
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 258fc138f032d34e57df69386b6849fc3a0650a0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547583"
---
# <a name="define-validation-constraints-for-uml-models"></a>Definir restrições de validação para modelos UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir restrições de validação que testam se o modelo atende a uma condição que você especificar. Por exemplo, você pode definir uma restrição para garantir que um usuário não crie um loop de relações de herança. A restrição é invocada quando o usuário tenta abrir ou salvar o modelo e também pode ser invocado manualmente. Se a restrição falhar, uma mensagem de erro que você definir será adicionada à janela de erro. Você pode empacotar essas restrições em uma extensão de integração do Visual Studio ([VSIX](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)) e distribuí-las a outros usuários do Visual Studio.

 Você também pode definir restrições que validam o modelo em relação a recursos externos, como bancos de dados. Se você quiser validar o código do programa em um diagrama de camada, consulte [Adicionar validação de arquitetura personalizada a diagramas de camada](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).

 Para ver quais versões do Visual Studio oferecem suporte a modelos UML, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="requirements"></a>Requisitos
 Consulte [requisitos](../modeling/extend-uml-models-and-diagrams.md#Requirements).

 Para ver quais versões do Visual Studio oferecem suporte a esse recurso, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="applying-validation-constraints"></a>Aplicando restrições de validação
 As restrições de validação são aplicadas em três casos: quando você salva um modelo; Quando você abre um modelo; e ao clicar em **validar modelo UML** no menu **arquitetura** . Em cada caso, somente as restrições que foram definidas para esse caso serão aplicadas, embora normalmente você defina cada restrição a ser aplicada em mais de um caso.

 Os erros de validação são relatados na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela erros e você pode clicar duas vezes no erro para selecionar os elementos do modelo que estão com erro.

 Para obter mais informações sobre como aplicar a validação, consulte [validar seu modelo UML](../modeling/validate-your-uml-model.md).

## <a name="defining-a-validation-extension"></a>Definindo uma extensão de validação
 Para criar uma extensão de validação para um designer UML, você deve criar uma classe que define as restrições de validação e inserir a classe em uma extensão de integração do Visual Studio (VSIX). O VSIX atua como um contêiner que pode instalar a restrição. Há dois métodos alternativos para definir uma extensão de validação:

- **Crie uma extensão de validação em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Use-o se você não quiser combinar suas restrições de validação com outros tipos de extensão, como comandos de menu, itens de caixa de ferramentas personalizados ou manipuladores de gestos. Você pode definir várias restrições em uma classe.

- **Crie projetos de classe de validação e VSIX separados.** Use esse método se desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se o comando de menu espera que o modelo Observe restrições específicas, você pode inseri-lo no mesmo VSIX como um método de validação.

#### <a name="to-create-a-validation-extension-in-its-own-vsix"></a>Para criar uma extensão de validação em seu próprio VSIX

1. Na caixa de diálogo **novo projeto** , em **modelagem de projetos**, selecione **extensão de validação**.

2. Abra o arquivo **. cs** no novo projeto e modifique a classe para implementar sua restrição de validação.

    Para obter mais informações, consulte [avaliando a restrição de validação](#Implementing).

   > [!IMPORTANT]
   > Verifique se os arquivos **. cs** contêm a seguinte `using` instrução:
   >
   >  `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`

3. Você pode adicionar restrições adicionais definindo novos métodos. Para identificar um método como um método de validação, ele deve ser marcado com os atributos da mesma maneira que o método de validação inicial.

4. Teste suas restrições pressionando F5. Para obter mais informações, consulte [executando uma restrição de validação](#Executing).

5. Instale o comando de menu em outro computador copiando o arquivo **bin \\ \* \\ \* . vsix** criado pelo seu projeto. Para obter mais informações, consulte [Instalando e desinstalando uma extensão](#Installing).

   Ao adicionar outros arquivos **. cs** , normalmente você precisará das seguintes `using` instruções:

```csharp
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Uml.Classes;

```

 Este é o procedimento alternativo:

#### <a name="to-create-a-separate-validation-constraint-in-a-class-library-project"></a>Para criar uma restrição de validação separada em um projeto de biblioteca de classes

1. Crie um projeto de biblioteca de classes, adicionando-o a uma solução VSIX existente ou criando uma nova solução.

    1. No menu **Arquivo**, escolha **Novo**, **Projeto**.

    2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**e, em seguida, na coluna do meio, escolha **biblioteca de classes**.

2. A menos que sua solução já contenha uma, crie um projeto VSIX:

    1. No **Gerenciador de soluções**, no menu de atalho da solução, escolha **Adicionar**, **novo projeto**.

    2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**, em seguida, escolha **extensibilidade**. Na coluna do meio, clique em **projeto VSIX**.

3. Defina o projeto VSIX como o projeto de inicialização da solução.

    - No Gerenciador de Soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.

4. Em **Source. Extension. vsixmanifest**, em **Content**, adicione o projeto de biblioteca de classes como um componente MEF:

    1. Na guia **metadados** , defina um nome para o VSIX.

    2. Na guia **instalar destinos** , defina as versões do Visual Studio como os destinos.

    3. Na guia **ativos** , escolha um **novo**e, na caixa de diálogo, defina:

         **Tipo**  =  de **Componente MEF**

         **Origem**  =  do **Um projeto na solução atual**

         **Projeto**  =  do *Seu projeto de biblioteca de classes*

#### <a name="to-define-the-validation-class"></a>Para definir a classe de validação

1. Você não precisará desse procedimento se tiver criado uma classe de validação com seu próprio VSIX do modelo de projeto de validação.

2. No projeto de classe de validação, adicione referências aos seguintes [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] assemblies:

     `Microsoft.VisualStudio.Modeling.Sdk.[version]`

     `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`

     `Microsoft.VisualStudio.Uml.Interfaces`

     `System.ComponentModel.Composition`

3. Adicione um arquivo ao projeto de biblioteca de classes que contém um código semelhante ao exemplo a seguir.

    - Cada restrição de validação está contida em um método marcado com um atributo específico. O método aceita um parâmetro de um tipo de elemento de modelo. Quando a validação é invocada, a estrutura de validação aplica cada método de validação a cada elemento de modelo que está em conformidade com seu tipo de parâmetro.

    - Você pode posicionar esses métodos em quaisquer classes e namespaces. Altere-os para sua preferência.

    ```
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using Microsoft.VisualStudio.Modeling.Validation;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    using Microsoft.VisualStudio.Uml.Classes;
    // You might also need the other Microsoft.VisualStudio.Uml namespaces.

    namespace Validation
    {
      public class MyValidationExtensions
      {
        // SAMPLE VALIDATION METHOD.
        // All validation methods have the following attributes.
        [Export(typeof(System.Action<ValidationContext, object>))]
        [ValidationMethod(
           ValidationCategories.Save
         | ValidationCategories.Open
         | ValidationCategories.Menu)]
        public void ValidateClassNames
          (ValidationContext context,
           // This type determines what elements
           // will be validated by this method:
           IClass elementToValidate)
        {
          // A validation method should not change the model.

          List<string> attributeNames = new List<string>();
          foreach (IProperty attribute in elementToValidate.OwnedAttributes)
          {
            string name = attribute.Name;
            if (!string.IsNullOrEmpty(name) && attributeNames.Contains(name))
            {
              context.LogError(
                string.Format("Duplicate attribute name '{0}' in class {1}", name, elementToValidate.Name),
                "001", elementToValidate);
            }
            attributeNames.Add(name);
          }

        }
        // Add more validation methods for different element types.
      }
    }
    ```

## <a name="executing-a-validation-constraint"></a><a name="Executing"></a>Executando uma restrição de validação
 Para fins de teste, execute seus métodos de validação no modo de depuração.

#### <a name="to-test-the-validation-constraint"></a>Para testar a restrição de validação

1. Pressione **F5**ou, no menu **depurar** , escolha **Iniciar Depuração**.

     Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciada.

     **Solução de problemas**: se um novo não [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Iniciar:

    - Se você tiver mais de um projeto, verifique se o projeto VSIX está definido como o projeto de inicialização da solução.

    - No Gerenciador de Soluções, no menu de atalho do projeto de inicialização ou somente, escolha **Propriedades**. No editor de propriedades do projeto, selecione a guia **depurar** . Verifique se a cadeia de caracteres no campo **Iniciar programa externo** é o nome de caminho completo de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , normalmente:

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem.

3. Para configurar um teste para a restrição de exemplo fornecida na seção anterior:

    1. Abra um diagrama de classe.

    2. Crie uma classe e adicione dois atributos que têm o mesmo nome.

4. No menu de atalho em qualquer lugar do diagrama, escolha **validar**.

5. Todos os erros no modelo serão relatados na janela erros.

6. Clique duas vezes no relatório de erros. Se os elementos mencionados no relatório estiverem visíveis na tela, eles serão realçados.

     **Solução de problemas**: se o comando **validar** não aparecer no menu, verifique se:

    - O projeto de validação é listado como um componente MEF na guia **ativos** em **Source. Extensions. manifest** no projeto VSIX.

    - Os atributos corretos `Export` e `ValidationMethod` são anexados aos métodos de validação.

    - `ValidationCategories.Menu`é incluído no argumento para o `ValidationMethod` atributo e é composto com outros valores usando OR lógico (&#124;).

    - Os parâmetros de todos os `Import` `Export` atributos e são válidos.

## <a name="evaluating-the-constraint"></a><a name="Implementing"></a>Avaliando a restrição
 O método de validação deve determinar se a restrição de validação que você deseja aplicar é true ou false. Se for true, ele não deverá fazer nada. Se for false, ele deverá relatar um erro usando os métodos fornecidos pelo `ValidationContext` parâmetro.

> [!NOTE]
> Os métodos de validação não devem alterar o modelo. Não há nenhuma garantia de quando ou em qual ordem as restrições serão executadas. Se você precisar passar informações entre execuções sucessivas de um método de validação em uma execução de validação, poderá usar o cache de contexto descrito em [coordenação de várias validações](#ContextCache).

 Por exemplo, se você quiser garantir que cada tipo (classe, interface ou enumerador) tenha um nome com pelo menos três caracteres, você pode usar este método:

```
public void ValidateTypeName(ValidationContext context, IType type)
{
  if (!string.IsNullOrEmpty(type.Name) && type.Name.Length < 3)
  {
    context.LogError(
      string.Format("Type name {0} is too short", type.Name),
               "001", type);
   }
 }
```

 Consulte [programação com a API UML](../modeling/programming-with-the-uml-api.md) para obter informações sobre os métodos e tipos que você pode usar para navegar e ler o modelo.

### <a name="about-validation-constraint-methods"></a>Sobre métodos de restrição de validação
 Cada restrição de validação é definida por um método da seguinte forma:

```
[Export(typeof(System.Action<ValidationContext, object>))]
 [ValidationMethod(ValidationCategories.Save
  | ValidationCategories.Menu
  | ValidationCategories.Open)]
public void ValidateSomething
  (ValidationContext context, IClassifier elementToValidate)
{...}
```

 Os atributos e parâmetros de cada método de validação são os seguintes:

|Assinatura|Descrição|
|-|-|
|`[Export(typeof(System.Action <ValidationContext, object>))]`|Define o método como uma restrição de validação usando Managed Extensibility Framework (MEF).|
|`[ValidationMethod (ValidationCategories.Menu)]`|Especifica quando a validação será executada. Use OR-bit ou (&#124;) se desejar combinar mais de uma opção.<br /><br /> `Menu`= invocado pelo menu validar.<br /><br /> `Save`= invocado ao salvar o modelo.<br /><br /> `Open`= invocado ao abrir o modelo. `Load`= invocado ao salvar o modelo, mas para um contravention avisa ao usuário que talvez não seja possível reabrir o modelo. Também chamado no carregamento, antes de o modelo ser analisado.|
|`public void ValidateSomething`<br /><br /> `(ValidationContext context,`<br /><br /> `IElement element)`|Substitua o segundo parâmetro `IElement` pelo tipo de elemento ao qual você deseja aplicar a restrição. O método de restrição será invocado em todos os elementos no tipo especificado.<br /><br /> O nome do método não é importante.|

 Você pode definir quantos métodos de validação desejar, com tipos diferentes no segundo parâmetro. Quando a validação é invocada, cada método de validação será chamado em cada elemento de modelo que esteja de acordo com o tipo de parâmetro.

### <a name="reporting-validation-errors"></a>Erros de validação de relatórios
 Para criar um relatório de erros, use os métodos fornecidos por `ValidationContext` :

 `context.LogError("error string", errorCode, elementsWithError);`

- `"error string"`aparece na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] lista de erros

- `errorCode`é uma cadeia de caracteres que deve ser um identificador exclusivo do erro

- `elementsWithError`identifica elementos no modelo. Quando o usuário clica duas vezes no relatório de erros, a forma que representa esse elemento será selecionada.

  `LogError(),``LogWarning()`e `LogMessage()` Coloque as mensagens em seções diferentes da lista de erros.

## <a name="how-validation-methods-are-applied"></a>Como os métodos de validação são aplicados
 A validação é aplicada a todos os elementos no modelo, incluindo relações e as partes de elementos maiores, como atributos de uma classe e parâmetros de uma operação.

 Cada método de validação é aplicado a cada elemento que está de acordo com o tipo em seu segundo parâmetro. Isso significa que, por exemplo, se você definir um método de validação com um segundo parâmetro de `IUseCase` e outro com seu supertipo `IElement` , então esses dois métodos serão aplicados a cada caso de uso no modelo.

 A hierarquia de tipos é resumida em [tipos de elementos de modelo UML](../modeling/uml-model-element-types.md).

 Você também pode acessar elementos seguindo as relações. Por exemplo, se você definiu um método de validação em `IClass` , poderia executar um loop pelas propriedades de propriedade dele:

```
public void ValidateTypeName(ValidationContext context, IClass c)
{
   foreach (IProperty property in c.OwnedAttributes)
   {
       if (property.Name.Length < 3)
       {
            context.LogError(
                 string.Format(
                        "Property name {0} is too short",
                        property.Name),
                 "001", property);
        }
   }
}
```

### <a name="creating-a-validation-method-on-the-model"></a>Criando um método de validação no modelo
 Se você quiser garantir que um método de validação seja chamado exatamente uma vez durante cada execução de validação, você poderá validar o `IModel` :

```
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs; ...
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{  foreach (IElement element in model.OwnedElements)
   { ...
```

### <a name="validating-shapes-and-diagrams"></a>Validando formas e diagramas
 Os métodos de validação não são invocados em elementos de exibição, como diagramas e formas, porque a principal finalidade dos métodos de validação é validar o modelo. Mas você pode acessar o diagrama atual usando o contexto do diagrama.

 Em sua classe de validação, declare `DiagramContext` como uma propriedade importada:

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
...
[Import]
public IDiagramContext DiagramContext { get; set; }
```

 Em um método de validação, você pode usar `DiagramContext` o para acessar o diagrama de foco atual, se houver:

```
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{
  IDiagram focusDiagram = DiagramContext.CurrentDiagram;
  if (focusDiagram != null)
  {
    foreach (IShape<IUseCase> useCaseShape in
              focusDiagram.GetChildShapes<IUseCase>())
    { ...
```

 Para registrar um erro, você deve obter o elemento de modelo que a forma representa, porque não é possível passar uma forma para `LogError` :

```
IUseCase useCase = useCaseShape.Element;
context.LogError(... , usecase);
```

### <a name="coordinating-multiple-validations"></a><a name="ContextCache"></a>Coordenação de várias validações
 Quando a validação é invocada, por exemplo, pelo usuário de um menu de diagrama, cada método de validação é aplicado a cada elemento de modelo. Isso significa que, em uma única invocação da estrutura de validação, o mesmo método pode ser aplicado muitas vezes a elementos diferentes.

 Isso apresenta um problema para validações que lidam com as relações entre os elementos. Por exemplo, você pode escrever uma validação que começa em, digamos, um caso de uso e percorre as relações de **inclusão** para verificar se não há loops. Mas quando o método é aplicado a cada caso de uso em um modelo que tem muitos links **include** , é provável que ele processe repetidamente as mesmas áreas do modelo.

 Para evitar essa situação, há um cache de contexto no qual as informações são preservadas durante uma execução de validação. Você pode usá-lo para passar informações entre diferentes execuções dos métodos de validação. Por exemplo, você pode armazenar uma lista dos elementos que já foram tratados com a nesta execução de validação. O cache é criado no início de cada execução de validação e não pode ser usado para passar informações entre execuções de validação diferentes.

|Sintaxe|Descrição|
|-|-|
|`context.SetCacheValue<T> (name, value)`|Armazenar um valor|
|`context.TryGetCacheValue<T> (name, out value)`|Obter um valor. Retornará true se for bem-sucedido.|
|`context.GetValue<T>(name)`|Obter um valor.|
|`Context.GetValue<T>()`|Obtém um valor do tipo especificado.|

## <a name="installing-and-uninstalling-an-extension"></a><a name="Installing"></a>Instalando e desinstalando uma extensão
 Você pode instalar uma [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão no seu próprio computador e em outros computadores.

#### <a name="to-install-an-extension"></a>Para instalar uma extensão

1. Em seu computador, localize o arquivo **. vsix** criado por seu projeto VSIX.

    1. No **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **abrir pasta no Windows Explorer**.

    2. Localize o arquivo **bin \\ \* \\ **_seuprojeto_**. vsix**

2. Copie o arquivo **. vsix** para o computador de destino no qual você deseja instalar a extensão. Este pode ser seu próprio computador ou outro.

    - O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou na **origem. Extension. vsixmanifest**.

3. No computador de destino, abra o arquivo **. vsix** .

     O **instalador de extensão do Visual Studio** é aberto e instala a extensão.

4. Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] .

#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão

1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.

2. Expanda **extensões instaladas**.

3. Selecione a extensão e escolha **desinstalar**.

   Raramente, uma extensão defeituosa não carrega e cria um relatório na janela de erro, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo do seguinte local em que *% LocalAppData%* normalmente é *driveName*: \Users \\ *username*\AppData\Local:

   *% LocalAppData%* **\Microsoft\VisualStudio \\ [versão] \Extensions**

## <a name="example"></a><a name="Example"></a>Exemplo
 Este exemplo localiza loops na relação de dependência entre elementos.

 Ele será validado em salvar e no comando de menu validar.

```
/// <summary>
/// Verify that there are no loops in the dependency relationsips.
/// In our project, no element should be a dependent of itself.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">Element to start validation from.</param>
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu
     | ValidationCategories.Save | ValidationCategories.Open)]
public void NoDependencyLoops(ValidationContext context, INamedElement element)
{
    // The validation framework will call this method
    // for every element in the model. But when we follow
    // the dependencies from one element, we will validate others.
    // So we keep a list of the elements that we don't need to validate again.
    // The list is kept in the context cache so that it is passed
    // from one execution of this method to another.
    List<INamedElement> alreadySeen = null;
    if (!context.TryGetCacheValue("No dependency loops", out alreadySeen))
    {
       alreadySeen = new List<INamedElement>();
       context.SetCacheValue("No dependency loops", alreadySeen);
    }

    NoDependencyLoops(context, element,
                new INamedElement[0], alreadySeen);
}

/// <summary>
/// Log an error if there is any loop in the dependency relationship.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">The element to be validated.</param>
/// <param name="dependants">Elements we've followed in this recursion.</param>
/// <param name="alreadySeen">Elements that have already been validated.</param>
/// <returns>true if no error was detected</returns>
private bool NoDependencyLoops(ValidationContext context,
    INamedElement element, INamedElement[] dependants,
    List<INamedElement> alreadySeen)
{
    if (dependants.Contains(element))
    {
        context.LogError(string.Format("{0} should not depend on itself", element.Name),
        "Fabrikam.UML.NoGenLoops", // unique code for this error
        dependants.SkipWhile(e => e != element).ToArray());
            // highlight elements that are in the loop
        return false;
    }
    INamedElement[] dependantsPlusElement =
        new INamedElement[dependants.Length + 1];
    dependants.CopyTo(dependantsPlusElement, 0);
    dependantsPlusElement[dependantsPlusElement.Length - 1] = element;

    if (alreadySeen.Contains(element))
    {
        // We have already validated this when we started
        // from another element during this validation run.
        return true;
    }
    alreadySeen.Add(element);

    foreach (INamedElement supplier in element.GetDependencySuppliers())
    {
        if (!NoDependencyLoops(context, supplier,
             dependantsPlusElement, alreadySeen))
        return false;
    }
    return true;
}
```

## <a name="see-also"></a>Consulte Também
 [Definir e instalar uma programação de extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md) [com a API UML](../modeling/programming-with-the-uml-api.md)

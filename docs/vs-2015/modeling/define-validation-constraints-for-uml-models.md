---
title: Definir restrições de validação para modelos UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, validation constraints
ms.assetid: 87b3b0da-122d-4121-9318-200c38ff49d0
caps.latest.revision: 49
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6647d37636ed0e79d817113e388ae5df23a88a29
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782408"
---
# <a name="define-validation-constraints-for-uml-models"></a>Definir restrições de validação para modelos UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir restrições de validação que testam se o modelo de atende a uma condição que você especificar. Por exemplo, você pode definir uma restrição para certificar-se de que um usuário não cria um loop de relações de herança. A restrição é invocada quando o usuário tenta abrir ou salvar o modelo e também pode ser invocado manualmente. Se a restrição falhar, uma mensagem de erro que você define é adicionada à janela de erro. Você pode empacotar essas restrições em uma extensão de integração do Visual Studio ([VSIX](http://go.microsoft.com/fwlink/?LinkId=160780)) e distribuí-lo para outros usuários do Visual Studio.  
  
 Você também pode definir restrições que validam o modelo em relação aos recursos externos, como bancos de dados. Se você quiser validar o código de programa em um diagrama de camada, consulte [adicionar validação de arquitetura personalizada a diagramas de camada](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).  
  
 Para ver quais versões do Visual Studio dão suporte a modelos UML, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="requirements"></a>Requisitos  
 Ver [requisitos de](../modeling/extend-uml-models-and-diagrams.md#Requirements).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="applying-validation-constraints"></a>Aplicando restrições de validação  
 Restrições de validação são aplicadas em três casos: quando você salvar um modelo; Quando você abre um modelo; e quando você clica em **validar modelo UML** sobre o **arquitetura** menu. Em cada caso, somente as restrições que foram definidas para esse caso serão aplicadas, embora normalmente você defina cada restrição para aplicar mais de um caso.  
  
 Erros de validação são relatados no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela de erros e você pode clicar duas vezes no erro para selecionar os elementos de modelo que estão no erro.  
  
 Para obter mais informações sobre como aplicar a validação, consulte [validar o modelo UML](../modeling/validate-your-uml-model.md).  
  
## <a name="defining-a-validation-extension"></a>Definindo uma extensão de validação  
 Para criar uma extensão de validação para um designer UML, você deve criar uma classe que define as restrições de validação e inserir a classe em um Visual Studio Integration VSIX (extensão). O VSIX atua como um contêiner que pode instalar a restrição. Há dois métodos alternativos de definição de uma extensão de validação:  
  
-   **Crie uma extensão de validação em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Usá-lo se você não deseja combinar suas restrições de validação com outros tipos de extensão, como comandos de menu, itens de caixa de ferramentas personalizada ou manipuladores de gesto. Você pode definir várias restrições em uma classe.  
  
-   **Crie classe separada de validação e projetos VSIX.** Use este método se você desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se seu comando de menu esperar que o modelo observe as restrições específicas, você poderá inseri-lo no mesmo VSIX que um método de validação.  
  
#### <a name="to-create-a-validation-extension-in-its-own-vsix"></a>Para criar uma extensão de validação em seu próprio VSIX  
  
1. No **novo projeto** caixa de diálogo **projetos de modelagem**, selecione **extensão de validação**.  
  
2. Abra o **. CS** de arquivos no novo projeto e modifique a classe para implementar a restrição de validação.  
  
    Para obter mais informações, consulte [avaliando a restrição de validação](#Implementing).  
  
   > [!IMPORTANT]
   >  Certifique-se de que seu **. CS** arquivos contêm o seguinte `using` instrução:  
   >   
   >  `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
3. Você pode adicionar outras restrições definindo novos métodos. Para identificar um método como um método de validação, ele deve ser marcado com os atributos da mesma maneira como o método de validação inicial.  
  
4. Teste suas restrições pressionando F5. Para obter mais informações, consulte [execução de uma restrição de validação](#Executing).  
  
5. Instalar o comando de menu em outro computador copiando o arquivo **bin\\\*\\\*. VSIX** que é compilado pelo seu projeto. Para obter mais informações, consulte [instalando e desinstalando uma extensão](#Installing).  
  
   Quando você adiciona outros **. CS** arquivos, normalmente, você precisará do seguinte `using` instruções:  
  
```csharp  
using System.Collections.Generic;  
using System.ComponentModel.Composition;  
using System.Linq;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.Modeling.Validation;  
using Microsoft.VisualStudio.Uml.Classes;  
  
```  
  
 Aqui está o procedimento alternativo:  
  
#### <a name="to-create-a-separate-validation-constraint-in-a-class-library-project"></a>Para criar uma restrição de validação separada em um projeto de biblioteca de classe  
  
1.  Crie um projeto de biblioteca de classes, adicionando-lo a uma solução existente de VSIX, ou criar uma nova solução.  
  
    1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**e, em seguida, na coluna do meio, escolha **biblioteca de classes**.  
  
2.  A menos que sua solução já contenha um, crie um projeto VSIX:  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho da solução, escolha **Add**, **novo projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, escolha **extensibilidade**. Na coluna do meio, clique em **VSIX Project**.  
  
3.  Defina o projeto VSIX como o projeto de inicialização da solução.  
  
    -   No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.  
  
4.  Na **vsixmanifest**, em **conteúdo**, adicione o projeto de biblioteca de classe como um componente de MEF:  
  
    1.  Sobre o **metadados** guia, defina um nome para o VSIX.  
  
    2.  Sobre o **instalar destinos** guia, defina as versões do Visual Studio como os destinos.  
  
    3.  Sobre o **ativos** guia, escolha um **New**e, na caixa de diálogo, defina:  
  
         **Tipo de** = **componente MEF**  
  
         **Código-fonte** = **um projeto na solução atual**  
  
         **Projeto** = *seu projeto de biblioteca de classes*  
  
#### <a name="to-define-the-validation-class"></a>Para definir a classe de validação  
  
1.  Você não precisará deste procedimento se você tiver criado uma classe de validação com seu próprio VSIX do modelo de projeto de validação.  
  
2.  No projeto de classe de validação, adicione referências para os seguintes [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] assemblies:  
  
     `Microsoft.VisualStudio.Modeling.Sdk.[version]`  
  
     `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`  
  
     `Microsoft.VisualStudio.Uml.Interfaces`  
  
     `System.ComponentModel.Composition`  
  
3.  Adicione um arquivo ao projeto de biblioteca de classes que contém o código que é semelhante ao exemplo a seguir.  
  
    -   Cada restrição de validação está contida dentro de um método marcado com um atributo específico. O método aceita um parâmetro de um tipo de elemento de modelo. Quando a validação é invocada, a estrutura de validação serão aplicadas a cada método de validação para cada elemento de modelo que está de acordo com seu tipo de parâmetro.  
  
    -   Você pode colocar esses métodos em qualquer classe e namespaces. Para alterá-los a sua preferência.  
  
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
  
##  <a name="Executing"></a> Execução de uma restrição de validação  
 Para fins de teste, execute os métodos de validação no modo de depuração.  
  
#### <a name="to-test-the-validation-constraint"></a>Para testar a restrição de validação  
  
1.  Pressione **F5**, ou o **depurar** menu, escolha **iniciar depuração**.  
  
     Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciado.  
  
     **Solução de problemas**: se um novo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não for iniciado:  
  
    -   Se você tiver mais de um projeto, certifique-se de que o projeto do VSIX está definido como o projeto de inicialização da solução.  
  
    -   No Gerenciador de soluções, no menu de atalho da inicialização ou somente projeto, escolha **propriedades**. No editor de propriedades de projeto, selecione a **depurar** guia. Certifique-se de que a cadeia de caracteres na **Iniciar programa externo** campo é o nome do caminho completo do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], normalmente:  
  
         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`  
  
2.  Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem.  
  
3.  Para configurar um teste para a restrição de exemplo fornecida na seção anterior:  
  
    1.  Abra um diagrama de classe.  
  
    2.  Criar uma classe e adicionar dois atributos que têm o mesmo nome.  
  
4.  No menu de atalho em qualquer lugar no diagrama, escolha **validar**.  
  
5.  Quaisquer erros no modelo serão relatados na janela de erros.  
  
6.  Clique duas vezes no relatório de erros. Se os elementos citados no relatório são visíveis na tela, eles serão realçados.  
  
     **Solução de problemas**: se o **Validate** comando não aparecer no menu, verifique se:  
  
    -   O projeto de validação está listado como um componente MEF na **ativos** guia **source.extensions.manifest** no projeto VSIX.  
  
    -   Correto `Export` e `ValidationMethod` atributos são anexados aos métodos de validação.  
  
    -   `ValidationCategories.Menu` está incluído no argumento para o `ValidationMethod` atributo e é composto com outros valores usando o ou lógico (&#124;).  
  
    -   Os parâmetros de todos os `Import` e `Export` atributos são válidos.  
  
##  <a name="Implementing"></a> Avaliando a restrição  
 O método de validação deve determinar se a restrição de validação que você deseja aplicar é true ou false. Se for true, ele deve fazer nada. Se false, ele deve relatar um erro usando os métodos fornecidos pelo `ValidationContext` parâmetro.  
  
> [!NOTE]
>  Métodos de validação não devem alterar o modelo. Não há nenhuma garantia de quando ou em que ordem que as restrições serão executadas. Se você tiver que passar informações entre as execuções sucessivas de um método de validação dentro de uma execução de validação, você pode usar o cache de contexto descrito em [Coordenando várias validações](#ContextCache).  
  
 Por exemplo, se você quiser garantir que todos os tipos (classe, interface ou enumerador) tem um nome que seja pelo menos três caracteres, você pode usar esse método:  
  
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
  
 Ver [Programando com a API UML](../modeling/programming-with-the-uml-api.md) para obter informações sobre os tipos e métodos que você pode usar para navegar e ler o modelo.  
  
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
  
 Os atributos e parâmetros de cada método de validação são da seguinte maneira:  
  
|||  
|-|-|  
|`[Export(typeof(System.Action <ValidationContext, object>))]`|Define o método como uma restrição de validação usando Managed Extensibility Framework (MEF).|  
|`[ValidationMethod (ValidationCategories.Menu)]`|Especifica quando a validação será executada. Uso OR bit a bit (&#124;) se você desejar combinar mais de uma opção.<br /><br /> `Menu` = invocado pelo menu validar.<br /><br /> `Save` = chamado ao salvar o modelo.<br /><br /> `Open` = chamado ao abrir o modelo. `Load` = chamado ao salvar o modelo, mas para uma contravenção avisará o usuário que pode não ser possível reabrir o modelo. Também chamado de carregamento, antes que o modelo é analisado.|  
|`public void ValidateSomething`<br /><br /> `(ValidationContext context,`<br /><br /> `IElement element)`|Substitua o segundo parâmetro `IElement` pelo tipo de elemento ao qual você deseja aplicar a restrição. O método de restrição será invocado em todos os elementos no tipo especificado.<br /><br /> O nome do método é importante.|  
  
 Você pode definir quantos métodos de validação você desejar, com tipos diferentes no segundo parâmetro. Quando a validação é invocada, cada método de validação será chamado em cada elemento de modelo que está de acordo com o tipo de parâmetro.  
  
### <a name="reporting-validation-errors"></a>Relatando erros de validação  
 Para criar um relatório de erros, use os métodos fornecidos pelo `ValidationContext`:  
  
 `context.LogError("error string", errorCode, elementsWithError);`  
  
- `"error string"` aparece no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] lista de erros  
  
- `errorCode` é uma cadeia de caracteres que deve ser um identificador exclusivo do erro  
  
- `elementsWithError` identifica os elementos no modelo. Quando o usuário clica duas vezes no relatório de erros, a forma que representa esse elemento será selecionada.  
  
  `LogError(),` `LogWarning()` e `LogMessage()` colocar mensagens em diferentes seções da lista de erros.  
  
## <a name="how-validation-methods-are-applied"></a>Como os métodos de validação são aplicados  
 A validação é aplicada a todos os elementos no modelo, inclusive relações e as partes dos elementos maiores, como atributos de uma classe e os parâmetros de uma operação.  
  
 Cada método de validação é aplicado a cada elemento que está de acordo com o tipo em seu segundo parâmetro. Isso significa que, por exemplo, se você definir um método de validação com um segundo parâmetro do `IUseCase` e outro com seu supertipo `IElement`, em seguida, ambos os métodos serão aplicados a cada caso de uso no modelo.  
  
 A hierarquia de tipos é resumida na [tipos de elemento de modelo UML](../modeling/uml-model-element-types.md).  
  
 Você também pode acessar elementos seguindo relações. Por exemplo, se você definir um método de validação em `IClass`, você pode executar um loop por meio de propriedades pertencentes:  
  
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
  
### <a name="creating-a-validation-method-on-the-model"></a>Criando um método de validação em um modelo  
 Se você quiser garantir que um método de validação é chamado exatamente uma vez durante cada execução de validação, você pode validar o `IModel`:  
  
```  
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs; ...  
[Export(typeof(System.Action<ValidationContext, object>))]  
[ValidationMethod(ValidationCategories.Menu)]  
public void ValidateModel(ValidationContext context, IModel model)  
{  foreach (IElement element in model.OwnedElements)  
   { ...  
```  
  
### <a name="validating-shapes-and-diagrams"></a>Validando formas e diagramas  
 Métodos de validação não são invocados nos elementos de exibição, como diagramas e formas, como a principal finalidade dos métodos de validação é validar o modelo. Mas você pode acessar o diagrama atual usando o contexto do diagrama.  
  
 Em sua classe de validação, declare `DiagramContext` como uma propriedade importada:  
  
```  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;   
...  
[Import]  
public IDiagramContext DiagramContext { get; set; }  
```  
  
 Em um método de validação, você pode usar `DiagramContext` para acessar o diagrama atual de foco, se houver um:  
  
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
  
 Para registrar em log um erro, você deve obter o elemento de modelo que representa a forma, porque você não pode passar uma forma para `LogError`:  
  
```  
IUseCase useCase = useCaseShape.Element;  
context.LogError(... , usecase);  
```  
  
###  <a name="ContextCache"></a> Coordenando validações múltiplas  
 Quando a validação é invocada, por exemplo pelo usuário de um menu de diagrama, cada método de validação é aplicado a cada elemento de modelo. Isso significa que, em uma única chamada de estrutura de validação, o mesmo método pode ser aplicado várias vezes a diferentes elementos.  
  
 Isso apresenta um problema para validações que lidam com as relações entre elementos. Por exemplo, você pode escrever uma validação que começa em, digamos, um caso de uso e percorre a **incluem** relações para verificar se há loops. Mas quando o método é aplicado a cada caso de uso em um modelo que tem muitas **incluem** links, é provável processar repetidamente as mesmas áreas do modelo.  
  
 Para evitar essa situação, há um cache de contexto no qual as informações são preservadas durante a execução de validação. Você pode usá-lo para passar informações entre execuções diferentes dos métodos de validação. Por exemplo, você pode armazenar uma lista dos elementos que têm já foram manipulados nesta execução de validação. O cache é criado no início de cada execução de validação e não pode ser usado para passar informações entre diferentes execuções de validação.  
  
|||  
|-|-|  
|`context.SetCacheValue<T> (name, value)`|Um valor de Store|  
|`context.TryGetCacheValue<T> (name, out value)`|Obter um valor. Retorna VERDADEIRO se for bem-sucedido.|  
|`context.GetValue<T>(name)`|Obter um valor.|  
|`Context.GetValue<T>()`|Obter um valor do tipo especificado.|  
  
##  <a name="Installing"></a> Instalando e desinstalando uma extensão  
 Você pode instalar um [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão em seu próprio computador e em outros computadores.  
  
#### <a name="to-install-an-extension"></a>Para instalar uma extensão  
  
1.  Em seu computador, localize o **VSIX** arquivo que foi criado pelo seu projeto VSIX.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **Abrir pasta no Windows Explorer**.  
  
    2.  Localize o arquivo **bin\\\*\\**_Seuprojeto_**. VSIX**  
  
2.  Cópia de **. VSIX** arquivo ao computador de destino no qual você deseja instalar a extensão. Isso pode ser seu próprio computador ou outro.  
  
    -   O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou no **vsixmanifest**.  
  
3.  No computador de destino, abra o **VSIX** arquivo.  
  
     **Instalador de extensão do Visual Studio** abre e instala a extensão.  
  
4.  Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão  
  
1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.  
  
2. Expandir **extensões instaladas**.  
  
3. Selecione a extensão e, em seguida, escolha **desinstalação**.  
  
   Raramente, uma extensão defeituosa Falha ao carregar e cria um relatório na janela de erros, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo no seguinte local no qual *% LocalAppData %* é normalmente *DriveName*: \Users\\*denomedeusuário*\AppData\Local:  
  
   *% LocalAppData %* **\Microsoft\VisualStudio\\\Extensions [versão]**  
  
##  <a name="Example"></a> Exemplo  
 Este exemplo localiza loops na relação de dependência entre elementos.  
  
 Validará no e salvar o comando de menu validar.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)




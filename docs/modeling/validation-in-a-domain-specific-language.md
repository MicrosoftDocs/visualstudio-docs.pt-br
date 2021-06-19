---
title: Validação em uma linguagem específica do domínio
description: Saiba como você pode definir restrições de validação para verificar se o modelo criado pelo usuário é significativo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, constraints
- Domain-Specific Language, validation
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6de3a8940c845b29d2d0c7454b7c585f4676dba0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388328"
---
# <a name="validation-in-a-domain-specific-language"></a>Validação em uma linguagem específica do domínio
Como o autor de uma linguagem específica de domínio (DSL), você pode definir restrições de validação para verificar se o modelo criado pelo usuário é significativo. Por exemplo, se a sua DSL permite que os usuários desenhem uma árvore genealógica das pessoas e os seus ancestrais, você pode escrever uma restrição que garanta que os filhos tenham datas de nascimento posteriores as dos seus pais.

 Você pode fazer com que as restrições de validação sejam executadas quando o modelo é salvo, quando ele é aberto e quando o usuário executa explicitamente o comando **de** menu Validar. Você também pode executar a validação no controle do programa. Por exemplo, você pode executar a validação em resposta à alteração de um valor de propriedade ou relação.

 A validação é particularmente importante se você estiver escrevendo modelos de texto ou outras ferramentas que processam os modelos dos usuários. A validação assegura que os modelos atendam as pré-condições presumidas por essas ferramentas.

> [!WARNING]
> Você também pode permitir que restrições de validação sejam definidas em extensões separadas para a sua DSL, com os comandos de menu e manipuladores de gestos de extensão. Os usuários podem optar por instalar essas extensões além da sua DSL. Para obter mais informações, [consulte Estender sua DSL usando MEF](../modeling/extend-your-dsl-by-using-mef.md).

## <a name="running-validation"></a>Executando a validação
 Quando um usuário está editando um modelo, ou seja, uma instância da sua linguagem específica de domínio, as seguintes ações podem executar a validação:

- Clique com o botão direito do mouse no diagrama e **selecione Validar Tudo.**

- Clique com o botão direito do mouse no nó superior no Explorer da sua DSL e selecione **Validar Tudo**

- Salve o modelo.

- Abra o modelo.

- Além disso, você pode escrever o código do programa que executada a validação, por exemplo, como parte de um comando de menu ou em resposta a uma alteração.

  Todos os erros de validação serão exibidos na janela **Lista de** Erros. O usuário pode clicar duas vezes em uma mensagem de erro para selecionar os elementos do modelo que são a causa do erro.

## <a name="defining-validation-constraints"></a>Definindo restrições de validação
 Você define restrições de validação adicionando métodos de validação às classes ou relações de domínio da sua DSL. Quando a validação é executada pelo usuário ou sob o controle do programa, alguns ou todos os métodos de validação são executados. Cada método é aplicado a cada instância de sua classe, não pode haver vários métodos de validação em cada classe.

 Cada método de validação relata os erros que encontra.

> [!NOTE]
> Os métodos de validação relatam erros, mas não alteram o modelo. Se você quiser ajustar ou impedir determinadas alterações, consulte [Alternativas à validação](#alternatives).

#### <a name="to-define-a-validation-constraint"></a>Para definir uma restrição de validação

1. Habilita a **validação no nó Editor\Validação:**

   1. Abra **Dsl\DslDefinition.dsl**.

   2. No DSL Explorer, expanda o **nó Editor** e selecione **Validação**.

   3. No janela Propriedades, de definir as **propriedades Usa**  como `true` . Esse é o modo mais conveniente de definir todas essas propriedades.

   4. Clique **em Transformar Todos os Modelos** na barra **Gerenciador de Soluções** ferramentas.

2. Escreva definições de classe parciais para uma ou mais de suas classes de domínio ou relações de domínio. Escreva essas definições em um novo arquivo de código no **projeto Dsl.**

3. Prefixe cada classe com este atributo:

   ```csharp
   [ValidationState(ValidationState.Enabled)]
   ```

   - Por padrão, esse atributo também permite a validação de classes derivadas. Se você deseja desabilitar a validação para uma classe derivada específica, use `ValidationState.Disabled`.

4. Adicione métodos de validação às classes. Cada método de validação pode ter qualquer nome, mas tem um parâmetro do tipo <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationContext>.

    Ele deve ser prefixado com um ou mais atributos `ValidationMethod`:

   ```csharp
   [ValidationMethod (ValidationCategories.Open | ValidationCategories.Save | ValidationCategories.Menu ) ]
   ```

    Os ValidationCategories especificam quando o método é executado.

   Por exemplo:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;

// Allow validation methods in this class:
[ValidationState(ValidationState.Enabled)]
// In this DSL, ParentsHaveChildren is a domain relationship
// from Person to Person:
public partial class ParentsHaveChildren
{
  // Identify the method as a validation method:
  [ValidationMethod
  ( // Specify which events cause the method to be invoked:
    ValidationCategories.Open // On file load.
  | ValidationCategories.Save // On save to file.
  | ValidationCategories.Menu // On user menu command.
  )]
  // This method is applied to each instance of the
  // type (and its subtypes) in a model:
  private void ValidateParentBirth(ValidationContext context)
  {
    // In this DSL, the role names of this relationship
    // are "Child" and "Parent":
     if (this.Child.BirthYear < this.Parent.BirthYear
        // Allow user to leave the year unset:
        && this.Child.BirthYear != 0)
      {
        context.LogError(
             // Description:
                       "Child must be born after Parent",
             // Unique code for this error:
                       "FAB001ParentBirthError",
              // Objects to select when user double-clicks error:
                       this.Child,
                       this.Parent);
    }
  }
```

 Observe os seguintes pontos sobre esse código:

- Você pode adicionar métodos de validação às classes de domínio ou relações de domínio. O código para esses tipos está **em Dsl\Generated Code\Domain \* .cs**.

- Cada método de validação é aplicado a todas as instâncias de sua classe e suas subclasses. No caso de uma relação de domínio, cada instância é um link entre dois elementos de modelo.

- Métodos de validação não são aplicados em ordem específica e cada método não é aplicado às instâncias da sua classe em ordem previsível.

- Geralmente, não é uma boa prática um método de validação atualizar o conteúdo do repositório, porque isso levaria a resultados inconsistentes. Em vez disso, o método deve relatar qualquer erro chamando `context.LogError`, `LogWarning` ou `LogInfo`.

- Na chamada LogError, você pode fornecer uma lista de elementos de modelo ou links de relações que serão selecionados quando o usuário clicar duas vezes na mensagem de erro.

- Para obter informações sobre como ler o modelo no código do programa, consulte Navegando e atualizando um [modelo no código do programa.](../modeling/navigating-and-updating-a-model-in-program-code.md)

  O exemplo aplica-se ao seguinte modelo de domínio. A relação ParentsHaveChildren tem funções que são nomeadas Child e Parent.

  ![Diagrama de definição de DSL &#45; de árvore de família](../modeling/media/familyt_person.png)

## <a name="validation-categories"></a>Categorias de validação
 No atributo <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute>, você especifica quando o método de validação deve ser executado.

|Categoria|Execução|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|Quando o usuário chama o comando de menu Validar.|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|Quando o arquivo de modelo é aberto.|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|Quando o arquivo é salvo. Se houver erros de validação, o usuário terá a opção de cancelar a operação de salvamento.|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|Quando o arquivo é salvo. Se houver erros de métodos nesta categoria, o usuário é avisado que pode não ser possível abrir o arquivo novamente.<br /><br /> Use essa categoria para métodos de validação que testem nomes duplicados ou IDs, ou outras condições que possam causar erros de carregamento.|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|Quando o método ValidateCustom é chamado. Validações nessa categoria podem ser invocadas somente a partir do código do programa.<br /><br /> Para obter mais informações, consulte [Categorias de validação personalizadas.](#custom)|

## <a name="where-to-place-validation-methods"></a>Onde colocar métodos de validação
 Normalmente, você pode conseguir o mesmo efeito colocando um método de validação em um tipo diferente. Por exemplo, você pode adicionar um método à classe Person, em vez da relação ParentsHaveChildren, e fazê-la iterar nos links:

```
[ValidationState(ValidationState.Enabled)]
public partial class Person
{[ValidationMethod
 ( ValidationCategories.Open
 | ValidationCategories.Save
 | ValidationCategories.Menu
 )
]
  private void ValidateParentBirth(ValidationContext context)
  {
    // Iterate through ParentHasChildren links:
    foreach (Person parent in this.Parents)
    {
        if (this.BirthYear <= parent.BirthYear)
        { ...
```

 **Agregando restrições de validação.**  Para aplicar validação em uma ordem previsível, defina um único método de validação em uma classe de proprietário, o elemento raiz do seu modelo. Essa técnica também permite agregar vários relatórios de erros em uma única mensagem.

 As desvantagens são que o método combinado é menos fácil de gerenciar e que todas as restrições devem ter as mesmas `ValidationCategories`. Por isso, recomendamos que você mantenha cada restrição em um método separado, se possível.

 **Passando valores no cache de contexto.**  O parâmetro de contexto tem um dicionário no qual você pode colocar valores arbitrários. O dicionário persiste durante a duração da execução da validação. Um método de validação específico pode, por exemplo, manter uma contagem de erros no contexto e usá-la para evitar sobrecarregar a janela de erro com mensagens repetidas. Por exemplo:

```csharp
List<ParentsHaveChildren> erroneousLinks;
if (!context.TryGetCacheValue("erroneousLinks", out erroneousLinks))
erroneousLinks = new List<ParentsHaveChildren>();
erroneousLinks.Add(this);
context.SetCacheValue("erroneousLinks", erroneousLinks);
if (erroneousLinks.Count < 5) { context.LogError( ... ); }
```

## <a name="validation-of-multiplicities"></a>Validação de multiplicidades
 Métodos de validação para verificar a multiplicidade mínima são gerados automaticamente para a sua DSL. O código é gravado **em Dsl\Generated Code\MultiplicityValidation.cs.** Esses métodos entrarão em vigor quando você habilitar a validação no **nó Editor\Validação** no DSL Explorer.

 Se você definir que a multiplicidade de uma função de uma relação de domínio como 1..* ou 1..1, mas o usuário não criar um link dessa relação, uma mensagem de erro de validação aparecerá.

 Por exemplo, se sua DSL tiver classes Person e Town e uma relação PersonLivesInLivesInLive com uma relação **1.. \\** * na função Cidade e, para cada Pessoa que não tem cidade, uma mensagem de erro será exibida.

## <a name="running-validation-from-program-code"></a>Executando a validação a partir do código do programa
 Você pode executar a validação acessando ou criando um ValidationController. Se você quiser que os erros sejam exibidos ao usuário na janela de erro, use o ValidationController anexado ao DocData do diagrama. Por exemplo, se você estiver escrevendo um comando de menu, `CurrentDocData.ValidationController` está disponível na classe de conjunto de comandos:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
partial class MyLanguageCommandSet
{
  private void OnMenuMyContextMenuCommand(object sender, EventArgs e)
  {
   ValidationController controller = this.CurrentDocData.ValidationController;
...
```

 Para obter mais informações, [consulte Como adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

 Você também pode criar um controlador de validação independente e gerenciar os erros. Por exemplo:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
Store store = ...;
VsValidationController validator = new VsValidationController(s);
// Validate all elements in the Store:
if (!validator.Validate(store, ValidationCategories.Save))
{
  // Deal with errors:
  foreach (ValidationMessage message in validator.ValidationMessages) { ... }
}
```

## <a name="running-validation-when-a-change-occurs"></a>Executando a validação quando ocorre uma alteração
 Se você deseja garantir que o usuário seja avisado imediatamente quando o modelo se tornar inválido, defina um evento de armazenamento que execute a validação. Para obter mais informações sobre eventos de armazenamento, consulte [Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

 Além do código de validação, adicione um arquivo de código personalizado ao seu **projeto DslPackage,** com conteúdo semelhante ao exemplo a seguir. Esse código usa o `ValidationController` que é anexado ao documento. Esse controlador exibe os erros de validação na lista Visual Studio erros.

```csharp
using System;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
namespace Company.FamilyTree
{
  partial class FamilyTreeDocData // Change name to your DocData.
  {
    // Register the store event handler:
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded();
      DomainClassInfo observedLinkInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(ParentsHaveChildren));
      DomainClassInfo observedClassInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(Person));
      EventManagerDirectory events = this.Store.EventManagerDirectory;
      events.ElementAdded
         .Add(observedLinkInfo, new EventHandler<ElementAddedEventArgs>(ParentLinkAddedHandler));
      events.ElementDeleted.Add(observedLinkInfo, new EventHandler<ElementDeletedEventArgs>(ParentLinkDeletedHandler));
      events.ElementPropertyChanged.Add(observedClassInfo, new EventHandler<ElementPropertyChangedEventArgs>(BirthDateChangedHandler));
    }
    // Handler will be called after transaction that creates a link:
    private void ParentLinkAddedHandler(object sender,
                                ElementAddedEventArgs e)
    {
      this.ValidationController.Validate(e.ModelElement,
           ValidationCategories.Save);
    }
    // Called when a link is deleted:
    private void ParentLinkDeletedHandler(object sender,
                                ElementDeletedEventArgs e)
    {
      // Don't apply validation to a deleted item!
      // - Validate store to refresh the error list.
      this.ValidationController.Validate(this.Store,
           ValidationCategories.Save);
    }
    // Called when any property of a Person element changes:
    private void BirthDateChangedHandler(object sender,
                      ElementPropertyChangedEventArgs e)
    {
      Person person = e.ModelElement as Person;
      // Not interested in changes in other properties:
      if (e.DomainProperty.Id != Person.BirthYearDomainPropertyId)
          return;

      // Validate all parent links to and from the person:
      this.ValidationController.Validate(
        ParentsHaveChildren.GetLinksToParents(person)
        .Concat(ParentsHaveChildren.GetLinksToChildren(person))
        , ValidationCategories.Save);
    }
  }
}
```

 Os manipuladores também são chamados depois de operações Undo ou Redo que afetam os links ou elementos.

## <a name="custom-validation-categories"></a><a name="custom"></a> Categorias de validação personalizadas
 Além das categorias de validação padrão, como Menu e Open, você pode definir suas próprias categorias. Você pode invocar essas categorias do código do programa. O usuário não pode invocá-las diretamente.

 Um uso típico de categorias personalizadas é definir uma categoria que teste se o modelo satisfaz as pré-condições de uma ferramenta específica.

 Para adicionar um método de validação à uma categoria específica, prefixe-o com um atributo como este:

```csharp
[ValidationMethod(CustomCategory = "PreconditionsForGeneratePartsList")]
[ValidationMethod(ValidationCategory.Menu)]
private void TestForCircularLinks(ValidationContext context)
{...}
```

> [!NOTE]
> Você pode prefixar um método com a quantidade de atributos `[ValidationMethod()]` você desejar. Você pode adicionar um método a categorias personalizadas e padrão.

 Para invocar a validação personalizada:

```csharp

// Invoke all validation methods in a custom category:
validationController.ValidateCustom
  (store, // or a list of model elements
   "PreconditionsForGeneratePartsList");
```

## <a name="alternatives-to-validation"></a><a name="alternatives"></a> Alternativas à validação
 As restrições de validação relatam erros, mas não alteram o modelo. Se, ao contrário, você deseja evitar que o modelo se torne inválido, você pode usar outras técnicas.

 No entanto, essas técnicas não são recomendadas. Normalmente, é melhor deixar que o usuário decida como corrigir um modelo inválido.

 **Ajuste a alteração para restaurar o modelo para validade.**  Por exemplo, se o usuário definir uma propriedade acima do valor máximo permitido, você pode redefinir a propriedade para o valor máximo. Para fazer isso, defina uma regra. Para obter mais informações, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

 **Reverta a transação, no caso de uma tentativa de alteração inválida.** Você também pode definir uma regra para essa finalidade, mas, em alguns casos, é possível substituir um manipulador de propriedades **OnValueChanging()** ou substituir um método como Para reverter uma transação, use Para obter mais informações, consulte Manipuladores de alteração de valor da propriedade de domínio `OnDeleted().` `this.Store.TransactionManager.CurrentTransaction.Rollback().` [](../modeling/domain-property-value-change-handlers.md).

> [!WARNING]
> Verifique se o usuário sabe que a alteração foi ajustada ou revertida. Por exemplo, use `System.Windows.Forms.MessageBox.Show("message").`

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md)

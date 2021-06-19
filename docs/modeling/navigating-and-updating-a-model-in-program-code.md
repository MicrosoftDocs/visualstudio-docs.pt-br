---
title: Navegando e atualizando um modelo no código do programa
description: Saiba como você pode escrever código para criar e excluir elementos de modelo, definir suas propriedades e criar e excluir links entre elementos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: be19b34c51744c6bab1c6021a006f7ec9b4da0f4
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390965"
---
# <a name="navigate-and-update-a-model-in-program-code"></a>Navegar e atualizar um modelo no código do programa

Você pode escrever código para criar e excluir elementos de modelo, definir suas propriedades e criar e excluir links entre elementos. Todas as alterações devem ser feitas em uma transação. Se os elementos forem exibidos em um diagrama, o diagrama será "corrigido" automaticamente no final da transação.

## <a name="an-example-dsl-definition"></a><a name="example"></a> Um exemplo de definição de DSL
 Essa é a parte principal do DslDefinition. DSL para os exemplos neste tópico:

 ![Diagrama de definição de DSL &#45; modelo de árvore da família](../modeling/media/familyt_person.png)

 Este modelo é uma instância desta DSL:

 ![Modelo de árvore da família Tudor](../modeling/media/tudor_familytreemodel.png)

### <a name="references-and-namespaces"></a>Referências e namespaces
 Para executar o código neste tópico, você deve fazer referência a:

 `Microsoft.VisualStudio.Modeling.Sdk.11.0.dll`

 Seu código usará este namespace:

 `using Microsoft.VisualStudio.Modeling;`

 Além disso, se você estiver gravando o código em um projeto diferente daquele em que seu DSL está definido, você deverá importar o assembly criado pelo projeto DSL.

## <a name="navigating-the-model"></a><a name="navigation"></a> Navegando no modelo

### <a name="properties"></a>Propriedades
 As propriedades de domínio definidas na definição de DSL se tornam propriedades que você pode acessar no código do programa:

 `Person henry = ...;`

 `if (henry.BirthDate < 1500) ...`

 `if (henry.Name.EndsWith("VIII")) ...`

 Se você quiser definir uma propriedade, deverá fazer isso dentro de uma [transação](#transaction):

 `henry.Name = "Henry VIII";`

 Se estiver na definição de DSL, o **tipo** de uma propriedade será **calculado**, você não poderá defini-la. Para obter mais informações, consulte [Propriedades de armazenamento calculadas e personalizadas](../modeling/calculated-and-custom-storage-properties.md).

### <a name="relationships"></a>Relações
 As relações de domínio que você define na definição de DSL se tornam pares de propriedades, uma na classe em cada extremidade da relação. Os nomes das propriedades aparecem no diagrama DslDefinition como rótulos nas funções em cada lado da relação. Dependendo da multiplicidade da função, o tipo da propriedade é a classe na outra extremidade da relação, ou uma coleção dessa classe...

 `foreach (Person child in henry.Children) { ... }`

 `FamilyTreeModel ftree = henry.FamilyTreeModel;`

 As propriedades em extremidades opostas de uma relação são sempre recíprocas. Quando um link é criado ou excluído, as propriedades de função em ambos os elementos são atualizadas. A expressão a seguir (que usa as extensões de `System.Linq` ) é sempre verdadeira para a relação ParentsHaveChildren no exemplo:

 `(Person p) => p.Children.All(child => child.Parents.Contains(p))`

 `&& p.Parents.All(parent => parent.Children.Contains(p));`

 **ElementLinks**. Uma relação também é representada por um elemento de modelo chamado de *link*, que é uma instância do tipo de relação de domínio. Um link sempre tem um elemento de origem e um elemento de destino. O elemento de origem e o elemento de destino podem ser iguais.

 Você pode acessar um link e suas propriedades:

 `ParentsHaveChildren link = ParentsHaveChildren.GetLink(henry, edward);`

 `// This is now true:`

 `link == null || link.Parent == henry && link.Child == edward`

 Por padrão, não é permitido que mais de uma instância de uma relação vincule qualquer par de elementos de modelo. Mas se, na definição de DSL, o `Allow Duplicates` sinalizador for verdadeiro para a relação, poderá haver mais de um link e você deverá usar `GetLinks` :

 `foreach (ParentsHaveChildren link in ParentsHaveChildren.GetLinks(henry, edward)) { ... }`

 Também há outros métodos para acessar links. Por exemplo:

 `foreach (ParentsHaveChildren link in     ParentsHaveChildren.GetLinksToChildren(henry)) { ... }`

 **Funções ocultas.** Se, na definição de DSL, a **Propriedade gerada** for **false** para uma função específica, nenhuma propriedade será gerada que corresponda a essa função. No entanto, você ainda pode acessar os links e percorrer os links usando os métodos da relação:

 `foreach (Person p in ParentsHaveChildren.GetChildren(henry)) { ... }`

 O exemplo usado com mais frequência é a <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação, que vincula um elemento de modelo à forma que o exibe em um diagrama:

 `PresentationViewsSubject.GetPresentation(henry)[0] as PersonShape`

### <a name="the-element-directory"></a>O diretório do elemento
 Você pode acessar todos os elementos no repositório usando o diretório do elemento:

 `store.ElementDirectory.AllElements`

 Também há métodos para localizar elementos, como o seguinte:

 `store.ElementDirectory.FindElements(Person.DomainClassId);`

 `store.ElementDirectory.GetElement(elementId);`

## <a name="accessing-class-information"></a><a name="metadata"></a> Acessando informações de classe
 Você pode obter informações sobre as classes, relações e outros aspectos da definição de DSL. Por exemplo:

 `DomainClassInfo personClass = henry.GetDomainClass();`

 `DomainPropertyInfo birthProperty =`

 `personClass.FindDomainProperty("BirthDate")`

 `DomainRelationshipInfo relationship =`

 `link.GetDomainRelationship();`

 `DomainRoleInfo sourceRole = relationship.DomainRole[0];`

 As classes ancestrals dos elementos de modelo são as seguintes:

- ModelElement-todos os elementos e relações são ModelElements

- ElementLink-todas as relações são ElementLinks

## <a name="perform-changes-inside-a-transaction"></a><a name="transaction"></a> Executar alterações dentro de uma transação
 Sempre que o código do programa altera qualquer coisa na loja, ele deve fazer isso dentro de uma transação. Isso se aplica a todos os elementos de modelo, relações, formas, diagramas e suas propriedades. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Modeling.Transaction>.

 O método mais conveniente de gerenciar uma transação é com uma `using` instrução colocada em uma `try...catch` instrução:

```
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 Você pode fazer qualquer número de alterações dentro de uma transação. Você pode abrir novas transações dentro de uma transação ativa.

 Para tornar as alterações permanentes, você deve fazer `Commit` a transação antes que ela seja descartada. Se ocorrer uma exceção que não é detectada dentro da transação, o repositório será redefinido para seu estado antes das alterações.

## <a name="creating-model-elements"></a><a name="elements"></a> Criando elementos de modelo
 Este exemplo adiciona um elemento a um modelo existente:

```csharp
FamilyTreeModel familyTree = ...; // The root of the model.
using (Transaction t =
    familyTree.Store.TransactionManager
    .BeginTransaction("update model"))
{
  // Create a new model element
  // in the same partition as the model root:
  Person edward = new Person(familyTree.Partition);
  // Set its embedding relationship:
  edward.FamilyTreeModel = familyTree;
          // same as: familyTree.People.Add(edward);
  // Set its properties:
  edward.Name = "Edward VII";
  t.Commit(); // Don't forget this!
}
```

 Este exemplo ilustra esses pontos essenciais sobre a criação de um elemento:

- Crie o novo elemento em uma partição específica do armazenamento. Para elementos de modelo e relações, mas não formas, essa é geralmente a partição padrão.

- Torne-o o destino de uma relação incorporada. No DslDefinition deste exemplo, cada pessoa deve ser o destino da relação incorporada FamilyTreeHasPeople. Para fazer isso, podemos definir a propriedade de função FamilyTreeModel do objeto Person ou adicionar a pessoa à propriedade de função People do objeto FamilyTreeModel.

- Defina as propriedades de um novo elemento, especialmente a propriedade para a qual `IsName` é verdadeira no DslDefinition. Esse sinalizador marca a propriedade que serve para identificar o elemento exclusivamente dentro de seu proprietário. Nesse caso, a propriedade Name tem esse sinalizador.

- A definição de DSL dessa DSL deve ter sido carregada no repositório. Se você estiver escrevendo uma extensão como um comando de menu, isso normalmente já será verdadeiro. Em outros casos, você pode carregar explicitamente o modelo na loja ou usar [ModelBus](/previous-versions/ee904639(v=vs.140)) para carregá-lo. Para obter mais informações, consulte [como: abrir um modelo do arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md).

  Quando você cria um elemento dessa forma, uma forma é criada automaticamente (se a DSL tiver um diagrama). Ele aparece em um local atribuído automaticamente, com forma padrão, cor e outros recursos. Se você quiser controlar onde e como a forma associada é exibida, consulte [criando um elemento e sua forma](#merge).

## <a name="creating-relationship-links"></a><a name="links"></a> Criando links de relacionamento
 Há duas relações definidas na definição de DSL de exemplo. Cada relação define uma *propriedade de função* na classe em cada extremidade da relação.

 Há três maneiras pelas quais você pode criar uma instância de uma relação. Cada um desses três métodos tem o mesmo efeito:

- Defina a propriedade do representante da função de origem. Por exemplo:

  - `familyTree.People.Add(edward);`

  - `edward.Parents.Add(henry);`

- Defina a propriedade do representante da função de destino. Por exemplo:

  - `edward.familyTreeModel = familyTree;`

       A multiplicidade dessa função é `1..1` , portanto, atribuímos o valor.

  - `henry.Children.Add(edward);`

       A multiplicidade dessa função é `0..*` , portanto, adicionamos à coleção.

- Construa uma instância da relação explicitamente. Por exemplo:

  - `FamilyTreeHasPeople edwardLink = new FamilyTreeHasPeople(familyTreeModel, edward);`

  - `ParentsHaveChildren edwardHenryLink = new ParentsHaveChildren(henry, edward);`

  O último método será útil se você quiser definir propriedades na própria relação.

  Quando você cria um elemento dessa forma, um conector no diagrama é criado automaticamente, mas tem uma forma padrão, cor e outros recursos. Para controlar como o conector associado é criado, consulte [criando um elemento e sua forma](#merge).

## <a name="deleting-elements"></a><a name="deleteelements"></a> Excluindo elementos

Exclua um elemento chamando `Delete()` :

`henry.Delete();`

Esta operação também será excluída:

- Os links de relação de e para o elemento. Por exemplo, `edward.Parents` não conterá mais `henry` .

- Elementos em funções para os quais o `PropagatesDelete` sinalizador é verdadeiro. Por exemplo, a forma que exibe o elemento será excluída.

Por padrão, cada relação de incorporação tem `PropagatesDelete` true na função de destino. A `henry` exclusão não exclui `familyTree` o , mas exclui todos os `familyTree.Delete()` `Persons` .

Por padrão, `PropagatesDelete` não é verdadeiro para as funções de relações de referência.

Você pode fazer com que as regras de exclusão omitam propagações específicas ao excluir um objeto. Isso será útil se você estiver substituindo um elemento por outro. Você fornece o GUID de uma ou mais funções para as quais a exclusão não deve ser propagada. O GUID pode ser obtido da classe de relação:

`henry.Delete(ParentsHaveChildren.SourceDomainRoleId);`

(Este exemplo específico não teria nenhum efeito, porque `PropagatesDelete` é para as funções da `false` `ParentsHaveChildren` relação.)

Em alguns casos, a exclusão é impedida pela existência de um bloqueio, seja no elemento ou em um elemento que seria excluído pela propagação. Você pode usar `element.CanDelete()` para verificar se o elemento pode ser excluído.

## <a name="deleting-relationship-links"></a><a name="deletelinks"></a> Excluindo links de relação
 Você pode excluir um link de relação removendo um elemento de uma propriedade de função:

 `henry.Children.Remove(edward); // or:`

 `edward.Parents.Remove(henry);  // or:`

 Você também pode excluir o link explicitamente:

 `edwardHenryLink.Delete();`

 Todos esses três métodos têm o mesmo efeito. Você só precisa usar um deles.

 Se a função tiver multiplicidade 0..1 ou 1...1, você poderá defini-la como `null` ou para outro valor:

 `edward.FamilyTreeModel = null;` Ou:

 `edward.FamilyTreeModel = anotherFamilyTree;`

## <a name="re-ordering-the-links-of-a-relationship"></a><a name="reorder"></a> Re-ordenando os links de uma relação
 Os links de uma relação específica que são de origem ou direcionados a um elemento de modelo específico têm uma sequência específica. Eles aparecem na ordem em que foram adicionados. Por exemplo, essa instrução sempre produzirá os filhos na mesma ordem:

 `foreach (Person child in henry.Children) ...`

 Você pode alterar a ordem dos links:

 `ParentsHaveChildren link = GetLink(henry,edward);`

 `ParentsHaveChildren nextLink = GetLink(henry, elizabeth);`

 `DomainRoleInfo role =`

 `link.GetDomainRelationship().DomainRoles[0];`

 `link.MoveBefore(role, nextLink);`

## <a name="locks"></a><a name="locks"></a> Fechaduras
 Suas alterações podem ser impedidas por um bloqueio. Os bloqueios podem ser definidos em elementos individuais, em partições e no armazenamento. Se qualquer um desses níveis tiver um bloqueio que impeça o tipo de alteração que você deseja fazer, uma exceção poderá ser lançada quando você tentar. Você pode descobrir se os bloqueios são definidos usando o elemento . GetLocks(), que é um método de extensão definido no namespace <xref:Microsoft.VisualStudio.Modeling.Immutability> .

 Para obter mais informações, [consulte Definindo uma política de bloqueio para criar Read-Only segmentos](../modeling/defining-a-locking-policy-to-create-read-only-segments.md).

## <a name="copy-and-paste"></a><a name="copy"></a> Copiar e colar
 Você pode copiar elementos ou grupos de elementos para um <xref:System.Windows.Forms.IDataObject> :

```csharp
Person person = personShape.ModelElement as Person;
Person adopter = adopterShape.ModelElement as Person;
IDataObject data = new DataObject();
personShape.Diagram.ElementOperations
      .Copy(data, person.Children.ToList<ModelElement>());
```

 Os elementos são armazenados como um grupo de elementos serializado.

 Você pode mesclar elementos de um IDataObject em um modelo:

```csharp
using (Transaction t = targetDiagram.Store.
        TransactionManager.BeginTransaction("paste"))
{
  adopterShape.Diagram.ElementOperations.Merge(adopter, data);
}
```

 `Merge ()` pode aceitar um `PresentationElement` ou um `ModelElement` . Se você der a ele `PresentationElement` um , também poderá especificar uma posição no diagrama de destino como um terceiro parâmetro.

## <a name="navigating-and-updating-diagrams"></a><a name="diagrams"></a> Navegando e atualizando diagramas
 Em uma DSL, o elemento de modelo de domínio, que representa um conceito como Person ou Song, é separado do elemento de forma, que representa o que você vê no diagrama. O elemento de modelo de domínio armazena as propriedades e relações importantes dos conceitos. O elemento de forma armazena o tamanho, a posição e a cor da exibição do objeto no diagrama e o layout de suas partes de componente.

### <a name="presentation-elements"></a>Elementos de apresentação
 ![Diagrama de classe de tipos de elemento e forma base](../modeling/media/dslshapesandelements.png)

 Em sua Definição de DSL, cada elemento especificado cria uma classe derivada de uma das classes padrão a seguir.

|Tipo de elemento|Classe base|
|-|-|
|Classe de domínio|<xref:Microsoft.VisualStudio.Modeling.ModelElement>|
|Relação de domínio|<xref:Microsoft.VisualStudio.Modeling.ElementLink>|
|Forma|<xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>|
|Connector|<xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>|
|Diagrama|<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>|

 Um elemento em um diagrama geralmente representa um elemento de modelo. Normalmente (mas nem sempre), um <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape> representa uma instância de classe de domínio e um representa uma instância de relação de <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape> domínio. A <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação vincula um nó ou forma de link ao elemento de modelo que ele representa.

 Cada forma de nó ou link pertence a um diagrama. Uma forma de link binário conecta duas formas de nó.

 As formas podem ter formas filho em dois conjuntos. Uma forma no `NestedChildShapes` conjunto é limitada à caixa delimitada de seu pai. Uma forma na lista pode aparecer fora ou parcialmente fora dos limites do pai, por exemplo, um `RelativeChildShapes` rótulo ou uma porta. Um diagrama não tem `RelativeChildShapes` e nenhum `Parent` .

### <a name="navigating-between-shapes-and-elements"></a><a name="views"></a> Navegando entre formas e elementos
 Elementos de modelo de domínio e elementos de forma estão relacionados pela <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação.

```csharp
// using Microsoft.VisualStudio.Modeling;
// using Microsoft.VisualStudio.Modeling.Diagrams;
// using System.Linq;
Person henry = ...;
PersonShape henryShape =
  PresentationViewsSubject.GetPresentation(henry)
    .FirstOrDefault() as PersonShape;
```

 A mesma relação vincula relações a conectores no diagrama:

```
Descendants link = Descendants.GetLink(henry, edward);
DescendantConnector dc =
   PresentationViewsSubject.GetPresentation(link)
     .FirstOrDefault() as DescendantConnector;
// dc.FromShape == henryShape && dc.ToShape == edwardShape
```

 Essa relação também vincula a raiz do modelo ao diagrama:

```
FamilyTreeDiagram diagram =
   PresentationViewsSubject.GetPresentation(familyTree)
      .FirstOrDefault() as FamilyTreeDiagram;
```

 Para obter o elemento de modelo representado por uma forma, use:

 `henryShape.ModelElement as Person`

 `diagram.ModelElement as FamilyTreeModel`

### <a name="navigating-around-the-diagram"></a>Navegando pelo diagrama
 Em geral, não é aconselhável navegar entre formas e conectores no diagrama. É melhor navegar pelas relações no modelo, movendo entre as formas e conectores somente quando for necessário trabalhar na aparência do diagrama. Esses métodos vinculam conectores às formas em cada extremidade:

 `personShape.FromRoleLinkShapes, personShape.ToRoleLinkShapes`

 `connector.FromShape, connector.ToShape`

 Muitas formas são compostas; elas são feitas de uma forma pai e de uma ou mais camadas de filhos. As formas posicionadas em relação a outra forma são os *filhos.* Quando a forma pai se move, os filhos se movem com ela.

 *Os filhos* relativos podem aparecer fora da caixa delimitada da forma pai. *Os filhos* aninhados aparecem estritamente dentro dos limites do pai.

 Para obter o conjunto superior de formas em um diagrama, use:

 `Diagram.NestedChildShapes`

 As classes ancestrais de formas e conectores são:

 <xref:Microsoft.VisualStudio.Modeling.ModelElement>

 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationElement>

 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement>

 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>

 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>

 ------- *YourShape*

 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.LinkShape>

 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>

 --------- *YourConnector*

### <a name="properties-of-shapes-and-connectors"></a><a name="shapeProperties"></a> Propriedades de formas e conectores
 Na maioria dos casos, não é necessário fazer alterações explícitas nas formas. Quando você alterou os elementos do modelo, as regras de "correção" atualizam as formas e os conectores. Para obter mais informações, consulte [Respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

 No entanto, é útil fazer algumas alterações explícitas em formas em propriedades que são independentes dos elementos do modelo. Por exemplo, você pode alterar estas propriedades:

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Size%2A> – determina a altura e a largura da forma.

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Location%2A> - posição em relação à forma ou diagrama pai

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.StyleSet%2A> – o conjunto de canetas e pincéis usados para desenhar a forma ou o conector

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Hide%2A> – torna a forma invisível

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Show%2A> – torna a forma visível após um `Hide()`

### <a name="creating-an-element-and-its-shape"></a><a name="merge"></a> Criando um elemento e sua forma

Quando você cria um elemento e o vincula à árvore de relações de incorporação, uma forma é criada automaticamente e associada a ele. Isso é feito pelas regras de "correção" que são executadas no final da transação. No entanto, a forma aparecerá em um local atribuído automaticamente e sua forma, cor e outros recursos terão valores padrão. Para controlar como a forma é criada, você pode usar a função de mesclagem. Primeiro, você deve adicionar os elementos que deseja adicionar a um ElementGroup e, em seguida, mesclar o grupo no diagrama.

Este método:

- Define o nome, se você atribuiu uma propriedade como o nome do elemento.

- Observa qualquer diretiva de mesclagem de elemento que você especificou na Definição de DSL.

Este exemplo cria uma forma na posição do mouse, quando o usuário clica duas vezes no diagrama. Na Definição de DSL para este exemplo, a `FillColor` propriedade `ExampleShape` de foi exposta.

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
partial class MyDiagram
{
  public override void OnDoubleClick(DiagramPointEventArgs e)
  {
    base.OnDoubleClick(e);

    using (Transaction t = this.Store.TransactionManager
        .BeginTransaction("double click"))
    {
      ExampleElement element = new ExampleElement(this.Store);
      ElementGroup group = new ElementGroup(element);

      { // To use a shape of a default size and color, omit this block.
        ExampleShape shape = new ExampleShape(this.Partition);
        shape.ModelElement = element;
        shape.AbsoluteBounds = new RectangleD(0, 0, 1.5, 1.0);
        shape.FillColor = System.Drawing.Color.Azure;
        group.Add(shape);
      }

      this.ElementOperations.MergeElementGroupPrototype(
        this,
        group.CreatePrototype(),
        PointD.ToPointF(e.MousePosition));
      t.Commit();
    }
  }
}
```

 Se você fornecer mais de uma forma, de definir suas posições relativas usando o `AbsoluteBounds` .

 Você também pode definir a cor e outras propriedades expostas de conectores usando esse método.

### <a name="use-transactions"></a>Usar transações
 Formas, conectores e diagramas são subtipos de <xref:Microsoft.VisualStudio.Modeling.ModelElement> e ao vivo na Store. Portanto, você deve fazer alterações neles somente dentro de uma transação. Para obter mais informações, [consulte Como usar transações para atualizar o modelo.](../modeling/how-to-use-transactions-to-update-the-model.md)

## <a name="document-view-and-document-data"></a><a name="docdata"></a> Exibição de documento e dados do documento
 ![Diagrama de classe de tipos de diagrama padrão](../modeling/media/dsldiagramsanddocs.png)

## <a name="store-partitions"></a>Armazenar partições
 Quando um modelo é carregado, o diagrama que o acompanha é carregado ao mesmo tempo. Normalmente, o modelo é carregado em Store.DefaultPartition e o conteúdo do diagrama é carregado em outra Partição. Normalmente, o conteúdo de cada partição é carregado e salvo em um arquivo separado.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Modeling.ModelElement>
- [Validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md)
- [Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)
- [Como usar transações para atualizar o modelo](../modeling/how-to-use-transactions-to-update-the-model.md)
- [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [Respondendo a alterações e propagando-as](../modeling/responding-to-and-propagating-changes.md)

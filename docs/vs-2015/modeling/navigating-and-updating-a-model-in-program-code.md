---
title: Navegando e atualizando um modelo no código de programa | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, programming domain models
ms.assetid: 1427ae91-be8a-4ce7-85df-00038faa2cbb
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6707f585e8f432a96c2a8cdeef06acb9e903c58e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863159"
---
# <a name="navigating-and-updating-a-model-in-program-code"></a>Navegando e atualizando um modelo no código do programa
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode escrever código para criar e excluir elementos de modelo, defina suas propriedades e criar e excluir links entre elementos. Todas as alterações devem ser feitas em uma transação. Se os elementos são exibidos em um diagrama, o diagrama será "corrigido para cima" automaticamente no final da transação.  
  
## <a name="in-this-topic"></a>Neste tópico  
 [Um exemplo de definição de DSL](#example)  
  
 [O modelo de navegação](#navigation)  
  
 [Acessando informações da classe](#metadata)  
  
 [Executar alterações dentro de uma transação](#transaction)  
  
 [Criar elementos de modelo](#elements)  
  
 [Criação de Links do relacionamento](#links)  
  
 [Excluir elementos](#deleteelements)  
  
 [Excluindo os Links do relacionamento](#deletelinks)  
  
 [Reordenando os Links de uma relação](#reorder)  
  
 [Bloqueios](#locks)  
  
 [Copiar e colar](#copy)  
  
 [Navegando e atualizando diagramas](#diagrams)  
  
 [Navegando entre as formas e elementos](#views)  
  
 [Propriedades de formas e conectores](#shapeProperties)  
  
 [DocView e DocData](#docdata)  
  
 Formas, conectores e diagramas e suas relações com elementos de modelo são descritas em um tópico separado. Para obter mais informações, consulte [como: navegar e atualizar um diagrama](../misc/how-to-navigate-and-update-a-diagram.md).  
  
##  <a name="example"></a> Um exemplo de definição de DSL  
 Essa é a parte principal do Dsldefinition para os exemplos neste tópico:  
  
 ![Diagrama de definição de DSL &#45; modelo de árvore genealógica](../modeling/media/familyt-person.png "FamilyT_Person")  
  
 Esse modelo é uma instância dessa DSL:  
  
 ![Modelo de árvore genealógica Tudor](../modeling/media/tudor-familytreemodel.png "Tudor_FamilyTreeModel")  
  
### <a name="references-and-namespaces"></a>Referências e Namespaces  
 Para executar o código neste tópico, você deve fazer referência:  
  
 `Microsoft.VisualStudio.Modeling.Sdk.11.0.dll`  
  
 Seu código usará este namespace:  
  
 `using Microsoft.VisualStudio.Modeling;`  
  
 Além disso, se você estiver escrevendo o código em um projeto diferente no qual sua DSL é definida, você deve importar o assembly que é compilado pelo projeto Dsl.  
  
##  <a name="navigation"></a> O modelo de navegação  
  
### <a name="properties"></a>Propriedades  
 Propriedades de domínio que você define na definição de DSL se tornam propriedades que você pode acessar no código do programa:  
  
 `Person henry = ...;`  
  
 `if (henry.BirthDate < 1500) ...`  
  
 `if (henry.Name.EndsWith("VIII")) ...`  
  
 Se você quiser definir uma propriedade, você deve fazer isso dentro de um [transação](#transaction):  
  
 `henry.Name = "Henry VIII";`  
  
 Se a definição de DSL, uma propriedade está em **tipo** é **Calculated**, você não pode defini-lo. Para obter mais informações, consulte [Calculated e propriedades de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md).  
  
### <a name="relationships"></a>Relações  
 As relações de domínio que você define na definição de DSL se tornam os pares de propriedades, uma na classe em cada extremidade da relação. Os nomes das propriedades aparecem no diagrama DslDefinition como rótulos em funções em cada lado da relação. Dependendo da multiplicidade da função, o tipo da propriedade é a classe na outra extremidade da relação ou uma coleção de classe.  
  
 `foreach (Person child in henry.Children) { ... }`  
  
 `FamilyTreeModel ftree = henry.FamilyTreeModel;`  
  
 As propriedades nas extremidades opostas de uma relação são sempre recíproco. Quando um link é criado ou excluído, as propriedades de função em ambos os elementos são atualizadas. A expressão a seguir (que usa as extensões de `System.Linq`) é sempre true para a relação ParentsHaveChildren no exemplo:  
  
 `(Person p) => p.Children.All(child => child.Parents.Contains(p))`  
  
 `&& p.Parents.All(parent => parent.Children.Contains(p));`  
  
 **ElementLinks**. Uma relação também é representada por um elemento de modelo chamado um *link*, que é uma instância do tipo de relação de domínio. Um link sempre tem o elemento de uma origem e um destino. O elemento de origem e o elemento de destino podem ser o mesmo.  
  
 Você pode acessar um link e suas propriedades:  
  
 `ParentsHaveChildren link = ParentsHaveChildren.GetLink(henry, edward);`  
  
 `// This is now true:`  
  
 `link == null || link.Parent == henry && link.Child == edward`  
  
 Por padrão, não mais de uma instância de uma relação é permitida para vincular qualquer par de elementos de modelo. Mas se na definição de DSL, o `Allow Duplicates` sinalizador é verdadeiro para a relação, em seguida, pode haver mais de um link, e você deve usar `GetLinks`:  
  
 `foreach (ParentsHaveChildren link in ParentsHaveChildren.GetLinks(henry, edward)) { ... }`  
  
 Também há outros métodos para acessar links. Por exemplo:  
  
 `foreach (ParentsHaveChildren link in     ParentsHaveChildren.GetLinksToChildren(henry)) { ... }`  
  
 **Funções ocultas.** Em caso de definição de DSL, **é a propriedade gerada** é **falso** para uma determinada função, em seguida, nenhuma propriedade é gerada que corresponde a essa função. No entanto, você ainda pode acessar os links e percorrer os links usando os métodos da relação:  
  
 `foreach (Person p in ParentsHaveChildren.GetChildren(henry)) { ... }`  
  
 O exemplo usado com mais frequência é o <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação, que vincula-se à forma que a exibe em um diagrama de um elemento de modelo:  
  
 `PresentationViewsSubject.GetPresentation(henry)[0] as PersonShape`  
  
### <a name="the-element-directory"></a>O diretório do elemento  
 Você pode acessar todos os elementos no repositório usando o elemento directory:  
  
 `store.ElementDirectory.AllElements`  
  
 Também há métodos para localizar elementos, como o seguinte:  
  
 `store.ElementDirectory.FindElements(Person.DomainClassId);`  
  
 `store.ElementDirectory.GetElement(elementId);`  
  
##  <a name="metadata"></a> Acessando informações da classe  
 Você pode obter informações sobre as classes, relacionamentos e outros aspectos da definição de DSL. Por exemplo:  
  
 `DomainClassInfo personClass = henry.GetDomainClass();`  
  
 `DomainPropertyInfo birthProperty =`  
  
 `personClass.FindDomainProperty("BirthDate")`  
  
 `DomainRelationshipInfo relationship =`  
  
 `link.GetDomainRelationship();`  
  
 `DomainRoleInfo sourceRole = relationship.DomainRole[0];`  
  
 As classes de ancestral de elementos de modelo são da seguinte maneira:  
  
-   ModelElement - todos os elementos e relações são encerrar outras  
  
-   ElementLink - todas as relações são ElementLinks  
  
##  <a name="transaction"></a> Executar alterações dentro de uma transação  
 Sempre que o código do programa é alterado nada na Store, deverá fazê-lo dentro de uma transação. Isso se aplica a todos os elementos de modelo, relações, formas, diagramas e suas propriedades. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Modeling.Transaction>.  
  
 O método mais conveniente de gerenciar uma transação é com um `using` instrução incluída em um `try...catch` instrução:  
  
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
  
 Você pode tornar qualquer número de alterações dentro de uma transação. Você pode abrir novas transações dentro de uma transação ativa.  
  
 Para tornar as alterações permanentes, você deve `Commit` a transação antes que ele seja descartado. Se ocorrer uma exceção que não é capturada dentro da transação, a Store será redefinido para seu estado antes das alterações.  
  
##  <a name="elements"></a> Criar elementos de modelo  
 Este exemplo adiciona um elemento a um modelo existente:  
  
```  
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
  
- Crie o novo elemento em uma partição específica do Store. Para elementos de modelo e relações, mas não formas, isso geralmente é a partição padrão.  
  
- Torna o destino de uma relação de incorporação. Em DslDefinition deste exemplo, cada pessoa deve ser o destino da relação FamilyTreeHasPeople incorporada. Para fazer isso, podemos pode definir a propriedade de função FamilyTreeModel do objeto Person ou adicionar a pessoa para a propriedade de função de pessoas do objeto FamilyTreeModel.  
  
- Definir as propriedades de um novo elemento, especialmente a propriedade para o qual `IsName` é verdadeiro para o DslDefinition. Esse sinalizador marca a propriedade que serve para identificar o elemento exclusivamente dentro de seu proprietário. Nesse caso, a propriedade de nome tem esse sinalizador.  
  
- A definição de DSL deste DSL deve ter sido carregada para a Store. Se você estiver escrevendo uma extensão como um comando de menu, isso geralmente será já true. Em outros casos, você pode explicitamente carregar o modelo para a Store, ou usar <xref:Microsoft.VisualStudio.Modeling.Integration.ModelBus> carregá-lo. Para obter mais informações, consulte [como: abrir um modelo de arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md).  
  
  Quando você cria um elemento dessa forma, uma forma é criada automaticamente (se a DSL tem um diagrama). Ele aparece em um local atribuído automaticamente, com a forma padrão, cor e outros recursos. Se você quiser controlar onde e como a forma associada é exibida, consulte [criação de um elemento e sua forma](#merge).  
  
##  <a name="links"></a> Criação de Links do relacionamento  
 Existem duas relações definidas no exemplo, a definição de DSL. Cada relação define uma *propriedades da função* na classe em cada extremidade da relação.  
  
 Há três maneiras em que você pode criar uma instância de uma relação. Cada um desses três métodos tem o mesmo efeito:  
  
- Defina a propriedade do representante da função de origem. Por exemplo:  
  
  -   `familyTree.People.Add(edward);`  
  
  -   `edward.Parents.Add(henry);`  
  
- Defina a propriedade do representante da função de destino. Por exemplo:  
  
  -   `edward.familyTreeModel = familyTree;`  
  
       A multiplicidade desta função é `1..1`, portanto, atribuímos o valor.  
  
  -   `henry.Children.Add(edward);`  
  
       A multiplicidade desta função é `0..*`, portanto, podemos adicionar à coleção.  
  
- Construa uma instância da relação explicitamente. Por exemplo:  
  
  -   `FamilyTreeHasPeople edwardLink = new FamilyTreeHasPeople(familyTreeModel, edward);`  
  
  -   `ParentsHaveChildren edwardHenryLink = new ParentsHaveChildren(henry, edward);`  
  
  O último método é útil se você quiser definir as propriedades na própria relação.  
  
  Quando você cria um elemento dessa forma, um conector no diagrama é criado automaticamente, mas ele tem uma forma padrão, cor e outros recursos. Para controlar como o conector associado é criado, consulte [criação de um elemento e sua forma](#merge).  
  
##  <a name="deleteelements"></a> Excluir elementos  
 Excluir um elemento chamando `Delete()`:  
  
 `henry.Delete();`  
  
 Esta operação excluirá também:  
  
- Links do relacionamento de e para o elemento. Por exemplo, `edward.Parents` não conterá mais `henry`.  
  
- Elementos em funções para o qual o `PropagatesDelete` sinalizador é verdadeiro. Por exemplo, a forma que exibe o elemento será excluída.  
  
  Por padrão, cada relação de incorporação tem `PropagatesDelete` verdadeira em que a função de destino. Excluindo `henry` não exclui o `familyTree`, mas `familyTree.Delete()` seria excluir todos os `Persons`. Para obter mais informações, consulte [Personalizando o comportamento de exclusão](../modeling/customizing-deletion-behavior.md).  
  
  Por padrão, `PropagatesDelete` não é verdadeiro para as funções de relações de referência.  
  
  Você pode fazer com que as regras de exclusão omitir as propagações específicas quando você exclui um objeto. Isso é útil se você estiver substituindo um elemento para outro. Você fornecer o GUID de uma ou mais funções para os quais não deveriam ser propagada exclusão. O GUID pode ser obtido da classe de relação:  
  
  `henry.Delete(ParentsHaveChildren.SourceDomainRoleId);`  
  
  (Esse exemplo específico não terá efeito algum, pois `PropagatesDelete` está `false` para funções do `ParentsHaveChildren` relacionamento.)  
  
  Em alguns casos, a exclusão é impedida pela existência de um bloqueio no elemento ou em um elemento que seria excluído pelo propagação. Você pode usar `element.CanDelete()` para verificar se o elemento pode ser excluído.  
  
##  <a name="deletelinks"></a> Excluindo os Links do relacionamento  
 Você pode excluir um link de relação, removendo um elemento de uma propriedade de função:  
  
 `henry.Children.Remove(edward); // or:`  
  
 `edward.Parents.Remove(henry);  // or:`  
  
 Você também pode excluir o link explicitamente:  
  
 `edwardHenryLink.Delete();`  
  
 Todos esses três métodos têm o mesmo efeito. Você só precisará usar um deles.  
  
 Se a função tem a multiplicidade de 0 a 1. 1 ou 1, você pode defini-lo `null`, ou a outro valor:  
  
 `edward.FamilyTreeModel = null;` ou:  
  
 `edward.FamilyTreeModel = anotherFamilyTree;`  
  
##  <a name="reorder"></a> Reordenação de Links de um relacionamento  
 Os links de uma relação específica que são originados ou destinado a um elemento de modelo específico têm uma sequência específica. Eles aparecem na ordem na qual eles foram adicionados. Por exemplo, essa instrução sempre produzirá os filhos na mesma ordem:  
  
 `foreach (Person child in henry.Children) ...`  
  
 Você pode alterar a ordem dos links:  
  
 `ParentsHaveChildren link = GetLink(henry,edward);`  
  
 `ParentsHaveChildren nextLink = GetLink(henry, elizabeth);`  
  
 `DomainRoleInfo role =`  
  
 `link.GetDomainRelationship().DomainRoles[0];`  
  
 `link.MoveBefore(role, nextLink);`  
  
##  <a name="locks"></a> Bloqueios  
 Suas alterações podem ser impedidas por um bloqueio. Bloqueios podem ser definidos em elementos individuais, partições e o armazenamento. Se qualquer um desses níveis possui um bloqueio que impede que o tipo de alteração que você deseja fazer, uma exceção pode ser lançada durante a tentativa de ele. Você pode descobrir se os bloqueios são definidos usando o elemento. GetLocks(), que é um método de extensão que é definido no namespace <xref:Microsoft.VisualStudio.Modeling.Immutability>.  
  
 Para obter mais informações, consulte [definindo uma política de bloqueio para criar segmentos de somente leitura](../modeling/defining-a-locking-policy-to-create-read-only-segments.md).  
  
##  <a name="copy"></a> Copiar e colar  
 Você pode copiar elementos ou grupos de elementos para um <xref:System.Windows.Forms.IDataObject>:  
  
```  
Person person = personShape.ModelElement as Person;  
Person adopter = adopterShape.ModelElement as Person;  
IDataObject data = new DataObject();  
personShape.Diagram.ElementOperations  
      .Copy(data, person.Children.ToList<ModelElement>());  
```  
  
 Os elementos são armazenados como um grupo de elementos serializados.  
  
 Você pode mesclar os elementos de um IDataObject em um modelo:  
  
```  
using (Transaction t = targetDiagram.Store.  
        TransactionManager.BeginTransaction("paste"))  
{  
  adopterShape.Diagram.ElementOperations.Merge(adopter, data);  
}  
```  
  
 `Merge ()` pode aceitar qualquer um uma `PresentationElement` ou um `ModelElement`. Se você atribuir a ela um `PresentationElement`, você também pode especificar uma posição no diagrama de destino como um terceiro parâmetro.  
  
##  <a name="diagrams"></a> Navegando e atualizando diagramas  
 Em uma DSL, o elemento de modelo de domínio, que representa um conceito como pessoa ou música, é separado do elemento forma, que representa o que você vê no diagrama. O elemento de modelo de domínio armazena as propriedades importantes e relações dos conceitos. O elemento de forma armazena o tamanho, a posição e a cor do modo de exibição do objeto no diagrama e o layout de seus componentes.  
  
### <a name="presentation-elements"></a>Elementos de apresentação  
 ![Diagrama de classes de tipos base de forma e o elemento](../modeling/media/dslshapesandelements.png "DSLshapesAndElements")  
  
 Em sua definição de DSL, cada elemento que você especificar cria uma classe derivada de uma das seguintes classes padrão.  
  
|Tipo de elemento|Classe base|  
|---------------------|----------------|  
|Classe de domínio|<xref:Microsoft.VisualStudio.Modeling.ModelElement>|  
|Relacionamento de domínio|<xref:Microsoft.VisualStudio.Modeling.ElementLink>|  
|Forma|<xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>|  
|Conector|<xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>|  
|Diagrama|<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>|  
  
 Normalmente, um elemento em um diagrama representa um elemento de modelo. Normalmente (mas nem sempre), uma <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape> representa uma instância da classe de domínio e um <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape> representa uma instância de relação de domínio. O <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação vincula uma forma de nó ou link para o elemento de modelo que ela representa.  
  
 Todas as formas de nó ou link pertence a um diagrama. Uma forma de link binário se conecta a duas formas de nó.  
  
 Formas podem ter formas filho em dois conjuntos. Uma forma no `NestedChildShapes` conjunto é restrito à caixa delimitadora de seu pai. Uma forma no `RelativeChildShapes` lista pode aparecer fora ou parcialmente fora dos limites do pai – por exemplo, um rótulo ou uma porta. Um diagrama não tem nenhum `RelativeChildShapes` e nenhum `Parent`.  
  
###  <a name="views"></a> Navegando entre as formas e elementos  
 Elementos de modelo de domínio e elementos de forma relacionados pelo <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> relação.  
  
```csharp  
// using Microsoft.VisualStudio.Modeling;  
// using Microsoft.VisualStudio.Modeling.Diagrams;  
// using System.Linq;  
Person henry = ...;  
PersonShape henryShape =   
  PresentationViewsSubject.GetPresentation(henry)  
    .FirstOrDefault() as PersonShape;  
```  
  
 A mesma relação vincula-se aos conectores no diagrama de relações:  
  
```  
Descendants link = Descendants.GetLink(henry, edward);  
DescendantConnector dc =  
   PresentationViewsSubject.GetPresentation(link)  
     .FirstOrDefault() as DescendantConnector;  
// dc.FromShape == henryShape && dc.ToShape == edwardShape  
```  
  
 Essa relação também vincula a raiz do modelo para o diagrama:  
  
```  
FamilyTreeDiagram diagram =   
   PresentationViewsSubject.GetPresentation(familyTree)  
      .FirstOrDefault() as FamilyTreeDiagram;  
```  
  
 Para obter o elemento de modelo representado por uma forma, use:  
  
 `henryShape.ModelElement as Person`  
  
 `diagram.ModelElement as FamilyTreeModel`  
  
### <a name="navigating-around-the-diagram"></a>Navegar em torno do diagrama  
 Em geral não é aconselhável para navegar entre as formas e conectores no diagrama. É melhor navegar pelas relações no modelo, movendo entre as formas e conectores somente quando é necessário para trabalhar na aparência do diagrama. Esses métodos link conectores para as formas em cada extremidade:  
  
 `personShape.FromRoleLinkShapes, personShape.ToRoleLinkShapes`  
  
 `connector.FromShape, connector.ToShape`  
  
 Muitas formas são compostos; eles são compostos de uma forma de pai e uma ou mais camadas de filhos. Formas que são posicionadas em relação à outra forma são consideradas seus *filhos*. Quando a forma pai é movido, os filhos movem com ele.  
  
 *Relativos filhos* pode aparecer fora da caixa delimitadora da forma pai. *Aninhado* filhos estritamente aparecem dentro dos limites do pai.  
  
 Para obter o conjunto superior de formas em um diagrama, use:  
  
 `Diagram.NestedChildShapes`  
  
 As classes de ancestral de formas e conectores são:  
  
 <xref:Microsoft.VisualStudio.Modeling.ModelElement>  
  
 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationElement>  
  
 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement>  
  
 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>  
  
 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>  
  
 ------- *YourShape*  
  
 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.LinkShape>  
  
 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>  
  
 --------- *YourConnector*  
  
###  <a name="shapeProperties"></a> Propriedades de formas e conectores  
 Na maioria dos casos, não é necessário fazer alterações explícitas às formas. Quando você tiver alterado os elementos de modelo, as regras de "corrigir" atualizam as formas e conectores. Para obter mais informações, consulte [respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).  
  
 No entanto, é útil fazer algumas alterações explícitas para as formas nas propriedades que são independentes dos elementos de modelo. Por exemplo, você pode alterar essas propriedades:  
  
-   <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Size%2A> -Determina a altura e largura da forma.  
  
-   <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Location%2A> -posição relativa a forma pai ou o diagrama  
  
-   <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.StyleSet%2A> -o conjunto de canetas e pincéis usados para desenhar a forma ou conector  
  
-   <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Hide%2A> -torna a forma invisível  
  
-   <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Show%2A> -torna a forma visível após um `Hide()`  
  
###  <a name="merge"></a> Criação de um elemento e sua forma  
 Quando você cria um elemento e vinculá-lo na árvore de relações inseridas, uma forma é automaticamente criada e associada a ele. Isso é feito pelas regras de "correção" executem no final da transação. No entanto, a forma aparecerá em um local atribuído automaticamente e sua forma, cor e outros recursos terão valores padrão. Para controlar como a forma é criada, você pode usar a função de mesclagem. Você deve primeiro adicionar os elementos que você deseja adicionar a um ElementGroup e, em seguida, mesclar o grupo no diagrama.  
  
 Esse método:  
  
- Define o nome, se você tiver atribuído a uma propriedade como o nome do elemento.  
  
- Observa quaisquer diretivas de mesclagem de elementos que você especificou na definição de DSL.  
  
  Este exemplo cria uma forma na posição do mouse, quando o usuário clica duas vezes o diagrama. Na definição de DSL para este exemplo, o `FillColor` propriedade de `ExampleShape` foi exposto.  
  
```  
  
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
  
 Se você fornecer mais de uma forma, definir suas posições relativas usando o `AbsoluteBounds`.  
  
 Você também pode definir a cor e outras propriedades expostas de conectores usando esse método.  
  
### <a name="use-transactions"></a>Usar transações  
 Formas, conectores e diagramas são subtipos de <xref:Microsoft.VisualStudio.Modeling.ModelElement> e em tempo real na Store. Portanto, você deve fazer alterações a eles somente dentro de uma transação. Para obter mais informações, consulte [como: usar transações para atualizar o modelo](../modeling/how-to-use-transactions-to-update-the-model.md).  
  
##  <a name="docdata"></a> Exibição de documentos e dados de documento  
 ![Diagrama de classe dos tipos de padrão de diagrama](../modeling/media/dsldiagramsanddocs.png "DSLDiagramsandDocs")  
  
## <a name="store-partitions"></a>Partições de Store  
 Quando um modelo é carregado, o diagrama que acompanha este artigo é carregado ao mesmo tempo. Normalmente, o modelo é carregado no Store.DefaultPartition, e o conteúdo de diagrama é carregado em outra partição. Normalmente, o conteúdo de cada partição é carregado e salvas em um arquivo separado.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Modeling.ModelElement>   
 [Validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)   
 [Código de geração de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)   
 [Como: usar transações para atualizar o modelo](../modeling/how-to-use-transactions-to-update-the-model.md)   
 [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)   
 [Respondendo a alterações e propagando-as](../modeling/responding-to-and-propagating-changes.md)




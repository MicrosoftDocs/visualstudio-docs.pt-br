---
title: Navegar no modelo UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API
ms.assetid: 6d789b6d-2aa9-4ceb-92c4-84a300065a76
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6f77e72c55c0984f66a6884b0582716e5529abd0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727768"
---
# <a name="navigate-the-uml-model"></a>Navegar no modelo UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico apresenta os principais tipos de modelo UML.  
  
## <a name="the-model-elements-model-and-model-store"></a>Os elementos de modelo, modelo e modelo Store  
 Os tipos definidos no assembly **VisualStudio** correspondem aos tipos definidos na [especificação UML, versão 2.1.2](http://www.omg.org/spec/UML/2.1.2/Superstructure/PDF/).  
  
 Tipos na especificação UML são percebidos como interfaces no Visual Studio. A letra 'I' é acrescentada ao nome de cada tipo. Por exemplo: <xref:Microsoft.VisualStudio.Uml.Classes.IElement>, <xref:Microsoft.VisualStudio.Uml.Classes.IClass>, <xref:Microsoft.VisualStudio.Uml.Interactions.IInteraction>, <xref:Microsoft.VisualStudio.Uml.Classes.IOperation>.  
  
 Todos os tipos, exceto iElement, herdam propriedades de um ou mais supertipos.  
  
-   Para obter um resumo dos tipos de modelo, consulte [tipos de elemento de modelo UML](../modeling/uml-model-element-types.md).  
  
-   Para obter detalhes completos da API, consulte [referência de API para extensibilidade de modelagem UML](../modeling/api-reference-for-uml-modeling-extensibility.md).  
  
### <a name="relationships"></a>Relações  
 Propriedades e relações que são definidas na especificação UML são implementadas como propriedades .NET.  
  
 A maioria das relações são navegáveis em ambas as direções. Uma relação corresponde a um par de propriedades, com uma propriedade no tipo em cada extremidade. Por exemplo, as propriedades `IElement.Owner` e `IElement.OwnedElements` representam duas extremidades de uma relação. Portanto, essa expressão será sempre avaliada como true:  
  
 `IElement c; ...  c.OwnedElements.All(x => x.Owner == c)`  
  
 Muitas relações, como IAssociation, também são representadas por um objeto que pode ter suas próprias propriedades.  
  
 Se você excluir um elemento do modelo, qualquer relacionamento no qual ele participa é excluído automaticamente e a propriedade na outra extremidade é atualizada.  
  
 Se a especificação de UML atribuir uma multiplicidade de 0 a 1 a uma propriedade, ela poderá ter o valor `null`. Uma multiplicidade com máximo maior que 1 significa que a propriedade .NET tem o tipo: `IEnumerable<` *tipo*`>`.  
  
 Para obter mais informações sobre relações de atravessamento, consulte [navegar em relações com a API UML](../modeling/navigate-relationships-with-the-uml-api.md).  
  
### <a name="the-ownership-tree"></a>A árvore de propriedade  
 Um modelo contém uma árvore de <xref:Microsoft.VisualStudio.Uml.Classes.IElement> objetos. Cada elemento tem propriedades `OwnedElements` e `Owner`.  
  
 Na maioria dos casos, os destinos do `Owner` e `OwnedElements` propriedades também são referenciadas por outras propriedades que têm um nome mais específico. Por exemplo, cada operação de UML pertence a uma classe UML. Portanto <xref:Microsoft.VisualStudio.Uml.Classes.IOperation> tem uma propriedade chamada <xref:Microsoft.VisualStudio.Uml.Classes.IOperation.Class%2A>e, em cada <xref:Microsoft.VisualStudio.Uml.Classes.IOperation> objeto, `Class == Owner`.  
  
 O elemento superior da árvore, que não tem nenhum proprietário, é um <xref:Microsoft.VisualStudio.Uml.AuxiliaryConstructs.IModel>. O IModel está contido em uma <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml.IModelStore>, no qual ele é o <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml.IModelStore.Root%2A>.  
  
 Cada elemento de modelo é criado com um proprietário. Para obter mais informações, consulte [criar elementos e relações em modelos UML](../modeling/create-elements-and-relationships-in-uml-models.md).  
  
 ![Diagrama de classe: elemento, diagrama, forma e modelo](../modeling/media/uml-mm1.png "UML_MM1")  
  
## <a name="shapes-and-diagrams"></a>Formas e diagramas  
 Elementos no modelo de UML podem ser exibidos em diagramas. Diferentes tipos de diagramas podem exibir subtipos diferentes de IElement.  
  
 Em alguns casos, um elemento pode aparecer em mais de um diagrama. Por exemplo, um elemento de IUseCase pode ter vários IShapes, que podem aparecer em um diagrama ou diagramas diferentes.  
  
 Formas são organizadas em uma árvore. As bordas da árvore são representadas pelas propriedades ParentShape e ChildShapes. Os diagramas são as únicas formas que não têm pais. As formas na superfície de um diagrama são compostas de partes menores. Por exemplo, uma forma de classe tem compartimentos para atributos e operações.  
  
 Para obter mais informações sobre formas, consulte [exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md).  
  
## <a name="access-to-the-model-in-extensions"></a>Acesso ao modelo em extensões  
 No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões definidas como componentes de MEF, você pode declarar propriedades que importam informações do contexto no qual a extensão é executada.  
  
|Tipo de atributo|Permite o acesso ao|Mais informações|  
|--------------------|----------------------------------|----------------------|  
|Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation<br /><br /> . IDiagramContext<br /><br /> (em Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll)|O diagrama atual de foco.|[Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|  
|Microsoft.VisualStudio.Modeling.ExtensionEnablement<br /><br /> . ILinkedUndoContext<br /><br /> (em Microsoft.VisualStudio.Modeling.Sdk. . dll de [versão])|Permite agrupar alterações em transações.|[Vincular atualizações de modelo UML usando transações](../modeling/link-uml-model-updates-by-using-transactions.md)|  
|Microsoft.VisualStudio.Shell. SVsServiceProvider<br /><br /> (em Microsoft.VisualStudio.Shell.Immutable. . dll de [versão])|O host [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. A partir daí, você pode acessar arquivos, projetos e outros aspectos.|[Abrir um modelo UML usando a API do Visual Studio](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)|  
  
### <a name="to-get-the-context"></a>Para obter o contexto  
 Declare uma ou ambas das seguintes interfaces dentro de sua classe de extensão:  
  
```  
[Import] public IDiagramContext DiagramContext { get; set; }  
  
```  
  
 O MEF Managed Extensibility Framework () as associará às definições das quais você pode obter o diagrama atual, armazenamento de modelos, objeto raiz e assim por diante:  
  
```  
IDiagram diagram = this.DiagramContext.CurrentDiagram;  
IClassDiagram classDiagram = diagram as IClassDiagram;  
       // or diagrams of other types  
IModelStore modelStore = diagram.ModelStore;  
IModel model = modelStore.Root;  
foreach (IDiagram diagram in modelStore.Diagrams) {...}  
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}  
```  
  
### <a name="to-get-the-current-selection"></a>Para obter a seleção atual  
  
```  
// All selected shapes and their elements  
foreach (IShape shape in diagram.SelectedShapes)  
{    
   IDiagram selectedDiagram = shape as IDiagram;  
   if (selectedDiagram != null)  
   { // no shape selected - user right-clicked the diagram  
     ... Context.CurrentDiagram ...  
   }  
   else  
   {  
     IElement selectedElement = shape.Element;  
   ...}  
// All selected shapes that display a specfic type of element  
foreach (IShape<IInterface> in   
   diagram.GetSelectedShapes<IInterface>())   
{...}  
```  
  
## <a name="accessing-another-model-or-diagrams"></a>Acessando outro modelo ou diagramas  
 Você pode:  
  
-   Use [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] barramento para criar links entre os elementos em modelos diferentes de modelo. Para obter mais informações, consulte [modelos de UML integrar com outros modelos e ferramentas](../modeling/integrate-uml-models-with-other-models-and-tools.md).  
  
-   Carregar um projeto de modelagem e diagramas no modo somente leitura sem torná-la visível no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] interface do usuário. Para obter mais informações, consulte [ler um modelo UML no código do programa](../modeling/read-a-uml-model-in-program-code.md).  
  
-   Abra um projeto de modelagem e seus diagramas no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]e, em seguida, acessar o conteúdo. Para obter mais informações, consulte [abrir um modelo UML usando a API do Visual Studio](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)




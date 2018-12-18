---
title: Obter elementos de modelo UML de IDataObject | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API, copy and paste
ms.assetid: e0b9cec8-3b93-4a24-8bd3-3e086501d387
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a560ce5116c52b8c2e83ce9b28252f060e2485f1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782070"
---
# <a name="get-uml-model-elements-from-idataobject"></a>Obter elementos de modelo UML de IDataObject
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando o usuário arrasta elementos de qualquer fonte para um diagrama, os elementos arrastados são codificados em um `System.Windows.Forms.IDataObject`. A codificação depende do tipo de objeto de origem. O fragmento a seguir demonstra como recuperar os elementos quando a fonte for um diagrama UML.  
  
> [!NOTE]
>  A maioria das operações que você precisa fazer em modelos de UML pode ser executada usando os tipos no definido nos assemblies **Microsoft.VisualStudio.Uml.Interfaces** e  **Microsoft.VisualStudio.ArchitectureTools.Extensibility**. Mas, para essa finalidade, você precisa usar algumas classes que fazem parte da implementação de ferramentas de modelagem UML. Por exemplo, `ShapeElement` neste fragmento não é o mesmo que UML `IShape`. Para reduzir o risco de colocar o modelo UML e diagramas em um estado inconsistente, é melhor evitar usar os métodos nessas classes de implementação, exceto onde não há nenhuma alternativa.  
  
## <a name="code-sample"></a>Exemplo de código  
 Seu projeto deve referenciar os seguintes [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] assemblies:  
  
 **Microsoft.VisualStudio.Modeling.Sdk. [versão]**  
  
 **Microsoft.VisualStudio.Modeling.Sdk.Diagrams. [versão]**  
  
 **System**  
  
```  
using Microsoft.VisualStudio.Modeling;    
  // for ElementGroupPrototype  
using Microsoft.VisualStudio.Modeling.Diagrams;    
  // for ShapeElement, DiagramDragEventArgs, DiagramPointEventArgs  
…   
  /// <summary>  
  /// Retrieves UML IElements from drag arguments.  
  /// Works for drags from UML diagrams.  
  /// </summary>  
  private IEnumerable<IElement> GetModelElementsFromDragEvent  
                  (DiagramDragEventArgs dragEvent)  
  {  
     //ElementGroupPrototype is the container for  
     //dragged and copied elements and toolbox items.  
     ElementGroupPrototype prototype =  
        dragEvent.Data.  
        GetData(typeof(ElementGroupPrototype))  
                     as ElementGroupPrototype;  
     // Locate the originals in the implementation store.  
     IElementDirectory implementationDirectory =   
        dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;  
  
     return  prototype.ProtoElements.Select(  
       prototypeElement =>   
       {  
          ModelElement element = implementationDirectory  
                .FindElement(prototypeElement.ElementId);  
          ShapeElement shapeElement = element as ShapeElement;  
          if (shapeElement != null)  
          {   
            // Dragged from a diagram.  
            return shapeElement.ModelElement as IElement;  
          }  
          else  
          {   
            // Dragged from UML Model Explorer.  
            return element as IElement;  
          }  
        });  
    }  
```  
  
 Para obter mais informações sobre `ElementGroupPrototype` e o `Store` em que as ferramentas de modelagem UML são implementadas, consulte [SDK de modelagem para Visual Studio - linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)




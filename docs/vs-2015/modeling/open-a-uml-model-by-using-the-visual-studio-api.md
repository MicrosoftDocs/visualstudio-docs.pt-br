---
title: Abrir um modelo UML usando a API do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API, opening models in Visual Studio
ms.assetid: 38423682-f2a7-4d2a-a2cd-fd680e9b4b4d
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 62b8700e85ccab271dbfdc4f9bac504ee64197a6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779613"
---
# <a name="open-a-uml-model-by-using-the-visual-studio-api"></a>Abrir um modelo UML usando a API do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você também pode abrir modelos e diagramas na interface do usuário do Visual Studio por meio da API.  
  
 Se você quiser ler um modelo no código do programa sem torná-la visível para o usuário, você pode usar os seguintes métodos:  
  
-   Visual Studio Model Bus permite que você acesse modelos e elementos dentro deles e fornece um método padrão de links de um modelo e outro. Para obter mais informações, consulte [modelos de UML integrar com outros modelos e ferramentas](../modeling/integrate-uml-models-with-other-models-and-tools.md).  
  
-   Você pode abrir um modelo no modo somente leitura. Para obter mais informações, consulte [ler um modelo UML no código do programa](../modeling/read-a-uml-model-in-program-code.md).  
  
##  <a name="Showing"></a> Abrindo modelos e diagramas no Visual Studio  
 Para abrir um modelo na interface do usuário, use a API padrão do Visual Studio `EnvDTE.DTE`. Há duas conversões úteis que podem ser executadas em itens de projeto de modelagem:  
  
- `EnvDTE.Project` pode ser convertido para e de `IModelingProject`, se o projeto é um projeto de modelagem, e se o projeto é carregado no AppDomain atual.  
  
- `EnvDTE.ProjectItem` pode ser convertido para e de `IDiagramContext`, se o item for um diagrama UML.  
  
  Para o exemplo a seguir, seu projeto deve importar essas referências:  
  
- EnvDTE  
  
- Microsoft.VisualStudio.ArchitectureTools.Extensibility  
  
- Microsoft.VisualStudio.Modeling.Sdk.[version]  
  
- Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]  
  
- Microsoft.VisualStudio.Shell.Immutable. [versão]  
  
- Microsoft.VisualStudio.Uml.Interfaces  
  
- System.ComponentModel.Composition  
  
  Este exemplo abre um modelo UML no Visual Studio:  
  
```  
using EnvDTE; // Visual Studio API for loading diagrams  
using   
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.Modeling;   
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;    
   // for ICommandExtension and other handler types  
using Microsoft.VisualStudio.Uml.Classes;   
   // for basic UML types  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
   // for model construction methods  
using EnvDTE;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;  
Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;   
                             // for IDiagram   
...  
```  
  
 Em uma extensão do Visual Studio, você pode fazer essa declaração para obter acesso ao provedor de serviço de host:  
  
```  
[Import] public Microsoft.VisualStudio.Shell.SVsServiceProvider ServiceProvider {get;set;}  
...  
```  
  
 Em um método, você pode acessar um projeto, por exemplo, o projeto atual:  
  
```  
DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));  
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;  
IModelingProject modelingProject = project as IModelingProject;  
if (modelingProject == null) return; // not a modeling project  
  
// Access the model's store and contents.  
IModelStore store = modelingProject.Store;  
foreach (IElement element in store.Root.OwnedElements) {...}  
  
// Open all the project's diagrams.  
foreach (ProjectItem item in project.ProjectItems)  
{   
     IDiagramContext modelingItem = item as IDiagramContext;  
     if (modelingItem == null)  
         continue; // not a model diagram  
     IDiagram diagram = modelingItem.CurrentDiagram;  
     if (diagram == null)  
     {  
        // Diagram is closed. Open it.  
        item.Open().Activate();  
        diagram = modelingItem.CurrentDiagram;  
     }  
     // Access the shapes.  
     foreach (IShape<IElement> shape   
               in diagram.GetChildShapes<IElement>())  
     {  
       IElement displayedElement = shape.Element;  
       ...  
     }  
   }  
}   
```  
  
## <a name="see-also"></a>Consulte também  
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)




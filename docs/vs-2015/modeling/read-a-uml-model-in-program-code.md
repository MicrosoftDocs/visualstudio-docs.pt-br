---
title: Ler um modelo UML no código do programa | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API, reading models
ms.assetid: 0f63105e-6079-498a-94f1-318c0f5f9621
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 62355c8b934b152aae8d3a4102432d2eb0553473
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721244"
---
# <a name="read-a-uml-model-in-program-code"></a>Ler um modelo UML no código do programa
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode carregar um modelo UML e seus diagramas usando a API UML.  
  
##  <a name="Reading"></a> Leitura de um modelo no código do programa  
 Para acessar o conteúdo de um modelo sem mostrá-lo em um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela, use `ModelingProject.LoadReadOnly()`.  
  
 Por exemplo:  
  
```  
using Microsoft.VisualStudio.Uml.Classes;   
               // for IElement  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;   
               // for ModelingProject  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
               // for IModelStore  
...   
string projectPath = @"C:\MyProjectFolder\MyProject.modelproj";  
using (IModelingProjectReader projectReader =  
           ModelingProject.LoadReadOnly(projectPath))  
{  
   IModelStore store = projectReader.Store;  
   foreach (IClass umlClass in store.AllInstances<IClass>())  
   {   
       ...  
   }  
}  
```  
  
 Se você quiser ler as formas em um diagrama, você deve ler o projeto e, em seguida, o diagrama.  
  
 Por exemplo:  
  
```  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;   
                             // for IDiagram  
...  
foreach (string diagramFile in projectReader. DiagramFileNames)  
{   
  IDiagram diagram = projectReader.LoadDiagram(diagramFile);  
  foreach (IShape<IElement> shape   
         in diagram.GetChildShapes<IElement>())  
  { ... }  
}  
```  
  
## <a name="alternative-methods"></a>Métodos alternativos  
 Para muitos aplicativos, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Modelbus permite a você referenciar modelos e elementos dentro deles, com maior robustez e flexibilidade do que com os métodos descritos neste tópico. Ele fornece um método padrão de criação de links entre elementos arbitrários, nos modelos de iguais ou diferentes. Para obter mais informações, consulte [modelos de UML integrar com outros modelos e ferramentas](../modeling/integrate-uml-models-with-other-models-and-tools.md).  
  
 Você também pode abrir modelos e diagramas na interface do usuário usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API. Para obter mais informações, consulte [abrir um modelo UML usando a API do Visual Studio](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md).  
  
##  <a name="Standalone"></a> Aplicativos autônomos  
 O exemplo na seção anterior funcionará em extensões do Visual Studio. É possível ler um modelo em um aplicativo autônomo, mas você deve adicionar algumas referências ao seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto.  
  
> [!NOTE]
>  Os detalhes de como ler um modelo em um aplicativo autônomo provavelmente mudar em futuras versões do produto. Alguns recursos que são acessíveis na versão atual podem não estar disponíveis em versões futuras.  
  
#### <a name="to-add-references-to-read-a-model-in-a-stand-alone-application"></a>Para adicionar referências para ler um modelo em um aplicativo autônomo.  
  
1. No Gerenciador de soluções, clique com botão direito do projeto no qual você está compilando o aplicativo e, em seguida, clique em **propriedades**. No editor de propriedades, nos **Application** guia, defina **estrutura de destino** para a versão necessária do .NET Framework.  
  
2. Adicionar o [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] referências necessárias para acessar os modelos UML, normalmente:  
  
   -   VisualStudio  
  
   -   Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll  
  
3. Além das referências listadas nas seções anteriores, adicione as seguintes referências de projeto do **\Program Files\Microsoft Visual Studio [versão] \Common7\IDE\PrivateAssemblies**:  
  
   - Microsoft.VisualStudio.Uml.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.ModelStore.Dsl.dll  
  
     Se desejar ler diagramas em seu aplicativo, você também pode exigir essas referências:  
  
   - Microsoft.VisualStudio.TeamArchitect.ActivityDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.ComponentDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.LogicalClassDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.SequenceDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.UseCase.Dsl.dll  
  
## <a name="see-also"></a>Consulte também  
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)




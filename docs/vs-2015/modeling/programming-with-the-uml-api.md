---
title: Programando com a API UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, API
- UML model, extending
ms.assetid: c5937139-49d0-4439-8a9f-89f5e0474618
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: d5670b0c0806d59119e1a1af87bae5642255c5a9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793167"
---
# <a name="programming-with-the-uml-api"></a>Programando com a API UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A UML API do Visual Studio permite escrever código para criar, ler e atualizar modelos e diagramas UML. Para ver quais versões do Visual Studio dão suporte a modelos UML, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Além das páginas de referência de API, os tópicos a seguir descrevem a API.  
  
|Tópico|Tipos de exemplo e os métodos descritos|Recursos descritos|  
|-----------|-----------------------------------------|------------------------|  
|[Navegar em relações com a API UML](../modeling/navigate-relationships-with-the-uml-api.md)|Elementos UML e suas propriedades e associações. Por exemplo, IElement e seus descendentes, incluindo: IClass, IActivity, IUseCase, IComponent, IInteraction, IModel, IPackage|No Visual Studio, modelos de UML estão em conformidade com a versão 2.1.2 de especificação, que pode ser obtida no UML a [página de recursos do UML](http://go.microsoft.com/fwlink/?LinkId=160796). Cada tipo é uma interface que tem o mesmo nome que o tipo UML, prefixado com "I".|  
|[Criar elementos e relações em modelos UML](../modeling/create-elements-and-relationships-in-uml-models.md)|IPackage.CreateClass()<br /><br /> IClass.CreateOperation()|Cada tipo de elemento tem métodos para a criação de seus filhos.|  
|[Exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md)|IShape, IDiagram<br /><br /> IShape.Move()|Cada elemento em um modelo pode ser representado como uma forma em um diagrama. Em alguns casos, você pode criar novas formas para cada objeto. Você pode mover, redimensionar, colorir e recolher ou expandir essas formas.|  
|[Navegar no modelo UML](../modeling/navigate-the-uml-model.md)|IModelStore<br /><br /> IDiagramContext|O modelo Store armazena o modelo.<br /><br /> O contexto do diagrama fornece acesso para o diagrama atual e o armazenamento.|  
|[Vincular atualizações de modelo UML usando transações](../modeling/link-uml-model-updates-by-using-transactions.md)|ILinkedUndoContext|Você pode vincular uma série de alterações em uma transação.|  
|[Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|IMenuCommand<br /><br /> IGestureExtension<br /><br /> ICommandExtension|Você pode estender a funcionalidade de um diagrama definindo os comandos chamados clicando duas vezes e arrastando para o diagrama.|  
|[Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)|ValidationContext|Você pode definir validação de regras que ajudam você certifique-se de que um modelo obedeça as restrições especificadas.|  
|[Obter elementos de modelo UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md)|IElement, IShape|Quando um elemento é arrastado do Gerenciador de modelos UML ou um diagrama UML para outro diagrama ou aplicativo, ele é serializado como um IDataObject.|  
|[Editar diagramas de sequência UML usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)|IInteraction, ILifeline, IMessage|Criação e atualização de um diagrama de interação são ligeiramente diferente do que trabalhar com outros tipos de diagrama.|  
|[Estender diagramas de camada](../modeling/extend-layer-diagrams.md)|ILayer, ILayerDiagram|Você pode escrever código para criar e editar diagramas de camada e também validar o código de programa em relação a elas.|  
  
## <a name="about-the-implementation"></a>Sobre a implementação  
 As ferramentas de modelagem UML são criadas em [!INCLUDE[dsl](../includes/dsl-md.md)]. Cada pacote e cada diagrama é representado por um [!INCLUDE[dsl](../includes/dsl-md.md)] modelo e uma coleção de regras e outros métodos mantém a consistência entre eles.  
  
 Tipos dessa plataforma são visíveis em alguns dos assemblies que referenciam para escrever extensões UML. Embora você possa fazer as extensões para ferramentas de UML acessando o [!INCLUDE[dsl](../includes/dsl-md.md)] API, você deve ter as seguintes considerações em mente:  
  
-   Você pode achar que algumas alterações aparentemente simples apresentam inconsistências e efeitos inesperados.  
  
-   A implementação pode ser alterada no futuro, para que as adaptações feitas usando o [!INCLUDE[dsl](../includes/dsl-md.md)] API pode não funcionar mais.  
  
## <a name="the-api-assemblies"></a>Os assemblies de API  
 Esta tabela resume os assemblies que fornecem extensibilidade para as ferramentas UML e os namespaces que são recomendadas para usar.  
  
|Assembly|Namespaces|Fornece acesso a:|  
|--------------|----------------|-------------------------|  
|Microsoft.VisualStudio.Uml.Interfaces|(Tudo)|Os tipos UML.|  
|Microsoft.VisualStudio.ArchitectureTools.Extensibility|<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml>|[Métodos de criação](../modeling/create-elements-and-relationships-in-uml-models.md)|  
||<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation>|[Diagramas e formas](../modeling/display-a-uml-model-on-diagrams.md)|  
||<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility>|[O projeto de modelagem](../modeling/read-a-uml-model-in-program-code.md)|  
|Microsoft.VisualStudio.Modeling.Sdk.[version]|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement>|[Extensão de comando de menu](../modeling/define-a-menu-command-on-a-modeling-diagram.md).<br /><br /> [Vinculado desfazer transações](../modeling/link-uml-model-updates-by-using-transactions.md).|  
||<xref:Microsoft.VisualStudio.Modeling.Validation>|[Validação](../modeling/define-validation-constraints-for-uml-models.md)|  
||(outros namespaces)|Recomendado somente para uso avançado.|  
|Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement>|[Manipuladores de gesto](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md).|  
||(outros namespaces)|Recomendado somente para uso avançado.|  
|Microsoft.VisualStudio.TeamFoundation.WorkItemTracking|<xref:Microsoft.VisualStudio.TeamFoundation.WorkItemTracking>|[Links para itens de trabalho](../modeling/define-a-work-item-link-handler.md).|  
|Microsoft.TeamFoundation.WorkItemTracking.Client|<xref:Microsoft.TeamFoundation.WorkItemTracking.Client>|[Itens de trabalho e seus campos](../modeling/define-a-work-item-link-handler.md).|  
|TeamFoundation|<xref:Microsoft.TeamFoundation.Client>|[Itens de trabalho e seus campos](../modeling/define-a-work-item-link-handler.md).|  
|System.ComponentModel.Composition|<xref:System.ComponentModel.Composition>|[Exportar e importar para componentes de MEF](../modeling/define-and-install-a-modeling-extension.md)|  
|System.Linq|<xref:System.Linq>|[Fácil manipulação de coleções, especialmente ao lidar com relações](../modeling/navigate-relationships-with-the-uml-api.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Referência de API para extensibilidade de modelagem UML](../modeling/api-reference-for-uml-modeling-extensibility.md)




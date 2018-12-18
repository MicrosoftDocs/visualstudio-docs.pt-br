---
title: Diagramas de classe de propriedades de tipos em UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.logicalclassdiagram.shapes.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: 6e1ef2d0-d67a-401a-bd64-d5e034decd2c
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: e8baad41658cc6144f08d0b6b4d415aa4ff6e499
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750108"
---
# <a name="properties-of-types-on-uml-class-diagrams"></a>Propriedades de tipos em diagramas de classes UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de classe UML, uma *tipo* é uma classe, uma interface ou uma enumeração.  
  
> [!NOTE]
>  Este tópico é sobre as propriedades de tipos em diagramas de classe UML. Para mais informações, consulte os seguintes tópicos:  
  
-   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)  
  
-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)  
  
-   [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)  
  
-   [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)  
  
-   [Propriedades de associações em diagramas de classes UML](../modeling/properties-of-associations-on-uml-class-diagrams.md)  
  
## <a name="properties"></a>Propriedades  
 Estas são as propriedades de uma classe, interface ou enumeração.  
  
 Para ver as propriedades de um tipo, com o botão direito do tipo no diagrama ou no **Gerenciador de modelos UML**e, em seguida, clique em **propriedades**. As propriedades aparecem na **propriedades** janela.  
  
|**Property**|**Padrão**|Aparece no|Descrição|  
|------------------|-----------------|----------------|-----------------|  
|**Nome**|Um nome padrão|Todos os elementos|Identifica o elemento.|  
|**Nome qualificado**|Que contém o pacote:: Nome do tipo|Todos os elementos|Identifica exclusivamente o elemento. O nome qualificado do pacote que contém o prefixo.|  
|**Cor**|Padrão para o tipo do tipo|Todos os elementos|A cor dessa forma. Ao contrário das outras propriedades, isso não é uma propriedade do elemento de modelo subjacente. Exibições diferentes do mesmo tipo podem ter cores diferentes.|  
|**É abstrato**|False|Classe|Se for true, a classe não pode ser instanciada e é destinada para uso como uma classe base.|  
|**É folha**|False|Classe, Interface|Se for true, o tipo não deve ter tipos derivados.|  
|**Está ativo**|False|Classe|Se for true, cada instância desse tipo é associada a um thread de controle.|  
|**Visibilidade**|Público|Classe, Interface, enumeração|-Public - visível globalmente.<br />-Private - esse tipo é visível dentro do pacote que ele pertence.<br />-Package - visível dentro do pacote.|  
|**Itens de trabalho**|0 associados|Todos os elementos|O número de itens de trabalho associado a este elemento. Para associar itens de trabalho, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Descrição**|(blank)|Todos os elementos|Você pode fazer observações gerais sobre o item aqui.|  
|**Associação de modelo**|(nenhum)|Classe, Interface, enumeração|Se não estiver vazio, esse tipo é definido ao associar os valores de parâmetro para essa classe de modelo. Expanda a propriedade para ver as associações de parâmetros de modelo.|  
|**Parâmetros de modelo**|(nenhum)|Classe, Interface, enumeração|Se não estiver vazio, isso é uma classe de modelo que tem os parâmetros listados aqui. Para adicionar parâmetros ou exibir as propriedades de parâmetros individuais, clique em **[...]** .|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)   
 [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [Propriedades de associações em diagramas de classe UML](../modeling/properties-of-associations-on-uml-class-diagrams.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)




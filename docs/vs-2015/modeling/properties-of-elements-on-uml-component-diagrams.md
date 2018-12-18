---
title: Propriedades de elementos em diagramas de componente UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.componentdiagram.shapes.properties
helpviewer_keywords:
- component diagrams, properties
- UML, element properties
ms.assetid: fa0a9460-6675-4642-aa00-50f8719a892d
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: fb99ea1efb070c3e79b294bd5d06eedf131623f0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790078"
---
# <a name="properties-of-elements-on-uml-component-diagrams"></a>Propriedades de elementos em diagramas de componente UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de componente UML, cada elemento no diagrama tem propriedades. Para ver as propriedades de um elemento, clique com botão direito do elemento no diagrama ou no **Gerenciador de modelos UML** e, em seguida, clique em **propriedades**. As propriedades aparecem na **propriedades** janela.  
  
> [!NOTE]
>  Este tópico é sobre as propriedades de elementos em diagramas de componente UML. Para obter mais informações sobre como ler diagramas de componente UML, consulte [diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md). Para obter mais informações sobre como desenhar diagramas de componente UML, consulte [diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md).  
  
## <a name="properties-of-elements"></a>Propriedades de elementos  
  
|Propriedade|Padrão|Elemento|Descrição|  
|--------------|-------------|-------------|-----------------|  
|**Nome**|Um nome padrão|Todos|Identifica o elemento.|  
|**Nome qualificado**|Namespace:: nome|Todos|Identifica exclusivamente o elemento.<br /><br /> Um componente ou o nome do tipo é prefixado com o nome qualificado do pacote que o contém.<br /><br /> Uma parte ou o nome da porta é prefixado com o nome qualificado do componente que ele pertence.|  
|**Itens de trabalho**|0 associados|Todos|O número de itens de trabalho associado a este elemento. Para associar itens de trabalho, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Descrição**|(nenhum)|Todos|Você pode fazer observações gerais sobre o elemento aqui.|  
|**Cor**|(padrão para o tipo)|Componente de parte, a delegação, parte de assembly|A cor da forma. Ao contrário de outras propriedades, essa é a cor da forma em vez do elemento de modelo que exibe a forma.|  
|**Is Indirectly Instantiated**|verdadeiro|Componente|O componente existe apenas como um artefato de design. Em tempo de execução, apenas suas partes existem.|  
|**É abstrato**|False|Componente|A definição de componente pode ser usada apenas como uma generalização do que outros componentes podem ser especializados.|  
|**Visibilidade**|Público|Componente de parte, a porta|**Público** - globalmente visível.<br /><br /> **Pacote** - visível dentro do pacote.<br /><br /> **Privada** - visível dentro do componente proprietário.<br /><br /> **Protegido** - visível para componentes derivados do proprietário.|  
|**Tipo**|Criação de tipo|Parte<br /><br /> Porta|O tipo de uma parte é uma classe ou um componente.<br /><br /> O tipo de uma porta é uma interface.|  
|**Multiplicidade**|1|Parte<br /><br /> Porta|Indica quantas instâncias da parte de formulário do tipo especificado do componente pai.<br /><br /> `1` -exatamente um.<br /><br /> `0..1` -um ou nenhum.<br /><br /> `*` -uma coleção de qualquer número.<br /><br /> `n..m` -uma coleção de n a m instâncias.|  
|**É o comportamento**|False|Porta|Se for true, as mensagens para essa porta são manipuladas pelo atividades ou operações que são descritas como parte do componente, em vez de suas partes.|  
|**É o serviço**|False|Porta|Se for true, essa porta é parte da interface publicado deste componente.|  
|**LinkedPackage**|Modelo|Diagrama|O namespace padrão para os elementos adicionados a este diagrama.|  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)




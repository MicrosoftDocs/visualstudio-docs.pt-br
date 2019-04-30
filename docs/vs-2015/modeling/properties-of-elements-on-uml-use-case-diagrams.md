---
title: Propriedades de elementos em UML usam diagramas de caso | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties
- vs.teamarch.usecasediagram.shapes.properties
helpviewer_keywords:
- use case diagrams, properties
ms.assetid: 2728fb26-a275-4fce-8a2c-5a78af6bee04
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b52afab80bc22c03dc5ff980b937cad53869f5db
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444399"
---
# <a name="properties-of-elements-on-uml-use-case-diagrams"></a>Propriedades de elementos em diagramas de caso de uso UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de caso de uso UML, cada elemento no diagrama tem propriedades. Para ver as propriedades de um elemento, clique com botão direito do elemento no diagrama ou no **Gerenciador de modelos UML** e, em seguida, clique em **propriedades**. As propriedades aparecem na **propriedades** janela.  
  
> [!NOTE]
> Este tópico é sobre as propriedades de elementos em diagramas de caso de uso UML. Para obter mais informações sobre como ler diagramas de atividade UML, consulte [diagramas de caso de uso UML: Referência](../modeling/uml-use-case-diagrams-reference.md). Para obter mais informações sobre como desenhar diagramas de atividade UML, consulte [diagramas de caso de uso UML: Diretrizes de](../modeling/uml-use-case-diagrams-guidelines.md).  
  
## <a name="properties-of-elements"></a>Propriedades de elementos  
  
|Propriedade|Padrão|Elemento|Descrição|  
|--------------|-------------|-------------|-----------------|  
|**Nome**|Um nome padrão|Todos|Identifica o elemento.|  
|**Nome qualificado**|Pacote:: Nome|Todos|Identifica exclusivamente o elemento. O nome qualificado do pacote que contém o prefixo.|  
|**Itens de trabalho**|0 associados|Todos|O número de itens de trabalho associado a este elemento. Para associar itens de trabalho, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Descrição**|(nenhum)|Todos|Você pode fazer observações gerais sobre o elemento aqui.|  
|**Cor**|(padrão)|Todos|A cor da forma. Ao contrário de outras propriedades, isso não é uma propriedade do elemento que exibe a forma.|  
|**Caminho da imagem**|(nenhum)|Ator|O caminho do arquivo de uma imagem que deve ser usado em vez do ícone padrão do ator. O ícone deve ser um arquivo de recurso dentro do projeto do Visual Studio.|  
|**Assuntos**|(nenhum)|Caso de uso|O subsistema ou outro tipo que possui o caso de uso.<br /><br /> Você pode defini-lo colocando o caso de uso em um subsistema no diagrama.|  
|**Visibilidade**|Público|Usar o subsistema de caso, o ator,|**Público** - globalmente visível.<br /><br /> **Pacote** - visível dentro do pacote.|  
|**IsAbstract**|False|Usar o subsistema de caso, o ator,|Se for true, o tipo não pode ser instanciado e destina-se como uma base para a especialização por outras definições.|  
|**Is Indirectly Instantiated**|verdadeiro|subsistema|O subsistema existe apenas como um artefato de design. Em tempo de execução, apenas suas partes existem.|  
|**Hiperlink**|(nenhum)|Artefato|O caminho de arquivo ou URL do documento ao qual o artefato fornece um link ou diagrama.|  
  
 Para obter uma lista das propriedades de associações, consulte [diagramas de classe de propriedades de associações em UML](../modeling/properties-of-associations-on-uml-class-diagrams.md).  
  
## <a name="see-also"></a>Consulte também  
 [Diagrama de casos de uso UML: Referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagrama de casos de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)

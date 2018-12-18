---
title: Diagramas de sequência de propriedades de elementos em UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.sequencediagram.combinedfragment.properties
- vs.teamarch.sequencediagram.shapes.properties
helpviewer_keywords:
- UML sequence diagrams, properties
- sequence diagrams, properties
ms.assetid: 475c10f3-a2d2-4a1e-b366-dc28997d437e
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 01d63e39967df361d87ff0182b1c85b6ecd2fdb6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793887"
---
# <a name="properties-of-elements-on-uml-sequence-diagrams"></a>Propriedades de elementos em diagramas de sequência UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de sequência UML, cada elemento no diagrama tem propriedades. Para ver as propriedades de um elemento, clique com botão direito do elemento no diagrama ou no **Gerenciador de modelos UML** e, em seguida, clique em **propriedades**. As propriedades aparecem na **propriedades** janela.  
  
> [!NOTE]
>  Este tópico é sobre as propriedades de elementos em diagramas de sequência UML. Para obter mais informações sobre como ler diagramas de sequência UML, consulte [diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md). Para obter mais informações sobre como desenhar diagramas de sequência UML, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
## <a name="properties-of-elements"></a>Propriedades de elementos  
  
|Propriedade|Padrão|Elemento|Descrição|  
|--------------|-------------|-------------|-----------------|  
|**Nome**|Um nome padrão|Todos|Identifica o elemento.|  
|**Nome qualificado**|Pacote:: nome|Todos|Identifica exclusivamente o elemento. O nome qualificado do pacote que contém o prefixo.|  
|**Itens de trabalho**|0 associados|Todos|O número de itens de trabalho associado a este elemento. Para associar itens de trabalho, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Descrição**|(blank)|Todos|Você pode fazer observações gerais sobre o item aqui.|  
|**Cor**|(padrão para o tipo de elemento)|Linha da vida, mensagens|A cor da forma. Esta é uma propriedade da forma, em vez do elemento é exibido.|  
|**Tipo**|(blank)|Linha de vida|O tipo da instância que representa a linha da vida.<br /><br /> Se houver um símbolo de referência exibido no cabeçalho da linha de vida, em seguida, dessa classe ou interface existe separadamente no Gerenciador de modelos UML e pode ser exibido em um diagrama de classe.|  
|**Ator**|False|Linha de vida|Indica se a linha da vida representa um componente de usuário, dispositivo ou software que é externo ao componente que trata do diagrama.|  
|**Tipo**|**Completa** -uma mensagem que tem o remetente e destinatário.<br /><br /> **Encontrado** -uma mensagem que tem um remetente não especificado.<br /><br /> **Perdido** -uma mensagem que tem um receptor não especificado.|Mensagem|Indica quais extremidades de uma mensagem anexadas a uma linha da vida.<br /><br /> Você não pode alterar essa propriedade. Ele é definido quando você cria a mensagem.|  
|**Classificação**|**AsynchCall** -uma mensagem assíncrona.<br /><br /> **SynchCall** -uma mensagem síncrona.<br /><br /> **Resposta** -a parte de retornada de uma mensagem síncrona.<br /><br /> **CreateMessage** -uma mensagem de criação de instância.|Mensagem|O tipo de mensagem. Você não pode alterar essa propriedade. Ele é determinado pela ferramenta que você use para criar a mensagem.|  
|**operação**|(vazio)|Mensagem|Um método chamado pela mensagem na linha de vida de recebimento.<br /><br /> Visível somente se a linha de vida de recebimento estiver vinculada a uma interface ou classe.|  
|**Refere-se ao**|Um diagrama de sequência|Uso da interação|O diagrama de sequência chamado pelo uso dessa interação.|  
|**Operador de interação**|Definido quando você tiver usado o **envolver com** comando|Fragmento combinado|O operador representado por este fragmento ou uma coleção de fragmentos.|  
|**Guard**|(vazio)|Operando de interação em um fragmento combinado|A sequência no fragmento não ocorrerá, a menos que o protetor é true.<br /><br /> Para selecionar o fragmento superior de qualquer fragmento combinado, clique abaixo do título do fragmento.|  
|**Mín., máx.**|(sem restrição)|Executar um loop fragmento combinado|O número mínimo e máximo de vezes que o loop é executado.|  
|**Mensagens**|(vazio)|Considere e<br /><br /> Ignorar fragmentos combinados|As mensagens que são consideradas ou ignoradas neste fragmento.|  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)   
 [Descrever o fluxo de controle com fragmentos em diagramas de sequência UML](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md)




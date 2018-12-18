---
title: Personalizando ferramentas de elemento | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6dac48b6-db68-4bcd-8aa2-422c2ad5d28b
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: cf2d48ee0ec4c8f2f9986f4655eb98b44583beef
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49220500"
---
# <a name="customizing-element-tools"></a>Ferramentas de elemento personalizadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em algumas definições de DSL, você pode representar um conceito único como um grupo de elementos. Por exemplo, se você criar um modelo no qual um componente tem um conjunto fixo de portas, você sempre queira as portas a serem criados ao mesmo tempo como seu componente pai. Portanto, você precisa personalizar a ferramenta de criação de elemento para que ele cria um grupo de elementos em vez de apenas um. Para fazer isso, você pode personalizar como a ferramenta de criação de elemento é inicializada.  
  
 Você também pode substituir o que acontece quando a ferramenta é arrastada para o diagrama ou um elemento.  
  
## <a name="customizing-the-content-of-an-element-tool"></a>Personalizar o conteúdo de uma ferramenta de elemento  
 Cada ferramenta do elemento armazena uma instância de um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> (EGP), que contém uma versão serializada de um ou mais elementos de modelo e links. Por padrão, o EGP de uma ferramenta de elemento contém uma instância da classe que você especificar para a ferramenta. Você pode alterar isso substituindo *YourLanguage*`ToolboxHelper.CreateElementToolPrototype`. Esse método é chamado quando o pacote DSL é carregado.  
  
 Um parâmetro do método é a ID da classe que você especificou na definição de DSL. Quando o método é chamado com a classe que você está interessado, você pode adicionar elementos adicionais no EGP.  
  
 O EGP deve incluir links de um elemento principal para os elementos da subsidiária de incorporação. Ele também pode incluir links de referência.  
  
 O exemplo a seguir cria um elemento principal e dois elementos incorporados. A classe principal é chamada Resistor, e ele tem duas relações de incorporação para elementos nomeados de Terminal. As propriedades da função de inserção são nomeadas Terminal1 e Terminal2 e ambos tenham uma multiplicidade de 1..1.  
  
```  
using Microsoft.VisualStudio.Modeling; ...    
public partial class CircuitDiagramToolboxHelper  
{  
  protected override ElementGroupPrototype    CreateElementToolPrototype(Store store, Guid domainClassId)  
  {  
    // A case for each tool to customize:    
    if (domainClassId == Resistor.DomainClassId)  
    {  
      // Set up the prototype elements and links:  
      Resistor resistor = new Resistor(store);  
      resistor.Terminal1 = new Terminal(store);   
      resistor.Terminal2 = new Terminal(store);  
      resistor.Terminal1.Name = "T1"; // embedding  
      resistor.Terminal2.Name = "T2"; // embedding  
      // We could also set up reference links.  
  
      // Create an element group prototype for the toolbox:  
      ElementGroup egp = new ElementGroup(store.DefaultPartition);  
      egp.AddGraph(resistor, true);  
      // We do not have to explicitly include embedded children.  
      return egp.CreatePrototype();  
    }  
    // Element tools for other classes:  
    else  
      return base.CreateElementToolPrototype(store, domainClassId);  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando a criação e o movimento de elementos](../modeling/customizing-element-creation-and-movement.md)




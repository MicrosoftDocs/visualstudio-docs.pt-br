---
title: Definindo formas e conectores | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fae548d-9288-4dd5-a24f-ff0d69c73628
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 61cd27b307b4761e3f7773f91583965466892285
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812940"
---
# <a name="defining-shapes-and-connectors"></a>Definindo formas e conectores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Há diversos tipos básicos de formas possíveis de serem usados para exibir informações em um diagrama em uma linguagem específica do domínio (DSL).  
  
##  <a name="shapeTypes"></a> Tipos básicos de formas e conectores  
 Um diagrama DSL mostra uma coleção de *formas* interconectadas por linhas ou *conectores*.  Geralmente, mas não sempre:  
  
- As formas são representações visíveis dos elementos de modelo.  
  
- Os conectores representam as relações de referência.  
  
- O diagrama representa a instância da raiz do modelo.  
  
- Relações de incorporações entre os elementos de modelo são mostradas por confinamento. Por exemplo, os elementos que representam portas de componentes são incorporados no componente.  
  
  Esses padrões não são impostos, mas têm melhor suporte. Quando você projetar uma DSL, tenha em mente que o design das relações de incorporação deve ser influenciado por como você deseja apresentar o modelo na tela. Por outro lado, as relações de referência devem refletir os conceitos de seu domínio dos negócios.  
  
  Os seguintes tipos de formas estão disponíveis:  
  
|Tipo de forma|Descrição|  
|----------------|-----------------|  
|Forma geométrica|Forma retangular ou elíptica de propósito geral. É possível exibir o texto e os decoradores de ícones em posições específicas relativas aos limites da forma.<br /><br /> Para aninhar formas dentro das formas geométricas, consulte [aninhar formas](../modeling/nesting-shapes.md).|  
|Forma do compartimento|Retângulo contendo um cabeçalho e compartimentos, com uma classe UML. Cada compartimento pode conter uma lista de linhas de texto.<br /><br /> As linhas geralmente representam elementos incorporados sob o elemento representado pela forma. Por exemplo, criar uma DSL a partir de um modelo de solução de Diagramas de Classe.|  
|Forma da imagem|Forma que exibe uma imagem.|  
|Forma da porta|Um pequeno retângulo projetado para anexar o esboço de outra forma. Geralmente usado em modelos do componente.<br /><br /> O elemento de modelo representado por uma porta normalmente é incorporado sob o elemento representado pela forma pai. Por exemplo, criar uma DSL usando o modelo de solução de Componentes.<br /><br /> Por padrão, uma forma de porta pode deslizar ao longo das laterais de seu pai. É possível definir uma Regra de Associação para restringi-la a uma determinada posição.<br /><br /> Fazendo uma forma de porta muito pequena e transparente, é possível usá-la para fornecer um ponto de conexão fixo na superfície da sua forma pai.|  
|Raias|Partição de raias de um diagrama em segmentos horizontais ou verticais. A raia sempre permanece abaixo de outras formas no diagrama.<br /><br /> Geralmente, os elementos de modelo da raia são criados na raiz do modelo e outros elementos são criados neles. Por exemplo, criar uma DSL a partir de um modelo de solução de Fluxo de Tarefa.|  
|Conectores|As linhas desenhadas entre as formas normalmente representam relações de referência. É possível ajustar opções para tornar um conector reto ou retilíneo e para ter diferentes tipos de seta.|  
  
##  <a name="shapeInheritance"></a> Herança da forma  
 Uma forma pode ser herdeira de outra forma. No entanto, as formas devem ser do mesmo tipo. Por exemplo, somente uma forma geométrica pode ser herdeira de uma forma geométrica. Formas herdadas possuem os compartimentos e decoradores de sua forma de base. Os conectores podem ser herdeiros dos conectores.




---
title: Sintaxe do caminho do domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, domain path
ms.assetid: 945994f9-72b9-42e0-81b2-e5fb3d0e282d
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: d4e98715bae8869619e8d9f2852c810153984777
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49254768"
---
# <a name="domain-path-syntax"></a>Sintaxe do caminho de domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As definições de DSL usam uma sintaxe semelhante a XPath para localizar elementos específicos em um modelo.  
  
 Normalmente, não é necessário trabalhar com essa sintaxe diretamente. Caso ela aparecer na janela Detalhes de DSL ou Propriedades, você pode clicar na seta para baixo e usar o editor de caminho. No entanto, o caminho aparecerá nesta forma no campo depois de você ter usado o editor.  
  
 Um caminho de domínio tem a seguinte forma:  
  
 *RelationshipName.PropertyName/!Role*  
  
 ![Relação de referência CommentReferencesSubjects](../modeling/media/dsl-reference.png "dsl_reference")  
  
 A sintaxe percorre a árvore do modelo. Por exemplo, a relação de domínio **CommentReferencesSubjects** na ilustração acima tem um **assuntos** função. O segmento de caminho **/! Subjectt** Especifica que o caminho termina em elementos acessados por meio de **assuntos** função.  
  
 Cada segmento inicia com o nome de uma relação de domínio. Se a passagem for de um elemento em uma relação, o segmento de caminho aparecerá como *Relationship*. Se o salto for de um link para um elemento, o segmento de caminho é exibido como *relação /! RoleName*.  
  
 Barras separam a sintaxe de um caminho. Cada segmento de caminho é um salto de um elemento para um link (uma instância de uma relação) ou de um link para um elemento. Os segmentos de caminho normalmente aparecem em pares. Um segmento de caminho representa um salto de um elemento para um link e o próximo segmento representa um salto do link para o elemento na outra extremidade. (Qualquer link também pode ser a origem ou destino de uma relação).  
  
 O nome que você usa para o salto do elemento ao link é o valor de `Property Name` da função. O nome que você usa para o salto do link ao elemento é o nome da função de destino.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)




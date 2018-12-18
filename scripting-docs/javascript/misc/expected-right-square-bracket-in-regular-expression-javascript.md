---
title: Esperado &#39;]&#39; na expressão regular (JavaScript) | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- javascript
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.WebClient.Help.SCRIPT5019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1ca2079a-44dd-479f-a1e3-e04a14d0739e
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 64ef929ba309f0b496e72f3cf740daf6970d08fb
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44283711"
---
# <a name="expected-3939-in-regular-expression-javascript"></a>Esperado &#39;]&#39; na expressão regular (JavaScript)
Você tentou criar uma classe de caractere para uma correspondência de expressão regular, mas não incluiu o colchete direito. Combinações de caracteres literal individuais podem ser montadas em classes de caracteres, colocando-os entre colchetes. Uma classe de caracteres corresponde a qualquer caractere que ele contém. Por exemplo, / [abc] corresponde a qualquer uma das letras "a", "b", ou "c".  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Adicione o colchete direito à expressão regular.  
  
    > [!NOTE]
    >  Se você deseja corresponder a um único colchete, isolá-lo com uma barra invertida - \\[, então ele não será interpretado como um caractere especial por [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de expressão regular](../../javascript/reference/regular-expression-object-javascript.md)   
 [Sintaxe de expressão regular (JavaScript)](https://msdn.microsoft.com/library/1400241x)
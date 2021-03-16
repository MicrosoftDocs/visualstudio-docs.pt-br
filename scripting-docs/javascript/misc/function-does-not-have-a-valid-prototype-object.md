---
description: Você tentou usar o instanceof para determinar se um objeto foi derivado de uma classe de função específica, mas você redefiniu a propriedade de protótipo do objeto como NULL ou um tipo de objeto externo (não objetos JavaScript válidos).
title: A função não tem um objeto de protótipo válido | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0356ac9ef7c63c77c0cc0dfca623ff24d3de24af
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571409"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>A função não tem um objeto de protótipo válido
Você tentou usar o **instanceof** para determinar se um objeto foi derivado de uma classe de função específica, mas redefiniu a propriedade do objeto `prototype` como `null` ou um tipo de objeto externo (não objetos válidos [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] ). Um objeto externo pode ser um objeto do modelo de objeto de host (por exemplo, o documento ou o objeto de janela do Internet Explorer) ou um objeto COM externo.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a propriedade da função `prototype` se refere a um [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] objeto válido.  
  
## <a name="see-also"></a>Confira também  
 [Objeto de função](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [Propriedade prototype (Object)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)

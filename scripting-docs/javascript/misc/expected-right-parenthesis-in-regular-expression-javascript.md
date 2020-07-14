---
title: Esperado ') ' na expressão regular (JavaScript) | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5020
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 2087ba1d-9783-4d40-b609-e8542f579f7f
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: af32127476c83100c0340021428e3abc572ef2f7
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815630"
---
# <a name="expected--in-regular-expression-javascript"></a>')' esperado na expressão regular (JavaScript)
Você tentou criar uma captura de expressão regular, asserção ou grupo, mas não incluiu o parêntese de fechamento. Os parênteses têm várias finalidades em expressões regulares. Principalmente, eles são usados para capturar subexpressãos, para especificar asserções ou agrupar padrões para que os itens possam ser tratados como uma única unidade por *, +,? e assim por diante.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione os parênteses de fechamento mais à direita.  
  
    > [!NOTE]
    > Se você quiser corresponder a um único parêntese, escape-o com uma barra invertida \\ (-para que ele não seja interpretado como um caractere especial [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] .  
  
## <a name="see-also"></a>Veja também  
 [Objeto de expressão regular](../../javascript/reference/regular-expression-object-javascript.md)   
 [Sintaxe de expressão regular (JavaScript)](https://msdn.microsoft.com/library/1400241x)
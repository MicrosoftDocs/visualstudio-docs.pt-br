---
title: Booliano esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5010
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 35d71b7f-53fd-44c4-a7c7-b1550c65cfd4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4dbb7e55f6afe6d3edfe4e98749807732ffa05ac
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817665"
---
# <a name="boolean-expected"></a>Booliano esperado
Você tentou invocar o método **booliano. prototype. ToString** ou **booliano. prototype. valueOf** em um objeto de um tipo diferente de `Boolean` . O objeto deste tipo de invocação deve ser do tipo `Boolean` . Por exemplo:

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Invocar apenas os métodos **Boolean. prototype. ToString** ou **Boolean. prototype. valueOf** em objetos do tipo **booliano.**

## <a name="see-also"></a>Veja também

- [Objeto Boolean](../../javascript/reference/boolean-object-javascript.md)
- [Tipos de dados](../../javascript/data-types-javascript.md)
- [Controlar o fluxo de programas](../../javascript/controlling-program-flow-javascript.md)
- [Copiar, passar e comparar dados](../../javascript/advanced/copying-passing-and-comparing-data-javascript.md)
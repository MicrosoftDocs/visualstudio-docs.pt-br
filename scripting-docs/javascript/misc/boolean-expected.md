---
title: Booliano esperado | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5010
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 35d71b7f-53fd-44c4-a7c7-b1550c65cfd4
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cb8ec8f7244b98cfa628794b485859dbec611c19
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868086"
---
# <a name="boolean-expected"></a>Booliano esperado
Você tentou invocar o **Boolean.prototype.toString** ou **Boolean.prototype.valueOf** método em um objeto de um tipo diferente de `Boolean`. O objeto desse tipo de invocação deve ser do tipo `Boolean`. Por exemplo:

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Invoque apenas o **Boolean.prototype.toString** ou **Boolean.prototype.valueOf** métodos em objetos do tipo **booliano.**

## <a name="see-also"></a>Consulte também

- [Objeto Boolean](../../javascript/reference/boolean-object-javascript.md)
- [Tipos de Dados](../../javascript/data-types-javascript.md)
- [Controlar o fluxo de programas](../../javascript/controlling-program-flow-javascript.md)
- [Copiar, passar e comparar dados](../../javascript/advanced/copying-passing-and-comparing-data-javascript.md)
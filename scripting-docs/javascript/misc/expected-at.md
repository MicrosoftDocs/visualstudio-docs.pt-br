---
title: Esperado ' @ ' | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1032
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 82ff8b74-1710-4358-9a26-dc92ab29c53b
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 209a8793c0940511b7ecb2abb32f537a614ebf8b
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814818"
---
# <a name="expected-"></a>Esperado ' \@ '
Você tentou criar uma variável a ser usada com instruções de compilação condicional usando a `@set` instrução, mas não localizou um sinal de arroba " **@** " antes do nome da variável.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione um sinal de arroba " **@** " imediatamente antes do nome da variável. Por exemplo:  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>Confira também  
 [@setPrivacidade](../../javascript/reference/at-set-statement-javascript.md)   
 [Compilação condicional](../../javascript/advanced/conditional-compilation-javascript.md)   
 [Variáveis de compilação condicional](../../javascript/advanced/conditional-compilation-variables-javascript.md)

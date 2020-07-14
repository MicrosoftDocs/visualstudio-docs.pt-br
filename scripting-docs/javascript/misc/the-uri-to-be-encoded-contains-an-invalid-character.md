---
title: O URI a ser codificado contém um caractere inválido | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5024
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: a3f0fdbb-8d4b-41ae-a396-43dfc9483760
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6091968dcbdd98240b1705e0fa7dc855dad3bda
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816066"
---
# <a name="the-uri-to-be-encoded-contains-an-invalid-character"></a>O URI a ser decodificado contém um caractere inválido
Você tentou codificar uma cadeia de caracteres como um URI (Uniform Resource Identifier), mas ele continha caracteres inválidos. Embora a maioria dos caracteres sejam válidos dentro de cadeias para serem convertidas em URIs, algumas sequências de caracteres Unicode são ilegais.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a cadeia de caracteres a ser codificada contém apenas sequências Unicode válidas. Um URI completo é composto de uma sequência de componentes e separadores. Os nomes entre colchetes angulares representam componentes e ":", "/", ";" e "?" são caracteres reservados usados como separadores. A forma geral é:  
  
    ```JavaScript  
    <Scheme>:<first>/<second>;<third>?<fourth>  
    ```  
  
## <a name="see-also"></a>Veja também  
 [Função encodeURI](../../javascript/reference/encodeuri-function-javascript.md)   
 [Função encodeURIComponent](../../javascript/reference/encodeuricomponent-function-javascript.md)
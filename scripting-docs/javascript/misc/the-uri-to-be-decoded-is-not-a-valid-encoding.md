---
title: O URI a ser decodificado não tem uma codificação válida | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5025
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 029e0790-ffd1-496d-8700-3b3dbac1b6fd
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2d37ca55dfd701aaeba2af729511a5ae6a4fa5f4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49841813"
---
# <a name="the-uri-to-be-decoded-is-not-a-valid-encoding"></a>O URI a ser decodificado não tem uma codificação válida
Tentativa de decodificar um formada incorretamente URI (Uniform Resource Identifier). URIs têm uma sintaxe especial; a maioria dos caracteres não alfanuméricos devem ser codificados antes que possam ser usados em um URI. Você pode usar o `encodeURI` e `encodeURIComponent` métodos para criar um URI de um normal [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] cadeia de caracteres.  
  
 Um URI completo é composto de uma sequência de componentes e separadores. O formato geral é:  
  
```JavaScript  
<Scheme>:<first>/<second>;<third>?<fourth>  
```  
  
 Os nomes entre colchetes angulares representam os componentes e o ":", "/", ";" e "?" são caracteres reservados usados como separadores.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Certifique-se de que você está tentando decodificar apenas URIs válidos. Você não consegue decodificar normal [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] cadeias de caracteres, como eles podem conter caracteres inválidos.  
  
## <a name="see-also"></a>Consulte também  
 [Função decodeURI](../../javascript/reference/decodeuri-function-javascript.md)   
 [Função DecodeURIComponent](../../javascript/reference/decodeuricomponent-function-javascript.md)
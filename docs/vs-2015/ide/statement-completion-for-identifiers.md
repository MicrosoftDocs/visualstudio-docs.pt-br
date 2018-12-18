---
title: Preenchimento de declaração para identificadores | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IntelliSense [JavaScript], statement completion
- statement completion, JavaScript IntelliSense
ms.assetid: c2cd4945-c67e-471b-8057-96cfd25f7fb2
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d58c5ecc1d787195f7f5c91a07da7a4e775fc27e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49827045"
---
# <a name="statement-completion-for-identifiers"></a>Conclusão de instrução para identificadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript não permite explícita de digitação para declarações de variável. Como resultado, o IntelliSense sempre não pode fornecer listas de conclusão para objetos. Isso pode ocorrer em várias situações. A seguir estão alguns problemas comuns.  
  
- Um parâmetro é declarado, mas ele não foi chamado em outro lugar no documento ativo, conforme mostrado no exemplo a seguir.  
  
  ```javascript  
  function illuminate(light) {  
           light.  // Accurate statement completion is not available   
                   // unless illuminate is called elsewhere with a   
                   // parameter that has a value. If it is called only  
                   // in a function that is a sibling to   
                   // illuminate(light) in the call hierarchy, the   
                   // IntelliSense engine also cannot determine the   
                   // parameter type.  
       }  
  
  // Sibling function. No statement completion for light   
  // object in preceding code.  
  function lightLamp() {  
      var x = illuminate(1);  
  }  
  
  // Uncomment the next line to obtain statement completion for  
  // light object in preceding code.  
  // var x = illuminate(1);  
  ```  
  
- Um objeto está em uma função que é chamada em resposta a um evento. Em tempo de design, o mecanismo IntelliSense não é possível determinar o tipo dos objetos usados nesta situação.  
  
   Se o mecanismo IntelliSense pode determinar que o evento deve ser chamado, normalmente através do uso de `addEventListener` para o evento no documento ativo, as informações mais precisas do IntelliSense são fornecidas.  
  
  Quando o IntelliSense não é possível identificar um objeto, o mecanismo IntelliSense preenche a lista de conclusão com entidades nomeadas ou identificadores, que estão presentes no documento ativo. Quando a lista de conclusão contém esses identificadores, ícones de informações aparecem ao lado deles. Além disso, uma dica de ferramenta para cada identificador indica que a expressão é desconhecida. A ilustração a seguir mostra as opções de preenchimento para um objeto do tipo de instrução `light` que não pode ser identificado como o objeto e suas propriedades são indefinidas. No entanto, o `intensity` propriedade está disponível na lista de identificador porque ele tem sido usado no `illuminate` função.  
  
  **Opções de preenchimento para um objeto que não pode ser identificado**  
  
  ![IntelliSense de JavaScript para identificadores](../ide/media/js-intellisense-identifiers.png "js_intellisense_identifiers")  
  
  Você pode substituir a lista de preenchimento para um objeto usando comentários de documentação XML ou recursos de extensibilidade JavaScript IntelliSense. Usar esses recursos, você pode fornecer informações de IntelliSense mais descritivas e informações de tipo quando ele pode não estar disponível. Para obter mais informações, consulte [Estendendo JavaScript IntelliSense](../ide/extending-javascript-intellisense.md) e [criar comentários da documentação XML](../ide/create-xml-documentation-comments-for-javascript-intellisense.md).  
  
## <a name="see-also"></a>Consulte também  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)




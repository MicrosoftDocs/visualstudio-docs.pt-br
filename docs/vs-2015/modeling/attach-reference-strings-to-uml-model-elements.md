---
title: Anexar cadeias de caracteres de referência a elementos de modelo UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending, reference strings
ms.assetid: 15dbed99-efce-42fe-a768-714a5804e7d1
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: cf8a9e7e023e9c75f61fdf9a6bfb608edc3a7123
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51804573"
---
# <a name="attach-reference-strings-to-uml-model-elements"></a>Anexar cadeias de caracteres de referência a elementos de modelo UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode escrever código para anexar cadeias de caracteres arbitrárias para elementos de modelo. Uma cadeia de caracteres pode ser, por exemplo, um URI, o resultado em cache de um cálculo ou uma referência do ModelBus para um elemento em outro modelo. Cada cadeia de caracteres está contida em um objeto IReference. Qualquer número de objetos IReference pode ser anexado a cada elemento de modelo.  
  
 Cada objeto IReference tem um nome. Você pode usar esse nome para indicar como o valor de referência deve ser interpretado. Por exemplo, você pode definir o nome para "URI" para indicar que o valor deve ser interpretado como um URI. Há alguns valores de nome de referência predefinidos usadas pelas ferramentas de modelagem.  
  
## <a name="attaching-a-reference-to-an-ielement"></a>Anexar uma referência a um IElement  
 Para usar os métodos a seguir, você deve adicionar uma referência a:  
  
 Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll  
  
 Você deve inserir esta diretiva em seu código:  
  
 `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
|Chamada de método|Descrição|  
|-----------------|-----------------|  
|`element.AddReference (nameString, valueString, duplicatesAllowed)`|Cria uma `IReference` com o nome fornecido e cadeias de caracteres de valor e o vincula ao `element`. Retorna o `IReference`.<br /><br /> Gera uma exceção se `duplicatesAllowed` é false e já houver uma `IReference` com o mesmo nome anexado a `element`.|  
|`element.GetReferences(name)`|Retorna todos os as `IReference` objetos vinculados `element` que têm o determinado `name`.|  
|`element.DeleteAllReferences(name)`|Exclui todas as `IReference` objetos vinculados ao elemento que tem o nome fornecido.|  
|`reference.Delete()`|Exclui essa `IReference`.|  
|`ReferenceConstants.WorkItem`|O valor usado para referências de nome do item de trabalho.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir um manipulador de link de item de trabalho](../modeling/define-a-work-item-link-handler.md)   
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)




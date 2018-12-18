---
title: Uma ou mais propriedades no arquivo .ofs não são válidas para a classe de mensagem selecionada
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cfae8533337bbe18c89dbb670fb58a0c89c6c54c
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34692493"
---
# <a name="one-or-more-properties-in-the-ofs-file-are-not-valid-for-the-message-class-selected"></a>Uma ou mais propriedades no arquivo .ofs não são válidas para a classe de mensagem selecionada
  Esse erro aparece quando você importa uma região de formulário projetada no Outlook, mas um ou mais campos na região de formulário não são compatíveis com as classes de mensagem que você selecionar na página final do **nova região de formulário** assistente.  

Por exemplo, você pode selecionar **tarefa (IPM. Tarefa)** na página final do **nova região de formulário** assistente. Se a região de formulário tem uma **endereço comercial** campo, você receberá esse erro porque uma tarefa não tem um endereço de negócios. Portanto, o **endereço comercial** campo não é compatível com o `IPM.Task` classe da mensagem.  
  
 Você pode selecionar **tarefa (IPM. Tarefa)** na página final do **nova região de formulário** assistente. Se a região de formulário tem uma **endereço comercial** campo, você receberá esse erro porque uma tarefa não tem um endereço de negócios. Portanto, o **endereço comercial** campo não é compatível com o `IPM.Task` classe da mensagem.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Na página final do **nova região de formulário** assistente, selecione a classe de mensagem que é compatível com os campos na região de formulário.  
  
-   No Designer de formulários no Outlook, remova os campos que não são compatíveis com as classes de mensagem. Remover os campos que você planeja para selecionar a página final de **nova região de formulário** assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Importar uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)  
  
  
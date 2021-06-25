---
title: Enumerador de mensagens | Microsoft Docs
description: Os membros desse enumerador são usados para a função TEXTOUTPROC, que é uma função de retorno de chamada que o IDE fornece quando chama o SccOpenProject.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77c49f79ccdcfc4aa0325b89dfb38f3f8d4da721
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902586"
---
# <a name="message-enumerator"></a>Enumerador de mensagem
Os sinalizadores a seguir são usados para a função , que é uma função de retorno de chamada que o IDE fornece quando chama `TEXTOUTPROC` [o SccOpenProject](../extensibility/sccopenproject-function.md) (consulte [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) para obter detalhes sobre a função de retorno de chamada).

 Se o IDE for solicitado a cancelar o processo, ele poderá receber uma das mensagens de cancelamento. Nesse caso, o plug-in de controle do código-fonte usa `SCC_MSG_STARTCANCEL` para pedir ao IDE para exibir o **botão** Cancelar. Depois disso, qualquer conjunto de mensagens normais pode ser enviado. Se algum deles retornar `SCC_MSG_RTN_CANCEL` , o plug-in encerrará a operação e retornará. O plug-in também `SCC_MSG_DOCANCEL` sonda periodicamente para determinar se o usuário cancelou a operação. Quando todas as operações são feitas ou se o usuário tiver cancelado, o plug-in enviará `SCC_MSG_STOPCANCEL` . Os tipos , SCC_MSG_WARNING e SCC_MSG_ERROR são usados para mensagens exibidas na `SCC_MSG_INFO` lista de rolagem de mensagens. `SCC_MSG_STATUS` é um tipo especial que indica que o texto deve aparecer em uma barra de status ou área de exibição temporária. Ele não permanece permanentemente na lista.

## <a name="syntax"></a>Sintaxe

```
enum { 
   SCC_MSG_RTN_CANCEL = -1, 
   SCC_MSG_RTN_OK = 0, 
   SCC_MSG_INFO = 1 
   SCC_MSG_WARNING, 
   SCC_MSG_ERROR, 
   SCC_MSG_STATUS, 
   SCC_MSG_DOCANCEL, 
   SCC_MSG_STARTCANCEL, 
   SCC_MSG_STOPCANCEL 
};
```

## <a name="members"></a>Membros
 SCC_MSG_RTN_CANCEL retornar do retorno de chamada para indicar o cancelamento.

 SCC_MSG_RTN_OK retornar do retorno de chamada para continuar.

 SCC_MSG_INFO Mensagem é informacional.

 SCC_MSG_WARNING Mensagem é um aviso.

 SCC_MSG_ERROR Mensagem é um erro.

 SCC_MSG_STATUS Mensagem é destinada à barra de status.

 SCC_MSG_DOCANCEL sem texto; O IDE retorna `SCC_MSG_RTN_OK` ou `SCC_MSG_RTN_CANCEL` .

 SCC_MSG_STARTCANCEL Inicia um loop de cancelamento.

 SCC_MSG_STOPCANCEL interrompe o loop de cancelamento.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)

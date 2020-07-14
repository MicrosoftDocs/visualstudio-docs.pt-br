---
title: IActiveScriptParseProcedure32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 387a856b-f5dc-4371-8620-bd574e046c2c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 16d432b6c150b53fdd059a48cc683d240bd1a50a
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835297"
---
# <a name="iactivescriptparseprocedure32"></a>IActiveScriptParseProcedure32
Se o mecanismo de script do Windows permitir que o texto do código-fonte de procedimentos seja adicionado ao script, ele implementará a `IActiveScriptParseProcedure32` interface. Para linguagens de script interpretadas que não têm um ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IActiveScriptParse32` ou `IPersist` *) para adicionar procedimentos de script ao namespace.  
  
## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable  
  
|||  
|-|-|  
|Método|Descrição|  
|[IActiveScriptParseProcedure32::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure32-parseproceduretext.md)|Analisa o procedimento de código fornecido e adiciona o procedimento ao namespace.|  
  
## <a name="see-also"></a>Confira também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)
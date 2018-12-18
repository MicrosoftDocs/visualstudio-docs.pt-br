---
title: IActiveScriptParseProcedure32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 387a856b-f5dc-4371-8620-bd574e046c2c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 8cd253db8cb63adad093b84c4bf47df07bd66d69
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645866"
---
# <a name="iactivescriptparseprocedure32"></a>IActiveScriptParseProcedure32
Se o mecanismo de Script do Windows permite que o texto do código de origem para obter os procedimentos a serem adicionados ao script, ele implementa o `IActiveScriptParseProcedure32` interface. Interpretado para linguagens de scripts com nenhum ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IActiveScriptParse32` ou `IPersist`*) para adicionar os procedimentos de script ao namespace.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|||  
|-|-|  
|Método|Descrição|  
|[IActiveScriptParseProcedure32::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure32-parseproceduretext.md)|Analisa o procedimento de código fornecido e adiciona o procedimento para o namespace.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)
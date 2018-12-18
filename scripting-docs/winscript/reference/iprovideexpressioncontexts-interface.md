---
title: Interface IProvideExpressionContexts | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IProvideExpressionContexts interface
ms.assetid: e4c70f2c-7d86-4fdc-a1cb-f5a0bb8ed037
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 402b439da6f1fa369accacb27f987ac77119e343
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728096"
---
# <a name="iprovideexpressioncontexts-interface"></a>Interface IProvideExpressionContexts
Fornece uma maneira de enumerar os contextos de expressão conhecidos por um determinado componente. Mecanismos de script geralmente implementam essa interface.  
  
 O Gerenciador de depuração do processo usa essa interface para localizar todos os contextos de expressão global associados a um determinado thread.  
  
> [!NOTE]
>  Essa interface é chamada de segmento de interesse. Cabe implementador para identificar a thread atual e retorna um enumerador apropriado.  
  
## <a name="methods"></a>Métodos  
 Além dos métodos herdados de `IUnknown`, o `IProvideExpressionContexts` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IProvideExpressionContexts::EnumExpressionContexts](../../winscript/reference/iprovideexpressioncontexts-enumexpressioncontexts.md)|Retorna um enumerador de contextos de expressão conhecido por este componente.|
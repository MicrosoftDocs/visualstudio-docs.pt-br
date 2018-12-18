---
title: Interface IActiveScriptParseProcedureOld | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld interface
ms.assetid: d94b391e-4c24-46da-a01f-2c134ca4f041
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 99cff9cd4d04c5d25489b6cc4c9b9af93792dc2a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724416"
---
# <a name="iactivescriptparseprocedureold-interface"></a>Interface IActiveScriptParseProcedureOld
Permite que o texto do código de origem para obter os procedimentos a serem adicionados ao script. Interpretado para linguagens de scripts que não têm um ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IActiveScriptParse` ou `IPersist*`) para adicionar os procedimentos de script para o espaço de nome.  
  
> [!NOTE]
>  Essa interface é preterida em favor do `IActiveScriptParseProcedure` interface.  
  
## <a name="methods"></a>Métodos  
 Além dos métodos herdados de `IUnknown`, o `IActiveScriptParseProcedureOld` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptParseProcedureOld::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedureold-parseproceduretext.md)|Analisa o procedimento de código fornecido e adiciona o procedimento para o espaço de nome.|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParseProcedure](../../winscript/reference/iactivescriptparseprocedure.md)
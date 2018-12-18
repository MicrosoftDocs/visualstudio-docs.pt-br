---
title: IActiveScriptParseProcedure | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptParseProcedure interface
ms.assetid: 741a35bb-5b92-489e-ba8a-a406b42125fc
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 77aaa60942855a71f7d71037fbefb06462336a13
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724376"
---
# <a name="iactivescriptparseprocedure"></a>IActiveScriptParseProcedure
Se o mecanismo de Script do Windows permite que o texto do código de origem para obter os procedimentos a serem adicionados ao script, ele implementa o `IActiveScriptParseProcedure` interface. Interpretado para linguagens de scripts com nenhum ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IActiveScriptParse` ou `IPersist`*) para adicionar os procedimentos de script ao namespace.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|||  
|-|-|  
|Método|Descrição|  
|[IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)|Analisa o procedimento de código fornecido e adiciona o procedimento para o namespace.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)
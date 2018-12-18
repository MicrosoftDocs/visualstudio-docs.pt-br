---
title: Interface IActiveScriptSiteDebug32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 03f42217-303d-46e7-9792-61a5ab95252c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: a752851aa6afd903747dc58fed79d2bc5b27e3e8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725116"
---
# <a name="iactivescriptsitedebug32-interface"></a>Interface IActiveScriptSiteDebug32
Hosts inteligentes implementam a `IActiveScriptSiteDebug32` para executar o gerenciamento de documentos e participem de depuração. O `IActiveScriptSite` objeto normalmente fornece uma implementação de `IActiveScriptSiteDebug32` interface. Se isso for feito, chame o `IActiveScriptSite::QueryInterface` método para obter o `IActiveScriptSiteDebug32` interface.  
  
 Além dos métodos herdados de `IUnknown`, o `IActiveScriptSiteDebug32` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptSiteDebug32::GetApplication](../../winscript/reference/iactivescriptsitedebug32-getapplication.md)|Retorna o objeto de aplicativo de depuração associado a este site de script.|  
|[IActiveScriptSiteDebug32::GetDocumentContextFromPosition](../../winscript/reference/iactivescriptsitedebug32-getdocumentcontextfromposition.md)|Usado pelo mecanismo de linguagem para delegar `IDebugCodeContext::GetSourceContext`.|
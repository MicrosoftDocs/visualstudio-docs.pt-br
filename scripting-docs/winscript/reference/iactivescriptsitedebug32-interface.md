---
title: Interface IActiveScriptSiteDebug32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 03f42217-303d-46e7-9792-61a5ab95252c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 2a55161f76fcd98b52ddb769c640aca0e903239b
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835258"
---
# <a name="iactivescriptsitedebug32-interface"></a>IActiveScriptSiteDebug32 Interface
Os hosts inteligentes implementam a `IActiveScriptSiteDebug32` interface para executar o gerenciamento de documentos e para participar da depuração. O `IActiveScriptSite` objeto geralmente fornece uma implementação da `IActiveScriptSiteDebug32` interface. Se isso for feito, chame o `IActiveScriptSite::QueryInterface` método para obter a `IActiveScriptSiteDebug32` interface.  
  
 Além dos métodos herdados do `IUnknown` , a `IActiveScriptSiteDebug32` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptSiteDebug32::GetApplication](../../winscript/reference/iactivescriptsitedebug32-getapplication.md)|Retorna o objeto de aplicativo de depuração associado a este site de script.|  
|[IActiveScriptSiteDebug32::GetDocumentContextFromPosition](../../winscript/reference/iactivescriptsitedebug32-getdocumentcontextfromposition.md)|Usado pelo mecanismo de linguagem para delegar `IDebugCodeContext::GetSourceContext` .|
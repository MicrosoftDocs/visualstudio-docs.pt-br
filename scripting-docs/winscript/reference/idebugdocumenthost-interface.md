---
title: Interface IDebugDocumentHost | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentHost interface
ms.assetid: 2fed4220-b6a2-47c6-bf28-daad7dd5c42d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: adaeb98f18a052106036a91885696dd4b4760dea
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726986"
---
# <a name="idebugdocumenthost-interface"></a>Interface IDebugDocumentHost
Expõe a funcionalidade específica do host, como coloração de sintaxe, o depurador. O `IDebugDocumentHelper::SetDebugDocumentHost` método usa essa interface como um argumento.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugDocumentHost` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugDocumentHost::GetDeferredText](../../winscript/reference/idebugdocumenthost-getdeferredtext.md)|Retorna um intervalo de caracteres que foram adicionados usando `IDebugDocumentHelper::AddDeferredText`, no documento original do host.|  
|[IDebugDocumentHost::GetScriptTextAttributes](../../winscript/reference/idebugdocumenthost-getscripttextattributes.md)|Retorna os atributos de texto de um bloco de texto do documento.|  
|[IDebugDocumentHost::OnCreateDocumentContext](../../winscript/reference/idebugdocumenthost-oncreatedocumentcontext.md)|Notifica o host que um novo contexto de documento está sendo criado e permite que o host se desejar retornar um objeto que controla o novo contexto.|  
|[IDebugDocumentHost::GetPathName](../../winscript/reference/idebugdocumenthost-getpathname.md)|Retorna o caminho completo (incluindo o nome do arquivo) do arquivo de origem do documento.|  
|[IDebugDocumentHost::GetFileName](../../winscript/reference/idebugdocumenthost-getfilename.md)|Retorna o nome do documento, sem informações de caminho.|  
|[IDebugDocumentHost::NotifyChanged](../../winscript/reference/idebugdocumenthost-notifychanged.md)|Notifica o host que tenha sido salva o arquivo de origem do documento e que seu conteúdo deve ser atualizado.|
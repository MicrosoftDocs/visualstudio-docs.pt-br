---
title: Interface IDebugDocumentText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentText interface
ms.assetid: 242bad79-9c0a-4a30-879a-9f43db4e022b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 763678b08c22fe34ec6ffebbe670fb8b50af6576
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843451"
---
# <a name="idebugdocumenttext-interface"></a>Interface IDebugDocumentText
Fornece acesso a uma versão somente texto do documento de depuração. Essa interface usa as seguintes convenções:  
  
- Posições de caracteres e números de linha são baseadas em zero.  
  
- Posições de caractere representam deslocamentos de caracteres; eles não representam o byte nem deslocamentos do word. Para Win32, uma posição de caractere é um deslocamento de Unicode.  
  
  Além dos métodos herdados de `IDebugDocument`, o `IDebugDocumentText` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugDocumentText::GetDocumentAttributes](../../winscript/reference/idebugdocumenttext-getdocumentattributes.md)|Retorna os atributos do documento.|  
|[IDebugDocumentText::GetSize](../../winscript/reference/idebugdocumenttext-getsize.md)|Retorna o número de linhas e o número de caracteres no documento.|  
|[IDebugDocumentText::GetPositionOfLine](../../winscript/reference/idebugdocumenttext-getpositionofline.md)|Retorna a posição do caractere correspondente para o primeiro caractere de uma linha.|  
|[IDebugDocumentText::GetLineOfPosition](../../winscript/reference/idebugdocumenttext-getlineofposition.md)|Retorna o número de linha e, opcionalmente, o deslocamento de caractere dentro da linha que corresponde à posição do caractere especificada.|  
|[IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)|Recupera os caracteres de e/ou os atributos de caracteres associados com um intervalo de posição do caractere.|  
|[IDebugDocumentText::GetPositionOfContext](../../winscript/reference/idebugdocumenttext-getpositionofcontext.md)|Retorna o intervalo de posição do caractere correspondente a um contexto de documento.|  
|[IDebugDocumentText::GetContextOfPosition](../../winscript/reference/idebugdocumenttext-getcontextofposition.md)|Cria um objeto de contexto do documento correspondente ao intervalo de posição de caractere fornecidos.|
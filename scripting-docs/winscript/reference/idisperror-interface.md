---
title: Interface IDispError | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDispError interface
ms.assetid: 3dc7b55e-94ba-4669-b20a-1e011f2d07cf
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9f139d317db5aa00f03f8e9abd71020e5ff35b03
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728106"
---
# <a name="idisperror-interface"></a>Interface IDispError
Fornece informações detalhadas do erro contextual.  
  
> [!NOTE]
>  Esta interface não é implementada.  
  
 Além dos métodos herdados de `IUnknown`, o `IDispError` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDispError::QueryErrorInfo](../../winscript/reference/idisperror-queryerrorinfo.md)|Recupera um tipo específico de informações de erro.|  
|[IDispError::GetNext](../../winscript/reference/idisperror-getnext.md)|Recupera a próxima `IDispError` objeto.|  
|[IDispError::GetHresult](../../winscript/reference/idisperror-gethresult.md)|Recupera o código de erro do `IDispError` objeto.|  
|[IDispError::GetSource](../../winscript/reference/idisperror-getsource.md)|Retorna o identificador programático dependentes de idioma para a classe ou o aplicativo que gerou o erro.|  
|[IDispError::GetHelpInfo](../../winscript/reference/idisperror-gethelpinfo.md)|Retorna o caminho do arquivo de Ajuda e a ID do contexto do tópico que explica o erro, se possível.|  
|[IDispError::GetDescription](../../winscript/reference/idisperror-getdescription.md)|Retorna uma descrição textual do erro.|
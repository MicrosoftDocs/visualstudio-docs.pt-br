---
description: Representa um provedor de símbolos que tem acesso direto a metadados e a interfaces de símbolo de núcleo.
title: IDebugSymbolProviderDirect | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect interface
ms.assetid: 872b04a8-70de-4ab5-aceb-684c81828545
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6cce774ff6c3ca3e1037a4a61f5c8b4f892aa1c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053146"
---
# <a name="idebugsymbolproviderdirect"></a>IDebugSymbolProviderDirect
Representa um provedor de símbolos que tem acesso direto a metadados e a interfaces de símbolo de núcleo.

## <a name="syntax"></a>Sintaxe

```
IDebugSymbolProviderDirect: IUnknown
```

## <a name="methods"></a>Métodos
 Essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetAppIDFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getappidfromaddress.md)|Recupera o identificador de domínio do aplicativo de acordo com o endereço de depuração.|
|[GetCurrentModulesInfo](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesinfo.md)|Recupera informações sobre os módulos no grupo de símbolos.|
|[GetCurrentModulesState](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesstate.md)|Recupera informações sobre o grupo de símbolos do qual o provedor de símbolos é membro.|
|[GetMetaDataImport](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmetadataimport.md)|Recupera as informações de importação de metadados.|
|[GetMethodFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmethodfromaddress.md)|Recupera informações sobre o método no endereço de depuração especificado.|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getsymunmanagedreader.md)|Recupera um leitor de símbolo para código não gerenciado.|

## <a name="remarks"></a>Comentários
 Essa interface pode ser usada em vez da maioria das outras interfaces de provedor de símbolos. Ele fornece acesso direto aos metadados e às `CorSym` interfaces.

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

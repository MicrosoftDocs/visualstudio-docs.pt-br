---
description: Obtém o nome da sessão que está depurando esse processo.
title: 'IDebugProcess2:: GetAttachedSessionName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 426904f777d65a25b92871767649cb26041e2af8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071539"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
Obtém o nome da sessão que está depurando esse processo. Um IDE pode exibir essas informações para um usuário que está depurando um processo específico em um determinado computador.

> [!NOTE]
> Esse método é preterido e sua implementação sempre deve retornar `E_NOTIMPL` .

## <a name="syntax"></a>Sintaxe

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

## <a name="parameters"></a>Parâmetros
`pbstrSessionName`\

## <a name="return-value"></a>Valor Retornado
 Esse método sempre deve retornar `E_NOTIMPL` .

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)

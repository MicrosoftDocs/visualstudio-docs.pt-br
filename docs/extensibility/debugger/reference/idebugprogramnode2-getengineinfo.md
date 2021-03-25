---
description: Obtém o nome e o identificador do mecanismo de depuração (DE) que executa um programa.
title: 'IDebugProgramNode2:: GetEngineInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetEngineInfo
helpviewer_keywords:
- IDebugProgramNode2::GetEngineInfo
ms.assetid: 664e7fe5-9100-4b7d-9dc5-e5a4dd0d0451
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0a902db31cb4d48810e673e7807bd3944c2a875
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053523"
---
# <a name="idebugprogramnode2getengineinfo"></a>IDebugProgramNode2::GetEngineInfo
Obtém o nome e o identificador do mecanismo de depuração (DE) que executa um programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEngineInfo ( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo(
   out string pbstrEngine,
   out Guid pguidEngine
);
```

## <a name="parameters"></a>Parâmetros
`pbstrEngine`\
fora Retorna o nome da execução do programa (específico do C++: esse pode ser um ponteiro nulo indicando que o chamador não está interessado no nome do mecanismo).

`pguidEngine`\
fora Retorna o identificador global exclusivo da execução do programa (específico do C++: esse pode ser um ponteiro nulo indicando que o chamador não está interessado no GUID do mecanismo).

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)

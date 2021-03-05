---
description: Obtém o nome de usuário do fornecedor da porta.
title: 'IDebugProcessSecurity:: GetUserName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04ad8bf6ba572a1f9e14e26ef2ca37d021f6e3a0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166197"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
Obtém o nome de usuário do fornecedor da porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetUserName(
    BSTR *pbstrUserName
);
```

```csharp
int GetUserName (
    string pbstrUserName
);
```

## <a name="parameters"></a>Parâmetros
`pbstrUserName`\
fora Uma cadeia de caracteres que contém o nome de usuário.

## <a name="return-value"></a>Valor Retornado
 Se o método for bem-sucedido, retornará `S_OK`. Caso contrário, ele retorna um código de erro.

## <a name="remarks"></a>Comentários
 `GetUserName` Retorna o nome de usuário exibido na coluna **nome de usuário** da caixa de diálogo **anexar ao processo** . Para exibir a caixa de diálogo **anexar ao processo** , clique em **anexar ao processo** no menu **ferramentas** no [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE).

## <a name="see-also"></a>Confira também
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)

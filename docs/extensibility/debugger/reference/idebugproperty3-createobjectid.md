---
title: IDebugProperty3::CreateObjectID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf17196b4dae8642a81664dd339eaa78c2d2d8e9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412743"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
Cria uma ID exclusiva para essa propriedade para garantir que ele seja exclusivo entre todas as outras propriedades.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado quando o Gerenciador de sessão de depuração quer ter certeza de que essa propriedade é identificada exclusivamente entre todas as outras propriedades. O mecanismo de depuração (DES) dá suporte a esse método, a menos que as propriedades que ele lida com são identificadas já exclusivamente. Se o DE não oferece suporte a esse método, ele retorna `E_NOTIMPL`.

 Qualquer ID exclusiva é criada com `CreateObjectID` é destruído quando o [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md) é chamado de método; isso também sinaliza o término da necessidade de identificando exclusivamente esta propriedade.

> [!NOTE]
> Não há nenhum método para recuperar essa ID exclusiva, portanto, o DE pode fazer o que quiser para IDs exclusivas quando o `CreateObjectID` método é chamado.

## <a name="see-also"></a>Consulte também
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
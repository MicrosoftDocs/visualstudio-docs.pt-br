---
description: Fornece suporte para um fornecedor de porta selecionar e interagir com um servidor principal.
title: IDebugPortSupplierEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierEx2 interface
ms.assetid: dae0050a-a50a-4f35-bfbd-e538f537b20f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2020f3efe2bd7562640fd44e45a10c9a3a6c767
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071838"
---
# <a name="idebugportsupplierex2"></a>IDebugPortSupplierEx2
Fornece suporte para um fornecedor de porta selecionar e interagir com um servidor principal.

## <a name="syntax"></a>Sintaxe

```
IDebugPortSupplierEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface para que ela possa selecionar o servidor principal a ser usado.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de **IDebugPortSupplierEx2**.

|Método|Descrição|
|------------|-----------------|
|[SetServer](../../../extensibility/debugger/reference/idebugportsupplierex2-setserver.md)|Define o servidor principal para o fornecedor da porta.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Portpriv. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)

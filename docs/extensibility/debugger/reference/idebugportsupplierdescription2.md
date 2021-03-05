---
description: Permite que a interface do usuário do Visual Studio exiba texto dentro da seção informações de transporte da caixa de diálogo anexar ao processo.
title: IDebugPortSupplierDescription2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c3cd8d6fbeaf020ea772c9bd5cae783b6e8d127
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150374"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
Permite que a [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário exiba texto dentro da seção **informações de transporte** da caixa de diálogo **anexar ao processo** .

## <a name="syntax"></a>Sintaxe

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por fornecedores de porta.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugPortSupplierDescription2` .

|Método|Descrição|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|Recupera os metadados de descrição e descrição para o fornecedor da porta.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

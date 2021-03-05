---
description: Representa uma interface do usuário personalizada para selecionar a porta.
title: IDebugPortPicker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 335a954603505d064f32e8f901ce428d6cb8dfa1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142628"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
Representa uma interface do usuário personalizada para selecionar a porta.

## <a name="syntax"></a>Sintaxe

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por fornecedores de porta. Um fornecedor de porta define seu seletor de porta expondo-o como um CLSID e apontando a `metricPortPickerCLSID` métrica no CLSID exposto.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugPortPicker` .

|Método|Descrição|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|Exibe a caixa de diálogo especificada que permite ao usuário selecionar uma porta.|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|Define o provedor de serviços.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

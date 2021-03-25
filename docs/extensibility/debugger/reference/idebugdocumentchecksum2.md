---
description: Representa uma soma de verificação para um documento de depuração e permite passar a soma de verificação entre componentes.
title: IDebugDocumentChecksum2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 518e5b089d0d34e2492297b27dd0829e5f00ef2f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066731"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
Representa uma soma de verificação para um documento de depuração e permite passar a soma de verificação entre componentes.

## <a name="syntax"></a>Sintaxe

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface pode ser implementada por qualquer componente que expõe a interface [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) . No entanto, ele é implementado principalmente por mecanismos de depuração para que a soma de verificação inserida em um arquivo de símbolo (*. pdb) possa ser passada de volta para o IDE e usada durante a localização de uma origem.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugDocumentChecksum2` .

|Método|Descrição|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|Recupera a soma de verificação do documento e o identificador do algoritmo de acordo com o número máximo de bytes a serem usados.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

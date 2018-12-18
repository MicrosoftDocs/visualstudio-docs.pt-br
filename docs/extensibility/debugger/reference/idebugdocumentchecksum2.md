---
title: IDebugDocumentChecksum2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 068447399a8cfd43cb5fe07ea82e7cf4400f460c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31106712"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
Representa uma soma de verificação para um documento de depuração e permite transmitir a soma de verificação entre os componentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugDocumentChecksum2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface pode ser implementada por qualquer componente que expõe o [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) interface. No entanto, ele principalmente é implementado por mecanismos de depuração para que a soma de verificação inserida em um arquivo de símbolo (*.pdb) pode ser passada de volta para o IDE e usada ao localizar uma fonte.  
  
## <a name="methods"></a>Métodos  
 A tabela a seguir mostra os métodos de `IDebugDocumentChecksum2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|Recupera o identificador de soma de verificação e o algoritmo de documento dado o número máximo de bytes a ser usado.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
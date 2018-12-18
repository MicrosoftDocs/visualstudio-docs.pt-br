---
title: DISASSEMBLY_STREAM_FIELDS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9489b8c4399ae72bf7f6a70011eec347d870ca80
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928328"
---
# <a name="disassemblystreamfields"></a>DISASSEMBLY_STREAM_FIELDS
Especifica quais informações devem ser recuperadas sobre um campo de desmontagem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_DISASSEMBLY_STREAM_FIELDS {   
   DSF_ADDRESS          = 0x00000001,  
   DSF_ADDRESSOFFSET    = 0x00000002,  
   DSF_CODEBYTES        = 0x00000004,  
   DSF_OPCODE           = 0x00000008,  
   DSF_OPERANDS         = 0x00000010,  
   DSF_SYMBOL           = 0x00000020,  
   DSF_CODELOCATIONID   = 0x00000040,  
   DSF_POSITION         = 0x00000080,  
   DSF_DOCUMENTURL      = 0x00000100,  
   DSF_BYTEOFFSET       = 0x00000200,  
   DSF_FLAGS            = 0x00000400,  
   DSF_OPERANDS_SYMBOLS = 0x00010000,  
   DSF_ALL              = 0x000107ff  
};  
typedef DWORD DISASSEMBLY_STREAM_FIELDS;  
```  
  
```csharp  
public enum enum_DISASSEMBLY_STREAM_FIELDS {   
   DSF_ADDRESS          = 0x00000001,  
   DSF_ADDRESSOFFSET    = 0x00000002,  
   DSF_CODEBYTES        = 0x00000004,  
   DSF_OPCODE           = 0x00000008,  
   DSF_OPERANDS         = 0x00000010,  
   DSF_SYMBOL           = 0x00000020,  
   DSF_CODELOCATIONID   = 0x00000040,  
   DSF_POSITION         = 0x00000080,  
   DSF_DOCUMENTURL      = 0x00000100,  
   DSF_BYTEOFFSET       = 0x00000200,  
   DSF_FLAGS            = 0x00000400,  
   DSF_OPERANDS_SYMBOLS = 0x00010000,  
   DSF_ALL              = 0x000107ff  
};  
```  
  
## <a name="members"></a>Membros  
 DSF_ADDRESS  
 Inicialização/usar o `bstrAddress` campo.  
  
 DSF_ADDRESSOFFSET  
 Inicialização/usar o `bstrAddressOffset` campo.  
  
 DSF_CODEBYTES  
 Inicialização/usar o `bstrCodeBytes` campo.  
  
 DSF_OPCODE  
 Inicialização/usar o `bstrOpCode` campo.  
  
 DSF_OPERANDS  
 Inicialização/usar o `bstrOperands` campo.  
  
 DSF_SYMBOL  
 Inicialização/usar o `bstrSymbol` campo.  
  
 DSF_CODELOCATIONID  
 Inicialização/usar o `uCodeLocationId` campo.  
  
 DSF_POSITION  
 Inicialização/usar o `posBeg` e `posEnd` campos.  
  
 DSF_DOCUMENTURL  
 Inicialização/usar o `bstrDocumentUrl` campo.  
  
 DSF_BYTEOFFSET  
 Inicialização/usar o `dwByteOffset` campo.  
  
 DSF_FLAGS  
 Inicialização/usar o `dwFlags` ([DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)) campo.  
  
 DSF_OPERANDS_SYMBOLS  
 Incluir nomes de símbolos no `bstrOperands` campo.  
  
 DSF_ALL  
 Especifica todos os campos para o fluxo de desmontagem.  
  
## <a name="remarks"></a>Comentários  
 Passado como um parâmetro para o [leitura](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) método para indicar quais campos da [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) são de estrutura a ser inicializado.  
  
 Usado para o `dwFields` membro o `DisassemblyData` estrutura para indicar quais campos são usados e válidos quando a estrutura é retornada.  
  
 Esses valores podem ser combinados com um bit a bit `OR`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)   
 [Leitura](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)   
 [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
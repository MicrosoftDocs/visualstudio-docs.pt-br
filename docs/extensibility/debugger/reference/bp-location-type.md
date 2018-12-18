---
title: BP_LOCATION_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- BP_LOCATION_TYPE
helpviewer_keywords:
- BP_LOCATION_TYPE structure
ms.assetid: 0248430a-3b61-4809-87a9-e9b6bb7d1130
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 087f6c3ce0cbde32bd06a614e562c3d36fc86888
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927353"
---
# <a name="bplocationtype"></a>BP_LOCATION_TYPE
Especifica o tipo de local do ponto de interrupção para uma solicitação de ponto de interrupção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
typedef DWORD BP_LOCATION_TYPE;  
```  
  
```csharp  
public enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
```  
  
## <a name="members"></a>Membros  
 BPLT_NONE  
 Não especifica nenhum local de ponto de interrupção.  
  
 BPLT_FILE_LINE  
 Especifica o tipo de local do ponto de interrupção como um arquivo de linha.  
  
 BPLT_FUNC_OFFSET  
 Especifica o tipo de local do ponto de interrupção como um deslocamento de função.  
  
 BPLT_CONTEXT  
 Especifica o tipo de local do ponto de interrupção como um contexto.  
  
 BPLT_STRING  
 Especifica o tipo de local do ponto de interrupção como uma cadeia de caracteres.  
  
 BPLT_ADDRESS  
 Especifica o tipo de local do ponto de interrupção como um endereço.  
  
 BPLT_RESOLUTION  
 Especifica o tipo de local do ponto de interrupção como uma resolução.  
  
 BPLT_CODE_FILE_LINE  
 Especifica o tipo de local do ponto de interrupção como uma linha de código-fonte.  
  
 BPLT_CODE_FUNC_OFFSET  
 Especifica o tipo de local do ponto de interrupção como um deslocamento de função de código.  
  
 BPLT_CODE_CONTEXT  
 Especifica o tipo de local do ponto de interrupção como um contexto de código.  
  
 BPLT_CODE_STRING  
 Especifica o tipo de local do ponto de interrupção como uma cadeia de caracteres de código.  
  
 BPLT_CODE_ADDRESS  
 Especifica o tipo de local do ponto de interrupção como um endereço de código.  
  
 BPLT_DATA_STRING  
 Especifica o tipo de local do ponto de interrupção como uma cadeia de caracteres de dados.  
  
 BPLT_TYPE_MASK  
 Especifica uma máscara de bits, para que o tipo de ponto de interrupção pode ser extraído fora o valor.  
  
 BPLT_LOCATION_TYPE_MASK  
 Especifica uma máscara de bits, para que o tipo de local de ponto de interrupção pode ser extraído fora o valor.  
  
## <a name="remarks"></a>Comentários  
 Passado como um parâmetro para o [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md) método.  
  
 Um tipo de local de ponto de interrupção é composto de um tipo de ponto de interrupção e um tipo de local. Isso significa que um tipo de local de ponto de interrupção nunca é apenas um tipo de ponto de interrupção (por exemplo, `BPT_CODE`) ou um tipo de local (por exemplo, `BPLT_FILE_LINE`). Constantes predefinidas para todos os tipos de local de ponto de interrupção atualmente com suporte estão incluídos nesta enumeração (`BPLT_CODE_FILE_LINE` por meio de `BPLT_DATA_STRING`).  
  
 `BPT_CODE` e `BPT_DATA` são membros de [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) enumeração.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)   
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
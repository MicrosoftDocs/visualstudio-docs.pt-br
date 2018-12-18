---
title: DEBUGPROP_INFO_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- DEBUGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS enumeration
ms.assetid: 1c7fe777-615e-4929-9ed4-970d9fe0eb81
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f92138aa9cb3867343ec1d83653d8b30f9b1a8a6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927588"
---
# <a name="debugpropinfoflags"></a>DEBUGPROP_INFO_FLAGS
Especifica quais informações devem ser recuperadas sobre um objeto de propriedade de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_DEBUGPROP_INFO_FLAGS {   
   DEBUGPROP_INFO_FULLNAME          = 0x00000001,  
   DEBUGPROP_INFO_NAME              = 0x00000002,  
   DEBUGPROP_INFO_TYPE              = 0x00000004,  
   DEBUGPROP_INFO_VALUE             = 0x00000008,  
   DEBUGPROP_INFO_ATTRIB            = 0x00000010,  
   DEBUGPROP_INFO_PROP              = 0x00000020,  
   DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,  
   DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,  
   DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,  
   DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000  
   DEBUGPROP_INFO_NONE              = 0x00000000,  
   DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |  
                                      DEBUGPROP_INFO_NAME |  
                                      DEBUGPROP_INFO_TYPE |  
                                      DEBUGPROP_INFO_VALUE,  
   DEBUGPROP_INFO_ALL               = 0xffffffff  
};  
typedef DWORD DEBUGPROP_INFO_FLAGS;  
```  
  
```csharp  
public enum enum_DEBUGPROP_INFO_FLAGS {   
   DEBUGPROP_INFO_FULLNAME          = 0x00000001,  
   DEBUGPROP_INFO_NAME              = 0x00000002,  
   DEBUGPROP_INFO_TYPE              = 0x00000004,  
   DEBUGPROP_INFO_VALUE             = 0x00000008,  
   DEBUGPROP_INFO_ATTRIB            = 0x00000010,  
   DEBUGPROP_INFO_PROP              = 0x00000020,  
   DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,  
   DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,  
   DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,  
   DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000  
   DEBUGPROP_INFO_NONE              = 0x00000000,  
   DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |  
                                      DEBUGPROP_INFO_NAME |  
                                      DEBUGPROP_INFO_TYPE |  
                                      DEBUGPROP_INFO_VALUE,  
   DEBUGPROP_INFO_ALL               = 0xffffffff  
};  
```  
  
## <a name="members"></a>Membros  
 DEBUGPROP_INFO_FULLNAME  
 Inicialização/usar o `bstrFullName` campo.  
  
 DEBUGPROP_INFO_NAME  
 Inicialização/usar o `bstrName` campo.  
  
 DEBUGPROP_INFO_TYPE  
 Inicialização/usar o `bstrType` campo.  
  
 DEBUGPROP_INFO_VALUE  
 Inicialização/usar o `bstrValue` campo.  
  
 DEBUGPROP_INFO_ATTRIB  
 Inicialização/usar o `dwAttrib` campo.  
  
 DEBUGPROP_INFO_PROP,  
 Inicialização/usar o `pProperty` campo que contém uma [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) interface.  
  
 DEBUGPROP_INFO_VALUE_AUTOEXPAND  
 Especifica que o campo de valor deve conter o valor expandida automaticamente, se disponível, para esse tipo de objeto.  
  
 DEBUGPROP_INFO_VALUE_NOFUNCEVAL  
 Preterido.  
  
 DEBUGPROP_INFO_VALUE_RAW  
 Não retornam todos os valores beautified ou membros (ou seja, não formatar os valores).  
  
 DEBUGPROP_INFO_VALUE_NO_TOSTRING  
 Não retornar nenhum valor de sintetizada especiais (por exemplo, não chame `ToString()` em um objeto para produzir um valor).  
  
 DEBUGPROP_INFO_NONE  
 Especifica que nenhum sinalizador está definido.  
  
 DEBUGPROP_INFO_STANDARD  
 Inicialização/usar o `dwAttrib`, `bstrName`, `bstrType`, e `bstrValue` campos.  
  
 DEBUGPROP_INFO_All  
 Indica uma máscara de todos os sinalizadores.  
  
## <a name="remarks"></a>Comentários  
 Esses valores são passados para o [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md), [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md), e [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) métodos para indicar quais campos devem ser inicializado a [ DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estrutura.  
  
 Esses valores também são usados para o `dwFields` membro o `DEBUG_PROPERTY_INFO` estrutura para indicar quais campos da estrutura são usados e válidos quando a estrutura é retornada.  
  
 Esses valores podem ser combinados com um bit a bit `OR`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)   
 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
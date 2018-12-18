---
title: FIELD_KIND | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- FIELD_KIND
helpviewer_keywords:
- FIELD_KIND enumeration
ms.assetid: fd522b9c-52e2-42fa-939d-343347d5c3b1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: df29c9bd876a437dbcf8d797f1dcc51fb05a296f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868190"
---
# <a name="fieldkind"></a>FIELD_KIND
Especifica o tipo do campo contido em um [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_FIELD_KIND {   
   FIELD_KIND_NONE       = 0x00000000,  
  
   // Type of field  
   FIELD_KIND_TYPE       = 0x00000001,  
   FIELD_KIND_SYMBOL     = 0x00000002,  
  
   // Storage type of the field  
   FIELD_TYPE_PRIMITIVE  = 0x00000010,  
   FIELD_TYPE_STRUCT     = 0x00000020,  
   FIELD_TYPE_CLASS      = 0x00000040,  
   FIELD_TYPE_INTERFACE  = 0x00000080,  
   FIELD_TYPE_UNION      = 0x00000100,  
   FIELD_TYPE_ARRAY      = 0x00000200,  
   FIELD_TYPE_METHOD     = 0x00000400,  
   FIELD_TYPE_BLOCK      = 0x00000800,  
   FIELD_TYPE_POINTER    = 0x00001000,  
   FIELD_TYPE_ENUM       = 0x00002000,  
   FIELD_TYPE_LABEL      = 0x00004000,  
   FIELD_TYPE_TYPEDEF    = 0x00008000,  
   FIELD_TYPE_BITFIELD   = 0x00010000,  
   FIELD_TYPE_NAMESPACE  = 0x00020000,  
   FIELD_TYPE_MODULE     = 0x00040000,  
   FIELD_TYPE_DYNAMIC    = 0x00080000,  
   FIELD_TYPE_PROP       = 0x00100000,  
   FIELD_TYPE_INNERCLASS = 0x00200000,  
   FIELD_TYPE_REFERENCE  = 0x00400000,  
   FIELD_TYPE_EXTENDED   = 0x00800000,  
  
   // Specific information about symbols  
   FIELD_SYM_MEMBER      = 0x01000000,  
   FIELD_SYM_LOCAL       = 0x02000000,  
   FIELD_SYM_PARAM       = 0x04000000,  
   FIELD_SYM_THIS        = 0x08000000,  
   FIELD_SYM_GLOBAL      = 0x10000000,  
   FIELD_SYM_PROP_GETTER = 0x20000000,  
   FIELD_SYM_PROP_SETTER = 0x40000000,  
   FIELD_SYM_EXTENDED    = 0x80000000,  
  
   FIELD_KIND_MASK       = 0x0000000f,  
   FIELD_TYPE_MASK       = 0x00fffff0,  
   FIELD_SYM_MASK        = 0xff000000,  
  
   FIELD_KIND_ALL        = 0xffffffff  
};  
typedef DWORD FIELD_KIND;  
```  
  
```csharp  
public enum enum_FIELD_KIND {  
   FIELD_KIND_NONE       = 0x00000000,  
  
   // Type of field  
   FIELD_KIND_TYPE       = 0x00000001,  
   FIELD_KIND_SYMBOL     = 0x00000002,  
  
   // Storage type of the field  
   FIELD_TYPE_PRIMITIVE  = 0x00000010,  
   FIELD_TYPE_STRUCT     = 0x00000020,  
   FIELD_TYPE_CLASS      = 0x00000040,  
   FIELD_TYPE_INTERFACE  = 0x00000080,  
   FIELD_TYPE_UNION      = 0x00000100,  
   FIELD_TYPE_ARRAY      = 0x00000200,  
   FIELD_TYPE_METHOD     = 0x00000400,  
   FIELD_TYPE_BLOCK      = 0x00000800,  
   FIELD_TYPE_POINTER    = 0x00001000,  
   FIELD_TYPE_ENUM       = 0x00002000,  
   FIELD_TYPE_LABEL      = 0x00004000,  
   FIELD_TYPE_TYPEDEF    = 0x00008000,  
   FIELD_TYPE_BITFIELD   = 0x00010000,  
   FIELD_TYPE_NAMESPACE  = 0x00020000,  
   FIELD_TYPE_MODULE     = 0x00040000,  
   FIELD_TYPE_DYNAMIC    = 0x00080000,  
   FIELD_TYPE_PROP       = 0x00100000,  
   FIELD_TYPE_INNERCLASS = 0x00200000,  
   FIELD_TYPE_REFERENCE  = 0x00400000,  
   FIELD_TYPE_EXTENDED   = 0x00800000,  
  
   // Specific information about symbols  
   FIELD_SYM_MEMBER      = 0x01000000,  
   FIELD_SYM_LOCAL       = 0x02000000,  
   FIELD_SYM_PARAM       = 0x04000000,  
   FIELD_SYM_THIS        = 0x08000000,  
   FIELD_SYM_GLOBAL      = 0x10000000,  
   FIELD_SYM_PROP_GETTER = 0x20000000,  
   FIELD_SYM_PROP_SETTER = 0x40000000,  
   FIELD_SYM_EXTENDED    = 0x80000000,  
  
   FIELD_KIND_MASK       = 0x0000000f,  
   FIELD_TYPE_MASK       = 0x00fffff0,  
   FIELD_SYM_MASK        = 0xff000000,  
  
   FIELD_KIND_ALL        = 0xffffffff  
};  
```  
  
## <a name="members"></a>Membros  
 FIELD_KIND_TYPE  
 Indica que o campo é somente um tipo.  
  
 FIELD_KIND_SYMBOL  
 Indica que o campo é um símbolo, com tipo, nome e outras informações.  
  
 FIELD_TYPE_PRIMITIVE  
 Indica que o campo é um tipo de dados primitivo.  
  
 FIELD_TYPE_STRUCT  
 Indica que o campo é uma estrutura.  
  
 FIELD_TYPE_CLASS  
 Indica que o campo é uma classe.  
  
 FIELD_TYPE_INTERFACE  
 Indica que o campo é uma interface.  
  
 FIELD_TYPE_UNION  
 Indica que o campo é uma união.  
  
 FIELD_TYPE_ARRAY  
 Indica que o campo é uma matriz.  
  
 FIELD_TYPE_METHOD  
 Indica que o campo é um método.  
  
 FIELD_TYPE_BLOCK  
 Indica que o campo é um bloco.  
  
 FIELD_TYPE_POINTER  
 Indica que o campo é um ponteiro.  
  
 FIELD_TYPE_ENUM  
 Indica que o campo é um tipo de dados enumerado.  
  
 FIELD_TYPE_LABEL  
 Indica que o campo é um rótulo.  
  
 FIELD_TYPE_TYPEDEF  
 Indica que o campo é um typedef.  
  
 FIELD_TYPE_BITFIELD  
 Indica que o campo é um campo de bits.  
  
 FIELD_TYPE_NAMESPACE  
 Indica que o campo é um namespace.  
  
 FIELD_TYPE_MODULE  
 Indica que o campo é um módulo.  
  
 FIELD_TYPE_DYNAMIC  
 Indica que o campo é dinâmico.  
  
 FIELD_TYPE_PROP  
 Indica que o campo é uma propriedade.  
  
 FIELD_TYPE_INNERCLASS  
 Indica que o campo é uma classe interna.  
  
 FIELD_TYPE_REFERENCE  
 Indica que o campo é uma referência.  
  
 FIELD_TYPE_EXTENDED  
 Reservado para uso futuro.  
  
 FIELD_SYM_MEMBER  
 Indica que o campo é um membro.  
  
 FIELD_SYM_LOCAL  
 Indica que o campo é local.  
  
 FIELD_SYM_PARAMETER  
 Indica que o campo é um parâmetro.  
  
 FIELD_SYM_THIS  
 Indica que o campo é o ponteiro "this".  
  
 FIELD_SYM_GLOBAL  
 Indica que o campo é global.  
  
 FIELD_SYM_PROP_GETTER  
 Indica que o campo recupera as propriedades.  
  
 FIELD_SYM_PROP_SETTER  
 Indica que o campo define as propriedades.  
  
 FIELD_SYM_EXTENDED  
 Reservado para uso futuro.  
  
 FIELD_KIND_MASK  
 Indica uma máscara para os tipos de campo.  
  
 FIELD_TYPE_MASK  
 Indica uma máscara para tipos de campo.  
  
 FIELD_SYM_MASK  
 Indica uma máscara para informações de símbolo.  
  
## <a name="remarks"></a>Comentários  
 Retornado de uma chamada para o [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) método.  
  
 Dependendo do tipo de campo, [QueryInterface](/cpp/atl/queryinterface) pode ser chamado na [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) interface para a forma mais específica de interface. Por exemplo, se [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) retorna `FIELD_TYPE_METHOD`, em seguida, você pode chamar `QueryInterface` em`DebugField` para obter o [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) interface.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)   
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
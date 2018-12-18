---
title: OBJECT_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- OBJECT_TYPE
helpviewer_keywords:
- OBJECT_TYPE enumeration
ms.assetid: c4d246f9-8a98-44ec-b2bb-ff5c684f668e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: eff83198e337a3f89c88663722bf34046d3d4f62
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905734"
---
# <a name="objecttype"></a>OBJECT_TYPE
Especifica o tipo de um objeto do avaliador de expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
typedef DWORD OBJECT_TYPE;  
```  
  
```csharp  
public enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
```  
  
## <a name="members"></a>Membros  
 OBJECT_TYPE_BOOLEAN  
 Indica que o objeto é um valor booliano.  
  
 OBJECT_TYPE_CHAR  
 Indica que o objeto é um caractere.  
  
 OBJECT_TYPE_I1  
 Indica que o objeto é um inteiro com sinal de um byte.  
  
 OBJECT_TYPE_U1  
 Indica que o objeto é um inteiro sem sinal de um byte.  
  
 OBJECT_TYPE_I2  
 Indica que o objeto é um inteiro com sinal de dois bytes.  
  
 OBJECT_TYPE_U2  
 Indica que o objeto é um inteiro sem sinal de dois bytes.  
  
 OBJECT_TYPE_I4  
 Indica que o objeto é um inteiro com sinal de quatro bytes.  
  
 OBJECT_TYPE_U4  
 Indica que o objeto é um inteiro sem sinal de quatro bytes.  
  
 OBJECT_TYPE_I8  
 Indica que o objeto é um inteiro com sinal de oito bytes.  
  
 OBJECT_TYPE_U8  
 Indica que o objeto é um inteiro sem sinal de oito bytes.  
  
 OBJECT_TYPE_R4  
 Indica que o objeto é um número de ponto flutuante de quatro bytes.  
  
 OBJECT_TYPE_R8  
 Indica que o objeto é um número de ponto flutuante de oito bytes.  
  
 OBJECT_TYPE_OBJECT  
 Indica que o objeto é um objeto.  
  
 OBJECT_TYPE_NULL  
 Indica que o objeto é nulo.  
  
 OBJECT_TYPE_CLASS  
 Indica que o objeto é uma classe.  
  
## <a name="remarks"></a>Comentários  
 Passado como um argumento para o [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md) e [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md) métodos.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)   
 [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)
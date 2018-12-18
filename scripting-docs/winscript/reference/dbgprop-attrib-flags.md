---
title: DBGPROP_ATTRIB_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBGPROP_ATTRIB_FLAGS
apilocation:
- scrobj.dll
f1_keywords:
- DBGPROP_ATTRIB_FLAGS
helpviewer_keywords:
- DBGPROP_ATTRIB_FLAGS
ms.assetid: 90314496-527b-4357-9df8-125a360bf216
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 831f12d11515e6796941b64e114bdc084309b87d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862405"
---
# <a name="dbgpropattribflags"></a>DBGPROP_ATTRIB_FLAGS
Descreve vários atributos para um `IDebugProperty`. Membro da estrutura `DebugPropertyInfo`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
enum {  
DBGPROP_ATTRIB_NO_ATTRIB  =0x00000000,  
   DBGPROP_ATTRIB_VALUE_IS_INVALID  =0x00000008,  
   DBGPROP_ATTRIB_VALUE_IS_EXPANDABLE  =0x00000010,  
   DBGPROP_ATTRIB_VALUE_READONLY  =0x00000800,  
   DBGPROP_ATTRIB_ACCESS_PUBLIC  =0x00001000,  
   DBGPROP_ATTRIB_ACCESS_PRIVATE  =0x00002000,  
   DBGPROP_ATTRIB_ACCESS_PROTECTED  =0x00004000,  
   DBGPROP_ATTRIB_ACCESS_FINAL  =0x00008000,  
   DBGPROP_ATTRIB_STORAGE_GLOBAL  =0x00010000,  
   DBGPROP_ATTRIB_STORAGE_STATIC  =0x00020000,  
   DBGPROP_ATTRIB_STORAGE_FIELD  =0x00040000,  
   DBGPROP_ATTRIB_STORAGE_VIRTUAL  =0x00080000,  
   DBGPROP_ATTRIB_TYPE_IS_CONSTANT  =0x00100000,  
   DBGPROP_ATTRIB_TYPE_IS_SYNCHRONIZED  =0x00200000,  
   DBGPROP_ATTRIB_TYPE_IS_VOLATILE  =0x00400000,  
   DBGPROP_ATTRIB_HAS_EXTENDED_ATTRIBS  =0x00800000  
   DBGPROP_ATTRIB_VALUE_IS_RETURN_VALUE  =0x08000000,  
};  
  
```  
  
## <a name="members"></a>Membros  
 DBGPROP_ATTRIB_NO_ATTRIB  
 Indica nenhum atributo.  
  
 DBGPROP_ATTRIB_VALUE_IS_INVALID  
 Indica que o valor no `DebugPropertyInfo::bstrValue` não é válido.  
  
 DBGPROP_ATTRIB_VALUE_IS_EXPANDABLE  
 Indica que a propriedade ou referência tem filhos.  
  
 DBGPROP_ATTRIB_VALUE_READONLY  
 Indica que o valor é somente leitura.  
  
 DBGPROP_ATTRIB_ACCESS_PUBLIC  
 Indica um objeto que tem acesso público.  
  
 DBGPROP_ATTRIB_ACCESS_PRIVATE  
 Indica um objeto que tem acesso privado.  
  
 DBGPROP_ATTRIB_ACCESS_PROTECTED  
 Indica um objeto que tem acesso protegido.  
  
 DBGPROP_ATTRIB_ACCESS_FINAL  
 Indica um objeto que tem acesso final.  
  
 DBGPROP_ATTRIB_STORAGE_GLOBAL  
 Indica o armazenamento global.  
  
 DBGPROP_ATTRIB_STORAGE_STATIC  
 Indica o armazenamento estático.  
  
 DBGPROP_ATTRIB_STORAGE_FIELD  
 Indica um objeto que é uma propriedade.  
  
 DBGPROP_ATTRIB_STORAGE_VIRTUAL  
 Indica o armazenamento virtual.  
  
 DBGPROP_ATTRIB_TYPE_IS_CONSTANT  
 Indica que o tipo de objeto é constante.  
  
 DBGPROP_ATTRIB_TYPE_IS_SYNCHRONIZED  
 Indica que este slot é um thread sincronizado.  
  
 DBGPROP_ATTRIB_TYPE_IS_VOLATILE  
 Indica que este slot é volátil com relação ao armazenamento persistente.  
  
 DBGPROP_ATTRIB_HAS_EXTENDED_ATTRIBS  
 Indica que este slot tem atributos além dos bits predefinidos.  
  
 DBGPROP_ATTRIB_VALUE_IS_RETURN_VALUE  
 Indica se o valor é um valor de retorno de uma função.  
  
## <a name="remarks"></a>Comentários  
 Esses sinalizadores também são usados para filtrar o filho de um objeto. Os valores podem ser combinados com um OR bit a bit.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugProperty](../../winscript/reference/idebugproperty-interface.md)   
 [Estrutura DebugPropertyInfo](../../winscript/reference/debugpropertyinfo-structure.md)
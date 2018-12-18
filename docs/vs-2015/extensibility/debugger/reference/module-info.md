---
title: MODULE_INFO | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f9a94e5013ba8d1b4a2ce56f49a21d47acb7d467
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755843"
---
# <a name="moduleinfo"></a>MODULE_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Descreve um módulo específico (DLL, EXE ou assembly).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
typedef struct tagMODULE_INFO {   
   MODULE_INFO_FIELDS dwValidFields;  
   BSTR               m_bstrName;  
   BSTR               m_bstrUrl;  
   BSTR               m_bstrVersion;  
   BSTR               m_bstrDebugMessage;  
   UINT64             m_addrLoadAddress;  
   UINT64             m_addrPreferredLoadAddress;  
   DWORD              m_dwSize;  
   DWORD              m_dwLoadOrder;  
   FILETIME           m_TimeStamp;  
   BSTR               m_bstrUrlSymbolLocation;  
   MODULE_FLAGS       m_dwModuleFlags;  
} MODULE_INFO;  
```  
  
```csharp  
public struct MODULE_INFO {   
   public uint     dwValidFields;  
   public string   m_bstrName;  
   public string   m_bstrUrl;  
   public string   m_bstrVersion;  
   public string   m_bstrDebugMessage;  
   public ulong    m_addrLoadAddress;  
   public ulong    m_addrPreferredLoadAddress;  
   public uint     m_dwSize;  
   public uint     m_dwLoadOrder;  
   public FILETIME m_TimeStamp;  
   public string   m_bstrUrlSymbolLocation;  
   public uint     m_dwModuleFlags;  
};  
```  
  
## <a name="members"></a>Membros  
 dwValidFields  
 Uma combinação de sinalizadores do [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) enumeração que especifica quais campos são preenchidos.  
  
 m_bstrName  
 O nome do módulo.  
  
 m_bstrUrl  
 A URL do módulo.  
  
 m_bstrVersion  
 A versão do módulo.  
  
 m_bstrDebugMessage  
 Uma mensagem opcional sobre o módulo, por exemplo, "símbolos não podem ser carregados."  
  
 m_addrLoadAddress  
 O endereço de carregamento do módulo.  
  
 m_addrPreferredLoadAddress  
 O endereço de carregamento preferido do módulo.  
  
 m_dwSize  
 O tamanho do módulo.  
  
 m_dwLoadOrder  
 A ordem de carregamento do módulo.  
  
 m_TimeStamp  
 A hora em que o arquivo de símbolo foi modificado pela última vez.  
  
 m_bstrUrlSymbolLocation  
 O local do arquivo de símbolo (por exemplo, ".\\") especificado no módulo. Usado como um local de partida para localizar símbolos para um módulo.  
  
 m_dwModuleFlags  
 Uma combinação de sinalizadores do [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md) enumeração que descreve o módulo.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é passada para o [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) método onde ele é preenchido.  
  
 Essa estrutura corresponde a cada módulo listado na **módulos** janela.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)   
 [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)


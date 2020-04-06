---
title: MODULE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59ab4d0bb2a7aaa4b08f616ea0a99be85b521bb0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714308"
---
# <a name="module_info"></a>MODULE_INFO
Descreve um módulo específico (DLL, EXE ou montagem).

## <a name="syntax"></a>Sintaxe

```cpp
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
 `dwValidFields`\
 Uma combinação de bandeiras da enumeração [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) que especifica quais campos são preenchidos.

 `m_bstrName`\
 O nome do módulo.

 `m_bstrUrl`\
 A URL do módulo.

 `m_bstrVersion`\
 A versão do módulo.

 `m_bstrDebugMessage`\
 Uma mensagem opcional sobre o módulo, por exemplo, "Símbolos não podem ser carregados".

 `m_addrLoadAddress`\
 O endereço de carga do módulo.

 `m_addrPreferredLoadAddress`\
 O endereço de carga preferido do módulo.

 `m_dwSize`\
 O tamanho do módulo.

 `m_dwLoadOrder`\
 A ordem de carga do módulo.

 `m_TimeStamp`\
 A vez que o arquivo símbolo foi modificado pela última vez.

 `m_bstrUrlSymbolLocation`\
 A localização do arquivo símbolo (por\\exemplo, ". ") especificada no módulo. Usado como local de partida para encontrar símbolos para um módulo.

 `m_dwModuleFlags`\
 Uma combinação de bandeiras da enumeração [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md) que descreve o módulo.

## <a name="remarks"></a>Comentários
 Essa estrutura é passada para o método [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) onde é preenchida.

 Esta estrutura corresponde a cada módulo listado na janela **Módulos.**

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Montagem: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)

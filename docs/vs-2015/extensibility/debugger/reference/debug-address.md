---
title: DEBUG_ADDRESS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS
helpviewer_keywords:
- DEBUG_ADDRESS structure
ms.assetid: 79f5e765-9aac-4b6e-82ef-bed88095e9ba
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d001d29433573fedde3b4310f989667538b4b69c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444965"
---
# <a name="debugaddress"></a>DEBUG_ADDRESS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa estrutura representa um endereço.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _tagDEBUG_ADDRESS {  
   ULONG32             ulAppDomainID;  
   GUID                guidModule;  
   _mdToken            tokClass;  
   DEBUG_ADDRESS_UNION addr;  
} DEBUG_ADDRESS;  
```  
  
```csharp  
public struct DEBUG_ADDRESS {  
   public uint                ulAppDomainID;  
   public Guid                guidModule;  
   public int                 tokClass;  
   public DEBUG_ADDRESS_UNION addr;  
}  
```  
  
## <a name="terms"></a>Termos  
 ulAppDomainID  
 A ID de processo.  
  
 guidModule  
 O GUID do módulo que contém esse endereço.  
  
 tokClass  
 O token de identificação de classe ou tipo desse endereço.  
  
> [!NOTE]
> Esse valor é específico para um provedor de símbolo e, portanto, não tem nenhum significado geral diferente de como um identificador para um tipo de classe.  
  
 addr  
 Um [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) estrutura, que contém uma união de estruturas que descrevem os tipos de endereço individual. O valor `addr`.`dwKind` é proveniente de [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) enumeração, que explica como interpretar a união.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é passada para o [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) método a ser preenchido.  
  
 **Aviso [C++ somente]**  
  
 Se `addr.dwKind` está `ADDRESS_KIND_METADATA_LOCAL` e, se `addr.addr.addrLocal.pLocal` não é um valor nulo, em seguida, você deve chamar `Release` no ponteiro de token:  
  
```  
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL &&  addr.addr.addrLocal.pLocal != NULL)  
{  
    addr.addr.addrLocal.pLocal->Release();  
}  
```  
  
## <a name="requirements"></a>Requisitos  
 Header: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)

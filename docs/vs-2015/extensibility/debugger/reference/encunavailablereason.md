---
title: EncUnavailableReason | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0ebdc5518579223a0081f30a0affd3a45e91604e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198767"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

`This is for internal use only!` Representa os motivos que **editar e continuar** não está disponível.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum tagEncUnavailableReason {  
   ENCUN_NONE,  
   ENCUN_INTEROP,  
   ENCUN_SQLCLR,  
   ENCUN_MINIDUMP,  
   ENCUN_EMBEDDED,  
   ENCUN_ATTACH,  
   ENCUN_WIN64  
};  
typedef enum tagEncUnavailableReason EncUnavailableReason;  
```  
  
```csharp  
public enum EncUnavailableReason {  
   ENCUN_NONE,  
   ENCUN_INTEROP,  
   ENCUN_SQLCLR,  
   ENCUN_MINIDUMP,  
   ENCUN_EMBEDDED,  
   ENCUN_ATTACH,  
   ENCUN_WIN64  
};  
```  
  
#### <a name="parameters"></a>Parâmetros  
 ENCUN_NONE  
 Nenhum motivo específico por que editar e continuar não está disponível.  
  
 ENCUN_INTEROP  
 Editar e continuar não está disponível durante uma chamada de interoperabilidade.  
  
 ENCUN_SQLCLR  
 Editar e continuar não está disponível durante uma chamada de procedimento do SQL que usa o tempo de execução de linguagem comum (CLR).  
  
 ENCUN_MINIDUMP  
 Editar e continuar não está disponível durante o processamento de um minidespejo.  
  
 ENCUN_EMBEDDED  
 Editar e continuar não está disponível durante o processamento de código inserido.  
  
 ENCUN_ATTACH  
 Editar e continuar não está disponível porque a sessão foi conectada a, não seja iniciado pelo depurador.  
  
 ENCUN_WIN64  
 Editar e continuar não está disponível durante o processamento de código do Windows de 64 bits.  
  
## <a name="remarks"></a>Comentários  
 Essa enumeração é para uso interno somente pela [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. O [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) e [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) métodos conforme implementado por um fornecedor de porta personalizado devem sempre retornar `E_NOTIMPL`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.idl  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)   
 [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)

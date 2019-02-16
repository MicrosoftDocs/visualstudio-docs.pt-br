---
title: EncUnavailableReason | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7ccc05c58eafe6f8902b3f8ac09b90dc771a3009
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56315677"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!` Representa os motivos que **editar e continuar** não está disponível.

## <a name="syntax"></a>Sintaxe

```cpp
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
Essa enumeração é para uso interno somente pela [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]. O [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) e [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) métodos conforme implementado por um fornecedor de porta personalizado devem sempre retornar `E_NOTIMPL`.

## <a name="requirements"></a>Requisitos
Header: msdbg.idl

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
[Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)


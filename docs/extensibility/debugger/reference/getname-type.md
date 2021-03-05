---
description: Especifica o tipo de nome dos arquivos a serem recuperados.
title: GETNAME_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- GETNAME_TYPE
helpviewer_keywords:
- GETNAME_TYPE enumeration
ms.assetid: 2f9f1679-e9e8-4c9c-ac90-aa07bfe69914
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9811312188e63017e074d12be6dfa67ab6929aa6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162440"
---
# <a name="getname_type"></a>GETNAME_TYPE
Especifica o tipo de nome dos arquivos a serem recuperados.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
typedef DWORD GETNAME_TYPE;
```

```csharp
public enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
```

## <a name="fields"></a>Campos
`GN_NAME`\
Especifica um nome amigável do documento ou contexto.

`GN_FILENAME`\
Especifica o caminho completo do documento ou contexto.

`GN_BASENAME`\
Especifica um nome de arquivo base em vez de um caminho completo do documento ou contexto.

`GN_MONIKERNAME`\
Especifica um nome exclusivo do documento ou contexto na forma de um moniker.

`GN_URL`\
Especifica um nome de URL do documento ou contexto.

`GN_TITLE`\
Especifica um título do documento, se houver.

`GN_STARTPAGEURL`\
Obtém a URL da página inicial para processos.

## <a name="remarks"></a>Comentários
Esses valores são passados como parâmetros para os métodos [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md), [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)e [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) para especificar o tipo de nome a ser retornado.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)

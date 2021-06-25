---
title: Posição do documento | Microsoft Docs
description: Saiba como uma posição de documento Visual Studio depuração fornece uma abstração de uma posição em um arquivo de origem, conforme conhecido pelo IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58a3ac3db62619c5d0eaa9e89e09d7d5def06ff1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898143"
---
# <a name="document-position"></a>Posição do documento
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, uma posição *de documento*:

- Fornece uma abstração de uma posição em um arquivo de origem, conforme conhecido pelo IDE. Para a maioria dos idiomas atualmente, uma posição de documento pode ser pensada como uma posição em um arquivo de origem.

- Descreve uma posição em um documento de origem para um mecanismo de depuração.

- É implementado por uma interface [IDebugDocumentPosition2.](../../extensibility/debugger/reference/idebugdocumentposition2.md)

## <a name="see-also"></a>Confira também
- [Contexto de código](../../extensibility/debugger/code-context.md)
- [Contexto do documento](../../extensibility/debugger/document-context.md)
- [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)
- [Interfaces do provedor de símbolos](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)

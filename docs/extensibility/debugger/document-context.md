---
title: Contexto de documento | Microsoft Docs
description: Saiba mais sobre o contexto de documento na depuração do Visual Studio, que representa uma posição em um arquivo de origem ou uma posição em um documento de origem para um contexto de código.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a4b7554e274977f23474f6cf3e8e1af30d9e73b3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898182"
---
# <a name="document-context"></a>Contexto do documento
Em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, um *contexto de documento*:

- Representa uma posição em um arquivo de origem. Para idiomas em que o arquivo de origem pode não estar presente, um contexto de documento identifica uma posição em um documento normalmente gerada pelo ambiente de tempo de execução. Por exemplo, um mecanismo de script pode gerar um documento a partir do script. Para obter mais informações, consulte [posição do documento](../../extensibility/debugger/document-position.md).

- Descreve uma posição em um documento de origem que corresponde a um contexto de código. O manipulador de símbolos mapeia um contexto de código para o contexto de documentação, usando informações geradas por um compilador ou intérprete.

- É implementado por uma interface [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) .

## <a name="see-also"></a>Confira também
- [Contexto de código](../../extensibility/debugger/code-context.md)
- [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)
- [Interfaces de provedor de símbolo](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)

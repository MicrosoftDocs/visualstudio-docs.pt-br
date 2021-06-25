---
title: Provedores de porta | Microsoft Docs
description: Este artigo descreve a definição e a função de um fornecedor de porta na arquitetura do depurador Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0526135f706a42c622617a069e501297570e3b49
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899115"
---
# <a name="port-suppliers"></a>Fornecedores de porta
Na arquitetura do depurador, um *fornecedor de porta*:

- Está contido por um servidor e fornece portas na solicitação para esse servidor.

- Pode adicionar e remover portas do servidor que o contém.

- Pode enumerar todas as portas fornecidas ao servidor.

- É representado por uma interface [IDebugPortSupplier2,](../../extensibility/debugger/reference/idebugportsupplier2.md) que é registrada com Visual Studio por meio do Registro. Essa interface pode ser obtida chamando [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md).

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece um fornecedor de porta padrão e uma porta padrão. Se uma porta personalizada precisar ser implementada, um fornecedor de porta personalizado também precisará ser implementado para fornecer essas portas personalizadas.

## <a name="see-also"></a>Confira também
- [Servidores](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [Portas](../../extensibility/debugger/ports.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)

---
title: Fornecedores de porta | Microsoft Docs
description: Este artigo descreve a definição e a função de um fornecedor de porta na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ace9a7072287fa26aee3fa2abd083cc9f7f1314
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067797"
---
# <a name="port-suppliers"></a>Fornecedores de porta
Na arquitetura do depurador, um *fornecedor de porta*:

- Está contido em um servidor e fornece portas na solicitação para esse servidor.

- Pode adicionar e remover portas do servidor que a contém.

- Pode enumerar todas as portas que ele forneceu para o servidor.

- É representado por uma interface [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) , que é registrada com o Visual Studio por meio do registro. Essa interface pode ser obtida chamando [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md).

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece um fornecedor de porta padrão e uma porta padrão. Se uma porta personalizada precisar ser implementada, um fornecedor de porta personalizado também precisará ser implementado para fornecer essas portas personalizadas.

## <a name="see-also"></a>Confira também
- [Servidores](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [Portas](../../extensibility/debugger/ports.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)

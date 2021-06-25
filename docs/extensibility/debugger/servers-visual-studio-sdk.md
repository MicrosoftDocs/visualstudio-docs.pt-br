---
title: Servidores (Visual Studio SDK) | Microsoft Docs
description: Este artigo descreve a definição e a função de um servidor na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 99f6c634053df9191ac419c8ee450dc99cf62c7c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902118"
---
# <a name="servers-visual-studio-sdk"></a>Servidores (SDK do Visual Studio)
Na arquitetura do depurador, um *servidor*:

- É um contêiner de portas e fornecedores de porta e comunica portas e fornecedores de porta para o SDM (gerenciador de depuração de sessão) e mecanismos de depuração.

- Pode se identificar por nome e enumerar suas portas e fornecedores de porta.

- É representado por uma interface [IDebugCoreServer2,](../../extensibility/debugger/reference/idebugcoreserver2.md) que é implementada apenas por Visual Studio (uma instância de um servidor para cada instância do Visual Studio em execução).

## <a name="see-also"></a>Confira também
- [Portas](../../extensibility/debugger/ports.md)
- [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)

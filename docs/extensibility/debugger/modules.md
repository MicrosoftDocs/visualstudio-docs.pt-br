---
title: Módulos | Microsoft Docs
description: Este artigo descreve a definição e a função de um módulo na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 03a3ad588b0a2e0f3aa6f04ddeb742ab66064bc9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902599"
---
# <a name="modules"></a>Módulos
Em termos da arquitetura do depurador, um *módulo*:

- É um contêiner físico de código, como um arquivo executável ou uma DLL.

- Pode recarregar seus símbolos e se descrever. As descrições de módulo são exibidas na janela módulos do IDE.

- É representado por uma interface [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) , criada por um mecanismo de depuração para descrever o módulo.

## <a name="see-also"></a>Confira também
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)

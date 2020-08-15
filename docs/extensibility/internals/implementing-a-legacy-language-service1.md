---
title: Implementando um Service1 de linguagem herdada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2535c527fc3d2d94609246959c5293e455b9808d
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238732"
---
# <a name="implementing-a-legacy-language-service-1"></a>Implementando um serviço de linguagem herdada 1
Você pode usar classes na MPF (estrutura de pacote gerenciada) para implementar um serviço de linguagem herdado que dá suporte a uma ampla variedade de recursos, como realce de sintaxe, correspondência de chaves e conclusão do IntelliSense.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar um serviço de linguagem, consulte [extensões de serviço de editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="in-this-section"></a>Nesta seção
- [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)

 Uma visão geral dos recursos de serviço de linguagem com suporte no MPF.

- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 Descreve o que é necessário para implementar um serviço de linguagem usando o MPF.

- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)

 Descreve as etapas necessárias para registrar um serviço de linguagem baseado em MPF com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 Descreve os dois analisadores que são necessários para implementar todos os recursos de um serviço de idioma usando o MPF.

- [Passo a passo: Criando um serviço de linguagem herdado](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 Fornece as etapas básicas necessárias para implementar um serviço de idioma do MPF em um VSPackage.

- [Passo a passo: Obtendo uma lista de snippets de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 Demonstra as técnicas de recuperação de uma lista de trechos de código instalados.

- [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)

 Fornece links para tópicos que detalham o que deve ser feito para implementar todos os recursos de um serviço de linguagem usando o MPF.

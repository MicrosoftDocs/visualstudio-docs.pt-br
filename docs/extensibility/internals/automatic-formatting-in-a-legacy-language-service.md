---
title: Formatação automática em um serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre a formatação automática em um serviço de linguagem herdada, que insere automaticamente um trecho de código quando você começa a digitar uma construção de código conhecida.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a08a56a6820917b3a954c162b1875430875c7585
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086268"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>Formatação automática em um serviço de idioma herdado
Com a formatação automática, um serviço de idioma insere automaticamente um trecho de código quando um usuário começa a digitar uma construção de código conhecida.

## <a name="automatic-formatting-behavior"></a>Comportamento de formatação automática
 Por exemplo, quando você digita *se*, o serviço de idioma insere automaticamente as chaves correspondentes ou, se você pressionar a tecla Enter, o serviço de idioma forçará o ponto de inserção na nova linha para o nível de recuo apropriado, dependendo se a linha anterior abre um novo escopo.

 O filtro de comando usado para o restante do serviço de idioma também pode ser usado para formatação automática. Você também pode realçar as chaves correspondentes chamando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> .

## <a name="see-also"></a>Confira também
- [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)

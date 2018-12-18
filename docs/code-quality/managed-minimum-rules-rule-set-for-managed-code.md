---
title: Gerenciado mínimo conjunto de regras para código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: bf05f4787cbd393173380be8123657abeddc0cd5
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39204503"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>Gerenciado mínimo conjunto de regras para código gerenciado

As regras de gerenciado mínimo enfocam os problemas mais críticos do código, inclusive falhas potenciais de segurança, falhas do aplicativo e outros erros importantes de lógica e design. Inclua este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos.

|Regra|Descrição|
|----------|-----------------|
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|Tipos que possuem campos descartáveis devem ser descartáveis|
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|Remova finalizadores vazios|
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|Campos descartáveis devem ser descartados|
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|Sobrecarregar operador equals ao substituir ValueType.Equals&lt;2}&lt;1}|

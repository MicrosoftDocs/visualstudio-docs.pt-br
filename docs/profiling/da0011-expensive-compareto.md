---
title: DA0011-CompareTo caro | Microsoft Docs
description: O método CompareTo de tipo é dispendioso ou aloca memória.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0011
- vs.performance.rules.DAExpensiveCompareTo
- vs.performance.11
- vs.performance.rules.DA0011
ms.assetid: 239a381d-0d97-4367-8668-746c93f5af2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 91219bed2ca0e8b4bbc28825e1505b9d5f78bbc8
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466148"
---
# <a name="da0011-expensive-compareto"></a>DA0011: Função CompareTo dispendiosa

|Item|Valor|
|-|-|
|ID de regra|DA0011|
|Categoria|Uso do .NET Framework|
|Métodos de criação de perfil|amostragem<br /><br /> Memória do .NET|
|Mensagem|As funções de CompareTo devem ser baratas e podem não alocar nenhuma memória. Reduza a complexidade da função CompareTo se possível.|
|Tipo de regra|Aviso|

## <a name="cause"></a>Causa
 O método CompareTo de tipo é dispendioso ou aloca memória.

## <a name="rule-description"></a>Descrição da regra
 Os métodos do CompareTo devem ser eficientes e não devem alocar memória.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Reduza a complexidade do método CompareTo.

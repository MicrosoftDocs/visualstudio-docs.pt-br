---
title: 'DA0011: CompareTo dispendioso | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0011
- vs.performance.rules.DAExpensiveCompareTo
- vs.performance.11
- vs.performance.rules.DA0011
ms.assetid: 239a381d-0d97-4367-8668-746c93f5af2c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4f6137c07ac6b920234a9772764b5ad758efdb1e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49818842"
---
# <a name="da0011-expensive-compareto"></a>DA0011: função CompareTo dispendiosa

|||  
|-|-|  
|ID de regra|DA0011|  
|Categoria|Uso do .NET Framework|  
|Métodos de criação de perfil|Amostragem<br /><br /> Memória do .NET|  
|Mensagem|As funções de CompareTo devem ser baratas e podem não alocar nenhuma memória. Reduza a complexidade da função CompareTo se possível.|  
|Tipo de regra|Aviso|  

## <a name="cause"></a>Causa  
 O método CompareTo de tipo é dispendioso ou aloca memória.  

## <a name="rule-description"></a>Descrição da regra  
 Os métodos do CompareTo devem ser eficientes e não devem alocar memória.  

## <a name="how-to-fix-violations"></a>Como corrigir violações  
 Reduza a complexidade do método CompareTo.
---
title: DA0029-versão do CLR sem suporte | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.29
- vs.performance.rules.DA0029
helpviewer_keywords:
- vs.performance.29
- vs.performance.DA0029
- vs.performance.rules.DA0029
ms.assetid: 76247259-c6f3-44c4-b3f9-d8dac16b5e0d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 14e0bb4290ad155b7094c0f60810df4f86cb8d65
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544632"
---
# <a name="da0029-unsupported-clr-version"></a>DA0029: versão do CLR não compatível

|Item|Valor|
|-|-|
|ID de regra|DA0029|
|Categoria|Uso das ferramentas de criação de perfil|
|Método de criação de perfil|Criação de perfil da linha de comando|
|Mensagem|Uma versão do CLR sem suporte foi detectada durante a coleta. Talvez os símbolos gerenciados não resolvam corretamente.|
|Tipo de regra|Informações.|

## <a name="cause"></a>Causa
 Você está tentando criar o perfil de um aplicativo que usa o [!INCLUDE[net_v11_long](../profiling/includes/net_v11_long_md.md)], que não é suportado pelas ferramentas de criação de perfil.

## <a name="rule-description"></a>Descrição da regra
 Você recebeu este aviso porque as ferramentas de criação de perfil são incapazes de resolver os símbolos para o código gerenciado em execução no aplicativo. As ferramentas de criação de perfil não podem resolver os símbolos de código gerenciado para aplicativos que estão executando o [!INCLUDE[net_v11_long](../profiling/includes/net_v11_long_md.md)].

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Nenhum.

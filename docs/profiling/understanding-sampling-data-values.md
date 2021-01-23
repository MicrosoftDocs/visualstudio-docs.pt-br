---
title: Noções básicas sobre valores de dados de amostragem | Microsoft Docs
description: Saiba como o método de criação de perfil de amostragem do Visual Studio Ferramentas de Criação de Perfil interrompe o processador do computador em intervalos definidos e coleta a pilha de chamadas de função.
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method
- Profiling Tools, sampling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 81efd0f20ba971555ec8c1333dfc322112f13e17
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98722159"
---
# <a name="understand-sampling-data-values"></a>Noções básicas sobre valores de dados de amostragem

O método de criação de perfil de *amostragem* das Ferramentas de Criação de Perfil do Visual Studio interrompe o processador do computador em intervalos definidos e coleta a pilha de chamadas de função. Uma *pilha de chamadas* é uma estrutura dinâmica que armazena informações sobre as funções que estão em execução no processador.

A análise do criador de perfil determina se o processador está executando código no processo de destino. Se o processador não está executando código no processo de destino, o exemplo é descartado.

Se o processador está executando o código de destino, o criador de perfil incrementa as contagens de amostragem para cada função na pilha de chamadas. No momento em que a amostra é coletada, apenas uma função na pilha de chamadas está executando código. As outras funções na pilha são pais na hierarquia de chamadas de função que estão aguardando para seus filhos retornarem.

Para o evento de exemplo, o criador de perfil incrementa a contagem de exemplo *exclusiva* da função que está executando as instruções de exemplo. Como um exemplo exclusivo também é parte do total de exemplos (*inclusivo*) da função, a contagem inclusiva de amostras da função atualmente ativa também será incrementada.

 O criador de perfil incrementa a contagem inclusiva de exemplo de todas as outras funções na pilha de chamadas.

## <a name="inclusive-samples"></a>Amostras inclusivas

O número total de amostras que são coletadas durante a execução da função de destino.

Isso inclui exemplos que são coletados durante a execução direta de código da função e exemplos que são coletados durante a execução de funções filho que são chamadas pela função de destino.

## <a name="exclusive-samples"></a>Amostras exclusivas

O número de amostras que são coletadas durante a execução direta de instruções da função de destino.

Amostras exclusivas não incluem exemplos que são coletados durante a execução de funções que são chamadas pela função de destino.

## <a name="inclusive-percent"></a>Porcentagem Inclusiva

O percentual do número total de amostras inclusivas na criação de perfil que são amostras inclusivas do intervalo de dados ou função.

## <a name="exclusive-percent"></a>Porcentagem Exclusiva

O percentual do número total de amostras exclusivas na criação de perfil que são amostras exclusivas do intervalo de dados ou função.

## <a name="see-also"></a>Confira também

[Como: escolher métodos](../profiling/how-to-choose-collection-methods.md) 
 de coleção [Analisar dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md)

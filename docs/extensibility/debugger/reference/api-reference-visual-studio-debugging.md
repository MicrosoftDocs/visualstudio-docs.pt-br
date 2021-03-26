---
description: A seção de referência inclui uma visão geral conceitual da API, um guia que mostra a sintaxe e o uso de todos os elementos da API e uma variedade de exemplos de código.
title: Referência de API (depuração do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], API reference
ms.assetid: e4e429da-3667-41f7-9158-a8207d13e91a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a8a43e4bae5afce98e07b196f5a01c33d44c72ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085540"
---
# <a name="api-reference-visual-studio-debugging"></a>Referência de API (depuração no Visual Studio)
A seção de referência inclui uma visão geral conceitual da API, um guia que mostra a sintaxe e o uso de todos os elementos da API e uma variedade de exemplos de código. Todas as referências são listadas alfabeticamente por categoria.

 A tabela a seguir mostra os `HRESULT` valores comuns retornados pelos métodos.

|Nome|Descrição|Valor|
|----------|-----------------|-----------|
|S_OK|Sucesso.|0x00000000|
|E_UNEXPECTED|Falha inesperada.|0x8000FFFF|
|E_NOTIMPL|Não implementado.|0x80004001|
|E_OUTOFMEMORY|Não há memória suficiente para concluir a operação.|0x8007000E|
|E_INVALIDARG|Um ou mais argumentos são inválidos.|0x80070057|
|E_NOINTERFACE|Não há suporte para essa interface.|0x80004002|
|E_POINTER|Ponteiro inválido.|0x80004003|
|E_HANDLE|Identificador inválido.|0x80070006|
|E_ABORT|Operação anulada.|0x80004004|
|E_FAIL|Falha inesperada.|0x80004005|
|E_ACCESSDENIED|Erro geral de acesso negado.|0x80070005|

> [!NOTE]
> Quando um [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] método de depuração retorna `S_OK` , supõe-se que todos os ponteiros de parâmetro out sejam válidos, ou seja, nenhuma validação é conduzida nos ponteiros de parâmetro out quando `S_OK` é retornada.
>
> [!NOTE]
> Parâmetros inválidos ou `NULL` [out] podem fazer com que o IDE falhe.

## <a name="see-also"></a>Confira também
- [Interfaces](../../../extensibility/debugger/reference/interfaces-visual-studio-debugging.md)
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Extensibilidade do depurador do Visual Studio](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)

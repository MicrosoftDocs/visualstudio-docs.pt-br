---
title: Enumeradores | Microsoft Docs
description: Saiba mais sobre os tipos de dados do enumerador na API de plug-in de controle do código-fonte, incluindo código de comando, mensagem, código de status do arquivo e código de status do diretório.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0bdc42901cbdad3b30bb6739ec93b8979b0d56ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075270"
---
# <a name="enumerators"></a>Enumeradores
Esta seção lista os tipos de dados do enumerador na API de plug-in de controle do código-fonte que o plug-in de controle do código-fonte deve conhecer.

## <a name="in-this-section"></a>Nesta seção
- [Código de comando](../extensibility/command-code-enumerator.md) Enumera as opções para as funções [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) e [SccPopulateList](../extensibility/sccpopulatelist-function.md) .

- [Mensagem](../extensibility/message-enumerator.md) de Enumera sinalizadores usados para o retorno de chamada de impressão, [LPTEXTOUTPROC](../extensibility/lptextoutproc.md).

- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md) Contém valores de constantes nomeados que especificam o estado de um arquivo sob controle do código-fonte.

- [Código de status do diretório](../extensibility/directory-status-code-enumerator.md) Contém valores de constantes nomeados que especificam o estado de um diretório sob controle do código-fonte.

## <a name="related-sections"></a>Seções relacionadas
- [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md) Define o SDK de plug-in de controle do código-fonte e descreve os recursos incluídos.

- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) Solicita ao usuário as opções avançadas para o comando fornecido.

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) Examina a lista de arquivos em busca de seu status atual. Além disso, o usa a `pfnPopulate` função para notificar o chamador quando um arquivo não corresponde aos critérios para o `nCommand` .

- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) Descreve a função de retorno de chamada usada pelo [SccOpenProject](../extensibility/sccopenproject-function.md) para exibir mensagens do plug-in de controle do código-fonte por meio do IDE.

- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md) Fornece uma listagem completa de todos os elementos na API de plug-in de controle do código-fonte.

---
title: Aplicar configurações em várias conexões de projeto
description: Saiba como aplicar configurações em várias conexões de projeto usando um plug-in de controle do código-fonte para executar uma operação em lote.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 71b4a3de89653ab63f57171bcb52ee32ddfcf07d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078988"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>Aplicação de configurações em várias conexões de projeto
Um plug-in de controle do código-fonte criado usando a API de plug-in de controle do código-fonte versão 1,2 pode usar uma operação em lote para executar a mesma operação de controle do código-fonte em vários projetos ou em vários contextos de conexão. Os lotes podem ser usados para eliminar caixas de diálogo redundantes por projeto da experiência do usuário.

 Se um usuário selecionar vários itens que pertencem a mais de uma conexão em um plug-in de controle do código-fonte criado usando a API de plug-in de controle do código-fonte versão 1,1 (por exemplo, dois projetos da Web em diferentes máquinas de compartilhamento de arquivos) e os verificar, o usuário verá a mesma caixa de diálogo repetidamente. Esse cenário ocorre mesmo se o usuário clicar na caixa de seleção **aplicar a todos** na caixa de diálogo, pois o IDE redefine seu estado para cada contexto de conexão.

## <a name="new-capability-flag"></a>Novo sinalizador de funcionalidade
 A `SccBeginBatch` função define o `SCC_CAP_BATCH` sinalizador para indicar que uma operação em lote está em andamento.

## <a name="new-functions"></a>Novas funções
As novas funções a seguir dão suporte à operação em lote:

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

A `SCCBeginBatch` função inicia um grupo de operações de controle do código-fonte. A `SccEndBatch` função fecha o grupo. Os grupos não podem ser aninhados.

## <a name="see-also"></a>Confira também
- [O que há de novo na API de plug-in de controle do código-fonte versão 1,2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

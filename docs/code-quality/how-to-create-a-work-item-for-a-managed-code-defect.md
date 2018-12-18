---
title: Como criar um item de trabalho para um defeito de código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- managed code, creating work items for code defects
- code analysis, creating work items
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: b251970bfd57b31842e1573e2e156e11a517c81a
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44279467"
---
# <a name="how-to-create-a-work-item-for-a-managed-code-defect"></a>Como criar um item de trabalho para um defeito de código gerenciado

Você pode usar o recurso de rastreamento de item de trabalho para o item de trabalho do log de dentro do Visual Studio. Para usar esse recurso, o projeto deve ser parte de um projeto de DevOps do Azure no [!INCLUDE[esprfound](../code-quality/includes/esprfound_md.md)].

## <a name="to-create-a-work-item-for-managed-code-defect"></a>Para criar um item de trabalho para defeitos de código gerenciado

1. No **análise de código** janela, selecione o aviso.

2. Escolher **ações**, em seguida, escolha **Criar Item de trabalho** e escolha o tipo de item de trabalho a ser criado.

     Um novo item de trabalho é criado para você especificar as informações de defeito.

## <a name="to-create-a-work-item-for-multiple-managed-code-defects"></a>Para criar um item de trabalho para vários defeitos de código gerenciado

1. No **Error List**, selecione vários avisos e, em seguida, clique com botão direito os avisos.

2. Aponte para **Criar Item de trabalho** e clique no tipo de item de trabalho para criar.

     Um único item de trabalho é criado para todos os avisos selecionados para que você especifique as informações de bug.
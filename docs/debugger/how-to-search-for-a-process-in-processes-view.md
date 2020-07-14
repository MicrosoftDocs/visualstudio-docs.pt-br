---
title: Como pesquisar um processo no modo de exibição de processos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e823ecb1f7523c1a6f094d5669f4a37a72e84f60
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349283"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>Como procurar um processo na exibição de processos
Você pode pesquisar um processo específico na exibição de processos usando sua ID de processo ou cadeia de caracteres de módulo como critérios de pesquisa. Você também pode especificar a direção inicial da pesquisa. Os campos na caixa de diálogo mostrarão os atributos do processo selecionado na árvore de processo.

### <a name="to-search-for-a-process-in-processes-view"></a>Para procurar um processo na exibição de processos

1. Organize suas janelas para que o Spy + + e uma janela de [exibição de processos](../debugger/processes-view.md) ativos fiquem visíveis.

2. No menu **Pesquisar** , escolha **Localizar processo**

    A [caixa de diálogo pesquisa de processo](../debugger/process-search-dialog-box.md) é aberta.

3. Digite a ID do processo ou uma cadeia de caracteres do módulo como critérios de pesquisa.

4. Desmarque os campos para os quais você não deseja especificar valores.

   > [!TIP]
   > Para localizar todos os processos pertencentes a um módulo, desmarque a caixa **processar** e digite o nome do módulo na caixa **módulo** . Em seguida, use **Localizar próximo** para continuar pesquisando processos.

5. Escolha para **cima** ou para **baixo** na direção inicial da pesquisa.

6. Clique em **OK**.

   Se um processo de correspondência for encontrado, ele será realçado na janela de **exibição de processo** .
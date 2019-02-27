---
title: 'Como: pesquisar por um processo na exibição de processos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c9cd618768268b5c0bc4e3e99fbffd4fd65e874
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56715083"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>Como procurar um processo na exibição de processos
Você pode procurar um processo específico na exibição de processos por meio de sua cadeia de caracteres de ID ou o módulo de processo como critérios de pesquisa. Você também pode especificar a direção inicial da pesquisa. Os campos na caixa de diálogo mostrará os atributos do processo selecionado na árvore de processo.

### <a name="to-search-for-a-process-in-processes-view"></a>Para pesquisar por um processo na exibição de processos

1. Organizar as janelas assim que Spy + + e um ativo [exibição de processos](../debugger/processes-view.md) janela são visíveis.

2. Dos **pesquisa** menu, escolha **localizar processo**

    O [caixa de diálogo de pesquisa de processo](../debugger/process-search-dialog-box.md) é aberta.

3. Como critérios de pesquisa, digite a ID do processo ou uma cadeia de caracteres do módulo.

4. Limpe todos os campos para o qual você deseja especificar valores.

   > [!TIP]
   >  Para localizar todos os processos pertencentes a um módulo, desmarque a **processo** caixa e digite o nome do módulo na **módulo** caixa. Em seguida, use **Localizar próximo** para continuar a pesquisa de processos.

5. Escolher **para cima** ou **para baixo** para a direção inicial da pesquisa.

6. Clique em **OK**.

   Se um processo de correspondência for encontrado, ele é realçado na **exibição de processo** janela.
---
title: Janela de métricas de código
ms.date: 12/12/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6aa1de7b3c4a029038072e84bea1918ea33031db
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967162"
---
# <a name="use-the-code-metrics-results-window"></a>Use a janela de resultados de métricas de código

O **resultados de métricas de código** janela exibe os dados que são gerados pela análise de métricas de código. Para obter mais informações sobre valores de dados de métricas de código, consulte [valores de métricas de código](../code-quality/code-metrics-values.md).

## <a name="display-code-metrics-results"></a>Exibir resultados de métricas de código

O **resultados de métricas de código** janela é exibida automaticamente quando você gera resultados de métricas de código. Você também pode exibir a janela a qualquer momento.

Você pode exibir a janela de resultados de métricas de código usando uma das sequências de menu a seguir:

- Sobre o **Analyze** menu, escolha **Windows** > **resultados de métricas de código**.

- Sobre o **modo de exibição** menu, escolha **Other Windows** > **resultados de métricas de código**.

O **resultados de métricas de código** janela é aberta, mesmo se ele não contém nenhum resultado.

### <a name="to-view-code-metrics-details"></a>Para exibir os detalhes das métricas de código

Se os resultados de métricas de código foram gerados, expanda a árvore na **hierarquia** coluna.

## <a name="filter-code-metrics-results"></a>Filtrar resultados de métricas de código

Você pode filtrar os resultados que são exibidos na **resultados de métricas de código** janela usando a barra de ferramentas na parte superior. Por exemplo, você talvez queira ver apenas os resultados que tem um índice de facilidade de manutenção abaixo 65.

O **filtro** caixa suspensa contém os nomes das colunas de resultados. Quando um filtro é definido, ele é adicionado à parte inferior da lista junto com um recuo. A lista pode conter os últimos 10 filtros que foram definidos.

### <a name="to-filter-the-code-metrics-results"></a>Para filtrar os resultados de métricas de código

1.  Dos **filtro** , selecione o nome da coluna.

2.  Na **Min**, digite o valor mínimo a ser exibido.

3.  Na **máx**, digite o valor máximo a ser exibido.

4.  Clique o **Aplicar filtro** botão.

5.  Para ver os detalhes do resultado, expanda a árvore de hierarquia.

## <a name="add-remove-and-rearrange-data-columns"></a>Adicionar, remover e reorganizar as colunas de dados

Você pode adicionar ou remover de colunas de resultados de **resultados de métricas de código** janela. Além disso, você pode reorganizar as colunas de resultados para que eles apareçam na ordem em que você deseja.

### <a name="add-or-remove-a-column"></a>Adicionar ou remover uma coluna

1. Clique o **Adicionar/remover colunas** botão, ou qualquer cabeçalho de coluna com o botão direito e, em seguida, clique em **Adicionar/remover colunas**.

1. No **Adicionar/remover colunas** caixa de diálogo, marque ou desmarque a caixa de seleção para a coluna que você deseja adicionar ou remover e, em seguida, escolha **Okey**.

### <a name="rearrange-columns"></a>Reorganizar colunas

1. Clique o **Adicionar/remover colunas** botão.

1. No **Adicionar/remover colunas** caixa de diálogo, selecione a coluna que você deseja mover e, em seguida, escolha a seta para cima ou seta para baixo.

1. Quando a coluna é posicionada onde você deseja, escolha **Okey**.

## <a name="copy-data-to-the-clipboard-or-excel"></a>Copiar dados para o Excel ou área de transferência

Você pode selecionar e copiar uma linha de dados de métricas de código selecionada para a área de transferência como uma cadeia de caracteres de texto que contém uma linha para o nome e valor de cada coluna de dados. Você também pode clicar **abrir seleção no Microsoft Excel** para exportar todos os resultados de métricas de código para uma planilha do Excel.

## <a name="create-a-work-item-based-on-code-metric-results"></a>Criar um item de trabalho com base nos resultados de métricas de código

Você pode criar uma [Azure quadros](/azure/devops/boards/index?view=vsts) resulta de item de trabalho que se baseia na **resultados de métricas de código** janela. Quando o item de trabalho é criado, o Visual Studio entra automaticamente em um título a **Title** dados de métricas de campo e o código sob o **histórico** guia.

Para obter mais informações sobre os quadros de Azure itens de trabalho, consulte [itens de trabalho](/azure/devops/boards/work-items/index?view=vsts).

### <a name="to-create-a-work-item-based-on-a-result"></a>Para criar um item de trabalho com base em um resultado

1.  Clique com botão direito o resultado.

2.  Aponte para **Criar Item de trabalho**e, em seguida, clique no tipo de item de trabalho que você deseja criar (**Bug**, **tarefa**e assim por diante).

3.  Conclua o formulário de item de trabalho ao preencher todos os campos obrigatórios.

4.  Sobre o **arquivo** menu, clique em **Salvar tudo** para salvar o item de trabalho.

### <a name="to-create-a-bug-based-on-a-result"></a>Para criar um bug com base em um resultado

1.  Clique no resultado para selecioná-lo.

2.  Clique o **Criar Item de trabalho** botão.

3.  Conclua o formulário de item de trabalho ao preencher todos os campos obrigatórios.

4.  Sobre o **arquivo** menu, clique em **Salvar tudo** para salvar o item de trabalho.

## <a name="see-also"></a>Consulte também

- [Valores de métricas de código](../code-quality/code-metrics-values.md)
- [Como: gerar dados de métricas de código](../code-quality/how-to-generate-code-metrics-data.md)
---
title: Trabalhando com dados de métricas de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
ms.assetid: 988193ec-b4a3-4e11-b5a1-7334979807d5
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: ca9d384b8c7b6d49e44826c65a156d715baa0786
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51775882"
---
# <a name="working-with-code-metrics-data"></a>Trabalhando com dados de métricas de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **resultados de métricas de código** janela exibe os dados que são gerados pela análise de métricas de código. Para obter mais informações sobre valores de dados de métricas de código, consulte [valores de métricas de código](../code-quality/code-metrics-values.md).  
  
 Esse tópico contém as seguintes seções:  
  
-   [Janela de resultados de métricas de código](../code-quality/working-with-code-metrics-data.md#BKMK_CodeMetricsResultsWindow)  
  
-   [Exibindo resultados de métricas de código](../code-quality/working-with-code-metrics-data.md#BKMK_DisplayingCodeMetricsResults)  
  
-   [Filtrando resultados de métricas de código](../code-quality/working-with-code-metrics-data.md#BKMK_FilteringCodeMetricsResults)  
  
-   [Adicionando, removendo e reorganizando as colunas de dados](../code-quality/working-with-code-metrics-data.md#BKMK_AddingRemovingandRearrangingDataColumns)  
  
-   [Copiando dados para a área de transferência ou o Excel](../code-quality/working-with-code-metrics-data.md#BKMK_Copying_Data_to_the_Clipboard_or_Excel)  
  
-   [Criando um Item de trabalho com base nos resultados de métricas de código](../code-quality/working-with-code-metrics-data.md#BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results)  
  
##  <a name="BKMK_CodeMetricsResultsWindow"></a> Janela de resultados de métricas de código  
 O **resultados de métricas de código** janela tem uma barra de ferramentas na parte superior e colunas para exibir os resultados calculados.  
  
|Column|Descrição|  
|------------|-----------------|  
|**hierarquia**|O **hierarquia** coluna contém uma exibição de árvore da hierarquia de código que você pode expandir ou recolher para ver o nível de detalhe que você deseja. As colunas restantes mostram os resultados calculados. Você pode ocultar ou organizar as colunas de resultados, como você deseja.|  
|**facilidade de manutenção**|O **facilidade de manutenção** coluna contém um ícone, bem como o resultado numérico. Um ícone verde indica um relativamente alto grau de facilidade de manutenção. Um ícone amarelo indica um nível moderado de facilidade de manutenção. Um ícone vermelho indica pouca facilidade de manutenção e um potencial ponto problemático. Esses indicadores de cor correspondem às categorias de gravidade que são usadas pela regra de FxCop AvoidUnmaintainableCode. Essa regra dispara um erro se o índice de facilidade de manutenção for inferior a 10, um aviso se o índice é entre 10 e 20 e não um erro nem um aviso se o índice for maior do que 20. O índice de facilidade de manutenção é uma síntese de três métricas: complexidade ciclomática, linhas de código e complexidade computacional. Seus valores não são expressos em unidades.|  
  
##  <a name="BKMK_DisplayingCodeMetricsResults"></a> Exibindo resultados de métricas de código  
 A janela resultados de métricas de código é exibida automaticamente quando você gera resultados de métricas de código. Você também pode exibir a janela a qualquer momento.  
  
#### <a name="to-display-the-code-metrics-results-window"></a>Para exibir a janela de resultados de métricas de código  
  
-   Sobre o **Analyze** menu, clique em **Windows** e, em seguida, clique em **resultados de métricas de código**.  
  
     \- ou -  
  
-   Sobre o **modo de exibição** , aponte para **Other Windows** e, em seguida, clique em **resultados de métricas de código**.  
  
     A janela resultados de métricas de código é exibida mesmo quando ele não contém nenhum resultado.  
  
#### <a name="to-view-code-metrics-details"></a>Para exibir os detalhes das métricas de código  
  
-   Se os resultados de métricas de código foram gerados, expanda a árvore na **hierarquia** coluna.  
  
##  <a name="BKMK_FilteringCodeMetricsResults"></a> Filtrando resultados de métricas de código  
 Você pode filtrar os resultados que são exibidos na **resultados de métricas de código** janela usando a barra de ferramentas na parte superior. Por exemplo, você talvez queira ver apenas os resultados que tem um índice de facilidade de manutenção abaixo 65.  
  
 O **filtro** caixa suspensa contém os nomes das colunas de resultados. Quando um filtro é definido, ele é adicionado à parte inferior da lista junto com um recuo. A lista pode conter os dez últimos filtros que foram definidos.  
  
#### <a name="to-filter-the-code-metrics-results"></a>Para filtrar os resultados de métricas de código  
  
1.  Dos **filtro** , selecione o nome da coluna.  
  
2.  Na **Min**, digite o valor mínimo a ser exibido.  
  
3.  Na **máx**, digite o valor máximo a ser exibido.  
  
4.  Clique o **Aplicar filtro** botão.  
  
5.  Para ver os detalhes do resultado, expanda a árvore de hierarquia.  
  
##  <a name="BKMK_AddingRemovingandRearrangingDataColumns"></a> Adicionando, removendo e reorganizando as colunas de dados  
 Você pode adicionar ou remover de colunas de resultados de **resultados de métricas de código** janela. Além disso, você pode reorganizar as colunas de resultados para que eles apareçam na ordem em que você deseja.  
  
#### <a name="to-remove-a-column"></a>Para remover uma coluna  
  
1.  Clique o **Adicionar/remover colunas** botão.  
  
     \- ou -  
  
     Qualquer título de coluna com o botão direito e, em seguida, clique em **Adicionar/remover colunas**.  
  
2.  No **Adicionar/remover colunas** caixa de diálogo, desmarque a caixa de seleção para a coluna que você deseja remover e, em seguida, clique em **Okey**.  
  
#### <a name="to-add-a-previously-removed-column"></a>Para adicionar uma coluna removida anteriormente  
  
1.  Clique o **Adicionar/remover colunas** botão.  
  
     \- ou -  
  
     Qualquer título de coluna com o botão direito e, em seguida, clique em **Adicionar/remover colunas**.  
  
2.  No **Adicionar/remover colunas** diálogo caixa, marque a caixa de seleção para a coluna que você deseja adicionar e, em seguida, clique em **Okey**.  
  
#### <a name="to-rearrange-columns"></a>Para reorganizar colunas  
  
1.  Clique o **Adicionar/remover colunas** botão.  
  
     \- ou -  
  
     Qualquer título de coluna com o botão direito e, em seguida, clique em **Adicionar/remover colunas**.  
  
2.  No **Adicionar/remover colunas** caixa de diálogo, selecione a coluna que você deseja mover e, em seguida, clique na seta para cima ou seta para baixo.  
  
3.  Quando a coluna é posicionada onde desejar, clique em **Okey**.  
  
##  <a name="BKMK_Copying_Data_to_the_Clipboard_or_Excel"></a> Copiando dados para a área de transferência ou o Excel  
 Você pode selecionar e copiar uma linha de dados de métricas de código selecionada para a área de transferência como uma cadeia de caracteres de texto que contém uma linha para o nome e valor de cada coluna de dados. Você também pode clicar **Abrir lista no Microsoft Excel** para exportar todos os resultados de métricas de código para uma planilha do Excel  
  
##  <a name="BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results"></a> Criando um Item de trabalho com base nos resultados de métricas de código  
 Você pode criar uma [!INCLUDE[esprfound](../includes/esprfound-md.md)] item de trabalho que se baseia no resulta nos **resultados de métricas de código** janela. Quando o item de trabalho é criado, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] entra automaticamente em um título a **Title** dados de métricas de campo e o código sob o **histórico** guia.  
  
 Para obter mais informações sobre como criar itens de trabalho, consulte [criar um item de trabalho &#91;redirecionado&#93;](http://msdn.microsoft.com/en-us/24b2e064-16ac-4bf0-8de4-98a1f48b8c4b).  
  
#### <a name="to-create-a-work-item-based-on-a-result"></a>Para criar um item de trabalho com base em um resultado  
  
1.  Clique com botão direito o resultado.  
  
2.  Aponte para **Criar Item de trabalho**e, em seguida, clique no tipo de item de trabalho que você deseja criar (**Bug**, **tarefa**e assim por diante).  
  
3.  Conclua o formulário de item de trabalho ao preencher todos os campos obrigatórios.  
  
4.  Sobre o **arquivo** menu, clique em **Salvar tudo** para salvar o item de trabalho.  
  
#### <a name="to-create-a-bug-based-on-a-result"></a>Para criar um bug com base em um resultado  
  
1.  Clique no resultado para selecioná-lo.  
  
2.  Clique o **Criar Item de trabalho** botão.  
  
3.  Conclua o formulário de item de trabalho ao preencher todos os campos obrigatórios.  
  
4.  Sobre o **arquivo** menu, clique em **Salvar tudo** para salvar o item de trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)   
 [Como gerar dados de métricas do código](../code-quality/how-to-generate-code-metrics-data.md)




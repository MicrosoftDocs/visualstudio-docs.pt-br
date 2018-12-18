---
title: 'Como: criar um conjunto de regras personalizado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- Development Edition, rule sets
ms.assetid: bcc42508-9592-4802-9f66-a50111641d73
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a5d8a5cb7e29cfd900ce81fa5f4b6253f0c49014
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812459"
---
# <a name="how-to-create-a-custom-rule-set"></a>Como criar um conjunto de regras personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)], [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)], e [!INCLUDE[vsPro](../includes/vspro-md.md)], você pode criar e modificar um personalizado *conjunto de regras* para atender às necessidades específicas do projeto associadas com a análise de código. Para criar uma regra personalizada definida, você abrir um ou mais padrão regra define no editor de conjunto de regras. Em seguida, você pode adicionar ou remover regras específicas, e você pode alterar a ação que ocorre quando a análise de código determina que uma regra foi violada.  
  
 Para criar uma nova regra personalizada definida, você pode salvá-lo usando um novo nome de arquivo. O conjunto de regras personalizado é atribuído automaticamente ao projeto.  
  
## <a name="opening-the-rule-set-editor"></a>Abrindo a regra de editor de conjunto  
  
#### <a name="to-open-an-empty-rule-set-file-in-the-rule-set-editor"></a>Para abrir um vazio regra definir o arquivo no editor de conjunto de regras  
  
1.  Sobre o **arquivo** menu de [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], aponte para **New** e, em seguida, clique em **arquivo**.  
  
2.  No **novo arquivo** caixa de diálogo, clique em **gerais** no **modelos instalados** lista e, em seguida, selecione **conjunto de regras de análise de código**.  
  
3.  O editor de conjunto de regras é exibida. Nenhuma regra for selecionada na lista de editor.  
  
#### <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>Para criar uma regra personalizada de um único conjunto de regras existente  
  
1. No Gerenciador de soluções, clique com botão direito no projeto e, em seguida, selecione **propriedades**.  
  
2. Sobre o **propriedades** , clique em **análise de código**.  
  
3. No **do conjunto de regras** lista suspensa, siga um destes procedimentos:  
  
   - Selecione o conjunto de regras que você deseja personalizar.  
  
     \- ou -  
  
   - Selecione  **\<procurar... >** especificar uma regra existente definida que não está na lista.  
  
4. Clique em **abrir** para exibir as regras no editor de conjunto de regras.  
  
#### <a name="to-create-a-custom-rule-set-from-multiple-existing-rule-sets"></a>Para criar uma regra personalizada definida de vários conjuntos de regra existente  
  
1.  No Gerenciador de soluções, clique com botão direito no projeto e, em seguida, selecione **propriedades**.  
  
2.  Sobre o **propriedades** , clique em **análise de código**.  
  
3.  Selecione  **\<escolher vários regra define... >** partir **executar este conjunto de regras**.  
  
4.  No **adicionar ou remover conjuntos de regras** caixa de diálogo, selecione os conjuntos de regras em que você deseja basear o novo conjunto de regra e, em seguida, clique em **Okey**.  
  
5.  Salve o novo conjunto de regras.  
  
     O nome do novo conjunto de regras é selecionado na **executar este conjunto de regras** lista. Você pode alterar o nome de exibição da regra definida na próxima etapa.  
  
6.  (Opcional) Para alterar o nome de exibição do conjunto de regras na **modo de exibição** menu, clique em **janela propriedades**. Digite o nome de exibição na **nome** caixa.  
  
7.  Para adicionar, remover, ou modificar as regras de análise de código específicos no novo conjunto de regras, clique em **aberto**.  
  
## <a name="modifying-a-rule-set"></a>Modificando um conjunto de regras  
  
#### <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>Para modificar uma regra definida no editor de conjunto de regras  
  
-   Para alterar o nome de exibição do conjunto de regras na **modo de exibição** menu, clique em **janela propriedades**. Insira o nome de exibição na **nome** caixa. Observe que o nome de exibição pode ser diferente do nome do arquivo.  
  
-   Para adicionar todas as regras do grupo a um conjunto de regras personalizadas, marque a caixa de seleção do grupo. Para remover todas as regras do grupo, desmarque a caixa de seleção.  
  
-   Para adicionar uma regra específica para o conjunto de regras personalizadas, marque a caixa de seleção da regra. Para remover a regra do conjunto de regras, desmarque a caixa de seleção.  
  
-   Para alterar a ação executada quando uma regra é violada em uma análise de código, clique no **ação** do campo para a regra e, em seguida, selecione um dos seguintes valores:  
  
     **Avisar** -gera um aviso.  
  
     **Erro** -gera um erro.  
  
     **Nenhum** -desabilita a regra. Essa ação é o mesmo que remover a regra do conjunto de regras.  
  
## <a name="changing-the-rule-set-editor-display"></a>Alterando a regra do conjunto de exibição do editor  
  
#### <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>Para agrupar, filtrar ou alterar os campos no editor de conjunto de regras usando a barra de ferramentas do editor de conjunto de regra  
  
-   Para expandir as regras em todos os grupos, clique em **Expandir tudo**.  
  
-   Para recolher as regras em todos os grupos, clique em **Recolher tudo**.  
  
-   Para alterar o campo que as regras são agrupadas por, selecione o campo do **Group By** lista. Para exibir as regras não agrupadas, selecione  **\<None >**.  
  
-   Para adicionar ou remover campos nas colunas de regra, clique em **opções de coluna**.  
  
-   Para ocultar as regras que não se aplicam à solução atual, **ocultar as regras que não se aplicam à solução atual**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a ação de erro, clique em **Mostrar regras que podem gerar erros de análise de código**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a ação de aviso, clique em **Mostrar regras que podem gerar avisos de análise de código**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a **None** ação, clique em **Mostrar regras que não estão habilitadas**.  
  
-   Para adicionar ou remover Microsoft conjuntos de regras do padrão para o conjunto de regras atual, clique em **adicionar ou remover conjuntos de regras filho**.  
  
## <a name="see-also"></a>Consulte também  
 [Como: configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)   
 [Referência do conjunto de regras de análise de código](../code-quality/code-analysis-rule-set-reference.md)




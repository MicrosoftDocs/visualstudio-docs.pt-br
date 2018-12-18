---
title: Usando conjuntos de regras para especificar as regras do C++ para execução | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ac3877e6-5349-4c03-9541-3d5be259f1e8
caps.latest.revision: 7
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 42c8926403825032f295c31e2ce113bef4ff1bbd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810255"
---
# <a name="using-rule-sets-to-specify-the-c-rules-to-run"></a>Usando conjuntos de regras para especificar as regras do C++ para execução
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] e [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)], você pode criar e modificar um personalizado *conjunto de regras* para atender às necessidades específicas do projeto associadas com a análise de código. Para criar uma regra de C++ personalizada definido, um projeto C/C++ deve ser aberto no IDE do Visual Studio. Você, em seguida, abra um conjunto de regras padrão no editor de conjunto de regras e, em seguida, adicionar ou remove regras específicas e, opcionalmente, altere a ação que ocorre quando a análise de código determina que uma regra foi violada.  
  
 Para criar uma nova regra personalizada definida, você pode salvá-lo usando um novo nome de arquivo. O conjunto de regras personalizado é atribuído automaticamente ao projeto.  
  
## <a name="opening-the-rule-set-editor"></a>Abrindo a regra de editor de conjunto  
  
#### <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>Para criar uma regra personalizada de um único conjunto de regras existente  
  
1. No Gerenciador de soluções, abra o menu de atalho para o projeto e, em seguida, escolha **propriedades**.  
  
2. Sobre o **propriedades** guia, escolha **análise de código**.  
  
3. No **do conjunto de regras** lista suspensa, siga um destes procedimentos:  
  
   - Escolha o conjunto de regras que você deseja personalizar.  
  
     \- ou -  
  
   - Escolher  **\<procurar... >** especificar uma regra existente definida que não está na lista.  
  
4. Escolher **abrir** para exibir as regras no editor de conjunto de regras.  
  
#### <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>Para modificar uma regra definida no editor de conjunto de regras  
  
-   Para alterar o nome de exibição do conjunto de regras na **modo de exibição** menu, escolha **janela propriedades**. Insira o nome de exibição na **nome** caixa. Observe que o nome de exibição pode ser diferente do nome do arquivo.  
  
-   Para adicionar todas as regras do grupo a um conjunto de regras personalizadas, marque a caixa de seleção do grupo. Para remover todas as regras do grupo, desmarque a caixa de seleção.  
  
-   Para adicionar uma regra específica para o conjunto de regras personalizadas, marque a caixa de seleção da regra. Para remover a regra do conjunto de regras, desmarque a caixa de seleção.  
  
-   Para alterar a ação executada quando uma regra é violada em uma análise de código, escolha o **ação** do campo para a regra e, em seguida, escolha um dos seguintes valores:  
  
     **Avisar** -gera um aviso.  
  
     **Erro** -gera um erro.  
  
     **Nenhum** -desabilita a regra. Essa ação é o mesmo que remover a regra do conjunto de regras.  
  
#### <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>Para agrupar, filtrar ou alterar os campos no editor de conjunto de regras usando a barra de ferramentas do editor de conjunto de regra  
  
-   Para expandir as regras em todos os grupos, escolha **Expandir tudo**.  
  
-   Para recolher as regras em todos os grupos, escolha **Recolher tudo**.  
  
-   Para alterar o campo que as regras são agrupadas por, escolha o campo do **Group By** lista. Para exibir as regras não agrupadas, escolha  **\<None >**.  
  
-   Para adicionar ou remover campos nas colunas de regra, escolha **opções de coluna**.  
  
-   Para ocultar as regras que não se aplicam à solução atual, escolha **ocultar as regras que não se aplicam à solução atual**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a ação de erro, escolha **Mostrar regras que podem gerar erros de análise de código**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a ação de aviso, escolha **Mostrar regras que podem gerar avisos de análise de código**.  
  
-   Para alternar entre mostrar e ocultar as regras que são atribuídas a **None** ação, escolha **Mostrar regras que não estão habilitadas**.  
  
-   Para adicionar ou remover Microsoft conjuntos de regras do padrão para o conjunto de regras atual, escolha **adicionar ou remover conjuntos de regras filho**.




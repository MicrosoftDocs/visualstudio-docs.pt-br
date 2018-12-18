---
title: Personalizando o Gerenciador de modelos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.explorerbehavior
helpviewer_keywords:
- Domain-Specific Language Tools, Domain-Specific Language Explorer
ms.assetid: d2926444-9408-41d8-a27e-3fd0c416f9ac
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 77999eea0a76088368ff5e7ee66f9088dc45efa5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49175936"
---
# <a name="customizing-the-model-explorer"></a>Personalizando o Gerenciador de Modelos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar a aparência e comportamento do explorer para o seu designer de linguagem específica do domínio da seguinte maneira:  
  
-   Altere o título da janela.  
  
-   Altere o ícone de guia.  
  
-   Altere os ícones para nós.  
  
-   Oculte nós.  
  
## <a name="changing-the-window-title"></a>Alterar o título da janela  
 Para alterar o título da janela do explorer gerado, selecione **comportamento do Gerenciador** na **Gerenciador de DSL**e, em seguida, no **propriedades** janela, defina o  **Título** propriedade para o título que você deseja.  
  
## <a name="changing-the-tab-icon"></a>Alterar o ícone de guia  
 Para alterar o ícone de guia do explorer, use um ícone de 16 x 16 pixels em um arquivo. bmp. Coloque o arquivo de ícone na pasta \DslPackage\Resources\ e, em seguida, altere o nome de arquivo para **ModelExplorerToolWindowBitmaps.bmp**. Por exemplo, você pode alterar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] setup.ico ícone de arquivo no formato. bmp e renomeie-o para **DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp**. O designer gerado exibirem este ícone na guia do seu Gerenciador de quando ela estiver encaixada junto com **Gerenciador de soluções**.  
  
## <a name="setting-custom-icons-on-explorer-nodes"></a>Definindo ícones personalizados em nós do Gerenciador  
 Você pode personalizar nós no Gerenciador de usando as configurações de nó do Gerenciador. O procedimento a seguir mostra como adicionar um ícone para um nó.  
  
#### <a name="to-add-an-icon-to-an-explorer-node"></a>Para adicionar um ícone para um nó no explorer  
  
1.  Criar um [!INCLUDE[dsl](../includes/dsl-md.md)] solução usando o modelo de solução de fluxo de tarefa.  
  
2.  Colocar um arquivo. bmp que contém um ícone de 16 x 16 pixels na **Dsl\Resources** pasta na solução.  
  
3.  No **Gerenciador de DSL**, clique com botão direito **comportamento do Gerenciador** e, em seguida, clique em **adicionar novas configurações do Gerenciador de nó**.  
  
     Uma **ExplorerNodeSettings** nó aparece sob o **configurações personalizadas de nó** nó.  
  
4.  Selecione **ExplorerNodeSettings**e, em seguida, o **propriedades** janela, defina **classe** para **ator**.  
  
5.  Definir **ícone para exibição** ao caminho do arquivo de ícone.  
  
6.  Transformar todos os modelos e, em seguida, compilar e executar a solução.  
  
7.  No designer gerado, abra o diagrama de exemplo.  
  
     O Explorer deve mostrar três **ator** nós que têm seu ícone.  
  
> [!NOTE]
>  Se você tiver definido um ícone de nó para qualquer elemento que é exibido no Gerenciador de gerado, todos os nós de explorer exibirá o ícone. Se nenhum ícone tiver sido definido, os nós exibirá o ícone padrão.  
  
## <a name="changing-the-name-displayed-on-an-explorer-node"></a>Alterando o nome exibido em um nó no Explorer  
 Você pode alterar como os nomes de elementos de modelo são exibidos no seu Explorador. O procedimento a seguir mostra como exibir o nome da **tarefa** que é referenciado por uma **comentário** no nó de comentário.  
  
#### <a name="to-display-a-property"></a>Para exibir uma propriedade  
  
1.  Abra a solução que você criou no procedimento anterior.  
  
2.  Certifique-se de que o **comentário** faz referência a apenas uma classe de domínio único, definindo a multiplicidade da função com o nome da propriedade **assuntos** para entre 0 e 1. O nome da propriedade deve se tornar **assunto**, e o nome da relação deve se tornar **CommentReferencesSubject**.  
  
3.  No **Gerenciador de DSL**, clique com botão direito **comportamento do Gerenciador** e, em seguida, clique em **adicionar novas configurações do Gerenciador de nó**.  
  
     Uma **ExplorerNodeSettings** nó aparece sob o **configurações personalizadas de nó** nó.  
  
4.  Selecione **ExplorerNodeSettings**e, em seguida, o **propriedades** janela, defina **classe** para **comentário**.  
  
5.  Clique com botão direito do **comentário** nó e clique **adicionar novo caminho de propriedade**.  
  
     Um novo nó aparece chamado **propriedade exibida**.  
  
6.  Selecione **propriedade exibida**e, em seguida, no **propriedades** janela, clique no campo de valor de **caminho para propriedade**. Selecione **comentário**, em seguida, **CommentReferencesSubject**, em seguida, **FlowElement**. O caminho resultante deve se parecer com **CommentReferencesSubject.Subject/! Assunto**.  
  
7.  No campo de valor de **propriedade**, selecione **nome**.  
  
8.  Transformar todos os modelos e, em seguida, compilar e executar sua solução.  
  
9. No designer gerado, abra o diagrama de exemplo.  
  
10. Desenhar um **conector de comentário** entre o elemento de comentário e o **Task1** elemento no diagrama.  
  
     O nó do Gerenciador deve exibir o comentário como **Task1**.  
  
## <a name="hiding-nodes"></a>Ocultar nós  
 Você pode ocultar um nó no Gerenciador de adicionando seu caminho para o **de nós ocultos** nó do **Gerenciador de DSL**. O procedimento a seguir mostra como ocultar **comentário** nós.  
  
#### <a name="to-hide-an-explorer-node"></a>Para ocultar um nó no explorer  
  
1.  Abra a solução que você criou no procedimento anterior.  
  
2.  No **Gerenciador de DSL**, clique com botão direito **Explorer comportamento** e, em seguida, clique em **adicionar novo caminho de domínio**.  
  
     Um **caminho de domínio** nó aparece sob **de nós ocultos**.  
  
3.  Selecione **caminho de domínio**e, em seguida, no **propriedades** janela, clique no campo de valor de **definição de caminho**. Selecione **grafos**, em seguida, **FlowGraphHasComments**. O caminho resultante deve se parecer com **FlowGraphHasComments.Comments**  
  
4.  Transformar todos os modelos e, em seguida, compilar e executar sua solução.  
  
5.  No designer gerado, abra o diagrama de exemplo.  
  
     O explorer deverá mostrar somente um **atores** nó e não deve mostrar a **comentários** nó.  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)




---
title: Caixa de diálogo Lista de Tarefas, Ambiente, Opções | Microsoft Docs
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
- VS.ToolsOptionsPages.Environment.Task_List
- VS.ToolsOptionsPag.Environment.Task_List
- VS.ToolsOptionsPages.Environment.TaskList
- VS.Environment.Task List
helpviewer_keywords:
- Token List
- tokens
- icons, in Task List
- Task List, customizing environment
- Options dialog box, Task List environment
- exclamation points
- comments, comment tasks in Task List
- tokens, and the Task List
- Task List, comment tasks
ms.assetid: 88327e04-fa3e-48db-995b-ad89e0dc4ed2
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 17404838fc567d37f23c683f6b8f83b7529a3dc8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49252532"
---
# <a name="task-list-environment-options-dialog-box"></a>Caixa de diálogo Lista de Tarefas, Ambiente, Opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Esta página Opções permite a você adicionar, excluir e alterar os tokens de comentário que geram lembretes da **Lista de Tarefas**. Para exibir essas configurações, selecione **Opções** no menu **Ferramentas**, expanda a pasta **Ambiente** e escolha **Lista de Tarefas**.  
  
## <a name="task-list-options"></a>Opções da Lista de Tarefas  
 Confirmar exclusão de tarefas  
 Quando selecionada, uma caixa de mensagem é exibida sempre que uma Tarefa de Usuário é excluída da **Lista de Tarefas**, permitindo que você confirme a exclusão. Essa opção é habilitada por padrão.  
  
> [!NOTE]
>  Para excluir um Comentário de Tarefa, use o link para localizar o comentário e, em seguida, remova-o do seu código.  
  
 Mostrar apenas nomes de arquivo  
 Quando selecionada, a coluna **Arquivo** da **Lista de Tarefas** exibe somente os nomes dos arquivos a serem editados, não seus caminhos completos.  
  
## <a name="tokens"></a>Tokens  
 Quando você inserir um comentário em seu código cujo texto começa com um token na **Lista de Tokens**, a **Lista de Tarefas** exibirá seu comentário como nova entrada sempre que o arquivo for aberto para edição. É possível clicar nessa entrada **Lista de Tarefas** para ir diretamente para a linha de comentário no seu código. Para obter mais informações, consulte [Usando a Lista de Tarefas](../../ide/using-the-task-list.md).  
  
 Lista de Tokens  
 Exibe uma lista de tokens e permite que você adicione ou remova tokens personalizados. Tokens de comentário diferenciam maiúsculas de minúsculas no Visual C# e no Visual C++, mas não no Visual Basic.  
  
> [!NOTE]
>  Se você não digitar o token desejado exatamente como ele é exibido na **Lista de Tokens**, uma tarefa de comentário não será exibida na **Lista de Tarefas**.  
  
 Prioridade  
 Define a prioridade das tarefas que usam o token selecionado. Os comentários de tarefa que começam com esse token recebem automaticamente a prioridade designada na **Lista de Tarefas**.  
  
 Nome  
 Insira a cadeia de caracteres do token. Isso habilita o botão **Adicionar**. Em **Adicionar**, essa cadeia de caracteres é incluída na **Lista de Tokens**, e os comentários que começam com esse nome serão exibidos na **Lista de Tarefas**.  
  
 Adicionar  
 Habilitado quando você insere um novo **Nome**. Clique para adicionar uma nova cadeia de caracteres do token usando os valores inseridos nos campos **Nome** e **Prioridade**.  
  
 Excluir  
 Clique para excluir o token selecionado na **Lista de Tokens**. Não é possível excluir o token de comentário padrão.  
  
 Alteração  
 Clique para fazer alterações em um token existente usando os valores inseridos nos campos **Nome** e **Prioridade**.  
  
> [!NOTE]
>  Não é possível renomear nem excluir o token de comentário padrão, mas é possível alterar seu nível de prioridade.  
  
## <a name="see-also"></a>Consulte também  
 [Usando a Lista de Tarefas](../../ide/using-the-task-list.md)   
 [Definindo indicadores no código](../../ide/setting-bookmarks-in-code.md)   
 [Caixa de diálogo Opções do Ambiente](../../ide/reference/environment-options-dialog-box.md)




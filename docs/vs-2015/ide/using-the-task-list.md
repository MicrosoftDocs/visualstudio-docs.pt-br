---
title: Usando a lista de tarefas | Microsoft Docs
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
- TaskListWindow
- VS.TaskList
- tasklist
helpviewer_keywords:
- task list
- Visual Studio, task list
ms.assetid: f46a75a8-47b3-4cb6-bb59-b72e3356a664
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d5662aebeb0e7b8da36c52c0c9fd727c860a4221
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49172023"
---
# <a name="using-the-task-list"></a>Usando a lista de tarefas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use a **Lista de Tarefas** para rastrear comentários de código que usam tokens, como `TODO` e `HACK`, ou tokens personalizados, e para gerenciar atalhos que levarão você diretamente a um local predefinido no código. Clique no item na lista para ir até seu local no código-fonte.  
  
 Neste tópico:  
  
-   [A janela Lista de Tarefas](../ide/using-the-task-list.md#taskListWindow)  
  
-   [Tarefas do usuário](../ide/using-the-task-list.md#userTasks)  
  
-   [Tokens e comentários](../ide/using-the-task-list.md#tokensComments)  
  
-   [Tokens personalizados](../ide/using-the-task-list.md#customTokens)  
  
-   [Comentários TODO em C++](../ide/using-the-task-list.md#cppComments)  
  
-   [Atalhos](../ide/using-the-task-list.md#shortcuts)  
  
##  <a name="taskListWindow"></a> A janela Lista de Tarefas  
 Quando a **Lista de Tarefas** é aberta, ela aparece na parte inferior da janela do aplicativo.  
  
#### <a name="to-open-the-task-list"></a>Para abrir a Lista de Tarefas  
  
-   No menu **Exibir**, escolha **Lista de Tarefas** (Teclado: Ctrl+\\,T).  
  
     ![Janela Lista de Tarefas](../ide/media/vs2015-task-list.png "vs2015_task_list")  
  
#### <a name="to-change-the-sort-order-of-the-list"></a>Para alterar a ordem de classificação da lista  
  
-   Clique no cabeçalho de qualquer coluna. Para refinar ainda mais os resultados da pesquisa, pressione Shift e clique em um segundo cabeçalho de coluna.  
  
     Se preferir, no menu de atalho, escolha **Classificar por** e escolha um cabeçalho. Para refinar ainda mais os resultados da pesquisa, pressione Shift e escolha um segundo cabeçalho.  
  
#### <a name="to-show-or-hide-columns"></a>Para mostrar ou ocultar colunas  
  
-   No menu de atalho, escolha **Mostrar Colunas**. Escolha as colunas que você deseja mostrar ou ocultar.  
  
#### <a name="to-change-the-order-of-the-columns"></a>Para alterar a ordem das colunas  
  
-   Arraste o cabeçalho de qualquer coluna para o local desejado.  
  
##  <a name="userTasks"></a> Tarefas do usuário  
 O recurso de tarefa de usuário foi removido no Visual Studio 2015. Quando você abre uma solução que tem dados de tarefa de usuário do Visual Studio 2013 e anteriores no Visual Studio 2015, os dados de tarefa do usuário em seu arquivo .suo não serão afetados, mas as tarefas do usuário não serão exibidas na lista de tarefas.  
  
 Se você quiser continuar a acessar e atualizar os dados de tarefa do usuário, abra o projeto no Visual Studio 2013 e copie o conteúdo de quaisquer tarefas do usuário para sua ferramenta de gerenciamento de projeto preferida (como o Team Foundation Server).  
  
##  <a name="tokensComments"></a> Tokens e comentários  
 Um comentário no código precedido por um marcador de comentário e um token predefinido também será exibido na janela **Lista de Tarefas**. Por exemplo, o seguinte comentário do C# tem três partes distintas:  
  
-   O marcador de comentário (`//`)  
  
-   O token, por exemplo (`TODO`)  
  
-   O comentário (o restante do texto)  
  
```  
// TODO: Load state from previously suspended application  
```  
  
 Uma vez que `TODO` é um token, esse comentário aparece como uma tarefa `TODO` na lista.  
  
###  <a name="customTokens"></a> Tokens personalizados  
 Por padrão, o Visual Studio inclui os seguintes tokens: HACK, TODO, UNDONE, NOTE. Eles não diferenciam maiúsculas de minúsculas.  
  
 Também é possível criar seus próprios tokens personalizados.  
  
##### <a name="to-create-a-custom-token"></a>Para criar um token personalizado  
  
1.  No menu **Ferramentas**, escolha **Opções**.  
  
2.  Abra a pasta **Ambiente** e escolha **Lista de Tarefas**.  
  
     A [Caixa de diálogo Lista de Tarefas, Ambiente, Opções](../ide/reference/task-list-environment-options-dialog-box.md) é exibida.  
  
     ![Lista de tarefas do Visual Studio](../ide/media/vs2015-task-list-options.png "vs2015_task_list_options")  
  
3.  Na categoria **Tokens**, na caixa de texto **Nome**, insira o nome do seu token, por exemplo, “BUG”.  
  
4.  Na lista suspensa **Prioridade**, escolha uma prioridade padrão para o novo token. Escolha o botão **Adicionar**.  
  
###  <a name="cppComments"></a> Comentários TODO em C++  
 Por padrão, os comentários TODO em C++ são exibidos na janela **Lista de Tarefas**. Você pode alterar esse comportamento.  
  
##### <a name="to-turn-off-c-todo-comments"></a>Para desligar os comentários TODO em C++  
  
1.  No menu **Ferramentas**, vá para **Opções &#124; Editor de Texto &#124; C/C++ &#124; Exibir &#124; Enumerar Tarefas de Comentário** e defina o valor como false.  
  
2.  Na caixa de diálogo **Opções**, abra **Editor de Texto**.  
  
3.  Em **C/C++**, escolha **Exibir** e defina **Enumerar Tarefas em Comentários** como **False**.  
  
##  <a name="shortcuts"></a> Atalhos  
 Um *atalho* é um indicador no código que é controlado na **Lista de Tarefas**; ele tem um ícone diferente de um indicador normal. Clique duas vezes no atalho na **Lista de Tarefas** para ir até o local correspondente no código.  
  
 ![Ícone de atalho de lista de tarefas do Visual Studio](../ide/media/vs2015-task-list-bookmark.png "vs2015_task_list_bookmark")  
  
#### <a name="to-create-a-shortcut"></a>Para criar um atalho  
  
-   Insira o ponteiro no código onde deseja colocar um atalho. Escolha **Editar &#124; Indicadores &#124; Adicionar Atalho da Lista de Tarefas** ou pressione (Teclado: Ctrl+K, Ctrl+H).  
  
     Para navegar pelos atalhos no código, escolha um atalho na lista e escolha **Próxima Tarefa** ou **Tarefa Anterior** no menu de atalho.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Lista de Tarefas, Ambiente, Opções](../ide/reference/task-list-environment-options-dialog-box.md)




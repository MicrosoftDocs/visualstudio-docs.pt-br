---
title: Usar a Lista de Tarefas
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- TaskListWindow
- VS.TaskList
- tasklist
helpviewer_keywords:
- task list
- Visual Studio, task list
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7766a7fd935cc1e1131c4780a5a88ef6fa54e838
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349382"
---
# <a name="use-the-task-list"></a>Usar a Lista de Tarefas

Use a **Lista de Tarefas** para rastrear comentários de código que usam tokens, como `TODO` e `HACK`, ou tokens personalizados, e para gerenciar atalhos que levarão você diretamente a um local predefinido no código. Clique no item na lista para ir até seu local no código-fonte.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Comentários da tarefa (Visual Studio para Mac)](/visualstudio/mac/task-comments).

## <a name="the-task-list-window"></a>A janela Lista de Tarefas

Quando a **Lista de Tarefas** é aberta, ela aparece na parte inferior da janela do aplicativo.

Para abrir a **Lista de Tarefas**, selecione **Exibir** > **Lista de Tarefas**, ou pressione no teclado **Ctrl**+**\\**,**T**.

![Janela Lista de Tarefas](../ide/media/vs2015_task_list.png)

Para alterar a ordem de classificação da lista, selecione o cabeçalho de qualquer coluna. Para refinar ainda mais os resultados da pesquisa, pressione **Shift** e clique em um segundo cabeçalho de coluna. Como alternativa, no menu de atalho, escolha **Classificar por** e escolha um cabeçalho. Para refinar ainda mais os resultados da pesquisa, pressione **Shift** e escolha um segundo cabeçalho.

Para mostrar ou ocultar colunas, no menu de atalho, escolha **Mostrar Colunas**. Selecione as colunas que você deseja mostrar ou ocultar.

Para alterar a ordem das colunas, arraste qualquer cabeçalho de coluna para o local desejado.

## <a name="user-tasks"></a>Tarefas do usuário

O recurso de tarefa do usuário foi removido no Visual Studio 2015. Quando você abrir uma solução que tem os dados de tarefa do usuário do Visual Studio 2013 e anterior, os dados de tarefa do usuário no arquivo *.suo* não serão afetados, mas as tarefas do usuário não serão exibidas na lista de tarefas.

Se você quiser continuar a acessar e atualizar os dados de tarefa do usuário, abra o projeto no Visual Studio 2013 e copie o conteúdo de quaisquer tarefas do usuário para sua ferramenta de gerenciamento de projeto preferida (como o Team Foundation Server).

## <a name="tokens-and-comments"></a>Tokens e comentários

Um comentário no código precedido por um marcador de comentário e um token predefinido também será exibido na janela **Lista de Tarefas**. Por exemplo, o seguinte comentário do C# tem três partes distintas:

- O marcador de comentário (`//`)

- O token, por exemplo (`TODO`)

- O comentário (o restante do texto)

```csharp
// TODO: Load state from previously suspended application
```

Uma vez que `TODO` é um token pré-definido, esse comentário aparece como uma tarefa `TODO` na lista.

### <a name="custom-tokens"></a>Tokens personalizados

Por padrão, o Visual Studio inclui os seguintes tokens: `HACK`, `TODO`, `UNDONE` e `UnresolvedMergeConflict`. Não diferenciam maiúsculas de minúsculas. Também é possível criar seus próprios tokens personalizados.

Para criar um token personalizado:

1. No menu **Ferramentas**, escolha **Opções**.

2. Abra a pasta **Ambiente** e escolha **Lista de Tarefas**.

   A [página de opções da lista de tarefas](../ide/reference/task-list-environment-options-dialog-box.md) é exibida.

   ![Lista de Tarefas do Visual Studio](../ide/media/vs2015_task_list_options.png)

3. Na caixa de texto **Nome**, insira o nome do seu token, por exemplo, **BUG**.

4. Na lista suspensa **Prioridade**, escolha uma prioridade padrão para o novo token.

5. Escolha **Adicionar**.

### <a name="c-todo-comments"></a>Comentários TODO do C++

Por padrão, os comentários TODO em C++ são exibidos na **Lista de Tarefas**.

Para desativar comentários TODO em C++ no menu **Ferramentas**, selecione **Opções** > **Editor de Texto** > **C/C++** > **Exibir** > **Enumerar Tarefas de Comentário** e defina o valor como **false**.

## <a name="shortcuts"></a>Atalhos

Um *atalho* é um indicador no código que é rastreado na **Lista de Tarefas**. Ele tem um ícone diferente de um indicador comum. Clique duas vezes no atalho na **Lista de Tarefas** para ir até o local correspondente no código.

![Ícone de atalho da Lista de Tarefas no Visual Studio](../ide/media/vs2015_task_list_bookmark.png)

### <a name="create-a-shortcut"></a>Criar um atalho

Para criar um atalho, insira o ponteiro no código no local em que deseja colocar um atalho. Escolha **Editar** > **Indicadores** > **Adicionar Atalho da Lista de Tarefas** ou pressione **Ctrl**+**K**, **Ctrl**+**H**.

Para navegar pelos atalhos no código, escolha um atalho na lista e escolha **Próxima Tarefa** ou **Tarefa Anterior** no menu de atalho.

## <a name="see-also"></a>Consulte também

- [Caixa de diálogo Lista de Tarefas, Ambiente, Opções](../ide/reference/task-list-environment-options-dialog-box.md)
- [Comentários da tarefa (Visual Studio para Mac)](/visualstudio/mac/task-comments)

---
title: Renomear um nome de arquivo para corresponder a um tipo no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8407e89d9e28c501358877df9c244175ca8155c8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942316"
---
# <a name="sync-a-type-to-a-filename-or-a-filename-to-a-type-refactoring"></a>Refatoração Sincronizar um tipo para um nome de arquivo ou um nome de arquivo para um tipo

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite que você renomeie um tipo para corresponder ao nome do arquivo, ou renomeie um nome de arquivo para corresponder ao tipo que ele contém.

**Quando:** você renomeou um arquivo ou tipo e ainda não atualizou o arquivo correspondente ou tipo a ser correspondido.

**Por quê:** se você colocar um tipo em um arquivo com um nome diferente, ou vice-versa, será difícil encontrar o que está procurando. Se você renomear o tipo ou nome de arquivo, o código se tornará mais legível e mais fácil de navegar.

## <a name="how-to"></a>Como fazer

1. realce ou coloque o cursor do texto dentro do nome do tipo para sincronizar:

   - C#:

       ![Código realçado – C#](media/synctype-highlight-cs.png)

   - Visual Basic:

       ![Código realçado – Visual Basic](media/synctype-highlight-vb.png)

2. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl**+**.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Renomear o arquivo para *TypeName*.cs** no pop-up da janela Visualização, onde *TypeName* é o nome do tipo selecionado.
      - Pressione **Ctrl**+**.** para disparar o menu **Ações Rápidas e Refatorações** e selecione **Renomear tipo para _Filename_** no pop-up da janela Visualização, onde *Filename* é o nome do arquivo atual.
   - **Mouse**
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Renomear o arquivo para *TypeName*.cs** no pop-up da janela Visualização, onde *TypeName* é o nome do tipo selecionado.
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Renomear o tipo para _Filename_** no pop-up da janela Visualização, onde *Filename* é o nome do arquivo atual.

   O tipo ou o arquivo foi renomeado.

   - C#: no exemplo abaixo, o arquivo **MyClass.cs** foi renomeado para **MyNewClass.cs** para corresponder ao nome do tipo.

       ![Resultado embutido em C#](media/synctype-result-cs.png)

   - Visual Basic: no exemplo abaixo, o arquivo **Employee.vb** foi renomeado para **Person.vb** para corresponder ao nome do tipo.

       ![Resultado embutido em Visual Basic](media/synctype-result-vb.png)

> ![NOTE] Esta refatoração ainda não está disponível para projetos .NET Core e .NET Standard.

## <a name="see-also"></a>Consulte também

- [Refatoração](../refactoring-in-visual-studio.md)

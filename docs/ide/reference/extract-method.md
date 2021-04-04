---
title: Extrair um método
description: Transforme um fragmento de código em seu próprio método selecionando o código e digitando Ctrl + R, Ctrl + M.
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 6ee11ec012ae0f104f5fefff7302d3982e43721a
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106083649"
---
# <a name="extract-a-method-refactoring"></a>Refatoração Extrair um método

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite transformar um fragmento de código em seu próprio método.

**Quando:** você tem um fragmento de código existente em algum método que precisa ser chamado desde outro método.

**Por quê:** você poderia copiar/colar esse código, mas que poderia levar à eliminação de duplicação. A melhor solução é refatorar esse fragmento em seu próprio método, o que pode ser chamado livremente por qualquer outro método.

## <a name="how-to"></a>Como fazer

1. realce o código a ser extraído:

   - C#:

       ![Captura de tela mostrando o código C# para a classe Program. Na função principal dessa classe, uma linha de código é realçada.](media/extractmethod-highlight-cs.png)

   - Visual Basic:

       ![Captura de tela mostrando o código Visual Basic para o principal sub. Nessa sub-rotina, uma linha de código é realçada.](media/extractmethod-highlight-vb.png)

2. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl+R**, em seguida, **Ctrl+M**. (Observe que o atalho de teclado pode ser diferente com base no perfil selecionado.)
      - Pressione **Ctrl** + **.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Extrair Método** no pop-up da janela Visualização.
   - **Mouse**
      - Selecione **Editar > Refatorar > Extrair Método**.
      - Clique com o botão direito do mouse no código e selecione **Refatorar > Extrair > Extrair Método**.
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Extrair Método** no pop-up da janela Visualização.

   O método será criado imediatamente. A partir daqui, agora você pode renomear o método digitando o novo nome.

   > [!TIP]
   > Também é possível atualizar os comentários e outras cadeias de caracteres para usar esse novo nome, bem como [visualizar as alterações](../../ide/preview-changes.md) antes de salvar usando as caixas de seleção na caixa **Renomear**, que aparece na parte superior direita do seu IDE.

   - C#:

      ![Captura de tela mostrando o código C# para a classe Program. Um nome de método é realçado e a janela pop-up de renomeação é aberta.](media/extractmethod-rename-cs.png)

   - Visual Basic:

      ![Captura de tela mostrando o código Visual Basic para o principal sub. Um nome de método é realçado e a janela pop-up de renomeação é aberta.](media/extractmethod-rename-vb.png)

3. Quando estiver satisfeito com a alteração, escolha **Aplicar** ou pressione **Enter** e as alterações serão confirmadas.

## <a name="see-also"></a>Confira também

- [Refatoração](../refactoring-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)

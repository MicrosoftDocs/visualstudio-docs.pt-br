---
title: Alterar assinatura do método
description: Adicione, remova ou altere a ordem dos parâmetros de um método. Clique com o botão direito do mouse no método, selecione Ações Rápidas e Refatorações e selecione Alterar Assinatura.
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.remove
- vs.csharp.refactoring.reorder
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 947f44700ef43815eb29bc3e90563afe1be68f2b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283860"
---
# <a name="change-a-method-signature-refactoring"></a>Refatoração Alterar uma assinatura de método

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite remover ou alterar a ordem dos parâmetros do método.

**Quando:** você deseja mover ou remover um parâmetro de método que está sendo usado em uma variedade de locais.

**Por quê:** você pode manualmente remover e reordenar os parâmetros e, em seguida, localizar todas as chamadas para esse método e alterá-las uma por uma, mas isso poderia levar a erros.  Essa ferramenta de refatoração executará a tarefa automaticamente.

## <a name="how-to"></a>Como fazer

1. realce ou coloque o cursor do texto dentro do nome do método para modificar, ou um de seus usos:

   - C#:

       ![Código em C# realçado](media/changesignature-highlight-cs.png)

   - VB:

       ![Código em Visual Basic realçado](media/changesignature-highlight-vb.png)

2. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl+R**, em seguida, **Ctrl+V**.  (Observe que o atalho de teclado pode ser diferente com base no perfil selecionado.)
      - Pressione **Ctrl** + **.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Alterar Assinatura** no pop-up da janela Visualização.
   - **Mouse**
      - Selecione **Editar > Refatorar > Remover Parâmetros**.
      - Selecione **Editar > Refatorar > Reordenar Parâmetros**.
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Alterar Assinatura** no pop-up da janela Visualização.

3. Na caixa de diálogo **Alterar Assinatura** que aparecer, você pode usar os botões à direita para alterar a assinatura do método:

   ![Caixa de diálogo Alterar Assinatura](media/change-signature.png)

   | Botão | Descrição
   | ------ | ---
   | **Para cima/baixo** | Mova o parâmetro selecionado para cima e para baixo na lista
   | **Adicionar** | Adicionar um novo parâmetro à lista
   | **Removerr** | Remova o parâmetro selecionado da lista
   | **Restaurar** | Restaurar o parâmetro selecionado e riscado na lista

   > [!TIP]
   > Use a caixa de seleção **Visualizar alterações de referência** para [ver qual será o resultado](../../ide/preview-changes.md) antes de confirmá-lo.

4. Selecionar **Adicionar** na caixa de diálogo **alterar assinatura** abrirá a caixa de diálogo **Adicionar parâmetro** . A caixa de diálogo **Adicionar Parâmetro** permite que você adicione um nome de tipo e um nome de parâmetro. Você pode optar por tornar o parâmetro necessário ou opcional com um valor padrão. Em seguida, você pode adicionar um valor no site de chamada e escolher um argumento nomeado para esse valor ou pode introduzir uma variável TODO. A variável TODO coloca um TODO em seu código para que você possa acessar cada erro e percorrer cada site de chamada de maneira independente e decidir o que passar. Para parâmetros opcionais, você tem a opção de omitir o site de chamada completamente.

    ![Caixa de diálogo Adicionar parâmetro-C #](media/add-parameter-dialog.png)

5. Quando terminar de adicionar um parâmetro, pressione o botão **OK** para visualizar as alterações.

    ![Caixa de diálogo Alterar Assinatura](media/change-signature.png)

6. Pressione **OK** para exibir as alterações.
   - C#:

      ![Resultado da alteração de assinatura – C#](media/changesignature-result-cs.png)

   - Visual Basic:

      ![Resultado da alteração de assinatura – Visual Basic](media/changesignature-result-vb.png)

## <a name="see-also"></a>Veja também

- [Refatoração](../refactoring-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)
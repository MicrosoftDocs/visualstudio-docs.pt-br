---
title: Implementar uma interface no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 9abc1d5fde69127f796dcfcd4c7c09cf8743c915
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295417"
---
# <a name="implement-an-interface-in-visual-studio"></a>Implementar uma interface no Visual Studio

Esta geração de código aplica-se a:

- C#

- Visual Basic

**O quê:** permite gerar imediatamente o código necessário para implementar uma interface.

**Quando:** você deseja herdar de uma interface.

**Por quê:** você pode implementar manualmente todas as interfaces uma por uma; no entanto, esse recurso gerará automaticamente todas as assinaturas de método.

## <a name="how-to"></a>Como fazer

1. coloque o cursor na linha em que há um rabisco vermelho indicando que você referenciou uma interface, mas não implementou todos os membros necessários.

   - C#:

       ![Código em C# realçado](media/interface-highlight-cs.png)

   - Visual Basic:

       ![Código em VB realçado](media/interface-highlight-vb.png)

2. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl**+**.** para acionar o menu **Ações e Refatorações Rápidas**.
   - **Mouse**
      - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.
      - Passe o mouse sobre o rabisco vermelho e clique no ícone de ![Lâmpada](media/bulb-cs.png) ícone que aparece.
      - Clique no ícone de ![Lâmpada](media/bulb-cs.png) ícone que aparece na margem esquerda quando o cursor de texto já está na linha com o rabisco vermelho.

3. Selecione **Implementar interface** no menu suspenso.

   ![Visualização da implementação de interface](media/interface-preview-cs.png)

   > [!TIP]
   > - Use o link **Visualizar alterações** na parte inferior da janela de visualização [para ver todas as alterações](../../ide/preview-changes.md) que serão feitas antes de fazer sua seleção.
   > - Use os links **Documento**, **Projeto** e **Solução** na parte inferior da janela de visualização para criar as assinaturas de método corretas em várias classes que implementam a interface.

   As assinaturas de método da interface foram criadas e estão prontas para serem implementadas.

   - C#:

       ![Resultado da implementação da interface em C#](media/interface-result-cs.png)

   - Visual Basic:

       ![Resultado da implementação da interface em VB](media/interface-result-vb.png)

   > [!TIP]
   > (Somente C#) Use a opção **Implementar interface explicitamente** para prefixar cada método gerado com o nome da interface a fim de evitar colisões de nome.
   >
   > ![Implementar o resultado de interface explicitamente](media/interface-explicitresult-cs.png);

## <a name="see-also"></a>Consulte também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar alterações](../../ide/preview-changes.md)
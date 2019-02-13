---
title: Gerar a classe ou o tipo
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- vsl.GenerateFromUsage
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: a1258e0448fe7be9dd7fa0180f52604d877b051d
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55953159"
---
# <a name="generate-a-class-or-type-in-visual-studio"></a>Gerar uma classe ou um tipo no Visual Studio

Esta geração de código aplica-se a:

- C#

- Visual Basic

**O quê:** Permite gerar imediatamente o código para uma classe ou um tipo.

**Quando:** Você introduz uma nova classe ou um tipo e deseja declará-lo correta e automaticamente.

**Por que:** Você pode declarar a classe ou o tipo antes de usá-lo; no entanto, essa funcionalidade gerará a classe ou o tipo automaticamente.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor na linha em que há um rabisco vermelho. O rabisco vermelho indica uma classe que ainda não existe.

   - C#:

       ![Código em C# realçado](media/class-highlight-cs.png)

   - Visual Basic:

       ![Código em VB realçado](media/class-highlight-vb.png)

2. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl**+**.** para acionar o menu **Ações e Refatorações Rápidas**.
   - **Mouse**
      - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.
      - Passe o mouse sobre o rabisco vermelho e clique no ícone de ![lâmpada de erro](media/error-bulb.png) ícone que aparece.
      - Clique no ícone de ![lâmpada de erro](media/error-bulb.png) ícone que aparece na margem esquerda quando o cursor de texto já está na linha com o rabisco vermelho.

      ![Gerar visualização de classe](media/class-preview-cs.png)

3. Selecione uma das opções no menu suspenso:

   - Gerar a classe ‘*TypeName*' no novo arquivo &mdash;Cria uma classe chamada *TypeName* em um arquivo chamado *TypeName*.cs/.vb
   - Gerar a classe ‘*TypeName*'&mdash;Cria uma classe chamada *TypeName* no arquivo atual.
   - Gerar classes aninhadas ‘*TypeName*'&mdash;Cria uma classe chamada *TypeName* aninhada na classe atual.
   - Gerar novo tipo...&mdash;Cria uma nova classe ou um novo struct com todas as propriedades especificadas.

   > [!TIP]
   > Use o link **Visualizar alterações** na parte inferior da janela de visualização [para ver todas as alterações](../../ide/preview-changes.md) que serão feitas antes de fazer sua seleção.

4. Se você tiver selecionado o item **Gerar novo tipo**, a caixa de diálogo **Gerar Tipo** será aberta. Configure a acessibilidade, o tipo e o local do novo tipo.

   ![Gerar tipo](media/class-newtype-cs.png)

   Seleção | Descrição
   --- | ---
   Acesso | Defina o tipo para ter acesso *Padrão*, *Interno* ou *Público*.
   Tipo | Isso pode ser definido como *classe* ou *struct*.
   Nome | Isso não pode ser alterado e será o nome que você já digitou.
   Projeto | Se houver vários projetos em sua solução, você poderá escolher onde deseja que a classe/struct viva.
   Nome do Arquivo | Você pode criar um novo arquivo ou pode adicionar o tipo a um arquivo existente.

A classe ou o struct é criado. Para C#, um construtor também é criado.

- C#

   ![Resultados da geração de classe em C#](media/class-result-cs.png)

- Visual Basic

   ![Resultados da geração de classe em VB](media/class-result-vb.png)

## <a name="see-also"></a>Consulte também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar alterações](../../ide/preview-changes.md)
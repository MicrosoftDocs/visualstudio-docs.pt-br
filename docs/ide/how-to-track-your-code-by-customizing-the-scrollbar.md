---
title: Modo de mapa e modo de barra da barra de rolagem
ms.date: 03/20/2020
ms.topic: how-to
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5d1b659dabed2337013ffb84ff48277f0edacb09
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283977"
---
# <a name="how-to-customize-the-scroll-bar"></a>Como: personalizar a barra de rolagem

Quando se trabalha com longos arquivos de código, às vezes torna-se difícil manter o controle de onde está tudo no arquivo. É possível personalizar a barra de rolagem do editor de código para ter um panorama geral do que está acontecendo no código.

## <a name="annotations"></a>Anotações

Você pode selecionar se a barra de rolagem deve mostrar anotações, como alterações de código, pontos de interrupção, indicadores, erros e posição do cursor.

   1. Abra a página de opções **Barras de rolagem** escolhendo **Ferramentas** > **Opções** > **Editor de Texto** > **Todos os Idiomas** > **Barras de rolagem**.

   2. Selecione **Mostrar anotações sobre a barra de rolagem vertical** e selecione as anotações que deseja ver. As anotações disponíveis são:

      - alterações
      - marcas
      - erros
      - posição do cursor

      > [!TIP]
      > A opção **Exibir marcas** inclui pontos de interrupção e indicadores.

Experimente abrir um arquivo de código grande e substituir algumas partes do texto que ocorrem em vários locais no arquivo. A barra de rolagem mostra o efeito das substituições, de modo que você pode desfazer suas alterações se tiver substituído algo que não deveria.

Esta é a aparência da barra de rolagem após o usuário pesquisar por uma cadeia de caracteres. Observe que todas as instâncias da cadeia de caracteres são exibidas na barra de rolagem.

![A barra de rolagem do Visual Studio após a pesquisa de uma cadeia de caracteres](../ide/media/enhancedscrollbarsearch.png)

Esta é a barra de rolagem após a substituição de todas as instâncias da cadeia de caracteres. As marcas vermelhas na barra de rolagem mostram em que local a substituição de texto introduziu erros.

![A barra de rolagem do Visual Studio depois da substituição de uma cadeia de caracteres com erros](../ide/media/enhancedscrollbarreplace.png)

## <a name="display-modes"></a>Modos de exibição

A barra de rolagem tem dois modos: o modo de barra e o modo de mapa.

### <a name="bar-mode"></a>Modo de barra

O *modo de barra* exibe indicadores de anotação na barra de rolagem. Clicando na barra de rolagem é possível rolar a página para cima ou para baixo, mas não ir para aquele local no arquivo.

### <a name="map-mode"></a>Modo de mapa

O *modo de mapa* exibe linhas de código, em miniatura, na barra de rolagem. É possível escolher a largura da coluna do mapa selecionando um valor em **Visão geral do Código-fonte**. Para habilitar uma visualização maior do código quando você parar o ponteiro no mapa, selecione a opção **Mostrar Dica de Ferramenta de Visualização**. As regiões recolhidas ficam sombreadas de forma diferente e são expandidas quando você clica duas vezes nelas.

> [!TIP]
> Você pode desabilitar a exibição de código em miniatura no modo de mapa definindo a opção **Visão geral do código-fonte** como **Desabilitada**. Se a opção **Mostrar Dica de Ferramenta de Visualização** estiver selecionada, você ainda verá uma visualização do código nesse local ao passar o ponteiro do mouse sobre a barra de rolagem e, o cursor ainda o levará para esse local no arquivo quando você clicar.

A imagem a seguir mostra o exemplo de pesquisa quando o modo de mapa está ativado e a largura está definida como **Média**:

![Barra de rolagem do Visual Studio no modo de mapa](../ide/media/enhancedscrollbar.png)

A imagem a seguir mostra a opção **Mostrar dica de ferramenta de visualização**:

![Barra de rolagem do Visual Studio com uma dica de ferramenta](../ide/media/enhancedscrollbarsearchtooltip.png)

> [!TIP]
> Para alterar as cores que você vê no modo de mapa, escolha **ferramentas**  >  **Opções**  >  **Environment**  >  **fontes e cores**do ambiente. Em seguida, em **itens de exibição**, escolha qualquer um dos itens precedidos de "visão geral", faça as alterações de cor desejadas e escolha **OK**.

## <a name="see-also"></a>Veja também

- [Recursos do editor de código](../ide/writing-code-in-the-code-and-text-editor.md)

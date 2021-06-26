---
title: Janela caixa de ferramentas
description: Saiba mais sobre a janela Caixa de Ferramentas e como ela exibe controles que você pode adicionar Visual Studio projetos.
ms.custom: SEO-VS-2020
ms.date: 06/01/2020
ms.topic: reference
f1_keywords:
- vs.toolbox.general
helpviewer_keywords:
- Toolbox [Visual Studio]
- custom controls [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a4947562eb49501e60711111d8765716cbae5c6
ms.sourcegitcommit: d3658667e768d7516cbf4461ec47bf24c8fcb7e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112925209"
---
# <a name="toolbox"></a>Caixa de Ferramentas

A janela **Caixa de Ferramentas** exibe os controles que você pode adicionar a projetos do Visual Studio. Para abrir **a Caixa de Ferramentas,** escolha **Exibir**  >  **Caixa de** Ferramentas na barra de menus ou pressione **Ctrl** + **Alt** + **X.**

![Captura de tela da janela Caixa de Ferramentas mostrando as opções na seção Contêineres.](media/vs-2019/toolbox.png "Captura de tela da janela Caixa de Ferramentas")

Você pode arrastar e soltar diferentes controles na superfície do designer que você está usando, redimensionar e posicionar os controles.

A caixa de ferramentas é exibida em conjunto com exibições de designer, como a exibição de designer de um arquivo XAML ou um projeto Windows Forms Aplicativo. A **Caixa de Ferramentas** exibe apenas os controles que podem ser usados ​​no designer atual. Você pode pesquisar na **Caixa de ferramentas** para filtrar ainda mais os itens que aparecem.

> [!NOTE]
> Para alguns tipos de projeto, a **Caixa de Ferramentas** pode não mostrar nenhum item.

A versão do .NET direcionada pelo projeto também afeta o conjunto de controles visíveis na Caixa de ferramentas. Altere a versão da estrutura de destino nas páginas de propriedades do projeto, se necessário. Selecione o nó do projeto no **Gerenciador de Soluções** e, na barra de menus, escolha **Projeto** > **Propriedades do nomedoprojeto**. Na guia **Aplicativo**, use o menu suspenso **Estrutura de destino**.

::: moniker range=">=vs-2019"

![Captura de tela da caixa de diálogo Aplicativo mostrando as opções na lista de menus da estrutura de destino.](media/vs-2019/toolbox-change-dotnet-version.png "Captura de tela da caixa de diálogo em que você pode alterar a versão do .NET")

::: moniker-end

## <a name="manage-the-toolbox-window-and-its-controls"></a>Gerenciar a janela Caixa de Ferramentas e seus controles

Por padrão, **a Caixa de** Ferramentas é recolhido ao longo do lado esquerdo do Visual Studio IDE e aparece quando o cursor é movido sobre ele. É possível fixar a **Caixa de Ferramentas** (clicando no ícone **Fixar** da barra de ferramentas) para que ela permaneça aberta enquanto você move o cursor. Você também pode desencaixar a janela **Caixa de Ferramentas** e arrastá-la para qualquer lugar na tela. Você pode encaixar, desencaixar e ocultar a **Caixa de Ferramentas**, clicando com o botão direito do mouse na barra de ferramentas e selecionando uma das opções.

> [!TIP]
> Se a Caixa de Ferramentas não aparecer mais como recolhido no lado esquerdo do IDE Visual Studio, você poderá adicioná-lo novamente escolhendo Layout da Janela de Redefinição de Janela na barra   >   de menus.

Você pode reorganizar  os itens em uma guia Caixa de Ferramentas ou adicionar guias e itens personalizados usando os seguintes comandos no menu de contexto do clique com o botão direito do mouse:

- **Renomear Item** – renomeia o item selecionado.

- **Exibição de Lista** – mostra os controles em uma lista vertical. Se todas as opções estiverem desmarcadas, os controles aparecem na horizontal.

- **Mostrar Todos** – mostra todos os controles possíveis (e não apenas os que se aplicam ao designer atual).

- **Escolher Itens** – abre a caixa de diálogo **Escolher Itens da Caixa de Ferramentas** para que você possa especificar os itens que aparecem na **Caixa de Ferramentas**. Você pode mostrar ou ocultar um item, marcando ou desmarcando a caixa de seleção.

- **Classificar itens em ordem alfabética** – classifica os itens por nome.

- **Redefinir Barra de Ferramentas**: restaura as configurações e os itens padrão da **Caixa de Ferramentas**.

- **Adicionar Guia** – adiciona uma nova guia da **Caixa de Ferramentas**.

- **Mover para Cima** – move o item selecionado para cima.

- **Mover para Baixo** – move o item selecionado para baixo.

## <a name="create-and-distribute-custom-toolbox-controls"></a>Criar e distribuir controles personalizados da Caixa de Ferramentas

Você pode criar controles personalizados da **Caixa de Ferramentas**, começando com um modelo de projeto baseado no [Windows Presentation Foundation](../../extensibility/creating-a-wpf-toolbox-control.md) ou no [Windows Forms](../../extensibility/creating-a-windows-forms-toolbox-control.md). Depois, você pode distribuir o controle personalizado para seus colegas de equipe ou publicá-lo na Web usando o [Instalador de Controles da Caixa de Ferramentas](https://download.microsoft.com/download/8/3/6/836657BD-9CCB-4ED4-B9D2-FB769473B284/TCI_whitepaper.docx).

## <a name="next-steps"></a>Próximas etapas

Use os links a seguir para saber mais sobre algumas das **guias** disponíveis da Caixa de Ferramentas:

- [Caixa de Ferramentas, Guia Dados](../../ide/reference/toolbox-data-tab.md)
- [Caixa de Ferramentas, Guia Componentes](../../ide/reference/toolbox-components-tab.md)
- [Caixa de Ferramentas, Guia HTML](../../ide/reference/toolbox-html-tab.md)

## <a name="see-also"></a>Confira também

- [Escolher itens da Caixa de Ferramentas, Componentes do WPF](choose-toolbox-items-wpf-components.md)

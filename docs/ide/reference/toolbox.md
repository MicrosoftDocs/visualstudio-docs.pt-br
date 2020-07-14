---
title: Janela caixa de ferramentas
ms.date: 06/01/2020
ms.topic: reference
f1_keywords:
- vs.toolbox.general
- vs.toolbox
helpviewer_keywords:
- Toolbox [Visual Studio]
- custom controls [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9807762a4573cdbc68a4af26bf9d73b46827c7af
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285317"
---
# <a name="toolbox"></a>Caixa de Ferramentas

A janela **Caixa de Ferramentas** exibe os controles que você pode adicionar a projetos do Visual Studio. Para abrir a **caixa de ferramentas**, escolha **Exibir**  >  **caixa de ferramentas** na barra de menus ou pressione **Ctrl** + **ALT** + **X**.

![Janela caixa de ferramentas](media/vs-2019/toolbox.png "Captura de tela da janela caixa de ferramentas")

Você pode arrastar e soltar diferentes controles na superfície do designer que você está usando, redimensionar e posicionar os controles.

A caixa de ferramentas aparece em conjunto com exibições de designer, como o modo de exibição de designer de um arquivo XAML ou um projeto de aplicativo Windows Forms. A **Caixa de Ferramentas** exibe apenas os controles que podem ser usados ​​no designer atual. Você pode pesquisar na **Caixa de ferramentas** para filtrar ainda mais os itens que aparecem.

> [!NOTE]
> Para alguns tipos de projeto, a **Caixa de Ferramentas** pode não mostrar nenhum item.

A versão do .NET direcionada pelo projeto também afeta o conjunto de controles visíveis na Caixa de ferramentas. Altere a versão da estrutura de destino nas páginas de propriedades do projeto, se necessário. Selecione o nó do projeto no **Gerenciador de Soluções** e, na barra de menus, escolha **Projeto** > **Propriedades do nomedoprojeto**. Na guia **Aplicativo**, use o menu suspenso **Estrutura de destino**.

::: moniker range="vs-2019"

![Janela caixa de ferramentas](media/vs-2019/toolbox-change-dotnet-version.png "Captura de tela da caixa de diálogo onde você pode alterar a versão do .NET")

::: moniker-end

## <a name="manage-the-toolbox-window-and-its-controls"></a>Gerenciar a janela Caixa de Ferramentas e seus controles

Por padrão, a **caixa de ferramentas** é recolhida ao longo do lado esquerdo do IDE do Visual Studio e aparece quando o cursor é movido sobre ele. É possível fixar a **Caixa de Ferramentas** (clicando no ícone **Fixar** da barra de ferramentas) para que ela permaneça aberta enquanto você move o cursor. Você também pode desencaixar a janela **Caixa de Ferramentas** e arrastá-la para qualquer lugar na tela. Você pode encaixar, desencaixar e ocultar a **Caixa de Ferramentas**, clicando com o botão direito do mouse na barra de ferramentas e selecionando uma das opções.

> [!TIP]
> Se a caixa de ferramentas não aparecer mais como recolhida ao longo do lado esquerdo do IDE do Visual Studio, você poderá adicioná- **Window**la de volta escolhendo  >  **layout da janela de redefinição** de janela na barra de menus.

Você pode reorganizar os itens em uma guia da **caixa de ferramentas** ou adicionar guias e itens personalizados usando os seguintes comandos no menu de contexto do clique com o botão direito do mouse:

- **Renomear item** – renomeia o item selecionado.

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

Veja os links a seguir para saber mais sobre algumas das guias da **caixa de ferramentas** disponíveis:

- [Caixa de Ferramentas, Guia Dados](../../ide/reference/toolbox-data-tab.md)
- [Caixa de Ferramentas, Guia Componentes](../../ide/reference/toolbox-components-tab.md)
- [Caixa de Ferramentas, Guia HTML](../../ide/reference/toolbox-html-tab.md)

## <a name="see-also"></a>Veja também

- [Escolher itens da Caixa de Ferramentas, Componentes do WPF](choose-toolbox-items-wpf-components.md)

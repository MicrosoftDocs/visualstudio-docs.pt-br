---
title: Criar um novo projeto
description: Saiba como criar um novo projeto no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 12/23/2020
ms.topic: how-to
f1_keywords:
- vs.newproject
helpviewer_keywords:
- projects [Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05cfb7cf053a3275b49b76b46bec8054fb105078
ms.sourcegitcommit: 529e1716924c3e1ac8a750550b996ad3c79f353b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2021
ms.locfileid: "112066950"
---
# <a name="create-a-new-project-in-visual-studio"></a>Criar um novo projeto no Visual Studio

Neste artigo, mostraremos como criar rapidamente um novo projeto no Visual Studio de um modelo.

::: moniker range="vs-2017"

## <a name="open-the-new-project-dialog"></a>Abrir a caixa de diálogo Novo Projeto

Há várias maneiras de criar um projeto no Visual Studio 2017. Na página Iniciar, você pode digitar o nome  de um modelo de projeto na caixa Pesquisar modelos de projeto ou selecionar o **link** Criar novo projeto para abrir a caixa de diálogo **Novo** Projeto. Além da página Iniciar, você também pode selecionar Arquivo Novo Projeto na barra de menus ou clicar no botão Novo  >    >   Projeto na barra de ferramentas. 

![Captura de tela da barra de menus Visual Studio com as opções Arquivo > Novo > Projeto selecionadas.](./media/vside-newproject1.png)

## <a name="select-a-template-type"></a>Selecione um tipo de modelo

Na caixa de diálogo **Novo Projeto**, os modelos de projeto disponíveis aparecem em uma lista sob a categoria **Modelos**. Os modelos são organizados por linguagem de programação e tipo de projeto, como Visual C#, JavaScript e Azure Data Lake.

![Captura de tela da caixa de diálogo Novo Projeto que mostra uma lista de modelos instalados.](./media/vside-newproject-templates-list.png)

> [!NOTE]
> A lista de linguagens e modelos de projeto disponíveis que é exibida depende da versão do Visual Studio que você está executando e das cargas de trabalho que estão instaladas. Para saber mais sobre como instalar cargas de trabalho adicionais, confira [Modificar o Visual Studio adicionando ou removendo cargas de trabalho e componentes](../install/modify-visual-studio.md).

Para mostrar a lista de modelos da linguagem de programação que você deseja usar, clique no triângulo próximo do nome da linguagem e, em seguida, escolha uma categoria de projeto (tal como Área de Trabalho do Windows).

A imagem a seguir mostra os modelos de projeto disponíveis para projetos .NET Core do Visual C#:

![Captura de tela da caixa de diálogo Novo Projeto que lista os modelos de projeto que você pode escolher.](./media/new-project-dialog-net-core.png)

## <a name="configure-your-project"></a>Configurar seu projeto

Digite um nome para o novo projeto na caixa **Nome**. Você pode salvar o projeto no local padrão em seu computador ou escolher o botão **Procurar** para encontrar outro local. Você também pode selecionar um nome de solução ou adicionar o novo projeto a um repositório Git (selecionando **Adicionar ao Controle do Código-Fonte).**

Clique em **OK** para criar a solução e o projeto.

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="open-the-create-a-new-project-page"></a>Abrir a página Criar um novo projeto

Há várias maneiras de criar um projeto no Visual Studio 2019. Quando você abre o Visual Studio, a janela inicial é exibida e, a partir daí, você pode selecionar **Criar um novo projeto.**

:::image type="content" source="media/vs-2019/start-window-create-new-project.png" alt-text="Captura de tela da caixa de diálogo &quot;Criar um novo projeto&quot; na janela de início Visual Studio 2019":::

Se o Visual Studio de desenvolvimento já estiver aberto, você poderá criar um novo projeto escolhendo Arquivo  >  **Novo**  >  **Projeto** na barra de menus. Você também pode clicar no **botão Novo Projeto** na barra de ferramentas ou pressionar **Ctrl** + **Shift** + **N**.

:::image type="content" source="media/vs-2019/new-project-button.png" alt-text="Captura de tela do botão Novo Projeto no Visual Studio 2019.":::

## <a name="select-a-template-type"></a>Selecione um tipo de modelo

Na página **Criar um novo projeto**, uma lista de seus modelos recentemente selecionados aparece à esquerda. Os modelos são classificados por *usados mais recentemente*.

Se não selecionar entre os modelos usados recentemente, você poderá filtrar todos os modelos de projeto disponíveis por **Linguagem de programação** (por exemplo, C# ou C++), **Plataforma** (por exemplo, Windows ou Azure) e **Tipo de projeto** (por exemplo, Desktop ou Web). Você também pode inserir texto de pesquisa na caixa de pesquisa para filtrar ainda mais os modelos, por exemplo, **asp.net**.

:::image type="content" source="media/vs-2019/create-new-project-filters.png" alt-text="Captura de tela dos filtros de modelo de projeto Visual Studio 2019.":::

As marcas que aparecem em cada modelo correspondem aos três filtros de lista suspensa (Tipo de projeto, Plataforma e Linguagem de programação).

> [!TIP]
> Se você não vir o modelo que está procurando, poderá estar faltando uma carga de trabalho para Visual Studio. Para instalar cargas de trabalho adicionais, por exemplo, **Desenvolvimento do Azure** ou **Desenvolvimento móvel com .NET**, clique no link **Instalar mais ferramentas e recursos** para abrir o Instalador do Visual Studio. A partir daí, selecione as cargas de trabalho que deseja instalar e, em seguida, **selecione Modificar**. Depois disso, modelos de projeto adicionais serão disponibilizados para sua escolha.
>
> :::image type="content" source="media/vs-2019/install-more-tools-features.png" alt-text="Captura de tela do link &quot;Instalar mais ferramentas e recursos&quot; no Visual Studio 2019.":::

Selecione um modelo e, em seguida, clique em **Avançar**.

## <a name="configure-your-project"></a>Configurar seu projeto

A **página Configurar seu novo** projeto tem opções para nomear seu projeto (e solução), selecionar um local de disco e selecionar uma versão do Framework (se aplicável ao modelo escolhido).

:::image type="content" source="media/vs-2019/configure-new-project.png" alt-text="Captura de tela da página &quot;Configurar seu novo projeto&quot; no Visual Studio 2019.":::

> [!NOTE]
> Se você criar um projeto quando já tiver um projeto ou solução aberta no Visual Studio, uma opção de configuração adicional estará disponível. Você pode optar por criar uma solução ou adicionar o novo projeto à solução que já está aberta.
>
> :::image type="content" source="media/vs-2019/configure-new-project-solution.png" alt-text="Captura de tela da caixa de diálogo &quot;Criar nova solução&quot; ou &quot;Adicionar à solução&quot; no Visual Studio 2019.":::

Clique em **Criar** para criar o projeto.

::: moniker-end

## <a name="add-additional-projects-to-a-solution"></a>Adicionar projetos adicionais a uma solução

Se você quiser adicionar um projeto adicional a uma solução, clique com o botão direito do mouse no nó da solução no Gerenciador de Soluções e selecione **Adicionar** Novo   >  **Projeto**.

> [!TIP]
> Para obter um exemplo de um projeto e uma solução criados do zero, completo com instruções passo a passo e código de exemplo, consulte Introdução a [projetos e soluções](../get-started/tutorial-projects-solutions.md).

## <a name="see-also"></a>Confira também

- [Introdução a projetos e soluções](../get-started/tutorial-projects-solutions.md)
- [Trabalhar com soluções e projetos](creating-solutions-and-projects.md)
- [Gerenciar propriedades do projeto e da solução](managing-project-and-solution-properties.md)
- [Criar projetos (Visual Studio para Mac)](/visualstudio/mac/create-new-projects)

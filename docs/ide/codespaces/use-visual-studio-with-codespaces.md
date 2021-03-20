---
title: Visual Studio com um codespace (visualização)
description: Saiba como usar o IDE do Visual Studio com o GitHub Codespaces para o desenvolvimento do Windows.
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: add43a5d130d8938193774d50bb643f48ecc3f8c
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104673041"
---
# <a name="how-to-use-visual-studio-with-a-codespace-preview"></a>Como usar o Visual Studio com um codespace (visualização)

> [!Important] 
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Incentivamos você a estar envolvido em nosso [Fórum da comunidade de desenvolvedores](https://developercommunity.visualstudio.com/home) para Visual Studio para obter informações sobre versões futuras e informações de roteiro. 

O Visual Studio tem excelente suporte para o desenvolvimento no GitHub Codespaces. Você pode criar e se conectar a um codespace e ter todo o poder do Visual Studio para trabalhar em seus projetos em um ambiente remoto e hospedado. Embora o código-fonte e as ferramentas estejam em um codespace e sua compilação e depuração estejam acontecendo na nuvem, sua experiência de desenvolvimento se sentirá tão rápida e sem interrupções como se você estivesse trabalhando localmente.

> [!NOTE]
> Este artigo descreve especificamente o uso do Visual Studio para se conectar ao GitHub Codespaces. Você pode aprender sobre como se conectar a um codespace com outros clientes na documentação do [Visual Studio Code](https://docs.github.com/github/developing-online-with-codespaces/connecting-to-your-codespace-from-visual-studio-code) ou do [GitHub](https://docs.github.com/github/developing-online-with-codespaces/developing-in-a-codespace) .

> [!NOTE]
> Se você ainda não tem o [Visual Studio 2019 Preview](https://aka.ms/vspreview) instalado, você pode baixá-lo em [VisualStudio.Microsoft.com](https://aka.ms/vspreview).

## <a name="enable-connect-to-github-codespaces"></a>Habilitar conexão com o GitHub Codespaces

A conexão ao GitHub Codespaces com a visualização do Visual Studio 2019 não está habilitada por padrão, portanto, primeiro você precisará habilitar a opção de recursos de visualização.

1. No Visual Studio 2019 Preview, use o   >  item de menu **Opções** de ferramentas para abrir a caixa de diálogo opções.

2. Em **ambiente**, selecione **recursos de visualização** e marque a **Codespaces conectar ao** recurso de visualização do github.

   ![Verificar o recurso conectar ao GitHub Codespaces Preview](media/connect-to-github-codespaces-preview-feature.png)

3. Será necessário reiniciar o Visual Studio para que o recurso esteja disponível.

## <a name="create-a-codespace"></a>Criar um codespace

Se você ainda não tiver um codespace, poderá criar um no Visual Studio.

1. Quando você iniciar o Visual Studio, a janela iniciar mostrará um botão **conectar a um codespace** em "introdução".

   ![Janela inicial do Visual Studio com conectar a um codespace](media/visual-studio-start-window.png)

2. Selecione **conectar-se a um codespace** e será solicitado que você entre no github. Você também pode criar uma conta do GitHub, se ainda não tiver uma.

   ![Entrar no GitHub do Visual Studio](media/visual-studio-sign-in-to-github.png)

   Depois de selecionar **entrar no GitHub**, siga o fluxo de trabalho de entrada do GitHub online.

3. Se você nunca criou um codespace, será solicitado que você crie um.

   Em "codespace Details", você precisa fornecer uma **URL de repositório**. O GitHub Codespaces clonará o repositório especificado em seu codespace quando ele for criado.

   Você também pode modificar o **tipo de instância** e **suspender após** o tempo limite por meio de seus menus suspensos. Depois de definir os detalhes do codespace, selecione o botão **criar e conectar** .

   ![Detalhes do Visual Studio codespace](media/visual-studio-codespace-details.png)

   O GitHub Codespaces começará a preparar o codespace e abrirá o Visual Studio, uma vez que o codespace estiver pronto.

   O nome do codespace será exibido no indicador remoto na barra de menus.

   ![Visual Studio conectado ao repositório eShopOnWeb codespace](media/visual-studio-eshoponweb-codespace.png)

4. Comece a usar o Visual Studio, da mesma forma que trabalharia localmente. Ações recomendadas:

   * Procure o código-fonte.
   * Selecione um arquivo de solução e Compile a solução (**Ctrl + Shift + B**).
   * Defina um ponto de interrupção em um arquivo de origem e pressione **F5** para iniciar o aplicativo no depurador.
   * Faça alterações e confirme-as em seu repositório.   

> [!NOTE]
> Neste momento, você não pode criar o GitHub Codespaces para Visual Studio por meio do [portal Codespaces](https://github.com/codespaces)do github. Você só pode criá-los usando o Visual Studio.

## <a name="connect-to-a-codespace"></a>Conectar-se a um codespace

Depois de criar seu codespace, você pode abrir seu codespace diretamente do Visual Studio.

1. Quando você iniciar o Visual Studio, a janela iniciar mostrará um botão **conectar a um codespace** em "introdução".

   ![Janela inicial do Visual Studio com conectar a um codespace](media/visual-studio-start-window.png)

   Se você já estiver no Visual Studio, poderá usar o **arquivo**  >  **conectar-se a um** item de menu codespace.

   ![Arquivo do Visual Studio conectar a um item de menu do codespace](media/visual-studio-file-connect-to-codespace.png)

2. Selecione **conectar-se a um codespace**. Você será solicitado a entrar no GitHub, se ainda não tiver feito isso.

3. Em seguida, você verá todos os seus codespaces do GitHub, juntamente com seus detalhes apresentados no painel à direita.

   ![Visual Studio exibindo detalhes e codespaces do GitHub disponíveis](media/visual-studio-connect-codespace.png)

   Qualquer codespaces que clonado um repositório DevOps do Azure só será visível aqui no Visual Studio e não na página Codespaces do GitHub.

4. Escolha um codespace e selecione o botão **conectar** . Se o codespace tiver sido suspenso, ele será reiniciado e o Visual Studio será aberto conectado a esse codespace.

   O nome do codespace será exibido no indicador remoto na barra de menus.

   ![Visual Studio conectado ao repositório eShopOnWeb codespace](media/visual-studio-eshoponweb-codespace.png)

5. Comece a usar o Visual Studio, da mesma forma que trabalharia localmente. Ações recomendadas:

   * Procure o código-fonte.
   * Selecione um arquivo de solução e Compile a solução (**Ctrl + Shift + B**).
   * Defina um ponto de interrupção em um arquivo de origem e pressione **F5** para iniciar o aplicativo no depurador.
   * Faça alterações e confirme-as em seu repositório.

<!-- TBD ## Suspend a codespace -->

<!-- TBD ## Disconnect from a codespace -->

## <a name="see-also"></a>Veja também

* [O que é o GitHub Codespaces?](codespaces-overview.md)
* [Como personalizar um codespace](customize-codespaces.md)
* [Recursos do Visual Studio com suporte](supported-features-codespaces.md)

---
title: Carregar um subconjunto de projetos
ms.date: 12/04/2018
ms.topic: conceptual
ms.prod: visual-studio-dev16
ms.technology: vs-ide-general
helpviewer_keywords:
- filtered solution
- solution filtering
author: gewarren
ms.author: stsu
manager: douge
ms.openlocfilehash: 655644e936bdfb1382e70d746f589b8fcfabf488
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52897133"
---
# <a name="filtered-solutions-in-visual-studio"></a>Soluções filtradas no Visual Studio

**Novidades no Visual Studio 2019 Preview 1**

Grandes equipes de desenvolvimento geralmente colaboram usando uma única solução grande com vários projetos. No entanto, os desenvolvedores individuais normalmente trabalham em um pequeno subconjunto desses projetos. Para melhorar o desempenho ao abrir soluções grandes, o Visual Studio 2019 Preview 1 introduz a *filtragem de solução*. A filtragem de soluções permite que você abra uma solução com apenas projetos seletivos carregados. Carregar um subconjunto de projetos em uma solução diminui a carga, o build e o tempo de execução de teste dessa solução e permite uma revisão mais focalizada.

Os seguintes recursos estão disponíveis:

- Você pode chegar ao código mais rapidamente abrindo uma solução sem carregar nenhum dos seus projetos. Depois que a solução é aberta, é possível escolher seletivamente quais projetos carregar.

- Quando você reabre uma solução, o Visual Studio lembra quais projetos foram carregados em sua sessão anterior e carrega apenas esses projetos.

- Você pode criar um arquivo de filtro de solução para salvar uma ou mais configurações de carregamento do projeto ou compartilhar a configuração com colegas de equipe.

## <a name="open-a-filtered-solution"></a>Abrir uma solução filtrada

Para abrir uma solução com apenas alguns dos seus projetos carregados, siga estas etapas:

1. Na barra de menus, escolha **Arquivo** > **Abrir** > **Projeto/Solução**.

2. Na caixa de diálogo **Novo projeto**, selecione a solução e selecione **Não carregar projetos**.

   ![Caixa de diálogo Abrir projeto do Visual Studio com a opção não carregar projetos marcada](media/filtered-solutions/do-not-load-projects.png)

3. Escolha **Abrir**.

   A solução é aberta com todos os seus projetos descarregados.

4. Na **Gerenciador de Soluções**, selecione os projetos que você deseja carregar (pressione **Ctrl** enquanto clica para selecionar mais de um projeto) e, em seguida, clique com o botão direito do mouse no projeto e escolha **Recarregar projeto**.

   ![Recarregar vários projetos no Gerenciador de Soluções do Visual Studio](media/filtered-solutions/reload-project.png)

   O Visual Studio lembrará de quais projetos estão carregados na próxima vez em que você abrir a solução localmente.

## <a name="toggle-unloaded-project-visibility"></a>Ativar/desativar a visibilidade do projeto descarregado

Você pode optar por ver todos os projetos na solução ou apenas aqueles carregados usando uma das seguintes opções no **Gerenciador de Soluções**:

- Clique com o botão direito do mouse em sua solução e selecione **Mostrar Projetos Descarregados** ou **Ocultar Projetos Descarregados**.

- Selecione o botão **Mostrar todos os arquivos** para ativar a visibilidade dos projetos descarregados.

   ![Botão Mostrar Todos os Arquivos no Gerenciador de Soluções do Visual Studio](media/filtered-solutions/show-all-files.PNG)

## <a name="solution-filter-files"></a>Arquivos do filtro de solução

Se quiser compartilhar sua configuração de carregamento do projeto ou confirmá-la ao controle do código-fonte, você poderá criar um arquivo de filtro de solução (que tenha a extensão *.slnf*). Quando você abre um arquivo de filtro de solução, a solução é aberta no Visual Studio com os projetos especificados carregados e todos os projetos descarregados ocultos. Você pode [ativar](#toggle-unloaded-project-visibility) a configuração para exibir os projetos descarregados.

Os arquivos de solução do filtro visualmente são diferenciados dos arquivos de solução comuns pelo glifo de funil adicional no ícone ao lado da solução no **Gerenciador de Soluções**. O nome do filtro e o número de projetos carregados também são mostrados ao lado do nome da solução.

![Arquivo de filtro de solução aberto no Gerenciador de Soluções do Visual Studio](media/filtered-solutions/solution-filter.PNG)

> [!NOTE]
> Se novos projetos forem adicionados à solução original depois de criar o arquivo de filtro de solução, eles aparecerão como projetos descarregados no **Gerenciador de Soluções**.

### <a name="create-a-solution-filter-file"></a>Criar um arquivo de filtro de solução

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução e selecione **Salvar como filtro de solução**.

   ![Menu Salvar como filtro de solução no Gerenciador de Soluções do Visual Studio](media/filtered-solutions/save-as-solution-filter.png)

2. Escolha um nome e uma localização para o arquivo de filtro de solução.

Depois de criar um arquivo de filtro de solução, ele é adicionado à sua lista de **Projetos e soluções recentes** para facilitar o acesso:

![Abrir recente no Visual Studio](media/filtered-solutions/open-recent.png)

## <a name="see-also"></a>Consulte também

- [Personalizar o aninhamento de arquivos no Gerenciador de Soluções](file-nesting-solution-explorer.md)
- [Otimizar o desempenho do Visual Studio](optimize-visual-studio-performance.md)
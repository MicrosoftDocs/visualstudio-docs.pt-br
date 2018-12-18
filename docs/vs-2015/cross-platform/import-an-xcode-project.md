---
title: Importar um projeto do XCode | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aa4b8161-d98f-4a1a-9db3-520133bfc82f
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.openlocfilehash: b0e42c167e87f19781f9544e20e7870789af4ef9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51754148"
---
# <a name="import-an-xcode-project"></a>Importar um projeto do XCode
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O Microsoft Visual C++ para Desenvolvimento Móvel Multiplataforma inclui o suporte para mover seus projetos XCode para o Visual Studio, onde você pode criar bibliotecas multiplataforma e compartilhar o código com outros projetos. O assistente Importar do XCode simplifica o processo de importação de projetos e divisão do código C++ nos destinos XCode para serem usados como uma biblioteca estática ou projeto de código compartilhado. Você pode gerenciar seu código específico do iOS no Visual Studio e ainda usar o XCode para fazer storyboards e build. Para obter informações sobre como mover facilmente código entre o Visual Studio e o XCode, consulte Mover as alterações entre o XCode e o Visual Studio.  
  
## <a name="using-the-import-from-xcode-wizard"></a>Usando o assistente Importar do XCode  
 Este tópico mostra como mover um projeto do XCode para o Visual Studio para aproveitar as soluções multiplataforma e o compartilhamento de código. Como pré-requisito, você deve emparelhar seu Mac com o Visual Studio para poder importar, exportar e compilar seu projeto. Para obter instruções sobre como configurar o emparelhamento, consulte [Instalar e configurar ferramentas de build usando o iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md). Você também deve compartilhar seu projeto XCode pela rede ou movê-lo para o computador do Visual Studio para usar o assistente Importar do XCode.  
  
#### <a name="import-from-xcode"></a>Importar do XCode  
  
1. No menu **Arquivo**, escolha **Novo**, **Importar**, **Importar do XCode**. Isso inicia a caixa de diálogo do assistente **Importar do XCode**.  
  
    ![Escolha o projeto de destino do XCode para importar](../cross-platform/media/cppmdd-u2-importxcode-choose.PNG "CPPMDD_U2_ImportXCode_Choose")  
  
2. No painel **Escolher um projeto**, escolha o botão Procurar para selecionar um arquivo .pbxproj do XCode. Navegue até o arquivo de projeto na caixa de diálogo **Selecionar arquivo de projeto do XCode** e escolha **Abrir**.  
  
    ![Selecione um arquivo de projeto na caixa de diálogo Selecionar arquivo de projeto do XCode](../cross-platform/media/cppmdd-u2-importxcode-browse.PNG "CPPMDD_U2_ImportXCode_Browse")  
  
    No assistente Importar do XCode, escolha **Avançar**.  
  
3. No painel **Destinos**, escolha os destinos do projeto do XCode para importar nos projetos do Visual Studio. Os destinos do XCode são semelhantes aos projetos do Visual Studio, a maioria é uma coleção de códigos e recursos que produzem um binário. O assistente Importar do XCode permite apenas a importação de destinos que produzem um binário, mas não uma biblioteca estática, como destinos. Os destinos de biblioteca estática do XCode são o assunto da próxima etapa.  
  
    ![Painel Destinos do assistente Importar do XCode](../cross-platform/media/cppmdd-u2-importxcode-destination.jpg "CPPMDD_U2_ImportXCode_Destination")  
  
    Para cada destino selecionado em **Destinos para importar**, o assistente detecta automaticamente os arquivos de código C++ que podem ser divididos em um projeto de biblioteca estática separado e os coloca na seção **Itens de projeto C++**. Outros recursos e código são deixados na seção **Itens do projeto do XCode**. Elas se tornam projetos de aplicativo e biblioteca estática separados no Visual Studio quando o assistente conclui o processo de importação. Por padrão, os destinos de estrutura e unidade de teste não são separados em projetos diferentes no assistente.  
  
    Para alterar quais arquivos estão em cada projeto, use os botões para cima e para baixo. Quando estiver satisfeito com os arquivos em cada projeto, escolha **Avançar** para continuar.  
  
4. No painel **Destinos da biblioteca**, escolha quais destinos da biblioteca estática do projeto do XCode para importar nos projetos do Visual Studio. Nesse painel, você pode escolher quais arquivos são colocados em um projeto de Código Compartilhado e quais são colocados em um projeto de biblioteca estática. Em cada um dos destinos na lista **Destinos para importar**, você pode controlar quais arquivos são colocados nos **Itens de projeto de Código Compartilhado** e nos **Itens de projeto de Biblioteca Estática** usando os botões para cima e para baixo.  
  
    ![Painel Destinos da Biblioteca de Importar do XCode](../cross-platform/media/cppmdd-u2-importxcode-library.jpg "CPPMDD_U2_ImportXCode_Library")  
  
    Um projeto de código compartilhado é uma maneira de compartilhar um conjunto de arquivos de código-fonte entre projetos no Visual Studio. O código é compilado como parte do projeto que o inclui, não como um projeto independente. Como os projetos que incluem o código compartilhado podem ter configurações e arquiteturas diferentes, essa é a melhor maneira de fornecer um único projeto que contém o código que pode ser compilado para muitos tipos de plataforma.  
  
    Quando estiver satisfeito com os arquivos em cada projeto, escolha **Avançar** para continuar.  
  
5. O painel **Propriedades Globais** pode ser usado para definir um caminho de pesquisa de estrutura e um caminho de pesquisa de cabeçalho de inclusão para todos os projetos de iOS no Visual Studio. O Visual Studio usa esses caminhos para navegação no código-fonte e para o IntelliSense. Esses caminhos globais são úteis quando você cria projetos de iOS que usam um conjunto comum de cabeçalhos e estruturas.  
  
    ![Painel Propriedades Globais de Importar do XCode](../cross-platform/media/cppmdd-u2-importxcode-global.jpg "CPPMDD_U2_ImportXCode_Global")  
  
    Esses caminhos globais também podem ser definidos no Visual Studio na caixa de diálogo **Opções**. Para encontrá-los, no menu **Ferramentas**, selecione **Opções**. Na caixa de diálogo **Opções**, expanda **Plataforma Cruzada**, **C++**, **iOS**, **Propriedades Globais**.  
  
    Escolha **Avançar** para continuar.  
  
6. O painel **Estruturas** é usado para configurar os caminhos usados pelo Visual Studio para navegar e IntelliSense para seu projeto. Os caminhos devem estar acessíveis para o Visual Studio para cada estrutura referenciada pelo seu projeto XCode. O assistente verifica as referências de estrutura nos projetos do XCode e mostra se o Visual Studio pode encontrar a estrutura. Qualquer caminho que você já configurou nas Propriedades Globais deve ser descoberto pelo Visual Studio. As exceções são listadas na lista Estruturas. Para cada estrutura listada com um X, forneça um caminho acessível do computador para o Visual Studio localizar a estrutura. Você pode usar o botão Procurar [...] para usar uma caixa de diálogo **Selecionar Pasta** para localizar o caminho. O caminho da estrutura pode ser para uma cópia local ou para um compartilhamento acessível pela rede no Mac.  
  
    ![Painel Estruturas de Importar do XCode](../cross-platform/media/cppmdd-u2-importxcode-frameworks.jpg "CPPMDD_U2_ImportXCode_Frameworks")  
  
    Escolha **Avançar** para continuar.  
  
7. O painel **Configurações do Projeto** permite que você altere as configurações de caminho de pesquisa de cabeçalho de inclusão e de estrutura para cada projeto que o assistente cria. Use este painel para definir caminhos específicos do projeto que são diferentes das configurações globais.  
  
    Para definir um caminho para um projeto específico, na lista suspensa **Projeto de destino**, selecione o arquivo de projeto e defina os valores nos controles **Caminho de Pesquisa de Estrutura** e **Incluir Caminho de Pesquisa de Cabeçalho**. Você pode usar o botão Procurar [...] ao lado de cada controle para usar uma caixa de diálogo **Selecionar Pasta** para localizar o caminho.  
  
    ![Painel Projetos de Importar do XCode](../cross-platform/media/cppmdd-u2-importxcode-projects.jpg "CPPMDD_U2_ImportXCode_Projects")  
  
    Se nenhum Mac remoto tiver sido emparelhado com este computador no Visual Studio, o link Configurar um Computador Remoto será exibido. Para obter instruções sobre como configurar o emparelhamento, consulte [Instalar e configurar ferramentas de build usando o iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md).  
  
    Para importar o projeto XCode usando as configurações do assistente, escolha **Importar**.  
  
   O assistente Importar do XCode cria projetos no Visual Studio que correspondem aos destinos de projeto XCode selecionados. O código que pode ser compartilhado com outros projetos do C++ é dividido em projetos de biblioteca estática e código compartilhado separados. O código restante é colocado em projetos de aplicativo e biblioteca iOS que podem ser compilados remotamente pelo Visual Studio. Para obter mais informações sobre como mover o código entre o Visual Studio e o XCode, consulte [Alterações de sincronização entre o XCode e o Visual Studio](../cross-platform/sync-changes-between-xcode-and-visual-studio.md).


---
title: 'Passo a passo: Criar um aplicativo'
ms.date: 09/25/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2987df6c8ed8a26c2cf95020e26f67c36721d676
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672776"
---
# <a name="walkthrough-build-an-application"></a>Passo a passo: Criar um aplicativo

Ao concluir este passo a passo, você ficará mais familiarizado com as várias opções que podem ser configuradas ao compilar aplicativos com o Visual Studio. Você criará uma configuração de build personalizada, ocultará determinadas mensagens de aviso e aumentará as informações de saída de build de um aplicativo de exemplo.

## <a name="install-the-sample-application"></a>Instalar o aplicativo de exemplo

Baixe a amostra [Introdução à criação de aplicativos WPF](https://code.msdn.microsoft.com/Introduction-to-Building-b8d16419). Escolha C# ou Visual Basic. Depois de baixar o arquivo *.zip*, extraia-o e abra o arquivo *ExpenseItIntro.sln* usando o Visual Studio.

## <a name="create-a-custom-build-configuration"></a>Criar uma configuração de build personalizada

Ao criar uma solução, as configurações de build de depuração e versão e seus destinos de plataforma padrão são definidos para a solução automaticamente. Depois, é possível personalizar essas configurações ou criar suas próprias. As configurações de build especificam o tipo de build. As plataformas de build especificam o sistema operacional que um aplicativo tem como destino para a configuração. Para obter mais informações, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md), [Noções básicas sobre plataformas de build](../ide/understanding-build-platforms.md) e [Como definir as configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md).

É possível alterar ou criar configurações e configurações de plataforma por meio da caixa de diálogo **Configuration Manager**. Neste procedimento, você criará uma configuração de build para testes.

### <a name="create-a-build-configuration"></a>Criar uma configuração de build

1. Abra a caixa de diálogo **Configuration Manager**.

   ![Menu Compilar, comando do Configuration Manager](../ide/media/buildwalk_configurationmanagerdialogbox.png)

1. Na lista **Configuração da solução ativa**, escolha **\<Nova....\>**.

1. Na caixa de diálogo **Nova Configuração da Solução**, dê à nova configuração o nome `Test`, copie as configurações da configuração **Depuração** existente e, em seguida, escolha o botão **OK**.

   ![Caixa de diálogo Nova Configuração da Solução](../ide/media/buildwalk_newsolutionconfigdlgbox.png)

1. Na lista **Plataforma da solução ativa**, escolha **\<Nova...\>**.

1. Na caixa de diálogo **Nova Plataforma de Solução**, escolha **x64** e não copie as configurações da plataforma x86.

   ![Caixa de diálogo Nova Plataforma da Solução](../ide/media/buildwalk_newsolutionplatform.png)

1. Escolha o botão **OK**.

   A configuração da solução ativa foi alterada para **Teste** com a plataforma da solução ativa definida como x64.

   ![Configuration Manager com configuração de Teste](../ide/media/buildwalk_configmanagertestconfig.png)

1. Escolha **Fechar**.

É possível verificar ou alterar de forma rápida a configuração da solução ativa usando a lista **Configurações da Solução** na barra de ferramentas **Padrão**.

![Configuração de solução opção Barra de ferramentas padrão](../ide/media/buildwalk_standardtoolbarsolutioncongfig.png)

## <a name="build-the-application"></a>Compilar o aplicativo

Em seguida, você compilará a solução com a configuração de build personalizada.

### <a name="build-the-solution"></a>Criar a solução

-   Na barra de menus, escolha **Compilar** > **Compilar Solução**.

    A Janela de **Saída** exibe os resultados do build. O build foi bem-sucedido.

## <a name="hide-compiler-warnings"></a>Ocultar avisos do compilador

Em seguida, apresentaremos alguns códigos que fazem com que um aviso seja gerado pelo compilador.

1. No projeto de C#, abra o arquivo *ExpenseReportPage.xaml.cs*. No método **ExpenseReportPage**, adicione o seguinte código: `int i;`.

    OU

    No projeto do Visual Basic, abra o arquivo *ExpenseReportPage.xaml.vb*. No construtor personalizado **Public Sub New...**, adicione o seguinte código: `Dim i`.

1. Compile a solução.

A Janela de **Saída** exibe os resultados do build. O build foi bem-sucedido, mas foram gerados avisos:

![Janela de Saída Visual Basic](../ide/media/buildwalk_vbbuildoutputwnd.png)

![Janela de Saída do Visual C&#35;](../ide/media/buildwalk_csharpbuildoutputwnd.png)

Temporariamente, é possível ocultar determinadas mensagens de aviso durante um build, em vez de deixá-las acumular a saída do build.

### <a name="hide-a-specific-c-warning"></a>Ocultar um aviso específico do C#

1. No **Gerenciador de Soluções**, escolha o nó do projeto de nível superior.

1. Na barra de menus, escolha **Exibir** > **Páginas de Propriedade**.

     O **Designer de Projeto** é aberto.

1. Escolha a página **Build** e, em seguida, na caixa **Suprimir avisos**, especifique o número de aviso **0168**.

     ![Página Build, Designer de Projeto](../ide/media/buildwalk_csharpsuppresswarnings.png)

     Para obter mais informações, consulte [Página Build, Designer de Projeto (C#)](../ide/reference/build-page-project-designer-csharp.md).

1. Compile a solução.

     A Janela de **Saída** exibe apenas informações de resumo do build.

     ![Janela de Saída, Visual C&#35; Avisos de build](../ide/media/buildwalk_visualcsharpbuildwarnings.png)

### <a name="suppress-all-visual-basic-build-warnings"></a>Suprimir todos os avisos de build do Visual Basic

1. No **Gerenciador de Soluções**, escolha o nó do projeto de nível superior.

2. Na barra de menus, escolha **Exibir** > **Páginas de Propriedade**.

     O **Designer de Projeto** é aberto.

3. Na página **Compilar**, marque a caixa de seleção **Desabilitar todos os avisos**.

     ![Página Compilar, Designer de Projeto](../ide/media/buildwalk_vbsuppresswarnings.png)

     Para obter mais informações, consulte [Configurar avisos no Visual Basic](../ide/configuring-warnings-in-visual-basic.md).

4. Compile a solução.

   A Janela de **Saída** exibe apenas informações de resumo do build.

   ![Janela de Saída, Avisos de build do Visual Basic](../ide/media/buildwalk_visualbasicbuildwarnings.png)

   Para obter mais informações, consulte [Como suprimir avisos do compilador](../ide/how-to-suppress-compiler-warnings.md).

## <a name="display-additional-build-details-in-the-output-window"></a>Exibir detalhes de build adicionais na janela Saída

É possível alterar a quantidade de informações sobre o processo de build exibidas na Janela de **Saída**. Geralmente, os detalhes de build são definidos como **Mínimos**, o que significa que a janela **Saída** exibe apenas um resumo do processo de build, junto com os avisos de prioridade alta ou erros. Exiba mais informações sobre o build usando a [caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md).

> [!IMPORTANT]
> Se você exibir mais informações, o build levará mais tempo para ser concluído.

### <a name="change-the-amount-of-information-in-the-output-window"></a>Alterar a quantidade de informações na janela Saída

1. Abra a caixa de diálogo **Opções**.

     ![Comando Opções no menu Ferramentas](../ide/media/exploreide-toolsoptionsmenu.png)

1. Escolha a categoria **Projetos e Soluções** e, em seguida, a página **Compilar e Executar**.

1. Na lista **Detalhes da saída de build do projeto do MSBuild**, escolha **Normal** e, em seguida, o botão **OK**.

1. Na barra de menus, escolha **Build** > **Limpar Solução**.

1. Compile a solução e, em seguida, examine as informações na Janela de **Saída**.

     As informações do build incluem a hora de início do build (localizada no início) e ordem em que os arquivos foram processados. Essas informações também incluem a sintaxe real do compilador que o Visual Studio executa durante o build.

     Por exemplo, no build do C#, a opção [/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) lista o código de aviso **1762**, que foi especificado anteriormente neste tópico, juntamente com três outros avisos.

     No build do Visual Basic, [/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) não inclui avisos específicos a serem excluídos e, portanto, nenhum aviso é exibido.

    > [!TIP]
    > Pesquise o conteúdo da janela **Saída** se você exibir a caixa de diálogo **Localizar** escolhendo as teclas **Ctrl**+**F**.

Para obter mais informações, consulte [Como exibir, salvar e configurar arquivos de log de build](../ide/how-to-view-save-and-configure-build-log-files.md).

## <a name="create-a-release-build"></a>Criar um build da versão

É possível compilar uma versão do aplicativo de exemplo que é otimizada para enviá-lo. Para o build de versão, você especificará que o arquivo executável é copiado para um compartilhamento de rede antes do início do build.

Para obter mais informações, consulte [Como alterar o diretório de saída do build](../ide/how-to-change-the-build-output-directory.md) e [Compilar e limpar projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md).

### <a name="specify-a-release-build-for-visual-basic"></a>Especificar um build de versão para o Visual Basic

1. Abra o **Designer de Projeto**.

     ![Menu Exibir, comando Páginas de propriedade](../ide/media/buildwalk_viewpropertypages.png)

1. Escolha a página **Compilar**.

1. Na lista **Configuração**, escolha **Versão**.

1. Na lista **Plataforma**, escolha **x86**.

1. Na caixa **Caminho de saída do build**, especifique um caminho de rede.

     Por exemplo, você pode especificar `\\myserver\builds`.

    > [!IMPORTANT]
    > Uma caixa de mensagem poderá ser exibida, avisando que o compartilhamento de rede especificado pode não ser um local confiável. Se você confiar no local especificado, escolha o botão **OK** na caixa de mensagem.

1. Compile o aplicativo.

     ![Comando Compilar solução no menu Compilar](../ide/media/exploreide-buildsolution.png)

### <a name="specify-a-release-build-for-c"></a>Especificar um build de versão para o C# #

1. Abra o **Designer de Projeto**.

     ![Menu Exibir, comando Páginas de propriedade](../ide/media/buildwalk_viewpropertypages.png)

1. Escolha a página **Build**.

1. Na lista **Configuração**, escolha **Versão**.

1. Na lista **Plataforma**, escolha **x86**.

1. Na caixa **Caminho de saída**, especifique um caminho de rede.

     Por exemplo, você pode especificar `\\myserver\builds`.

    > [!IMPORTANT]
    > Uma caixa de mensagem poderá ser exibida, avisando que o compartilhamento de rede especificado pode não ser um local confiável. Se você confiar no local especificado, escolha o botão **OK** na caixa de mensagem.

1. Na **barra de ferramentas Padrão**, defina as Configurações da solução como **Versão** e as Plataformas da solução como **x86**.

1. Compile o aplicativo.

     ![Comando Compilar solução no menu Compilar](../ide/media/exploreide-buildsolution.png)

   O arquivo executável é copiado para o caminho de rede especificado. Seu caminho será `\\myserver\builds\\FileName.exe`.

Parabéns! Você concluiu este passo a passo com êxito.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Criar um projeto (C++)](/cpp/ide/walkthrough-building-a-project-cpp)
- [Visão geral da pré-compilação de projeto de aplicativo Web ASP.NET](/previous-versions/aspnet/aa983464\(v\=vs.110\))
- [Passo a passo: Usar o MSBuild](../msbuild/walkthrough-using-msbuild.md)
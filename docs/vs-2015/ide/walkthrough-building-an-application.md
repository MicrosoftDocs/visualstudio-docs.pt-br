---
title: 'Passo a passo: Criando um aplicativo | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4842955d-8959-4e4e-98b8-2358360179b3
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e6c45a552e66c2d256c191f6bd8296f5b2ca2c61
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220193"
---
# <a name="walkthrough-building-an-application"></a>Instruções passo a passo: criando um aplicativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao concluir este passo a passo, você ficará mais familiarizado com as várias opções que podem ser configuradas ao compilar aplicativos com o Visual Studio. Você criará uma configuração de build personalizada, ocultará determinadas mensagens de aviso e aumentará as informações de saída de build, entre outras tarefas, de um aplicativo de exemplo.  
  
 Esse tópico contém as seguintes seções:  
  
 [Instalar o aplicativo de exemplo](../ide/walkthrough-building-an-application.md#BKMK_installapp)  
  
 [Criar uma configuração de build personalizada](../ide/walkthrough-building-an-application.md#BKMK_CreateBuildConfig)  
  
 [Compilar o aplicativo](../ide/walkthrough-building-an-application.md#BKMK_building)  
  
 [Ocultar avisos do compilador](../ide/walkthrough-building-an-application.md#BKMK_hidewarning)  
  
 [Exibir detalhes de build adicionais na Janela de Saída](../ide/walkthrough-building-an-application.md#BKMK_outputdetails)  
  
 [Criar um build da versão](../ide/walkthrough-building-an-application.md#BKMK_releasebuild)  
  
##  <a name="BKMK_installapp"></a> Instalar o aplicativo de exemplo  
 Você usará a caixa de diálogo **Extensões e Atualizações** para encontrar e instalar a amostra [Introdução à compilação de aplicativos WPF](http://code.msdn.microsoft.com/Introduction-to-Building-b8d16419?SRC=VSIDE) da Galeria de Amostras no site da Microsoft. A Galeria de Amostras fornece uma variedade de projetos e códigos de exemplo que podem ser baixados e examinados conforme você planeja e desenvolve seus aplicativos.  
  
#### <a name="to-install-the-sample-application"></a>Para instalar o aplicativo de exemplo  
  
1. Na barra de menus, escolha **Ferramentas**, **Extensões e Atualizações**.  
  
2. Escolha a categoria **Online** e, em seguida, a categoria **Galeria de Amostras**.  
  
3. Especifique `Introduction` na caixa de pesquisa para encontrar a amostra.  
  
    ![Caixa de diálogo Extensões e Atualizações](../ide/media/buildwalk-extensionsdialogsampledownload.png "BuildWalk_ExtensionsDialogSampleDownload")  
  
4. Na lista de resultados, escolha **Introdução à compilação de aplicativos WPF (Visual C#)** ou **Introdução à compilação de aplicativos WPF (Visual Basic)**.  
  
5. Escolha o botão **Baixar** e, em seguida, o botão **Fechar**.  
  
   A amostra Introdução à compilação de aplicativos WPF é exibida na caixa de diálogo **Novo Projeto**.  
  
#### <a name="to-create-a-solution-for-the-sample-application"></a>Para criar uma solução para o aplicativo de exemplo  
  
1.  Abra a caixa de diálogo **Novo Projeto**.  
  
     ![Na barra de menus, escolha Arquivo, Novo, Projeto](../ide/media/exploreide-filenewproject.png "ExploreIDE-FileNewProject")  
  
2.  Na categoria **Instaladas**, escolha a categoria **Amostras** para exibir a amostra Introdução à compilação de aplicativos WPF.  
  
3.  Nomeie a solução `IntroWPFcsharp` do Visual C#.  
  
     ![Caixa de diálogo Novo Projeto, Amostras Instaladas](../ide/media/buildwalk-newprojectdlgintrotowpfsample.png "BuildWalk_NewProjectdlgIntrotoWPFsample")  
  
     OU  
  
     Nomeie a solução `IntroWPFvb` do Visual Basic.  
  
     ![Caixa de diálogo Novo Projeto, Amostra do Visual Basic](../ide/media/buildwalk-newprojectdlgintrotowpfsamplevb.png "BuildWalk_NewProjectdlgIntrotoWPFsampleVB")  
  
4.  Escolha o botão **OK**.  
  
##  <a name="BKMK_CreateBuildConfig"></a> Criar uma configuração de build personalizada  
 Ao criar uma solução, as configurações de build de depuração e versão e seus destinos de plataforma padrão são definidos para a solução automaticamente. Depois, é possível personalizar essas configurações ou criar suas próprias. As configurações de build especificam o tipo de build. As plataformas de build especificam o sistema operacional que um aplicativo tem como destino para a configuração. Para obter mais informações, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md), [Noções básicas sobre plataformas de build](../ide/understanding-build-platforms.md) e [Configurações de depuração e versão do projeto](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
 É possível alterar ou criar configurações e configurações de plataforma por meio da caixa de diálogo **Configuration Manager**. Neste procedimento, você criará uma configuração de build para testes.  
  
#### <a name="to-create-a-build-configuration"></a>Para criar uma configuração de build  
  
1. Abra a caixa de diálogo **Configuration Manager**.  
  
    ![Menu Build, comando do Configuration Manager](../ide/media/buildwalk-configurationmanagerdialogbox.png "BuildWalk_ConfigurationManagerDialogBox")  
  
2. Na lista **Configuração da solução ativa**, escolha **Nova**.  
  
3. Na caixa de diálogo **Nova Configuração da Solução**, nomeie a nova configuração `Test`, copie as configurações da configuração de Depuração existentes e, em seguida, escolha o botão **OK**.  
  
    ![Caixa de diálogo Nova Configuração da Solução](../ide/media/buildwalk-newsolutionconfigdlgbox.png "BuildWalk_NewSolutionConfigDlgBox")  
  
4. Na lista **Plataforma da solução ativa**, escolha **Nova**.  
  
5. No **nova plataforma de solução** diálogo caixa, escolha **x64**e não copie as configurações de x86 plataforma.  
  
    ![Caixa de diálogo Nova Plataforma da Solução](../ide/media/buildwalk-newsolutionplatform.png "BuildWalk_NewSolutionPlatform")  
  
6. Escolha o botão **OK**.  
  
   A configuração da solução ativa foi alterada para Teste com a plataforma da solução ativa definida como x64.  
  
   ![Configuration Manager com a configuração de Teste](../ide/media/buildwalk-configmanagertestconfig.png "BuildWalk_ConfigManagerTestconfig")  
  
   É possível verificar ou alterar de forma rápida a configuração da solução ativa usando a lista **Configurações da Solução** na barra de ferramentas **Padrão**.  
  
   ![Opção de Configuração da Solução na barra de ferramentas Padrão](../ide/media/buildwalk-standardtoolbarsolutioncongfig.png "BuildWalk_StandardToolbarSolutionCongfig")  
  
##  <a name="BKMK_building"></a> Compilar o aplicativo  
 Em seguida, você compilará a solução com a configuração de build personalizada.  
  
#### <a name="to-build-the-solution"></a>Para compilar a solução  
  
- Na barra de menus, escolha **Compilar**, **Compilar Solução**.  
  
  A Janela de **Saída** exibe os resultados do build. O build foi bem-sucedido, mas várias mensagens de aviso foram geradas.  
  
  Figura 1: Avisos do Visual Basic  
  
  ![Janela de Saída do Visual Basic](../ide/media/buildwalk-vbbuildoutputwnd.png "BuildWalk_VBBuildOutputWnd")  
  
  Figura 2: Avisos do Visual C#  
  
  ![Janela de Saída do Visual C&#35;](../ide/media/buildwalk-csharpbuildoutputwnd.png "BuildWalk_CsharpBuildOutputWnd")  
  
##  <a name="BKMK_hidewarning"></a> Ocultar avisos do compilador  
 Temporariamente, é possível ocultar determinadas mensagens de aviso durante um build, em vez de deixá-las acumular a saída do build.  
  
#### <a name="to-hide-a-specific-visual-c-warning"></a>Para ocultar um aviso específico do Visual C#  
  
1.  No **Gerenciador de Soluções**, escolha o nó do projeto de nível superior.  
  
2.  Na barra de menus, escolha **Exibir**, **Páginas de Propriedade**.  
  
     O **Designer de Projeto** é aberto.  
  
3.  Escolha a página **Build** e, em seguida, na caixa **Suprimir avisos**, especifique o número de aviso `1762`.  
  
     ![Página Build, Designer de projeto](../ide/media/buildwalk-csharpsuppresswarnings.png "BuildWalk_CsharpSuppressWarnings")  
  
     Para obter mais informações, consulte [Página Build, Designer de Projeto (C#)](../ide/reference/build-page-project-designer-csharp.md).  
  
4.  Compile a solução.  
  
     A Janela de **Saída** exibe apenas informações de resumo do build.  
  
     ![Janela de Saída, Avisos de Build do Visual C&#35;](../ide/media/buildwalk-visualcsharpbuildwarnings.png "BuildWalk_VisualCsharpBuildWarnings")  
  
#### <a name="to-suppress-all-visual-basic-build-warnings"></a>Para suprimir todos os avisos de build do Visual Basic  
  
1. No **Gerenciador de Soluções**, escolha o nó do projeto de nível superior.  
  
2. Na barra de menus, escolha **Exibir**, **Páginas de Propriedade**.  
  
    O **Designer de Projeto** é aberto.  
  
3. Na página **Compilar**, marque a caixa de seleção **Desabilitar todos os avisos**.  
  
    ![Página de compilação, Designer de projeto](../ide/media/buildwalk-vbsuppresswarnings.png "BuildWalk_VBSuppressWarnings")  
  
    Para obter mais informações, consulte [Configurando avisos no Visual Basic](../ide/configuring-warnings-in-visual-basic.md).  
  
4. Compile a solução.  
  
   A Janela de **Saída** exibe apenas informações de resumo do build.  
  
   ![Janela de Saída, Avisos de Build do Visual Basic](../ide/media/buildwalk-visualbasicbuildwarnings.png "BuildWalk_VisualBasicBuildWarnings")  
  
   Para obter mais informações, consulte [Como suprimir avisos do compilador](../ide/how-to-suppress-compiler-warnings.md).  
  
##  <a name="BKMK_outputdetails"></a> Exibir detalhes de build adicionais na Janela de Saída  
 É possível alterar a quantidade de informações sobre o processo de build exibidas na Janela de **Saída**. Geralmente, os detalhes de build são definidos como Mínimos, o que significa que a Janela de **Saída** exibe apenas um resumo do processo de build, junto com os avisos de prioridade alta ou erros. É possível exibir mais informações sobre o build usando a [Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md).  
  
> [!IMPORTANT]
>  Se você exibir mais informações, o build levará mais tempo para ser concluído.  
  
#### <a name="to-change-the-amount-of-information-in-the-output-window"></a>Para alterar a quantidade de informações na Janela de Saída  
  
1. Abra a caixa de diálogo **Opções**.  
  
    ![Comando Opções no menu Ferramentas](../ide/media/exploreide-toolsoptionsmenu.png "ExploreIDE-ToolsOptionsmenu")  
  
2. Escolha a categoria **Projetos e Soluções** e, em seguida, a página **Compilar e Executar**.  
  
3. Na lista **Detalhes da saída de build do projeto do MSBuild**, escolha **Normal** e, em seguida, o botão **OK**.  
  
4. Na barra de menus, escolha **Build**, **Limpar Solução**.  
  
5. Compile a solução e, em seguida, examine as informações na Janela de **Saída**.  
  
    As informações do build incluem a hora de início do build (localizada no início), a ordem em que os arquivos foram processados e o tempo que o processo levou para ser concluído (localizado no final). Essas informações também incluem a sintaxe real do compilador que o Visual Studio executa durante o build.  
  
    Por exemplo, no build do Visual C#, a opção [/nowarn](http://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) lista o código de aviso 1762, que foi especificado anteriormente neste tópico, juntamente com três outros avisos.  
  
    No build do Visual Basic, [/nowarn](http://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) não inclui avisos específicos a serem excluídos e, portanto, nenhum aviso é exibido.  
  
   > [!TIP]
   >  É possível pesquisar o conteúdo da Janela de **Saída** se você exibir a caixa de diálogo **Localizar** escolhendo as teclas Ctrl+F.  
  
   Para obter mais informações, consulte [Como exibir, salvar e configurar arquivos de log de build](../ide/how-to-view-save-and-configure-build-log-files.md).  
  
##  <a name="BKMK_releasebuild"></a> Criar um build da versão  
 É possível compilar uma versão do aplicativo de exemplo que é otimizada para enviá-lo. Para o build de versão, você especificará que o executável é copiado para um compartilhamento de rede antes do início do build.  
  
 Para obter mais informações, consulte [Como alterar o diretório de saída do build](../ide/how-to-change-the-build-output-directory.md) e [Criando e limpando projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md).  
  
#### <a name="to-specify-a-release-build-for-visual-basic"></a>Para especificar um build de versão para o Visual Basic  
  
1.  Abra o **Designer de Projeto**.  
  
     ![Menu Exibir, comando Páginas de Propriedades](../ide/media/buildwalk-viewpropertypages.png "BuildWalk_ViewPropertyPages")  
  
2.  Escolha a página **Compilar**.  
  
3.  Na lista **Configuração**, escolha **Versão**.  
  
4.  Na lista **Plataforma**, escolha **x86**.  
  
5.  Na caixa **Caminho de saída do build**, especifique um caminho de rede.  
  
     Por exemplo, é possível especificar \\\myserver\builds.  
  
    > [!IMPORTANT]
    >  Uma caixa de mensagem poderá ser exibida, avisando que o compartilhamento de rede especificado pode não ser um local confiável. Se você confiar no local especificado, escolha o botão **OK** na caixa de mensagem.  
  
6.  Compile o aplicativo.  
  
     ![Comando Compilar Solução no menu Compilar](../ide/media/exploreide-buildsolution.png "ExploreIDE-BuildSolution")  
  
#### <a name="to-specify-a-release-build-for-visual-c"></a>Para especificar um build de versão para o Visual C#  
  
1. Abra o **Designer de Projeto**.  
  
    ![Menu Exibir, comando Páginas de Propriedades](../ide/media/buildwalk-viewpropertypages.png "BuildWalk_ViewPropertyPages")  
  
2. Escolha a página **Build**.  
  
3. Na lista **Configuração**, escolha **Versão**.  
  
4. Na lista **Plataforma**, escolha **x86**.  
  
5. Na caixa **Caminho de saída**, especifique um caminho de rede.  
  
    Por exemplo, você poderia especificar \\\myserver\builds.  
  
   > [!IMPORTANT]
   >  Uma caixa de mensagem poderá ser exibida, avisando que o compartilhamento de rede especificado pode não ser um local confiável. Se você confiar no local especificado, escolha o botão **OK** na caixa de mensagem.  
  
6. Compile o aplicativo.  
  
    ![Comando Compilar Solução no menu Compilar](../ide/media/exploreide-buildsolution.png "ExploreIDE-BuildSolution")  
  
   O arquivo executável é copiado para o caminho de rede especificado. O caminho será \\\myserver\builds\\*FileName*.exe.  
  
   Parabéns, você concluiu este passo a passo com êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Compilando um projeto (C++)](http://msdn.microsoft.com/library/d459bc03-88ef-48d0-9f9a-82d17f0b6a4d)   
 [Visão geral da pré-compilação de projeto de aplicativo Web ASP .NET](http://msdn.microsoft.com/en-us/b940abbd-178d-4570-b441-52914fa7b887)   
 [Passo a passo: usando o MSBuild](../msbuild/walkthrough-using-msbuild.md)




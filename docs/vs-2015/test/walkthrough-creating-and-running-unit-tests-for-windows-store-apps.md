---
title: 'Passo a passo: Criar e executar testes de unidade para aplicativos da Windows Store | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests
- unit tests, Windows Store apps
- unit tests, running
ms.assetid: dd3e8a6a-b366-433e-a409-b9a9b89da89a
caps.latest.revision: 23
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f5e62fe83d644b577d7d0a5f87312642f438c490
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851180"
---
# <a name="walkthrough-creating-and-running-unit-tests-for-windows-store-apps"></a>Explicação passo a passo: Criando e executando testes de unidade de aplicativos da Windows Store
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visual Studio inclui suporte para aplicativos do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] gerenciados por testes de unidade e inclui modelos de biblioteca de teste de unidade para o Visual C#, Visual Basic e Visual C++.

> [!TIP]
> Para saber mais sobre como desenvolver aplicativos do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)], consulte [Introdução aos aplicativos da Windows Store](https://msdn.microsoft.com/windows/apps/br211386.aspx).

 O Visual Studio fornece a seguinte funcionalidade de teste de unidade:

- [Criar projetos de teste de unidade](#CreateAndRunUnitTestWin8Tailored_Create)

- [Editar o manifesto para o projeto de teste de unidade](#CreateAndRunUnitTestWin8Tailored_Manifest)

- [Codificar o teste de unidade](#CreateAndRunUnitTestWin8Tailored_Code)

- [Executar testes de unidade](#CreateAndRunUnitTestWin8Tailored_Run)

  Os procedimentos a seguir descrevem as etapas para criar, executar e depurar testes de unidade para aplicativos do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] Windows 8 gerenciado .

## <a name="prerequisites"></a>{1&gt;{2&gt;Pré-requisitos&lt;2}&lt;1}
 {1&gt;Visual Studio&lt;1}

## <a name="CreateAndRunUnitTestWin8Tailored_Create"></a> Criar projetos de teste de unidade

#### <a name="to-create-a-unit-test-project-for-a-windows-store-app"></a>Para criar um projeto de teste de unidade para um aplicativo da Windows Store

1. No menu **Arquivo**, escolha **Novo**.

     A caixa de diálogo Novo Projeto é exibida.

2. Em Modelos, escolha a linguagem de programação com a qual você quer criar o teste de unidade e escolha a biblioteca de teste de unidade do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] associada. Por exemplo, escolha **Visual C#** , depois escolha **Windows Store** e escolha **Biblioteca de Teste de Unidade (aplicativos da Windows Store)** .

    > [!NOTE]
    > O Visual Studio inclui modelos de biblioteca de teste de unidade para Visual C#, Visual Basic e Visual C++.

3. (Opcional) Na caixa de texto **Nome**, digite o nome que você quer usar para o projeto de teste de unidade do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)].

4. (Opcional) Modifique o caminho onde você deseja criar o projeto inserindo-o na caixa de texto **Local**, ou escolhendo o botão **Procurar**.

5. (Opcional) Na caixa de texto **Nome da solução**, insira o nome que você deseja usar para sua solução.

6. Deixe a opção **Criar diretório para solução** selecionada e escolha o botão **OK**.

     ![Biblioteca de teste de unidade personalizada](../test/media/unit-test-win8-1.png "Unit_Test_Win8_1")

     O Gerenciador de soluções é preenchido com seu novo projeto de teste de unidade do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] e o editor de códigos exibe o teste de unidade padrão intitulado UnitTest1.

     ![Novo projeto de teste de unidade personalizado](../test/media/unit-test-win8-unittestexplorer-newprojectcreated.png "Unit_Test_Win8_UnitTestExplorer_NewProjectCreated")

## <a name="CreateAndRunUnitTestWin8Tailored_Manifest"></a> Editar o manifesto para o projeto de teste de unidade
 Talvez seja necessário editar o manifesto do projeto de teste de unidade a fim de fornecer os recursos necessários para executar o aplicativo.

#### <a name="to-edit-the-unit-test-projects-windows-store-application-manifest-file"></a>Para editar o arquivo manifesto do aplicativo da Windows Store do projeto de teste de unidade

1. No Gerenciador de Soluções, no novo projeto de teste de unidade do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)], clique com o botão direito no arquivo de manifesto Package.appxmanifest e escolha **Abrir**.

     O Designer de Manifesto é exibido para edição.

2. No Designer de Manifesto, escolha a guia **Funcionalidades**.

3. Na lista em **Funcionalidades**, selecione as funcionalidades que seu teste de unidade e o código testado precisam. Por exemplo, marque a caixa de seleção **Internet** se o teste de unidade precisar e se o código testado precisar ter a capacidade de acessar a internet.

    > [!NOTE]
    > As funcionalidades selecionadas devem incluir somente o necessário para o funcionamento correto do teste de unidade do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]. As funcionalidades nunca deverão incluir funcionalidades que não fazem parte do aplicativo do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] que está sendo testado, e normalmente deve ser um subconjunto das funcionalidades especificadas para o aplicativo do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]em teste.

     Para saber mais sobre o Designer de Manifesto, consulte [Configurar um pacote do aplicativo do Windows 8.1 usando o designer de manifesto](https://msdn.microsoft.com/library/24c58b7f-9c6d-41c3-b385-c1e8497d5b2d).

     ![Manifesto de teste de unidade](../test/media/unit-test-win8.png "Unit_Test_Win8_")

## <a name="CreateAndRunUnitTestWin8Tailored_Code"></a> Codificar o Teste de Unidade

#### <a name="to-code-the-unit-test-for-a-windows-store-app"></a>Para codificar o teste de unidade para um aplicativo da Windows Store

1. No Editor de Código, edite o teste de unidade e adicione as declarações e a lógica necessárias para o teste.

     Para saber mais, consulte [Usar as classes Assert](https://msdn.microsoft.com/library/ms182530.aspx) na biblioteca da MSDN.

## <a name="CreateAndRunUnitTestWin8Tailored_Run"></a> Executar testes de unidade

#### <a name="to-build-the-solution-and-run-the-unit-test-using-test-explorer"></a>Para compilar a solução e executar o teste de unidade usando o Gerenciador de Testes

1. No menu **Teste**, escolha **Windows** e **Gerenciador de Testes**.

     O Gerenciador de Testes aparecerá sem o seu teste listado.

2. No menu **Compilação**, escolha **Compilar Solução**.

     Agora seu teste de unidade está listado.

    > [!NOTE]
    > Você deve compilar a solução para atualizar a lista de testes de unidade no Gerenciador de Testes.

    > [!WARNING]
    > Problema conhecido do Visual Studio: você deve abrir o Gerenciador de Testes antes de compilar o projeto de teste.

3. No Gerenciador de Testes, escolha o teste de unidade que você criou.

    > [!TIP]
    > O Gerenciador de Testes fornece um link para o código-fonte ao lado de **Fonte:** .

4. Escolha **Executar Todos**.

     ![Teste de unidade &#45; de execução do Gerenciador de testes de unidade](../test/media/unit-test-win8-unittestexplorer-contextmenurun.png "Unit_Test_Win8_UnitTestExplorer_ContextMenuRun")

    > [!TIP]
    > Selecione um ou mais testes de unidade listados no Gerenciador, clique com botão direito e escolha **Executar Testes Selecionados**.
    >
    >  Além disso, você pode optar por **Depurar os Testes Selecionados**, **Abrir Teste**e usar a opção **Propriedades**.
    >
    >  ![Menu de contexto &#45; de teste uni do Gerenciador de teste de unidade](../test/media/unit-test-win8-unittestexplorer-contextmenu.png "Unit_Test_Win8_UnitTestExplorer_ContextMenu")

     O teste de unidade é executado. Após a conclusão, o Gerenciador de Testes exibirá o status do teste, o tempo decorrido e fornecerá um link para a fonte.

     ![Teste do Gerenciador &#45; de testes de unidade concluído](../test/media/unit-test-win8-unittestexplorer-done.png "Unit_Test_Win8_UnitTestExplorer_Done")

## <a name="external-resources"></a>Recursos Externos

### <a name="videos"></a>Vídeos
 [Canal 9: teste de unidade dos aplicativos da Windows Store criados com XAML](https://channel9.msdn.com/Events/BUILD/BUILD2011/TOOL-529T)

### <a name="forums"></a>Fóruns
 [Teste de unidade do Visual Studio](https://social.msdn.microsoft.com/Forums/en/vsunittest/threads)

### <a name="msdn-library"></a>Biblioteca MSDN
 [Biblioteca MSDN – Criar e executar testes de unidade para o código existente (Visual Studio 2010)](https://msdn.microsoft.com/library/hh270865(v=vs.110).aspx)

## <a name="see-also"></a>Veja também
 [Testando aplicativos da loja com o Visual Studio](../test/testing-store-apps-with-visual-studio.md) [Compilar e testar um aplicativo da Windows Store usando o Team Foundation Build](https://msdn.microsoft.com/library/d0ca17bb-deae-4f3d-a18d-1a99bebceaa9)

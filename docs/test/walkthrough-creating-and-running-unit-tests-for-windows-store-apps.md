---
title: Criando e executando testes de unidade para aplicativos da UWP no Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests
- unit tests, UWP apps
- unit tests, running
ms.author: gewarren
manager: douge
ms.workload:
- uwp
author: gewarren
ms.openlocfilehash: d4640616b12a07c475503d45f9297c1bbf663f91
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44284114"
---
# <a name="walkthrough-create-and-run-unit-tests-for-uwp-apps"></a>Passo a passo: criar e executar testes de unidade para aplicativos UWP

O Visual Studio dá suporte para realizar testes de unidade em aplicativos da UWP (Plataforma Universal do Windows). Ele inclui modelos do projeto de teste de unidade para Visual C#, Visual Basic e Visual C++.

> [!TIP]
> Para obter mais informações sobre como desenvolver aplicativos da UWP, consulte [Introdução aos aplicativos UWP](/windows/uwp/get-started/).

Os procedimentos a seguir descrevem as etapas para criar, executar e depurar testes de unidade para um aplicativo da UWP.

## <a name="create-a-unit-test-project-for-a-uwp-app"></a>Criar um projeto de teste de unidade para um aplicativo da UWP

1.  No menu **Arquivo**, escolha **Novo**.

     A caixa de diálogo **Novo Projeto** é exibida.

2.  Em Modelos, escolha a linguagem de programação com a qual você quer criar os testes de unidade e escolha a biblioteca de testes de unidade associada da Plataforma Universal do Windows. Por exemplo, escolha **Visual C#**, depois escolha **Windows Universal** e, em seguida, escolha **Biblioteca de Teste de Unidade (Universal Windows)**.

3.  (Opcional) Na caixa de texto **Nome**, digite o nome que você quer usar para o projeto.

4.  (Opcional) Modifique o caminho em que você deseja criar o projeto inserindo-o na caixa de texto **Local** ou escolhendo o botão **Procurar**.

5.  (Opcional) Na caixa de texto **Nome da solução**, insira o nome que você deseja usar para sua solução.

6.  Deixe a opção **Criar diretório para solução** selecionada e escolha o botão **OK**.

     ![Biblioteca de teste de unidade adaptada](../test/media/unit_test_win8_1.png)

     O **Gerenciador de Soluções** é populado com o projeto de teste de unidade UWP e o editor de código exibe o teste de unidade padrão intitulado UnitTest1.

     ![Novo projeto de teste de unidade adaptado](../test/media/unit_test_win8_unittestexplorer_newprojectcreated.png)

## <a name="edit-the-unit-test-projects-uwp-application-manifest-file"></a>Editar o arquivo de manifesto do aplicativo da UWP do projeto de teste de unidade

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo *Package.appxmanifest* e escolha **Abrir**.

     O **Designer de Manifesto** é exibido para edição.

2.  No **Designer de Manifesto**, escolha a guia **Funcionalidades**.

3.  Na lista em **Funcionalidades**, selecione as funcionalidades que seu teste de unidade e o código testado precisam. Por exemplo, marque a caixa de seleção **Internet** se o teste de unidade precisar e se o código testado precisar ter a capacidade de acessar a internet.

    > [!NOTE]
    > As funcionalidades selecionadas devem incluir somente o necessário para o funcionamento correto do teste de unidade.

     ![Manifesto do teste de unidade](../test/media/unit_test_win8_.png)

## <a name="code-the-unit-test-for-a-uwp-app"></a>Codificar o teste de unidade para um aplicativo UWP

No **Editor de Códigos**, edite o teste de unidade e adicione as declarações e a lógica necessárias ao teste.

## <a name="run-unit-tests"></a>Executar testes de unidade

### <a name="to-build-the-solution-and-run-the-unit-test-using-test-explorer"></a>Para compilar a solução e executar o teste de unidade usando o Gerenciador de Testes

1.  No menu **Teste**, escolha **Windows** e **Gerenciador de Testes**.

     O **Gerenciador de Testes** é exibido sem o teste listado.

2.  No menu **Compilação**, escolha **Compilar Solução**.

     Agora seu teste de unidade está listado.

    > [!NOTE]
    > Você deve compilar a solução para atualizar a lista de testes de unidade no Gerenciador de Testes.

3.  No **Gerenciador de Testes**, escolha o teste de unidade criado.

    > [!TIP]
    > O Gerenciador de Testes fornece um link para o código-fonte ao lado de **Fonte:**.

4.  Escolha **Executar Todos**.

     ![Gerenciador de Testes de Unidade &#45; executar teste de unidade](../test/media/unit_test_win8_unittestexplorer_contextmenurun.png)

    > [!TIP]
    > Selecione um ou mais testes de unidade listados no Gerenciador, clique com botão direito e escolha **Executar Testes Selecionados**.
    >
    > Além disso, você pode optar por **Depurar os Testes Selecionados**, **Abrir Teste**e usar a opção **Propriedades**.
    >
    > ![Gerenciador de Testes de Unidade &#8211; menu de contexto de teste de unidade](../test/media/unit_test_win8_unittestexplorer_contextmenu.png)

    O teste de unidade é executado. Após a conclusão, o **Gerenciador de Testes** exibirá o status do teste, o tempo decorrido e fornecerá um link para a fonte.

    ![Gerenciador de Testes de Unidade &#45; teste concluído](../test/media/unit_test_win8_unittestexplorer_done.png)

## <a name="see-also"></a>Consulte também

- [Testar aplicativos UWP com o Visual Studio](../test/testing-store-apps-with-visual-studio.md)
- [Compilar e testar um aplicativo da UWP](/azure/devops/pipelines/apps/windows/universal?tabs=vsts)

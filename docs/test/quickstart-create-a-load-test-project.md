---
title: Criar um projeto de teste de desempenho Web e teste de carga no Visual Studio
ms.date: 03/14/2018
ms.topic: quickstart
helpviewer_keywords:
- load testing, quickstart
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: f2e0f06eddee4acd500e6bf4a8094dde4efc0d14
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896283"
---
# <a name="quickstart-create-a-load-test-project"></a>Início rápido: criar um projeto de teste de carga

Neste guia de início rápido de 10 minutos, você aprenderá a criar e executar um projeto de teste de carga e de desempenho Web no Visual Studio. Testes de carga executam testes de desempenho Web ou testes de unidade para simular muitos usuários acessando um servidor ao mesmo tempo.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="software-requirements"></a>Requisitos de software

Projetos de teste de carga e de desempenho Web só estão disponíveis na edição Enterprise do Visual Studio.

## <a name="install-the-load-testing-component"></a>Instalar a componente de teste de carga

Se ainda não tiver o componente de ferramentas de teste de carga e de desempenho Web instalado, você precisará instalá-lo usando o Instalador do Visual Studio.

1. Abra o **Instalador do Visual Studio** no menu **Iniciar** do Windows. Você também pode acessá-lo no Visual Studio na caixa de diálogo **Novo Projeto** ou escolhendo **Ferramentas** > **Obter Ferramentas e Recursos** na barra de menus.

1. No **Instalador do Visual Studio**, escolha a guia **Componentes individuais** e role para baixo até a seção **Depuração e testes**. Selecione **Ferramentas de teste de carga e desempenho Web**.

   ![Componente de ferramentas de teste de carga e desempenho Web](media/web-perf-load-testing-tools-component.png)

1. Escolha o botão **Modificar**.

   O componente das ferramentas de teste de carga e desempenho na Web está instalado.

## <a name="create-a-load-test-project"></a>Criar um projeto de teste de carga

Nesta seção, criaremos um projeto de teste de carga em C#. Você também pode criar um projeto de teste de carga do Visual Basic se preferir.

1. Abra o Visual Studio e escolha **Arquivo** > **Novo** > **Projeto** na barra de menus.

   A caixa de diálogo **Novo Projeto** é aberta.

1. Na caixa de diálogo **Novo Projeto**, expanda **Instalado**, expanda **Visual C#** e selecione a categoria **Testar**. Escolha o modelo **Projeto de teste de carga e desempenho na Web**.

   ![Modelo de projeto de teste de carga e desempenho Web](media/web-perf-load-test-project-template.png)

1. Insira um nome para o projeto se não quiser usar o nome padrão e, em seguida, escolha **OK**.

   O Visual Studio cria o projeto e o exibe os arquivos no **Gerenciador de Soluções**. Inicialmente, o projeto contém um arquivo de teste da Web chamado *WebTest1.webtest*.

## <a name="add-a-load-test-to-the-project"></a>Adicionar um teste de carga ao projeto

1. No menu de clique com o botão direito do mouse ou no menu de contexto do nó do projeto no **Gerenciador de Soluções**, escolha **Adicionar** > **Teste de Carga**.

   O **Novo assistente de teste de carga** é aberto.

1. Selecione a opção **Teste de Carga no Local** e, em seguida, escolha **Avançar**. Você pode saber mais sobre o teste de carga baseado em nuvem [aqui](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts).

   ![Novo assistente de teste de carga – primeira página](media/load-test-wizard-page-1.png)

1. Escolha **Avançar** para percorrer o assistente até chegar à página **Adicionar testes a um cenário de teste de carga e editar a combinação de testes**. Escolha o botão **Adicionar**.

   A caixa de diálogo **Adicionar testes** é aberta.

1. Em **Testes disponíveis**, selecione **WebTest1** e clique na seta à direita para movê-lo para a caixa **Testes selecionados**. Escolha o botão **OK**.

   ![Caixa de diálogo Adicionar testes](media/add-tests-dialog-box.png)

1. Volte ao **Novo Assistente de Teste de Carga**, escolha o botão **Concluir**.

   O teste de carga é adicionado ao projeto e o arquivo de teste de carga é aberto na janela do editor.

## <a name="run-the-load-test"></a>Executar o teste de carga

Criamos um teste de carga que não faz muita coisa, mas vamos executá-lo mesmo assim.

No menu que aparece após você clicar com o botão direito do mouse ou no menu de contexto do teste de carga aberto no editor, escolha **Executar Teste de Carga**.

![Menu Executar Teste de Carga](media/run-load-test.png)

O teste de carga começará a ser executado. A janela **Resultados do Teste** mostra que o teste está em andamento e o analisador de teste de carga será exibido na janela do editor. Após a conclusão do teste, que deve levar cinco minutos se você aceitar os padrões, um resumo será mostrado no editor. Você pode escolher **Gráficos**, **Tabelas** ou **Detalhes** para obter diferentes informações sobre os resultados do teste de carga.

![Janela do analisador de teste de carga](media/load-test-analyzer.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você criou um projeto de teste de carga simples, a próxima etapa é configurar cenários, conjuntos de contadores e configurações de execução.

> [!div class="nextstepaction"]
> [Editar configurações de teste](edit-load-tests.md)

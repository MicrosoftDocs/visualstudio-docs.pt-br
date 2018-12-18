---
title: Tutorial sobre como trabalhar com o Python, etapa 6, trabalhar com o Git
description: Etapa 6 de um passo a passo básico do Python no Visual Studio, abordando os recursos relacionados ao Git do Visual Studio.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: e958046bb5574cb1a9b9799482fa3c96c203b013
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219400"
---
# <a name="step-6-work-with-git"></a>Etapa 6: Trabalhar com o Git

**Etapa anterior: [instalar pacotes e gerenciar o ambiente do Python](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)**

O Visual Studio fornece integração direta com repositórios locais do GIT e repositórios remotos em serviços como o GitHub e o Azure Repos. A integração inclui clonagem de um repositório, confirmação de alterações e gerenciamento de branches.

Este artigo fornece uma visão geral básica da criação de um repositório Git local para um projeto existente e visa familiarizar você com alguns dos recursos do Visual Studio relacionados ao Git.

1. Com um projeto aberto no Visual Studio, como o projeto da [etapa anterior](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md), clique com o botão direito do mouse na solução e selecione **Adicionar Solução ao Controle do Código-Fonte**. O Visual Studio cria um repositório local do Git que contém o código do projeto.

1. Quando o Visual Studio detecta que o projeto é gerenciado em um repositório do Git, controles relacionados com o Git também aparecem na parte inferior direita da janela do Visual Studio. Os controles mostram confirmações pendentes, alterações, o nome do repositório e o branch. Passe o mouse sobre os controles para ver informações adicionais.

    ![Informações adicionais são exibidas ao passar o mouse sobre um controle de Git na janela do Visual Studio](media/working-with-git-01.png)

1. Quando você cria um novo repositório ou seleciona qualquer um dos controles do Git, o Visual Studio abre a janela **Team Explorer**. (É possível abrir a janela a qualquer momento com o comando de menu **Exibir** > **Team Explorer**.) A janela possui três painéis principais, entre os quais é possível alternar usando o menu suspenso no cabeçalho **Team Explorer**. O painel **Sincronizar**, que fornece operações de publicação, também será exibido quando você escolher o controle **Push** (o ícone de seta para cima):

    ![Team Explorer no Visual Studio depois de criar um repositório local](media/working-with-git-02.png)

1. Selecione **Alterações** (ou o controle do Git como ícone de lápis) para examinar as alterações não confirmadas e confirmá-las quando desejado.

    ![Team Explorer no Visual Studio mostrando as alterações não confirmadas](media/working-with-git-03.png)

    Clique duas vezes em um arquivo na lista **Alterações** para abrir um modo de exibição de comparação do arquivo:

    ![Modo de exibição de comparação para alterações em um arquivo](media/working-with-git-05.png)

1. Selecione **Branches** (ou o controle do Git com um nome de branch) para examinar os branches e executar operações de mesclagem e troca de base:

    ![Team Explorer no Visual Studio mostrando branches](media/working-with-git-04.png)

1. Com a seleção do controle do Git com o nome do repositório (**CosineWave** em uma imagem anterior), o **Team Explorer** mostra uma interface **Conectar** com a qual é possível alternar totalmente para outro repositório com rapidez.

1. Ao usar um repositório local, as alterações confirmadas vão diretamente para o repositório. Se você estiver conectado a um repositório remoto, escolha o cabeçalho no **Team Explorer**, escolha **Sincronizar** para mudar para a seção **Sincronização** e trabalhar com os comandos **Pull** e **Fetch** que são apresentados.

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

Para ver breves instruções sobre a criação de um projeto de um repositório remoto do Git, confira [Início Rápido: clonar um repositório de código do Python no Visual Studio](quickstart-03-python-in-visual-studio-project-from-repository.md).

Para obter um tutorial muito mais abrangente, incluindo informações sobre como lidar com conflitos de mesclagem, revisar código com solicitações de pull, trocar a base e fazer cherry-picking de alterações entre branches, confira [Introdução ao GIT e ao Azure Repos](/azure/devops/repos/git/gitquickstart?toc=/visualstudio/version-control/toc.json&bc=/azure/devops/repos/git/breadcrumb/vc/toc.json&view=vsts&tabs=visual-studio).

## <a name="tutorial-review"></a>Análise do tutorial

Parabéns por concluir este tutorial sobre Python no Visual Studio. Neste tutorial, você aprendeu como:

- Criar projetos e exibir o conteúdo do projeto.
- Use o editor de código e executar um projeto.
- Use a janela **Interativa** para desenvolver um novo código e copiar facilmente esse código para o editor.
- Executar um programa concluído no depurador do Visual Studio.
- Instalar pacotes e gerenciar ambientes do Python.
- Trabalhar com o código em um repositório do Git.

Agora, explore os Conceitos e guias de Instruções, incluindo os seguintes artigos:

- [Criar uma extensão do C++ para o Python](working-with-c-cpp-python-in-visual-studio.md)
- [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [Criação de perfil](profiling-python-code-in-visual-studio.md)
- [Teste de unidade](unit-testing-python-in-visual-studio.md)

---
title: Tutorial sobre como trabalhar com o Python, etapa 1, criar um projeto
description: Visão geral e Etapa 1 de um passo a passo básico das funcionalidades do Python no Visual Studio, incluindo pré-requisitos e a criação de um novo projeto do Python.
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
ms.openlocfilehash: 2eb9871aeda7134f6d488b7efe55c5ec149677a5
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220076"
---
# <a name="tutorial-work-with-python-in-visual-studio"></a>Tutorial: Trabalhar com Python no Visual Studio

O Python é uma linguagem de programação popular confiável, flexível, fácil de aprender, de uso gratuito em todos os sistemas operacionais e com suporte em uma sólida comunidade de desenvolvedores e várias bibliotecas gratuitas. A linguagem é compatível com todas as formas de desenvolvimento, incluindo aplicativos Web, serviços Web, aplicativos de área de trabalho, scripts e computação científica e, da mesma forma, é usada por diversas universidades, vários cientistas e desenvolvedores casuais e profissionais.

O Visual Studio fornece suporte de linguagem de primeira classe para o Python. Este tutorial orienta você nas seguintes etapas:

- [Etapa 0: instalação](tutorial-working-with-python-in-visual-studio-step-00-installation.md)
- [Etapa 1: criar um projeto do Python (este artigo)](#step-1-create-a-new-python-project)
- [Etapa 2: escrever e executar código para ver o IntelliSense do Visual Studio funcionando](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)
- [Etapa 3: criar mais código na janela REPL interativa](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)
- [Etapa 4: executar o programa concluído no depurador do Visual Studio](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)
- [Etapa 5: instalar pacotes e gerenciar ambientes do Python](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)
- [Etapa 6: trabalhar com o Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

[!INCLUDE[tutorial-prereqs](includes/tutorial-prereqs.md)]

## <a name="step-1-create-a-new-python-project"></a>Etapa 1: criar um novo projeto do Python

Um *projeto* é a forma como o Visual Studio gerencia todos os arquivos que são reunidos para produzir um único aplicativo, incluindo código-fonte, recursos, configurações e assim por diante. Um projeto formaliza e mantém a relação entre todos os arquivos do projeto, bem como os recursos externos que são compartilhados entre vários projetos. Sendo assim, os projetos permitem que seu aplicativo expanda facilmente e cresça de maneira muito mais fácil do que simplesmente gerenciar relacionamentos de um projeto em pastas ad-hoc, scripts, arquivos de texto e até mesmo em sua própria mente.

Neste tutorial você começará com um projeto simples, contendo um único arquivo de código vazio.

1. No Visual Studio, selecione **Arquivo** > **Novo** > **Projeto** (**Ctrl**+**Shift**+**N**), que abrirá a caixa de diálogo **Novo Projeto**. Aqui você pode procurar modelos em diversas linguagens, selecionar um para o seu projeto e especificar o local em que o Visual Studio colocará os arquivos.

1. Para exibir modelos do Python, selecione **Instalado** > **Python** à esquerda ou pesquise por "Python". O uso da pesquisa é uma ótima maneira de localizar um modelo quando você não se lembra da localização na árvore de linguagens.

    ![Nova caixa de diálogo mostrando os projetos do Python](media/vs-getting-started-python-01-new-project.png)

    Observe como o suporte do Python no Visual Studio inclui uma variedade de modelos de projeto, incluindo aplicativos Web usando as estruturas Bottle, Flask e Django. No entanto, para as finalidades deste passo a passo, vamos começar com um projeto vazio.

1. Selecione o modelo **Aplicativo Python**, especifique um nome para o projeto e selecione **OK**.

1. Após alguns instantes, o Visual Studio mostrará a estrutura do projeto na janela **Gerenciador de Soluções** (1). O arquivo de código padrão será aberto no editor (2). A janela **Propriedades** (3) também será exibida para mostrar informações adicionais sobre qualquer item selecionado no **Gerenciador de Soluções**, incluindo sua localização exata no disco.

    ![Gerenciador de Soluções com um projeto do Python](media/vs-getting-started-python-02-windows.png)

1. Gaste alguns minutos para se familiarizar com o **Gerenciador de Soluções**, que é o local em que você poderá procurar arquivos e pastas em seu projeto.

    ![Gerenciador de Soluções expandido para mostrar vários recursos](media/vs-getting-started-python-03-solution-explorer.png)

    (1) O seu projeto está realçado em negrito, usando o nome que você forneceu na caixa de diálogo **Novo Projeto**. No disco, esse projeto é representado por um arquivo *.pyproj* na pasta do projeto.

    (2) No nível superior está uma *solução* que, por padrão, tem o mesmo nome que o seu projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados. Por exemplo, se você escreve uma extensão de C++ para o seu aplicativo Python, o projeto de C++ poderá residir na mesma solução. A solução também pode conter um projeto para um serviço Web, juntamente com projetos para programas de teste dedicados. 

    (3) No seu projeto, você vê os arquivos de origem, neste caso, um único arquivo *.py*. Quando se seleciona um arquivo, as respectivas propriedades são exibidas na janela **Propriedades**. Ao clicar duas vezes em um arquivo, ele será aberto da forma que for apropriada para esse arquivo.

    (4) Também no projeto está o nó **Ambientes do Python**. Quando expandido, você verá os interpretadores de Python que estão disponíveis. Expanda um nó de interpretador para ver as bibliotecas que estão instaladas naquele ambiente (5).

    Clique com o botão direito do mouse em qualquer nó ou item no **Gerenciador de Soluções** para acessar um menu de comandos aplicáveis. Por exemplo, o comando **Renomear** permite que você altere o nome de qualquer nó ou item, incluindo o projeto e a solução.

## <a name="next-step"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Escrever e executar código](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Projetos do Python no Visual Studio](managing-python-projects-in-visual-studio.md).
- [Saiba mais sobre a linguagem Python em python.org](https://www.python.org)
- [Python para iniciantes](https://www.python.org/about/gettingstarted/) (python.org)
- [Cursos gratuitos do Python na Microsoft Virtual Academy](https://mva.microsoft.com/search/SearchResults.aspx#!q=python)
- [Top Python Questions (Principais perguntas sobre Python) na Microsoft Virtual Academy](https://aka.ms/mva-top-python-questions)

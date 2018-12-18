---
title: Compilando e criando
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- builds [Visual Studio], about building in Visual Studio
- custom build steps, types of builds
ms.assetid: c7958821-285f-4e28-9e7a-b5d8b40336a1
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ae06d11e1bdd193ebda5223c7c638c3132984147
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53052644"
---
# <a name="compiling-and-building-in-visual-studio"></a>Compilando e criando no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível usar o Visual Studio para compilar aplicativos e criar assemblies e programas executáveis em intervalos frequentes durante um ciclo de desenvolvimento. Compilando seu código com frequência, é possível identificar erros em tempo de build, como sintaxe incorreta, palavras-chave com erros de ortografia e erros de digitação mais precocemente. Também é possível detectar e corrigir erros em tempo de execução, como erros lógicos e semânticos ao compilar e executar frequentemente versões de depuração do código.

 Quando você tiver desenvolvido completamente e depurado suficientemente um projeto ou solução, será possível compilar seus componentes em um build de versão. Por padrão, um build de versão é otimizada e projetada para ser menor e para ser executada mais rapidamente do que uma versão de depuração. Para obter mais informações, consulte [passo a passo: Criando um aplicativo](../ide/walkthrough-building-an-application.md).

## <a name="choosing-a-build-method"></a>Escolhendo um método de build
 É possível criar um aplicativo usando as opções de build padrão no IDE, em um prompt de comando, ou usando o Build do Team Foundation. Cada uma dessas opções usam o MSBuild como a tecnologia subjacente e cada abordagem tem benefícios específicos, como mostra a tabela a seguir.

|Método de build|Benefícios|Para obter mais informações|
|------------------|--------------|--------------------------|
|Como usar o IDE|– É possível criar e executar compilações de maneira mais fácil imediatamente.<br />– É possível executar compilações em multiprocessador para projetos C++ e C#.<br />– É possível personalizar alguns aspectos do sistema de build.|[Compilando e limpando projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)|
|Executando uma linha de comando do MSBuild|– É possível criar projetos sem instalar o Visual Studio.<br />– É possível executar compilações em multiprocessador para todos os tipos de projeto.<br />– É possível personalizar a maioria das áreas do sistema de build.|[MSBuild](../msbuild/msbuild.md)|
|Usando o Build do Team Foundation|–   É possível automatizar seu processo de build. Por exemplo, será possível criar um ou mais projetos à noite ou sempre que o check-in do código for feito. Também é possível criar projetos em servidores de build compartilhados em vez de no seu computador de desenvolvimento.<br />– É possível especificar rapidamente o código que você deseja compilar, os testes que você deseja executar e outras opções comuns.<br />– É possível modificar o fluxo de trabalho do build e, conforme necessário, criar atividades de build para realizar tarefas profundamente personalizadas.|[Compilar o aplicativo](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)|

## <a name="building-from-the-ide"></a>Compilando no IDE
 Ao criar um projeto, as configurações de build padrão são definidas para ele e uma configuração de build da solução é atribuída a ele para fornecer contexto para compilações. As configurações da solução definem a maneira como os projetos na solução são criados e implantados. As configurações do projeto são um conjunto de propriedades do projeto exclusivas para um tipo de plataforma e de build (por exemplo, versão Win32). É possível editar essas configurações padrão e é possível criar suas próprias configurações. Para obter mais informações, consulte [Introdução ao Designer de projeto](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7) e [NIB como: Modificar as propriedades do projeto e as definições de configuração](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67).

 Dentro do IDE, é possível realizar as seguintes tarefas adicionais:

-   [Alterar o diretório de saída do build](../ide/how-to-change-the-build-output-directory.md).

-   [Identificar projetos que dependem da saída de outro projeto para compilar corretamente](../ide/how-to-create-and-remove-project-dependencies.md).

-   [Alterar a quantidade de informações incluídas no log de build ou na janela de saída para builds](../ide/how-to-view-save-and-configure-build-log-files.md).

-   [Ocultar avisos específicos do compilador para Visual C#, Visual C++ ou Visual Basic](../ide/how-to-suppress-compiler-warnings.md).

-   [Especificar ações personalizadas pré e pós-compilação para um build](../ide/specifying-custom-build-events-in-visual-studio.md).

-   Melhorar o desempenho do build usando builds paralelas. Para obter mais informações, consulte [Building Multiple Projects in Parallel (Criando vários projetos paralelamente)](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md) ou a postagem do blog [Tuning C++ build parallelism (Ajustando o paralelismo de build do C++)](http://blogs.msdn.com/b/msbuild/archive/2010/03/08/tuning-c-build-parallelism-in-vs2010.aspx).

## <a name="see-also"></a>Consulte também
 [Passo a passo: Criando um aplicativo](../ide/walkthrough-building-an-application.md) [Noções básicas sobre configurações de Build](../ide/understanding-build-configurations.md) [Noções básicas sobre plataformas de Build](../ide/understanding-build-platforms.md) [criando (compilando) projetos de Site](http://msdn.microsoft.com/library/a9cbb88c-8fff-4c67-848b-98fbfd823193) [Como: criar e remover dependências de projeto](../ide/how-to-create-and-remove-project-dependencies.md)

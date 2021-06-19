---
title: Como executar um programa (C#)
description: Guia para iniciantes sobre como executar um programa em C# Visual Studio.
ms.custom: vs-acquisition, get-started
ms.date: 10/16/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e20caabb55e65801224177168f5c936f81402bbd
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385221"
---
# <a name="how-to-run-a-c-program-in-visual-studio"></a>Como executar um programa C# no Visual Studio

O que você precisa fazer para executar um programa depende do que você está começando, de qual tipo de programa, aplicativo ou serviço ele é e se você deseja executar o programa no depurador ou não. No caso mais simples, quando você tem um projeto aberto no Visual Studio, crie e execute-o pressionando **Ctrl** + **F5** ( Iniciar sem **depuração**) ou **F5** ( Iniciar com **depuração**) ou pressione a seta verde (**Botão** Iniciar ) na barra de ferramentas Visual Studio principal.

![Captura de tela mostrando o botão Iniciar](media/vs-start-button.png)

## <a name="starting-from-a-project"></a>Começando em um projeto

Se você tiver um projeto C# (*arquivo .csproj),* poderá executar, se for um programa que pode ser executado. Se um projeto contiver um arquivo C# com um método e sua saída for um executável (EXE), provavelmente ele será executado se for `Main` construído com êxito.

Se você já tiver o código do programa em um projeto Visual Studio, abra o projeto. Para abrir o projeto, clique duas vezes ou toque no *.csproj* do Windows Explorador de Arquivos ou, no Visual Studio, escolha Abrir um **projeto,** navegue até encontrar o arquivo *(.csproj)* do projeto e escolha o arquivo de projeto.

Depois que os projetos são carregados Visual Studio, pressione **Ctrl** + **F5** (  Iniciar sem **depuração)** ou use o botão verde Iniciar na barra de ferramentas Visual Studio para executar o programa.  Se houver vários projetos, aquele com o `Main` método deverá ser definido como o projeto de inicialização. Para definir o projeto de inicialização, clique com o botão direito do mouse em um nó de projeto e escolha **Definir como projeto de inicialização.**

![Definir projeto de inicialização](media/set-as-startup-project.png)

Visual Studio tenta criar e executar seu projeto.  Se houver erros de build, você verá  a saída do build na janela Saída e os erros na janela **Lista de** Erros.

Se o build for bem-sucedido, o aplicativo será executado de uma maneira apropriada para o tipo de projeto. Os aplicativos de console são executados em uma janela de terminal, os aplicativos da área de trabalho do Windows começam em uma nova janela, os aplicativos Web começam no navegador (hospedados por IIS Express) e assim por diante.

## <a name="starting-from-code"></a>Começando com o código

Se você estiver começando com uma listagem de código, arquivo de código ou um pequeno número de arquivos, primeiro certifique-se de que o código que você deseja executar seja de uma fonte confiável e seja um programa que pode ser executado. Se ele tiver um método, ele provavelmente se destina a ser um programa que pode ser executado e você pode usar o modelo aplicativo de console para criar um projeto para trabalhar com ele `Main` Visual Studio.

### <a name="code-listing-for-a-single-file"></a>Listagem de código para um único arquivo

Inicie Visual Studio, abra um projeto de console C# vazio, selecione todo o código no arquivo .cs que já está no projeto e exclua-o. Em seguida, colar o conteúdo do código no arquivo .cs. Quando você colar o código, substituir ou excluir o código que estava lá antes. Renomeie o arquivo para corresponder ao código original.

### <a name="code-listings-for-a-few-files"></a>Listagem de código para alguns arquivos

Inicie Visual Studio, abra um projeto de console C# vazio, selecione todo o código no arquivo .cs que já está no projeto e exclua-o. Em seguida, colar o conteúdo do primeiro arquivo de código no arquivo .cs. Renomeie o arquivo para corresponder ao código original. 

Para um segundo arquivo, clique com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** para abrir o menu de atalho do projeto e escolha **Adicionar > Item** Existente (ou use a combinação de teclas **Shift** Alt A ) e selecione os arquivos de +  + código.

### <a name="multiple-files-on-disk"></a>Vários arquivos em disco

1. Crie um novo projeto do tipo apropriado (use o Aplicativo **de Console** C#, se você não tiver certeza).

2. Clique com o botão direito do mouse no nó do projeto, se **Adicionar** Item Existente para selecionar os arquivos e  >   importá-los para seu projeto.  

### <a name="starting-from-a-folder"></a>Começando em uma pasta

Quando você estiver trabalhando com uma pasta de muitos arquivos, primeiro veja se há um projeto ou solução.  Se o programa tiver sido criado com Visual Studio, você deverá encontrar um arquivo de projeto ou um arquivo de solução. Procure arquivos com a extensão *.csproj* ou a extensão .sln e, no Windows Explorador de Arquivos, clique duas vezes em um deles para abri-los Visual Studio. Consulte [Iniciando em uma solução Visual Studio ou projeto .](#starting-from-a-project)

Se você não tiver um arquivo de projeto, como se o código foi desenvolvido em outro ambiente de desenvolvimento, abra a pasta de nível superior usando o método **Abrir** pasta no Visual Studio. Consulte [Desenvolver código sem projetos ou soluções](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="starting-from-a-github-or-azure-devops-repo"></a>Começando em um repositório GitHub ou Azure DevOps

Se o código que você deseja executar estiver no GitHub ou em um repositório Azure DevOps, você poderá usar o Visual Studio para abrir o projeto diretamente do repositório. Consulte [Abrir um projeto de um repo](../tutorial-open-project-from-repo.md).

## <a name="run-the-program"></a>Execute o programa

Para iniciar o programa, pressione a seta verde (**botão** Iniciar) na barra de ferramentas Visual Studio principal ou pressione **F5** ou **Ctrl** F5 para executar +  o programa. Quando você usa o **botão Iniciar,** ele é executado no depurador.  Visual Studio tenta criar o código em seu projeto e execute-o.  Se isso for bem-sucedido, ótimo! Mas, caso não, continue lendo algumas ideias sobre como fazer com que ela seja construída com êxito.

## <a name="troubleshooting"></a>Solução de problemas

Seu código pode ter erros, mas se o código estiver correto, mas depende apenas de alguns outros assemblies ou pacotes NuGet ou foi escrito para direcionar uma versão diferente do .NET, você poderá corrigi-lo facilmente.

### <a name="add-references"></a>Adicionar referências

Para ser criado corretamente, o código deve estar correto e ter as referências corretas configuradas para bibliotecas ou outras dependências. Você pode ver as linhas vermelha e  a Lista de Erros para ver se o programa tem erros, mesmo antes de compilá-lo e executar. Se você estiver vendo erros relacionados a nomes não resolvidos, provavelmente precisará adicionar uma referência ou uma diretiva using ou ambos. Se o código referenciar assemblies ou pacotes NuGet, você precisará adicionar essas referências ao projeto.

Visual Studio tenta ajudá-lo a identificar referências ausentes. Quando um nome não está resolvido, um ícone de lâmpada é exibido no editor. Se você clicar na lâmpada, poderá ver algumas sugestões sobre como corrigir o problema. As correções podem ser:

- adicionar uma diretiva using
- adicionar uma referência a um assembly ou
- instalar um pacote NuGet.

#### <a name="missing-using-directive"></a>Diretiva using ausente

Por exemplo, na tela a seguir, você pode optar por adicionar ao início do arquivo de código para resolver o nome `using System;` não `Console` resolvido:

![Captura de tela da lâmpada para adicionar uma diretiva using](media/name-does-not-exist2.png)

#### <a name="missing-assembly-reference"></a>Referência de assembly ausente

As referências do .NET podem estar na forma de assemblies ou pacotes NuGet. Normalmente, se você encontrar o código-fonte, o editor ou autor explicará de quais assemblies são necessários e de quais pacotes o código depende. Para adicionar uma referência a um projeto manualmente, clique com o botão direito do mouse no nó Referências no Gerenciador de Soluções **,** escolha Adicionar Referência **e** localize o assembly necessário. 

![Captura de tela do menu Adicionar Referência](media/add-reference.png)

Você pode encontrar assemblies e adicionar referências seguindo as instruções em Adicionar ou remover referências [usando o gerenciador de referências](../../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md).

#### <a name="missing-nuget-package"></a>Pacote NuGet ausente

Se Visual Studio detectar um pacote NuGet ausente, uma lâmpada será exibida e lhe dará a opção de instalá-lo:

![Captura de tela da lâmpada para instalar o pacote](media/lightbulb-add-package.png)

Se isso não resolver o problema e Visual Studio não conseguir localizar o pacote, tente pesquisar por ele online. Consulte [Instalar e usar um pacote NuGet no Visual Studio](/nuget/quickstart/install-and-use-a-package-in-visual-studio).

## <a name="use-the-right-version-of-net"></a>Usar a versão correta do .NET

Como diferentes versões do .NET Framework têm algum grau de compatibilidade com versões anteriores, uma estrutura mais nova pode executar o código escrito para uma estrutura mais antiga sem nenhuma modificação. Mas, às vezes, você precisa direcionar uma estrutura específica. Talvez seja necessário instalar uma versão específica do .NET Framework ou do .NET Core, se ela ainda não estiver instalada. Consulte [Modificar Visual Studio](../../install/modify-visual-studio.md).

Para alterar a estrutura de destino, consulte [Alterar a estrutura de destino](../../ide/visual-studio-multi-targeting-overview.md#select-a-target-framework-version). Para obter mais informações, consulte [Solução de .NET Framework erros de direcionamento](../../msbuild/troubleshooting-dotnet-framework-targeting-errors.md).

## <a name="next-steps"></a>Próximas etapas

Explore o ambiente Visual Studio de desenvolvimento lendo [Bem-vindo ao Visual Studio IDE.](../visual-studio-ide.md)

## <a name="see-also"></a>Confira também

[Criar seu primeiro aplicativo em C#](tutorial-console.md)

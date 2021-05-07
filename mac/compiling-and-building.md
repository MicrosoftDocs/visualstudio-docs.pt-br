---
title: Compilando e criando
description: Este artigo descreve como compilar e criar projetos e soluções no Visual Studio para Mac
ms.topic: overview
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/03/2021
ms.assetid: FB253757-DB00-4889-A6BF-E44722E25BD1
ms.openlocfilehash: a24c57907afedb4f02068a071d2c9f81eb8962bb
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108640968"
---
# <a name="compiling-and-building-in-visual-studio-for-mac"></a>Compilação e criação no Visual Studio para Mac

O Visual Studio para Mac pode ser usado para compilar aplicativos e criar assemblies durante o desenvolvimento do seu projeto. É importante compilar seu código com frequência para permitir a identificação rápida de tipos incompatíveis, erros de sintaxe, palavras escritas incorretamente e outros erros de tempo de compilação. Ao complicar depois de depurar, você também pode encontrar e corrigir erro em tempo de execução, como erros de lógica, E/S e de divisão por zero.

Um build bem-sucedido significa que o código-fonte contém a sintaxe correta e que todas as referências estáticas a bibliotecas, assemblies e outros componentes podem ser resolvidas. O processo de compilação produz um executável de aplicativo. Então esse executável pode ser testado por depuração e passar por diferentes tipos de testes automatizados e manuais para validar a qualidade do código. Depois que o aplicativo for completamente testado, você poderá compilar uma versão de lançamento a ser implantada em seus clientes.

No Mac, você pode usar qualquer um dos seguintes métodos para criar seu aplicativo: Visual Studio para Mac, ferramentas de linha de comando do MSBuild ou Azure Pipelines.

| Método de build | Benefícios |
| --- |--- | --- |
| Visual Studio para Mac |– Criar compilações imediatamente e testá-las em um depurador.<br />– Executar builds em multiprocessador para projetos C#.<br />– Personalizar diferentes aspectos do sistema de build. |
| Linha de comando do MSBuild| – Compilar projetos sem instalar o Visual Studio para Mac.<br />– Executar builds em multiprocessador para todos os tipos de projeto.<br />– Personalizar a maioria das áreas do sistema de build.|
| Azure Pipelines | – Automatizar o processo de build como parte de um pipeline de integração contínua/entrega contínua.<br />– Aplicar testes automatizados com cada compilação.<br />– Empregar recursos baseados em nuvem praticamente ilimitados para processos de build.<br />– Modificar o fluxo de trabalho de compilação e, conforme necessário, criar atividades de compilação para realizar tarefas profundamente personalizadas.|

A documentação nesta seção detalha mais o processo de compilação baseado no IDE. Para criar aplicativos a partir da linha de comando sem instalar o Visual Studio para Mac, você pode instalar a [SDK do .NET Core](https://dotnet.microsoft.com/download)mais recente. Saiba mais sobre a compilação de aplicativos por linha de comando em [MSBuild](/visualstudio/msbuild/msbuild). Saiba mais sobre a compilação de aplicativos com o Azure Pipelines em [Azure Pipelines](/azure/devops/pipelines).


> [!NOTE]
> Este tópico se aplica ao Visual Studio para Mac. Para o Visual Studio no Windows, confira [Compilar e criar no Visual Studio](/visualstudio/ide/compiling-and-building-in-visual-studio).


## <a name="building-from-the-ide"></a>Compilando no IDE

O Visual Studio para Mac permite criar e executar builds imediatamente, fornecendo ainda controle sobre a funcionalidade de build. Quando você cria um projeto, o Visual Studio para Mac define uma configuração padrão de build que aplica um contexto aos builds. Você pode editar as configurações padrão de build e também criar suas próprias configurações. Criar ou modificar essas configurações atualizará automaticamente o arquivo de projeto, que é usado pelo MSBuild para compilar o projeto.

Para obter mais informações sobre como compilar projetos e soluções no IDE, consulte o guia [Compilação e limpeza de Projetos e Soluções](building-and-cleaning-projects-and-solutions.md).

O Visual Studio para Mac também pode ser usado para fazer o seguinte:

* Alterar o caminho de saída. Isso é editado nas opções do Projeto:

    ![Alterar o caminho de saída](media/compiling-and-building-image4.png)

* Alterar o nível de detalhes da saída de build:

    ![Alterar o nível de detalhes de build](media/compiling-and-building-image5.png)

* Adicione comandos personalizados antes, durante ou depois da Compilação ou Limpeza:

    ![adicionar comandos personalizados](media/compiling-and-building-image6.png)


## <a name="see-also"></a>Confira também

- [Compilar e criar (Visual Studio no Windows)](/visualstudio/ide/compiling-and-building-in-visual-studio)

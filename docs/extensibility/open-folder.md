---
title: Visão geral da extensibilidade de pastas abertas do Visual Studio | Microsoft Docs
ms.date: 02/21/2018
ms.topic: overview
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: d213a7add358c46f7088f504d8c54352cda44a1c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905977"
---
# <a name="open-folder-extensibility"></a>Abrir extensibilidade de pasta

O recurso [abrir pasta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) permite que os usuários abram qualquer base de código no Visual Studio sem a necessidade de arquivos de projeto ou solução. Abrir pasta fornece os recursos que os usuários esperam do Visual Studio, como:

* Integração e pesquisa de Gerenciador de Soluções
* Colorização do editor
* Ir para navegação
* Localizar na pesquisa de arquivos

Quando usado com cargas de trabalho, como para desenvolvimento em .NET e C++, os usuários também recebem:

* IntelliSense avançado
* Funcionalidade específica a um idioma

Com a pasta aberta, os autores de extensão podem criar recursos avançados para qualquer linguagem. Há APIs para dar suporte à criação, depuração e pesquisa de símbolo para qualquer arquivo na base de código de um usuário. Os extensores atuais podem atualizar seus recursos existentes do Visual Studio para entender o código sem o backup de projetos ou uma solução.

## <a name="an-api-without-project-systems"></a>Uma API sem sistemas de projeto

Historicamente, o Visual Studio entendeu apenas os arquivos em uma solução e seus projetos usando sistemas de projetos. Um sistema de projeto é responsável pela funcionalidade e pelas interações de usuário de um projeto carregado. Ele compreende os arquivos que seu projeto contém, a representação visual do conteúdo do projeto, as dependências de outros projetos e a modificação do arquivo de projeto subjacente. É por meio dessas hierarquias e recursos que outros componentes funcionam em nome do usuário. Nem todas as bases de código são bem representadas em uma estrutura de projeto e solução. As linguagens de script e o código-fonte aberto escritos em C++ para Linux são bons exemplos. Com o Open Folder, o Visual Studio oferece aos usuários uma nova maneira de interagir com seu código-fonte.

As APIs de pasta aberta estão sob o `Microsoft.VisualStudio.Workspace.*` namespace e estão disponíveis para extensores produzirem e consumirem dados ou ações em torno de arquivos na pasta aberta. As extensões podem usar essas APIs para fornecer funcionalidade para muitas áreas, incluindo:

- [Espaços de trabalho](workspaces.md) -o ponto inicial da extensibilidade de pasta aberta é o espaço de trabalho e suas APIs.
- [Contextos e ações de arquivo](workspace-file-contexts.md) – inteligência de código específica de arquivo fornecida por meio de contextos de arquivo.
- [Indexação](workspace-indexing.md) – coletar e persistir dados sobre espaços de trabalho de pastas abertas.
- [Serviços de linguagem](workspace-language-services.md) – integre serviços de idiomas em espaços de trabalho de pasta aberta.
- [Compilação](workspace-build.md) -suporte de compilação para espaços de trabalho de pasta aberta.

Os recursos que usam os seguintes tipos precisarão adotar novas APIs para dar suporte à pasta aberta:

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>Comentários, comentários, problemas

Abra a pasta e as `Microsoft.VisualStudio.Workspace.*` APIs estão em desenvolvimento ativo. Se você vir um comportamento inesperado, consulte os problemas conhecidos para o lançamento de interesse. A [comunidade de desenvolvedores](https://developercommunity.visualstudio.com) é o lugar recomendado para votar e criar problemas. Para cada comentário, é altamente recomendável uma descrição detalhada do seu problema. Inclua a versão do Visual Studio para a qual você está desenvolvendo, as APIs que você está usando (tanto o que você implementou e o que está interagindo), o resultado esperado e o resultado real. Se possível, inclua um despejo do processo de devenv.exe. Use o rastreamento de problemas do GitHub para fornecer comentários sobre este e sobre a documentação relacionada.

## <a name="next-steps"></a>Próximas etapas

* [Espaços de trabalho](workspaces.md) -saiba mais sobre a API de espaço de trabalho de pasta aberta.
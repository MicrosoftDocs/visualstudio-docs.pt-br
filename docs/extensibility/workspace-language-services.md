---
title: Espaços de trabalho e serviços de linguagem no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 8631ffea-83c8-4fd4-a01e-c59772e89c84
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: be9fb8c1e3ae363898e0438bdd1ec34c9fd23727
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51735460"
---
# <a name="workspaces-and-language-services"></a>Espaços de trabalho e serviços de linguagem

Serviços de linguagem podem fornecer [Abrir pasta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) os mesmos recursos de linguagem avançada de usuários que eles são usados para ao trabalhar com soluções e projetos. Um serviço de linguagem pode ser ativados automaticamente com base na extensão de arquivo ou conteúdo de um documento aberto, embora este serviço de linguagem de "arquivo flexível" é limitado ao realce de sintaxe. Informações adicionais são necessárias para fornecer uma experiência mais rica ao editar/revisar o código-fonte. Cada serviço de linguagem tem sua própria API para inicialização com esses dados contextuais extra para um documento. Normalmente, isso é gerenciado por um sistema de projeto, que é rigidamente ligado tanto para o serviço de linguagem para o sistema de compilação.

## <a name="initialization"></a>Inicialização

Em um [espaço de trabalho](workspaces.md), serviços de linguagem são inicializados por um <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> ponto de extensão que é especializada somente no serviço de linguagem e não souber nada sobre a criação de compilação. Dessa forma, um proprietário de serviço de linguagem pode manter uma única pasta aberta extensão independentemente de quantos padrões existir dentro de pastas e arquivos para a execução de seu compilador durante a compilação (por exemplo MSBuild, makefiles, etc.). Quando os arquivos da qual um contexto de arquivo foi criado são alterados no disco e o contexto do arquivo é atualizado, o provedor de serviço de linguagem de programação é notificado do conjunto atualizado de contextos de arquivo. O provedor de serviço de linguagem de programação, em seguida, pode atualizar seu modelo.

Quando um documento é aberto no editor, o Visual Studio só considera linguagem provedores de serviços que exigem tipos de contexto do arquivo para o qual um provedor de contexto do arquivo correspondente pode ser encontrado. Em seguida, passa os contextos de arquivo dos provedores de correspondência para o provedor de serviços de idioma selecionado por meio de `ILanguageServiceProvider.InitializeAsync`. O que o provedor de serviço de linguagem faz com que os dados de contexto do arquivo são um detalhe de implementação do provedor de serviços de linguagem, mas a experiência do usuário esperado é um serviço de linguagem mais avançado para que abriu o documento.

## <a name="using-ilanguageserviceprovider"></a>Usando ILanguageServiceProvider

O serviço de linguagem será notificado quando um contexto de arquivo é criado com um `ContextType` que corresponde a um do `SupportedContextTypes` valores do servidor de linguagem de exportar o atributo.

Para dar suporte a um serviço de linguagem, uma extensão será necessário:

- Um único `Guid`. Isso será usado para `SupportedContextTypes` argumentos de atributo e, em um `FileContext` objeto.
- Contexto do arquivo de linguagem
  - Fábrica de provedor
    - `ExportFileContextProviderAttribute` atributo acima exclusivamente gerado `Guid` em `SupportedContextTypes`
    - Implementa `IWorkspaceProviderFactory<IFileContextProvider>`
  - Implementação de provedor de `IFileContextProvider.GetContextsForFileAsync`
    - Construir uma nova `FileContext` com o `contextType` argumento do construtor como exclusivamente gerado `Guid`
    - Use o `Context` propriedade do `FileContext` para fornecer dados adicionais para o `ILanguageServiceProvider`
- serviço de linguagem
  - Fábrica de provedor
    - `ExportLanguageServiceProvider` atributo acima exclusivamente gerado `Guid` em `SupportedContextTypes`
    - Implementa `IWorkspaceProviderFactory<ILanguageServiceProvider>`
  - Provider
    - Implementa `ILanguageServiceProvider`
    - Use `ILanguageServiceProvider.InitializeAsync` para habilitar serviços de linguagem para os argumentos fornecidos quando um arquivo é aberto.
    - Use `ILanguageServiceProvider.UninitializeAsync` para desabilitar os serviços de linguagem para os argumentos fornecidos quando um arquivo é fechado

>[!WARNING]
>O `ILanguageServiceProvider` métodos podem ser invocados pelo espaço de trabalho no thread principal. Considere agendar o trabalho em um thread diferente para evitar a introdução de atrasos de interface do usuário.

## <a name="language-server-protocol"></a>Language Server Protocol

O `Microsoft.VisualStudio.Workspace.*` APIs não são a única maneira de habilitar o serviço de linguagem em Abrir pasta. Outra opção é usar um servidor de linguagem. Para obter mais informações, leia sobre o [protocolo de idioma do servidor](language-server-protocol.md).

## <a name="related-interfaces"></a>Interfaces relacionadas

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> é invocado quando um arquivo de correspondência de tipos de arquivo é aberto ou fechado para edição.

## <a name="next-steps"></a>Próximas etapas

* [Compilação de espaço de trabalho](workspace-build.md) -Abrir pasta suporta cria sistemas como o MSBuild e makefiles. 
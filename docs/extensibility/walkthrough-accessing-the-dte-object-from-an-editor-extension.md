---
title: Acessar o objeto DTE de uma extensão do editor
description: Saiba como acessar o objeto DTE de uma extensão do editor usando o exemplo de código neste passo a passo.
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: tutorial
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 094a37960fa5b32d018eebe3becee4fde43cc392
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905118"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>Passo a passo: acessar o objeto DTE de uma extensão do editor

No VSPackages, você pode obter o objeto DTE chamando o método <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> com o tipo do objeto DTE. Em Managed Extensibility Framework (MEF), você pode importar e chamar o <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> método com um tipo de <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> <xref:EnvDTE.DTE> .

## <a name="prerequisites"></a>Pré-requisitos

Para seguir este passo a passo, você deve instalar o Visual Studio SDK. Para obter mais informações, [consulte Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="get-the-dte-object"></a>Obter o objeto DTE

1. Crie um projeto VSIX em C# e nomee-o **DTETest.** Adicione um modelo de item **do Classificador** de Editor e nomee-o **DTETest.**

   Para obter mais informações, [consulte Criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

::: moniker range=">=vs-2019"

2. Adicione as seguintes referências de assembly ao projeto:

    - Microsoft.VisualStudio.Shell.Framework
    - Microsoft.VisualStudio.Shell.Immutable.10.0

3. No arquivo *DTETestProvider.cs,* adicione as seguintes `using` diretivas:

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. Na classe `DTETestProvider` , importe um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> .

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. No método `GetClassifier()` , adicione o seguinte código antes da `return` instrução :

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. Adicione as seguintes referências de assembly ao projeto:

   - Envdte
   - Microsoft.VisualStudio.Shell.Framework

3. No arquivo *DTETestProvider.cs,* adicione as seguintes `using` diretivas:

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. Na classe `DTETestProvider` , importe um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> .

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. No método `GetClassifier()` , adicione o seguinte código antes da `return` instrução :

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>Confira também

- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
- [Iniciar o Visual Studio usando DTE](launch-visual-studio-dte.md)

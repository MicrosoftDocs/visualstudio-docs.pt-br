---
title: Migrando um serviço de linguagem herdada | Microsoft Docs
description: Saiba como atualizar um serviço de idioma para a versão mais recente do Visual Studio atualizando o projeto e adicionando um arquivo. Extension. vsixmanifest de origem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: afe98f2d96618999aa02dd01f03f55395af46e19
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063260"
---
# <a name="migrating-a-legacy-language-service"></a>Migrando um serviço de linguagem herdado
Você pode migrar um serviço de idioma herdado para uma versão posterior do Visual Studio atualizando o projeto e adicionando um arquivo Source. Extension. vsixmanifest ao projeto. O próprio serviço de linguagem continuará a funcionar como antes, porque o editor do Visual Studio o adapta.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar um serviço de linguagem, consulte [extensões de serviço de editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Migrando uma solução de serviço de linguagem do Visual Studio 2008 para uma versão posterior
 As etapas a seguir mostram como adaptar um exemplo do Visual Studio 2008 chamado RegExLanguageService. Você pode encontrar esse exemplo em uma instalação do SDK do Visual Studio 2008, na pasta *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\.

> [!IMPORTANT]
> Se o serviço de linguagem não definir cores, você deverá definir explicitamente <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> como `true` no VSPackage:

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Para migrar um serviço de linguagem do Visual Studio 2008 para uma versão posterior

1. Instale as versões mais recentes do Visual Studio e do SDK do Visual Studio. Para obter mais informações sobre as maneiras de instalar o SDK, consulte [instalando o SDK do Visual Studio](../../extensibility/installing-the-visual-studio-sdk.md).

2. Edite o arquivo RegExLangServ. csproj (sem carregá-lo no Visual Studio.

     No `Import` nó que se refere ao arquivo Microsoft. VsSDK. targets, substitua o valor pelo texto a seguir.

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3. Salve o arquivo e feche-o.

4. Abra a solução RegExLangServ. sln.

5. A janela de **atualização unidirecional** é exibida. Clique em **OK**.

6. Atualize as propriedades do projeto. Abra a janela de **Propriedades do projeto** selecionando o nó do projeto na **Gerenciador de soluções**, clicando com o botão direito do mouse e selecionando **Propriedades**.

    - Na guia **aplicativo** , altere **estrutura de destino** para **4.6.1**.

    - Na guia **depurar** , na caixa **Iniciar programa externo** , digite **\<Visual Studio installation path>\Common7\IDE\devenv.exe.**.

         Na caixa **argumentos de linha de comando** , digite/**rootsuffix exp**.

7. Atualize as seguintes referências:

    - Remova a referência a Microsoft.VisualStudio.Shell.9.0.dll e, em seguida, adicione referências a Microsoft.VisualStudio.Shell.14.0.dll e Microsoft.VisualStudio.Shell.Immutable.11.0.dll.

    - Remova a referência a Microsoft.VisualStudio.Package.LanguageService.9.0.dll e, em seguida, adicione uma referência a Microsoft.VisualStudio.Package.LanguageService.14.0.dll.

    - Adicione uma referência a Microsoft.VisualStudio.Shell.Interop.10.0.dll.

8. Abra o arquivo VsPkg. cs e altere o valor do `DefaultRegistryRoot` atributo para

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. O exemplo original não registra seu serviço de idioma, portanto, você deve adicionar o seguinte atributo a VsPkg. cs.

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. Você deve adicionar um arquivo. Extension. vsixmanifest de origem.

    - Copie esse arquivo de uma extensão existente para o diretório do projeto. (Uma maneira de obter esse arquivo é criar um projeto VSIX (em **arquivo**, clique em **novo** e, em seguida, clique em **projeto**. Em Visual Basic ou C#, clique em **extensibilidade** e selecione **projeto VSIX**.)

    - Adicione o arquivo ao seu projeto.

    - Nas **Propriedades** do arquivo, defina **ação de compilação** como **nenhum**.

    - Abra o arquivo com o **Editor de manifesto do VSIX**.

    - Altere os seguintes campos:

    - **ID**: RegExLangServ

    - **Nome do produto**: RegExLangServ

    - **Descrição**: um serviço de linguagem de expressão regular.

    - Em **ativos**, clique **em novo**, selecione o **tipo** para **Microsoft. VisualStudio. VSPackage**, defina a **origem** para **um projeto na solução atual** e, em seguida, defina o **projeto** como **RegExLangServ**.

    - Salve e feche o arquivo.

11. Compile a solução. Os arquivos criados são implantados no **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ \\**.

12. Inicie a depuração. Uma segunda instância do Visual Studio aberta.

## <a name="see-also"></a>Confira também
- [Extensibilidade do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-extensibility.md)

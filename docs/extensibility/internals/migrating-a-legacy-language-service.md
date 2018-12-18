---
title: Migrando um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 412b09016a3f889e0d6c5e40ff75895d5ae8ff48
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31135844"
---
# <a name="migrating-a-legacy-language-service"></a>Migrando um serviço de linguagem herdado
Você pode migrar um serviço de linguagem herdados para uma versão posterior do Visual Studio atualizando o projeto e adicionar um arquivo source.extension.vsixmanifest ao projeto. O serviço de linguagem continuará funcionando como antes, porque o editor do Visual Studio se adapta a ele.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de idioma, consulte [Editor e extensões de serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Migrando uma solução de serviço de linguagem do Visual Studio 2008 para uma versão posterior  
 As etapas a seguir mostram como adaptar um exemplo do Visual Studio 2008 denominado RegExLanguageService. Você pode encontrar esse exemplo em uma instalação do SDK do Visual Studio 2008, além de *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ pasta.  
  
> [!IMPORTANT]
>  Se o serviço de linguagem não definir cores, você deve definir explicitamente <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> para `true` sobre o VSPackage:  
  
```  
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]  
```  
  
#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Para migrar um serviço de linguagem do Visual Studio 2008 para uma versão posterior  
  
1.  Instale as versões mais recentes do Visual Studio e o SDK do Visual Studio. Para obter mais informações sobre como instalar o SDK, consulte [instalar o SDK do Visual Studio](../../extensibility/installing-the-visual-studio-sdk.md).  
  
2.  Editar o arquivo RegExLangServ.csproj (sem carregá-lo no Visual Studio.  
  
     No `Import` nó refere-se ao arquivo Microsoft.VsSDK.targets, substitua o valor com o seguinte texto.  
  
    ```  
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets  
    ```  
  
3.  Salve o arquivo e, em seguida, fechá-lo.  
  
4.  Abra a solução RegExLangServ.sln.  
  
5.  O **atualização unidirecional** janela é exibida. Clique em **OK**.  
  
6.  Atualize as propriedades do projeto. Abra o **propriedades do projeto** selecionando o nó do projeto no **Solution Explorer**, com o botão direito e selecionando **propriedades**.  
  
    -   Sobre o **aplicativo** , altere **framework de destino** para **4.6.1**.  
  
    -   Sobre o **depurar** guia o **Iniciar programa externo** , digite  **\<caminho de instalação do Visual Studio > \Common7\IDE\devenv.exe.**.  
  
         No **argumentos de linha de comando** , digite /**rootsuffix Exp**.  
  
7.  Atualize as seguintes referências:  
  
    -   Remova a referência ao Microsoft.VisualStudio.Shell.9.0.dll e adicionar referências a Microsoft.VisualStudio.Shell.14.0.dll e Microsoft.VisualStudio.Shell.Immutable.11.0.dll.  
  
    -   Remova a referência à Microsoft.VisualStudio.Package.LanguageService.9.0.dll e adicione uma referência a Microsoft.VisualStudio.Package.LanguageService.14.0.dll.  
  
    -   Adicione uma referência a Microsoft.VisualStudio.Shell.Interop.10.0.dll.  
  
8.  Abra o arquivo VsPkg.cs e altere o valor da `DefaultRegistryRoot` atributo  
  
    ```  
    "Software\\Microsoft\\VisualStudio\\14.0Exp"  
    ```  
  
9. O exemplo original não registrar seu serviço de linguagem, assim você deve adicionar o seguinte atributo para VsPkg.cs.  
  
    ```  
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]  
    ```  
  
10. Você deve adicionar um arquivo source.extension.vsixmanifest.  
  
    -   Copie esse arquivo de extensão existente para o diretório do projeto. (Uma maneira de obter esse arquivo é criar um projeto do VSIX (em **arquivo**, clique em **novo**, em seguida, clique em **projeto**. Clique em Visual Basic ou c# **extensibilidade**, em seguida, selecione **projeto VSIX**.)  
  
    -   Adicione o arquivo ao seu projeto.  
  
    -   O arquivo **propriedades**, defina **ação de compilação** para **nenhum**.  
  
    -   Abra o arquivo com o **Editor de manifesto do VSIX**.  
  
    -   Altere os campos a seguir:  
  
    -   **ID**: RegExLangServ  
  
    -   **Nome do produto**: RegExLangServ  
  
    -   **Descrição**: um serviço de linguagem de expressão regular.  
  
    -   Em **ativos**, clique em **novo**, selecione o **tipo** para **Microsoft.VisualStudio.VsPackage**, defina o **fonte** para **um projeto na solução atual**e, em seguida, defina o **projeto** para **RegExLangServ**.  
  
    -   Salve e feche o arquivo.  
  
11. Compile a solução. Os arquivos compilados são implantados em **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ\\**.  
  
12. Inicie a depuração. Uma segunda instância do Visual Studio é aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Extensibilidade do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-extensibility.md)
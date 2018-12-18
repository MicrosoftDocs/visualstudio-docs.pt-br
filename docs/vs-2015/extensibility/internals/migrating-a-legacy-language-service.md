---
title: Migrando um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 826a27fd3e3041e99f34acce0474a8e71837c69d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807602"
---
# <a name="migrating-a-legacy-language-service"></a>Migrando um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Você pode migrar um serviço de linguagem herdado para uma versão posterior do Visual Studio atualizando o projeto e adicionando um arquivo vsixmanifest ao projeto. O serviço de linguagem continuará a funcionar como antes, porque o editor do Visual Studio se adapta a ele.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de linguagem, consulte [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Migrando uma solução de serviço de linguagem do Visual Studio 2008 para uma versão posterior  
 As etapas a seguir mostram como adaptar um exemplo do Visual Studio 2008 chamado RegExLanguageService. Você pode encontrar esse exemplo em uma instalação do SDK do Visual Studio 2008, além de *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ pasta.  
  
> [!IMPORTANT]
>  Se seu serviço de linguagem não define as cores, você deve definir explicitamente <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> para `true` em VSPackage:  
  
```  
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]  
```  
  
#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Para migrar um serviço de linguagem do Visual Studio 2008 para uma versão posterior  
  
1.  Instale as versões mais recentes do Visual Studio e SDK do Visual Studio. Para obter mais informações sobre as maneiras de instalar o SDK, consulte [instalando o SDK do Visual Studio](../../extensibility/installing-the-visual-studio-sdk.md).  
  
2.  Edite o arquivo de RegExLangServ.csproj (sem carregá-los no Visual Studio.  
  
     No `Import` nó que se refere ao arquivo Microsoft.VsSDK.targets, substitua o valor com o texto a seguir.  
  
    ```  
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets  
    ```  
  
3.  Salve o arquivo e, em seguida, fechá-lo.  
  
4.  Abra a solução RegExLangServ.sln.  
  
5.  O **atualização unidirecional** janela é exibida. Clique em **OK**.  
  
6.  Atualize as propriedades do projeto. Abra o **propriedades do projeto** selecionando o nó do projeto na **Gerenciador de soluções**, com o botão direito e selecionando **propriedades**.  
  
    -   Sobre o **Application** , altere **estrutura de destino** para **4.6.1**.  
  
    -   No **Debug** guia, o **Iniciar programa externo** , digite  **\<caminho de instalação do Visual Studio > \Common7\IDE\devenv.exe.**.  
  
         No **argumentos de linha de comando** , digite /**rootsuffix Exp**.  
  
7.  Atualize as referências a seguir:  
  
    -   Remova a referência ao Microsoft.VisualStudio.Shell.9.0.dll e, em seguida, adicionar referências a Microsoft.VisualStudio.Shell.14.0.dll e Microsoft.VisualStudio.Shell.Immutable.11.0.dll.  
  
    -   Remova a referência ao Microsoft.VisualStudio.Package.LanguageService.9.0.dll e, em seguida, adicionar uma referência ao Microsoft.VisualStudio.Package.LanguageService.14.0.dll.  
  
    -   Adicione uma referência ao Microsoft.VisualStudio.Shell.Interop.10.0.dll.  
  
8.  Abra o arquivo VsPkg.cs e altere o valor da `DefaultRegistryRoot` atributo  
  
    ```  
    "Software\\Microsoft\\VisualStudio\\14.0Exp"  
    ```  
  
9. O exemplo original não registrar seu serviço de linguagem, você deve adicionar o seguinte atributo para VsPkg.cs.  
  
    ```  
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]  
    ```  
  
10. Você deve adicionar um arquivo vsixmanifest.  
  
    -   Copie esse arquivo de uma extensão existente no diretório do projeto. (Uma maneira de obter esse arquivo é criar um projeto do VSIX (sob **arquivo**, clique em **New**, em seguida, clique em **projeto**. Clique em Visual Basic ou c# **extensibilidade**, em seguida, selecione **projeto VSIX**.)  
  
    -   Adicione o arquivo ao seu projeto.  
  
    -   No arquivo de **propriedades**, defina **Build Action** para **None**.  
  
    -   Abra o arquivo com o **Editor de manifesto do VSIX**.  
  
    -   Altere os campos a seguir:  
  
    -   **ID**: RegExLangServ  
  
    -   **Nome do produto**: RegExLangServ  
  
    -   **Descrição**: um serviço de linguagem de expressão regular.  
  
    -   Sob **ativos**, clique em **New**, selecione o **tipo** para **VSPackage**, defina o **fonte** ao **um projeto na solução atual**e, em seguida, defina as **projeto** para **RegExLangServ**.  
  
    -   Salve e feche o arquivo.  
  
11. Compile a solução. Os arquivos criados são implantados **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ\\**.  
  
12. Inicie a depuração. Uma segunda instância do Visual Studio é aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Extensibilidade do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-extensibility.md)


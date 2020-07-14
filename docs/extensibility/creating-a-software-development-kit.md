---
title: Criando um Software Development Kit | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61e547be5f240cafccc058eb7ea2249fd492554b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904110"
---
# <a name="create-a-software-development-kit"></a>Criar um Software Development Kit

Um Software Development Kit (SDK) é uma coleção de APIs que você pode referenciar como um único item no Visual Studio. A caixa de diálogo **Gerenciador de referências** lista todos os SDKs que são relevantes para o projeto. Quando você adiciona um SDK a um projeto, as APIs estão disponíveis no Visual Studio.

Há dois tipos de SDKs:

- Os SDKs de plataforma são componentes obrigatórios para o desenvolvimento de aplicativos para uma plataforma. Por exemplo, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK é necessário para desenvolver [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos.

- Os SDKs de extensão são componentes opcionais que estendem uma plataforma, mas que não são obrigatórios para o desenvolvimento de aplicativos para essa plataforma.

As seções a seguir descrevem a infraestrutura geral de SDKs e como criar um SDK de plataforma e um SDK de extensão.

## <a name="platform-sdks"></a>SDKs de plataforma

Os SDKs de plataforma são necessários para desenvolver aplicativos para uma plataforma. Por exemplo, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK é necessário para desenvolver aplicativos para o [!INCLUDE[win81](../debugger/includes/win81_md.md)] .

### <a name="installation"></a>Instalação

Todos os SDKs de plataforma serão instalados em *HKLM\Software\Microsoft\Microsoft SDKs \\ [TPI] \V [TPV] \\ @InstallationFolder = [raiz do SDK]*. Da mesma forma, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK é instalado em *HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1*.

### <a name="layout"></a>Layout

Os SDKs de plataforma têm o seguinte layout:

```
\[InstallationFolder root]
            SDKManifest.xml
            \References
                  \[config]
                        \[arch]
            \DesignTime
                  \[config]
                        \[arch]
```

| Nó | Descrição |
|------------------------| - |
| Pasta de *referências* | Contém binários que contêm APIs que podem ser codificadas. Eles podem incluir arquivos de metadados do Windows (WinMD) ou assemblies. |
| Pasta *designtime* | Contém arquivos que são necessários apenas em tempo de execução/depuração. Eles podem incluir documentos XML, bibliotecas, cabeçalhos, binários de tempo de design da caixa de ferramentas, artefatos do MSBuild e assim por diante<br /><br /> Os documentos XML seriam, de preferência, colocados na pasta *\DesignTime* , mas os documentos XML para referências continuarão a ser colocados junto com o arquivo de referência no Visual Studio. Por exemplo, o documento XML de uma referência<em>\References \\ [config] \\ [Arch] \sample.dll</em> será *\References \\ [config] \\ [Arch] \sample.xml*e a versão localizada desse documento será *\References \\ [config] \\ [Arch] \\ [localidade] \sample.xml*. |
| Pasta de *configuração* | Pode haver apenas três pastas: *debug*, *Retail* e *CommonConfiguration*. Os autores do SDK podem posicionar seus arquivos em *CommonConfiguration* se o mesmo conjunto de arquivos do SDK for consumido, independentemente da configuração que o consumidor do SDK direcionará. |
| Pasta de *arquitetura* | Qualquer pasta de *arquitetura* com suporte pode existir. O Visual Studio dá suporte às seguintes arquiteturas: x86, x64, ARM e neutro. Observação: o Win32 mapeia para x86 e AnyCPU é mapeado para neutro.<br /><br /> O MSBuild só tem a aparência de *\CommonConfiguration\neutral* para SDKs de plataforma. |
| *SDKManifest.xml* | Este arquivo descreve como o Visual Studio deve consumir o SDK. Examine o manifesto do SDK para [!INCLUDE[win81](../debugger/includes/win81_md.md)] :<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName:** O valor que o pesquisador de objetos exibe na lista de procura.<br /><br /> **PlatformIdentity:** A existência desse atributo diz ao Visual Studio e ao MSBuild que o SDK é um SDK de plataforma e que as referências adicionadas dele não devem ser copiadas localmente.<br /><br /> **TargetFramework:** Esse atributo é usado pelo Visual Studio para garantir que apenas projetos direcionados às mesmas estruturas, conforme especificado no valor desse atributo, possam consumir o SDK.<br /><br /> **MinVSVersion:** Esse atributo é usado pelo Visual Studio para consumir apenas os SDKs que se aplicam a ele.<br /><br /> **Referência:** Esse atributo deve ser especificado somente para as referências que contêm controles. Para obter informações sobre como especificar se uma referência contém controles, consulte abaixo. |

## <a name="extension-sdks"></a>SDKs de extensão

As seções a seguir descrevem o que você precisa fazer para implantar um SDK de extensão.

### <a name="installation"></a>Instalação

Os SDKs de extensão podem ser instalados para um usuário específico ou para todos os usuários sem especificar uma chave do registro. Para instalar um SDK para todos os usuários, use o seguinte caminho:

*% Program Files%\Microsoft SDKs \<target platform\> \v<número de versão da plataforma \> \ExtensionSDKs*

Para uma instalação específica do usuário, use o seguinte caminho:

*%USERPROFILE%\AppData\Local\Microsoft SDKs \<target platform\> \v<número de versão da plataforma \> \ExtensionSDKs*

Se você quiser usar um local diferente, deverá executar uma das duas ações a seguir:

1. Especifique-o em uma chave do registro:

     **HKLM\Software\Microsoft\Microsoft SDKs \<target platform> \v<número de versão da plataforma \> \ExtensionSDKs\<SDKName>\<SDKVersion>**\

     e adicione uma subchave (padrão) que tenha um valor de `<path to SDK><SDKName><SDKVersion>` .

2. Adicione a Propriedade MSBuild `SDKReferenceDirectoryRoot` ao seu arquivo de projeto. O valor dessa propriedade é uma lista delimitada por ponto e vírgula de diretórios nos quais os SDKs de extensão que você deseja referenciar residem.

### <a name="installation-layout"></a>Layout da instalação

Os SDKs de extensão têm o seguinte layout de instalação:

```
\<ExtensionSDKs root>
           \<SDKName>
                 \<SDKVersion>
                        SDKManifest.xml
                        \References
                              \<config>
                                    \<arch>
                        \Redist
                              \<config>
                                    \<arch>
                        \DesignTime
                               \<config>
                                     \<arch>

```

1. \\<SDKName \> \\<SDKVersion \> : o nome e a versão do SDK da extensão são derivados dos nomes de pastas correspondentes no caminho para a raiz do SDK. O MSBuild usa essa identidade para localizar o SDK no disco e o Visual Studio exibe essa identidade na janela **Propriedades** e na caixa de diálogo **Gerenciador de referências** .

2. Pasta *References* : os binários que contêm as APIs. Eles podem ser arquivos de metadados do Windows (WinMD) ou assemblies.

3. Pasta *Redist* : os arquivos necessários para tempo de execução/depuração e devem ser empacotados como parte do aplicativo do usuário. Todos os binários devem ser colocados sob *\redist \\<config \> \\<Arch \> *e os nomes binários devem ter o seguinte formato para garantir a exclusividade: *]* \<company> . \<product> . \<purpose> \<extension> . <em>. Por exemplo, * Microsoft.Cpp.Build.dll</em>. Todos os arquivos com nomes que podem colidir com nomes de arquivos de outros SDKs (por exemplo, JavaScript, CSS, PRI, XAML, png e arquivos jpg) devem ser colocados sob <em>\redist \\<config \> \\<Arch \> \\<sdkname \> \* , exceto pelos arquivos associados aos controles XAML. Esses arquivos devem ser colocados abaixo de * \redist \\<config \> \\<Arch \> \\<ComponentName \> \\ </em>.

4. Pasta *designtime* : os arquivos que são necessários somente em tempo de execução/depuração e não devem ser empacotados como parte do aplicativo do usuário. Eles podem ser documentos XML, bibliotecas, cabeçalhos, binários de tempo de design da caixa de ferramentas, artefatos do MSBuild e assim por diante. Qualquer SDK destinado ao consumo por um projeto nativo deve ter um arquivo *SDKName. props* . A seguir, é mostrado um exemplo desse tipo de arquivo.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <ExecutablePath>C:\Temp\ExecutablePath;$(ExecutablePath)</ExecutablePath>
       <IncludePath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\CommonConfiguration\Neutral\include;$(IncludePath)</IncludePath>
       <AssemblyReferencePath>C:\Temp\AssemblyReferencePath;(AssemblyReferencePath)</AssemblyReferencePath>
       <LibraryPath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\Debug\ARM;$(LibraryPath)</LibraryPath>
       <SourcePath>C:\Temp\SourcePath\X64;$(SourcePath)</SourcePath>
       <ExcludePath>C:\Temp\ExcludePath\X64;$(ExcludePath)</ExcludePath>
       <_PropertySheetDisplayName>DevILSDK, 1.0</_PropertySheetDisplayName>
     </PropertyGroup>
   </Project>

   ```

    Os documentos de referência XML são colocados junto com o arquivo de referência. Por exemplo, o documento de referência XML do *\References \\<config \> \\<Arch \>\sample.dll* assembly é *\References \\<config<\> \\ Arch \> *\sample.xmle a versão localizada desse documento é *\References \\<config \> \\<Arch \> \\<locale \>\sample.xml*.

5. Pasta de *configuração* : três subpastas: *debug*, *Retail*e *CommonConfiguration*. Os autores do SDK podem posicionar seus arquivos em *CommonConfiguration* quando o mesmo conjunto de arquivos do SDK deve ser consumido, independentemente da configuração de destino do consumidor do SDK.

6. Pasta de *arquitetura* : há suporte para as seguintes arquiteturas: x86, x64, ARM, neutro. O Win32 mapeia para x86 e AnyCPU é mapeado para neutro.

### <a name="sdkmanifestxml"></a>SDKManifest.xml

O arquivo *SDKManifest.xml* descreve como o Visual Studio deve consumir o SDK. Veja um exemplo a seguir:

```
<FileList>
DisplayName = "My SDK"
ProductFamilyName = "My SDKs"
TargetFramework = ".NETCore, version=v4.5.1; .NETFramework, version=v4.5.1"
MinVSVersion = "14.0"
MaxPlatformVersion = "8.1"
AppliesTo = "WindowsAppContainer + WindowsXAML"
SupportPrefer32Bit = "True"
SupportedArchitectures = "x86;x64;ARM"
SupportsMultipleVersions = "Error"
CopyRedistToSubDirectory = "."
DependsOn = "SDKB, version=2.0"
MoreInfo = "https://msdn.microsoft.com/MySDK">
<File Reference = "MySDK.Sprint.winmd" Implementation = "XNASprintImpl.dll">
<Registration Type = "Flipper" Implementation = "XNASprintFlipperImpl.dll" />
<Registration Type = "Flexer" Implementation = "XNASprintFlexerImpl.dll" />
<ToolboxItems VSCategory = "Toolbox.Default" />
</File>
</FileList>
```

A lista a seguir fornece os elementos do arquivo:

1. DisplayName: o valor que aparece no Gerenciador de referências, Gerenciador de Soluções, pesquisador de objetos e outros locais na interface do usuário para o Visual Studio.

2. ProductFamilyName: o nome geral do produto SDK. Por exemplo, o [!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] SDK é denominado "Microsoft. winjs. 1.0" e "Microsoft. winjs. 2.0", que pertence à mesma família de família de produtos SDK, "Microsoft. winjs". Esse atributo permite que o Visual Studio e o MSBuild façam essa conexão. Se esse atributo não existir, o nome do SDK será usado como o nome da família de produtos.

3. FrameworkIdentity: especifica uma dependência em uma ou mais bibliotecas de componentes do Windows. O valor desse atributo é colocado no manifesto do aplicativo de consumo. Esse atributo é aplicável somente a bibliotecas de componentes do Windows.

4. TargetFramework: especifica os SDKs que estão disponíveis no Gerenciador de referências e na caixa de ferramentas. Esta é uma lista delimitada por ponto-e-vírgula dos monikers da estrutura de destino, por exemplo, ".NET Framework, Version = v 2.0; .NET Framework, Version = v 4.5.1". Se várias versões da mesma estrutura de destino forem especificadas, o Gerenciador de referências usará a versão mais baixa especificada para fins de filtragem. Por exemplo, se ".NET Framework, versão = v 2.0; .NET Framework, versão = v 4.5.1" for especificado, o Gerenciador de referências usará ".NET Framework, versão = v 2.0". Se um perfil específico da estrutura de destino for especificado, somente esse perfil será usado pelo Gerenciador de referências para fins de filtragem. Por exemplo, quando "Silverlight, Version = v 4.0, Profile = WindowsPhone" for especificado, o Gerenciador de referências filtrará apenas o perfil de Windows Phone; um projeto direcionado para a estrutura completa do Silverlight 4,0 não vê o SDK no Gerenciador de referências.

5. MinVSVersion: a versão mínima do Visual Studio.

6. MaxPlatformVerson: a versão máxima da plataforma de destino deve ser usada para especificar as versões da plataforma nas quais o seu SDK de extensão não funcionará. Por exemplo, o pacote de tempo de execução do Microsoft Visual C++ v 11.0 deve ser referenciado somente por projetos do Windows 8. Portanto, o MaxPlatformVersion do projeto do Windows 8 é 8,0. Isso significa que o Gerenciador de referências filtra Microsoft Visual C++ pacote de tempo de execução para um projeto Windows 8.1 e o MSBuild gera um erro quando um [!INCLUDE[win81](../debugger/includes/win81_md.md)] projeto faz referência a ele. Observação: esse elemento tem suporte a partir do [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] .

7. Aplica-se a: especifica os SDKs que estão disponíveis no Gerenciador de referências especificando os tipos de projeto aplicáveis do Visual Studio. Nove valores são reconhecidos: WindowsAppContainer, Visual c++, VB, CSharp, WindowsXAML, JavaScript, Managed e Native. O autor do SDK pode usar and ("+") ou ("&#124;"), não ("!") operadores para especificar exatamente o escopo dos tipos de projeto que se aplicam ao SDK.

    WindowsAppContainer identifica projetos para [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos.

8. SupportPrefer32Bit: os valores com suporte são "true" e "false". O padrão é "true". Se o valor for definido como "false", o MSBuild retornará um erro para [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] projetos (ou um aviso para projetos da área de trabalho) se o projeto que faz referência ao SDK tiver o Prefer32Bit habilitado. Para obter mais informações sobre Prefer32Bit, consulte página [de compilação, designer de projeto (C#)](../ide/reference/build-page-project-designer-csharp.md) ou [página de compilação, designer de projeto (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md).

9. SupportedArchitectures: uma lista delimitada por ponto e vírgula de arquiteturas que o SDK dá suporte. O MSBuild exibirá um aviso se a arquitetura do SDK de destino no projeto de consumo não tiver suporte. Se esse atributo não for especificado, o MSBuild nunca exibirá esse tipo de aviso.

10. SupportsMultipleVersions: se esse atributo for definido como **erro** ou **aviso**, o MSBuild indica que o mesmo projeto não pode fazer referência a várias versões da mesma família do SDK. Se esse atributo não existir ou estiver definido como **permitir**, o MSBuild não exibirá esse tipo de erro ou aviso.

11. AppX: especifica o caminho para os pacotes de aplicativos para a biblioteca de componentes do Windows no disco. Esse valor é passado para o componente de registro da biblioteca de componentes do Windows durante a depuração local. A Convenção de nomenclatura para o nome do arquivo é * \<Company> . \<Product> . \<Architecture> . \<Configuration> \<Version> . Appx*. A configuração e a arquitetura são opcionais no nome do atributo e no valor do atributo se eles não se aplicam à biblioteca de componentes do Windows. Esse valor é aplicável somente a bibliotecas de componentes do Windows.

12. CopyRedistToSubDirectory: especifica onde os arquivos na pasta *\redist* devem ser copiados em relação à raiz do pacote do aplicativo (ou seja, o **local do pacote** escolhido no Assistente para **criar pacote de aplicativo** ) e a raiz do layout do tempo de execução. O local padrão é a raiz do pacote do aplicativo e o layout **F5** .

13. Depende: uma lista de identidades do SDK que definem os SDKs dos quais esse SDK depende. Esse atributo aparece no painel de detalhes do Gerenciador de referências.

14. MoreInfo: a URL para a página da Web que fornece ajuda e mais informações. Esse valor é usado no link mais informações no painel direito do Gerenciador de referências.

15. Tipo de registro: especifica o registro de WinMD no manifesto do aplicativo e é necessário para o WinMD nativo, que tem uma DLL de implementação equivalente.

16. Referência de arquivo: especificada somente para as referências que contêm controles ou são WinMDs nativas. Para obter informações sobre como especificar se uma referência contém controles, consulte [especificar o local dos itens da caixa de ferramentas](#ToolboxItems) abaixo.

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a>Especificar o local dos itens da caixa de ferramentas

O elemento **ToolBoxItems** do esquema de *SDKManifest.xml* especifica a categoria e o local dos itens da caixa de ferramentas nos SDKs de plataforma e extensão. Os exemplos a seguir mostram como especificar locais diferentes. Isso é aplicável a referências WinMD ou DLL.

1. Coloque os controles na categoria padrão da caixa de ferramentas.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. Coloque os controles sob um nome de categoria específico.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory= "MyCategoryName"/>
    </File>
    ```

3. Coloque os controles sob nomes de categoria específicos.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems VSCategory = "Data">
        <ToolboxItems />
    </File>
    ```

4. Coloque controles sob diferentes nomes de categoria no Blend e no Visual Studio.

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. Enumere controles específicos de forma diferente no Blend e no Visual Studio.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. Enumere controles específicos e coloque-os no caminho comum do Visual Studio ou somente no grupo todos os controles.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. Enumere controles específicos e mostre apenas um conjunto específico em ChooseItems sem que eles estejam na caixa de ferramentas.

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>Confira também

- [Walkthrough: criar um SDK usando C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [Walkthrough: criar um SDK usando C# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [Gerenciar referências em um projeto](../ide/managing-references-in-a-project.md)

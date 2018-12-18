---
title: Criando um Software Development Kit | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: dea4acc347094657bdb916a7d5be386dcd54f8ad
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349550"
---
# <a name="create-a-software-development-kit"></a>Criar um kit de desenvolvimento de software
Um software development kit (SDK) é uma coleção de APIs que pode ser referenciado como um único item no Visual Studio. O **Gerenciador de referências** caixa de diálogo lista todos os SDKs que são relevantes para o projeto. Quando você adiciona um SDK a um projeto, as APIs estão disponíveis no Visual Studio.  

 Há dois tipos de SDKs:  

- SDKs de plataforma são componentes obrigatórios para o desenvolvimento de aplicativos para uma plataforma. Por exemplo, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK é necessário para desenvolver [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos.  

- SDKs de extensão são componentes opcionais que estendem uma plataforma, mas não são obrigatórios para o desenvolvimento de aplicativos para a plataforma.  

  As seções a seguir descrevem a infraestrutura geral de SDKs e como criar um SDK de plataforma e um SDK de extensão.  

- [SDKs de plataforma](#PlatformSDKs)  

- [SDKs de extensão](#ExtensionSDKs)  

##  <a name="PlatformSDKs"></a> SDKs de plataforma  
 SDKs de plataforma são necessários para desenvolver aplicativos para uma plataforma. Por exemplo, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK é necessário para desenvolver aplicativos para [!INCLUDE[win81](../debugger/includes/win81_md.md)].  

### <a name="installation"></a>Instalação  
 Serão instalado em todos os SDKs de plataforma*SDKs HKLM\Software\Microsoft\Microsoft\\[TPI] \v [TPV]\\ @InstallationFolder = [raiz do SDK]*. Da mesma forma, o [!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK está instalado na *HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1*.  

### <a name="layout"></a>Layout  
 SDKs de plataforma terá o seguinte layout:  

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
| *Referências* pasta | Contém os binários que contêm APIs que podem ser codificadas contra. Eles podem incluir arquivos de metadados do Windows (WinMD) ou assemblies. |
| *Tempo de design* pasta | Contém arquivos que são necessários apenas em tempo de pré-execução/depuração. Eles podem incluir documentos XML, bibliotecas, cabeçalhos, binários de tempo de design de caixa de ferramentas, MSBuild artefatos e assim por diante<br /><br /> Documentos XML seriam, o ideal são colocados na *\DesignTime* pasta, mas os documentos XML para referências continuarão a ser colocada junto com o arquivo de referência no Visual Studio. Por exemplo, o documento XML para obter uma referência<em>\References\\[configuração]\\[arch]\sample.dll</em> estará *\References\\[configuração]\\[arch]\sample.xml*, e será a versão localizada do que doc *\References\\[configuração]\\[arch]\\[locale]\sample.xml*. |
| *Configuração* pasta | Pode haver apenas três pastas: *Debug*, *varejo* e *CommonConfiguration*. Os autores do SDK podem colocar seus arquivos sob *CommonConfiguration* se o mesmo conjunto de arquivos do SDK deve ser consumido, independentemente da configuração que o consumidor do SDK têm como destino. |
| *Arquitetura* pasta | Qualquer suportado *arquitetura* pasta pode existir. O Visual Studio suporta as seguintes arquiteturas: x86, x64, ARM e neutral. Observação: O Win32 mapeia para x86 e AnyCPU mapeia para neutro.<br /><br /> MSBuild procura somente sob *\CommonConfiguration\neutral* dos SDKs de plataforma. |
| *Sdkmanifest* | Esse arquivo descreve como o Visual Studio deve consumir o SDK. Examinar o manifesto do SDK para [!INCLUDE[win81](../debugger/includes/win81_md.md)]:<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName:** o valor que o Pesquisador de objetos exibe na lista de pesquisa.<br /><br /> **PlatformIdentity:** a existência desse atributo informa ao Visual Studio e o MSBuild que o SDK é uma plataforma SDK e que as referências adicionadas dele não devem ser copiadas localmente.<br /><br /> **TargetFramework:** este atributo é usado pelo Visual Studio para garantir que somente projetos que segmentam as estruturas mesmas conforme especificado no valor deste atributo pode consumir o SDK.<br /><br /> **MinVSVersion:** esse atributo é usado pelo Visual Studio para consumir apenas os SDKs que se aplicam a ele.<br /><br /> **Referência:** esse atributo deve ser especificado para apenas essas referências que contêm controles. Para obter informações sobre como especificar se uma referência contém controles, consulte abaixo. |

##  <a name="ExtensionSDKs"></a> SDKs de extensão  
 As seções a seguir descrevem o que você precisa fazer para implantar um SDK de extensão.  

### <a name="installation"></a>Instalação  
 SDKs de extensão podem ser instalados para um usuário específico ou para todos os usuários sem especificar uma chave do registro. Para instalar um SDK para todos os usuários, use o seguinte caminho:  

 *% Programa Files%\Microsoft SDKs\<plataforma de destino > \v<platform version number>\ExtensionSDKs*  

 Para uma instalação específica do usuário, use o seguinte caminho:  

 *SDKs de %USERPROFILE%\AppData\Local\Microsoft\<plataforma de destino > \v<platform version number>\ExtensionSDKs*  

 Se você quiser usar um local diferente, você deve fazer uma das duas coisas:  

1.  Especifique-a uma chave do registro:  

     **SDKs HKLM\Software\Microsoft\Microsoft\<plataforma de destino > \v<platform version number>\ExtensionSDKs\<SDKName >\<SDKVersion >**\  

     e adicione uma subchave (padrão) que tem um valor de `<path to SDK><SDKName><SDKVersion>`.  

2.  Adicione a propriedade MSBuild `SDKReferenceDirectoryRoot` ao arquivo de projeto. O valor dessa propriedade é uma lista de ponto e vírgula delimitado de diretórios em que residem os SDKs de extensão que você deseja referenciar.  

### <a name="installation-layout"></a>Layout de instalação  
 SDKs de extensão tem o seguinte layout de instalação:  

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

1. \\< SDKName\>\\< SDKVersion\>: o nome e a versão da extensão do SDK é derivado dos nomes de pastas correspondentes no caminho para a raiz do SDK. O MSBuild usa essa identidade para encontrar o SDK no disco, e o Visual Studio exibe essa identidade na **propriedades** janela e **Gerenciador de referências** caixa de diálogo.  

2. *Referências* pasta: os binários que contêm as APIs. Eles podem ser arquivos de metadados do Windows (WinMD) ou módulos (assemblies).  

3. *Pacote redistribuível* pasta: os arquivos que são necessários para o tempo de execução/depuração e devem obter empacotados como parte do aplicativo do usuário. Todos os binários devem ser colocados sob *\redist\\< config\>\\< arch\>*, e os nomes de binários devem ter o seguinte formato para garantir a exclusividade: *]* \<empresa >. \<produto >. \<finalidade >. \<extensão ><em>. Por exemplo, *Microsoft.Cpp.Build.dll</em>. Todos os arquivos com nomes que entrem em conflito com nomes de arquivo de outros SDKs (por exemplo, arquivos javascript, css, pri, xaml, png e jpg) devem ser colocados sob <em>\redist\\< config\>\\< arch\> \\< sdkname\> \* , exceto para os arquivos que estão associados com XAML controla. Esses arquivos devem ser colocados sob * \redist\\< config\>\\< arch\>\\< componentname\>\\</em>.  

4. *Tempo de design* pasta: os arquivos que são necessários no somente pré-execução/depuração de tempo e não deve ser empacotados como parte do aplicativo do usuário. Eles podem ser documentos XML, bibliotecas, cabeçalhos, binários de tempo de design de caixa de ferramentas, MSBuild artefatos e assim por diante. Qualquer SDK que se destina para consumo por um projeto nativo deve ter uma *Sdkname* arquivo. O exemplo a seguir mostra um exemplo desse tipo de arquivo.  

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

    Documentos de referência do XML serão posicionados junto com o arquivo de referência. Por exemplo, o documento de referência XML para o *\References\\< config\>\\< arch\>\sample.dll* assembly é *\References\\ < config\>\\< arch\>\sample.xml*, e é a versão localizada do que doc *\References\\< config\>\\< arch\>\\< localidade\>\sample.xml*.  

5. *Configuração* pasta: três subpastas: *Debug*, *varejo*, e *CommonConfiguration*. Os autores do SDK podem colocar seus arquivos sob *CommonConfiguration* quando o mesmo conjunto de arquivos do SDK deve ser consumido, independentemente da configuração direcionada pelo cliente do SDK.  

6. *Arquitetura* pasta: arquiteturas a seguir são suportadas: x86, x64, ARM, neutro. Win32 mapeia para x86 e AnyCPU mapeia para neutro.  

### <a name="sdkmanifestxml"></a>Sdkmanifest  
 Esse arquivo descreve como o Visual Studio deve consumir o SDK. Confira o exemplo abaixo.  

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

 A lista a seguir fornece os elementos do arquivo.  

1. DisplayName: o valor que aparece no Gerenciador de referências, Gerenciador de soluções, pesquisador de objetos e outros locais na interface do usuário para o Visual Studio.  

2. ProductFamilyName: O geral do SDK nome do produto. Por exemplo, o [!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] SDK é denominada "Microsoft.WinJS.1.0" e "Microsoft.WinJS.2.0", que pertencem à mesma família da família de produtos do SDK, "Microsoft". Esse atributo permite que o Visual Studio e o MSBuild fazer essa conexão. Se esse atributo não existir, o nome do SDK é usado como o nome da família de produtos.  

3. FrameworkIdentity: Especifica uma dependência em uma ou mais bibliotecas de componentes de Windows que o valor desse atributo é colocado no manifesto do aplicativo de consumo. Esse atributo é aplicável somente às bibliotecas de componentes do Windows.  

4. TargetFramework: Especifica os SDKs que estão disponíveis no Gerenciador de referências e a caixa de ferramentas. Isso é uma lista delimitada por ponto e vírgula de monikers de estrutura de destino, por exemplo ".NET Framework, versão = v 2.0; .NET Framework, versão = v4.5.1". Se várias versões da mesma estrutura de destino for especificadas, o Gerenciador de referência usa a versão mais antiga especificada para fins de filtragem. Por exemplo, se ".NET Framework, versão = v 2.0; .NET Framework, versão = v4.5.1" for especificado, usará o Gerenciador de referências ".NET Framework, versão = v 2.0". Se um perfil de framework de destino específico for especificado, somente esse perfil será ser usado pelo Gerenciador de referências para fins de filtragem. Por exemplo, quando "Silverlight, versão = v 4.0, perfil = WindowsPhone" for especificado, Gerenciador de referências filtra somente o perfil do Windows Phone; um projeto direcionado ao Silverlight 4.0 Framework completo não vê o SDK no Gerenciador de referências.  

5. MinVSVersion: O Visual Studio versão mínima.  

6. MaxPlatformVerson: A versão da plataforma de destino máximo deve ser usada para especificar as versões de plataforma na qual o SDK de extensão não funcionará. Por exemplo, o Microsoft Visual C++ Runtime Package v11.0 deve ser referenciado somente por projetos do Windows 8. Assim, MaxPlatformVersion do projeto Windows 8 é 8.0. Isso significa que o Gerenciador de referências filtra pacote de tempo de execução do Microsoft Visual C++ para um projeto do Windows 8.1 e MSBuild gera um erro quando um [!INCLUDE[win81](../debugger/includes/win81_md.md)] projeto faz referência a ele. Observação: esse elemento tem suporte do [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)].  

7. AppliesTo: Especifica os SDKs que estão disponíveis no Gerenciador de referências, especificando os tipos de projeto do Visual Studio aplicáveis. Nove valores são reconhecidos: WindowsAppContainer, VisualC, VB, CSharp, WindowsXAML, JavaScript, gerenciado e nativo. O autor do SDK pode usar e ("+'), ou ("&#124;"), e não ("! ") operadores para especificar exatamente o escopo dos tipos de projeto que se aplicam ao SDK.  

    WindowsAppContainer identifica projetos para [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos.  

8. SupportPrefer32Bit: Os valores com suporte são "True" e "False". O padrão é "True". Se o valor é definido como "False", o MSBuild retornará um erro para [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] projetos (ou um aviso para projetos da área de trabalho) se o projeto que referencia o SDK tem Prefer32Bit habilitado. Para obter mais informações sobre Prefer32Bit, consulte [página de Build, Designer de projeto (c#)](../ide/reference/build-page-project-designer-csharp.md) ou [página de compilação, Designer de projeto (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md).  

9. SupportedArchitectures: Um ponto e vírgula lista delimitada por das arquiteturas que o SDK oferece suporte. MSBuild exibirá um aviso se não há suporte para a arquitetura do SDK do destino no projeto consumidor. Se esse atributo não for especificado, o MSBuild nunca exibe esse tipo de aviso.  

10. SupportsMultipleVersions: Se esse atributo for definido como **erro** ou **aviso**, MSBuild indica que o mesmo projeto não pode fazer referência a várias versões da mesma família de SDK. Se esse atributo não existe ou está definido como **permitir**, MSBuild não exibe este tipo de erro ou aviso.  

11. AppX: Especifica o caminho para os pacotes de aplicativos para a biblioteca de componentes do Windows no disco. Esse valor é passado para o componente de registro da biblioteca de componente do Windows durante a depuração local. É a convenção de nomenclatura para o nome do arquivo  *\<empresa >.\< Produto >. \<Arquitetura >. \<Configuration >. \<Versão >. AppX*. Configuração e arquitetura são opcionais em nome do atributo e o valor do atributo se eles não se aplicam para a biblioteca de componentes do Windows. Esse valor é aplicável somente às bibliotecas de componentes do Windows.  

12. CopyRedistToSubDirectory: Especifica onde os arquivos sob o *\redist* pasta deve ser copiada em relação à raiz do pacote de aplicativo (ou seja, o **local do pacote** escolhido no **criar aplicativo Pacote** Assistente) e a raiz de layout de tempo de execução. O local padrão é a raiz do pacote do aplicativo e **F5** layout.  

13. DependsOn: Uma lista de identidades do SDK que definem os SDKs do qual esse SDK depende. Esse atributo é exibido no painel de detalhes do Gerenciador de referência.  

14. MoreInfo: A URL para a página da web que fornece ajuda e informações adicionais. Esse valor é usado no link mais informações no painel à direita do Gerenciador de referência.  

15. Tipo de registro: Especifica o registro WinMD no manifesto do aplicativo e é necessário para o WinMD nativo, que tem uma implementação de equivalente DLL.  

16. Referência de arquivo: Especificado para apenas essas referências que contêm controles ou são WinMDs nativos. Para obter informações sobre como especificar se uma referência contém controles, consulte [especificar o local dos itens de caixa de ferramentas](#ToolboxItems) abaixo.  

##  <a name="ToolboxItems"></a> Especifique o local dos itens de caixa de ferramentas  
 O elemento ToolBoxItems do *Sdkmanifest* esquema Especifica a categoria e o local dos itens de caixa de ferramentas nos SDKs de extensão e plataforma. Os exemplos a seguir mostram como especificar locais diferentes. Isso é aplicável às referências WinMD ou DLL.  

1.  Coloque os controles na categoria da caixa de ferramentas padrão.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Toolbox.Default"/>       
    </File>  
    ```  

2.  Coloque controles em um nome de categoria específico.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory= "MyCategoryName"/>  
    </File>  
    ```  

3.  Coloque controles em nomes de categoria específica.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Graph">  
        <ToolboxItems/>  
        <ToolboxItems VSCategory = "Data">  
        <ToolboxItems />  
    </File>  
    ```  

4.  Coloque controles em nomes de categoria diferentes no Blend e o Visual Studio.  

    ```  
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">   
        <ToolboxItems />  
    </File>  
    ```  

5.  Enumere controles específicos de modo diferente no Blend e o Visual Studio.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Graph">  
        <ToolboxItems/>  
        <ToolboxItems BlendCategory = "Controls/sample/Graph">  
        <ToolboxItems/>  
    </File>  
    ```  

6.  Enumerar os controles específicos e colocá-los em um caminho comum do Visual Studio ou apenas no grupo todos os controles.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Toolbox.Common">  
        <ToolboxItems />  
        <ToolboxItems VSCategory = "Toolbox.All">  
        <ToolboxItems />  
    </File>  
    ```  

7.  Enumerar os controles específicos e mostrar apenas um conjunto específico em ChooseItems sem eles sendo na caixa de ferramentas.  

    ```  
    <File Reference = "sample.winmd">  
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">  
        <ToolboxItems />  
    </File>  
    ```  

## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criar um SDK usando C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)   
 [Passo a passo: Criar um SDK usando c# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)   
 [Gerenciar referências em um projeto](../ide/managing-references-in-a-project.md)
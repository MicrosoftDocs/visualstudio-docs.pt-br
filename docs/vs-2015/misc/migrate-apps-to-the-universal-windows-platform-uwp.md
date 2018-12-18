---
title: Migrar aplicativos para a plataforma Universal do Windows (UWP) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5279ab9b-71d9-4be5-81f6-a1f24b06f5fb
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8d4bc5d8e8a24483c30ac813d3253626e58dd353
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791742"
---
# <a name="migrate-apps-to-the-universal-windows-platform-uwp"></a>Migrar aplicativos para a UWP (Plataforma Universal do Windows)
Verifique as alterações manuais necessárias em seus arquivos de projeto existente para aplicativos da Windows Store 8.1, aplicativos Windows Phone 8.1 ou aplicativos do Universal Windows criados com o Visual Studio 2015 RC, para que eles podem ser usados com o Visual Studio 2015 RTM. (Se você tiver um aplicativo universal do Windows 8.1 com um projeto de aplicativo do Windows e o projeto do Windows Phone, você precisará seguir as etapas para migrar cada projeto.)  
  
 Com a plataforma Universal do Windows, você agora direcionar seu aplicativo para um ou mais famílias de dispositivos. Se você deseja obter mais informações sobre os aplicativos do Windows Universal, dê uma olhada neste [guia da plataforma](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx).  
  
- [Migrar seus aplicativos existentes do C em c# /VB Windows Store 8.1 ou Windows Phone 8.1](#MigrateCSharp) para usar a plataforma Universal do Windows.  
  
- [Migrar seus aplicativos existentes do C++ Windows Store 8.1 ou Windows Phone 8.1](#MigrateCPlusPlus) para usar a plataforma Universal do Windows.  
  
- [As alterações necessárias para os aplicativos Universal Windows existentes criados com o Visual Studio 2015 RC](#PreviousVersions).  
  
- [As alterações necessárias para projetos de teste de unidade existentes para aplicativos Universal Windows criados com o Visual Studio 2015 RC](#MigrateUnitTest).  
  
  Se você não quiser fazer todas essas alterações, saiba como [seus aplicativos existentes da porta](http://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) em um novo projeto do Windows Universal.  
  
##  <a name="MigrateCSharp"></a> Migrar seus C# /VB aplicativos do Windows Store 8.1 ou Windows Phone 8.1 para usar a plataforma Universal do Windows  
  
#### <a name="migrate-your-cvb-project-files"></a>Migrar seus arquivos de projeto do C em c# /VB  
  
1.  Para localizar qual plataforma Universal do Windows que você tiver instalado, abra essa pasta: **\Program arquivos (x86) \Windows Kits\10\Platforms\UAP**. Ela contém uma lista de pastas para cada plataforma Universal do Windows que está instalada. O nome da pasta é a versão da plataforma Universal do Windows que você instalou. Por exemplo, este dispositivo Windows 10 tem versão 10.0.10240.0 da plataforma Universal do Windows instalada.  
  
     ![Abra a pasta para exibir as versões instaladas](../misc/media/uap-uwpversions.png "UAP_UWPVersions")  
  
     Mais de uma versão da plataforma Universal do Windows pode ser instalada. É recomendável que você use a versão mais recente para seu aplicativo.  
  
2.  Usando o Explorador de arquivos, vá para a pasta em que o seu projeto UWP está armazenado. Crie um arquivo. JSON nesta pasta. Nomeie o arquivo: Project. JSON e, em seguida, adicione o seguinte conteúdo para este arquivo:  
  
    ```json  
    {  
      "dependencies": {  
        "Microsoft.ApplicationInsights": "1.0.0",  
        "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",  
        "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",  
        "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"  
      },  
      "frameworks": {  
        "uap10.0": {}  
      },  
      "runtimes": {  
        "win10-arm": {},  
        "win10-arm-aot": {},  
        "win10-x86": {},  
        "win10-x86-aot": {},  
        "win10-x64": {},  
        "win10-x64-aot": {}  
      }  
    }  
  
    ```  
  
3.  Crie um arquivo chamado RD com o seguinte conteúdo. Se você tiver um projeto do VB, adicione esse arquivo para o diretório do meu projeto para seu projeto. Se você tiver um projeto c#, adicione esse arquivo para o diretório de propriedades para seu projeto.  
  
    ```xml  
    <?xml version="1.0"?>  
    <!-- This file contains Runtime Directives used by .NET Native. The defaults here are suitable for most developers. However, you can modify these parameters to modify the behavior of the .NET Native optimizer. Runtime Directives are documented at http://go.microsoft.com/fwlink/?LinkID=391919 To fully enable reflection for App1.MyClass and all of its public/private members <Type Name="App1.MyClass" Dynamic="Required All"/> To enable dynamic creation of the specific instantiation of AppClass<T> over System.Int32 <TypeInstantiation Name="App1.AppClass" Arguments="System.Int32" Activate="Required Public" /> Using the Namespace directive to apply reflection policy to all the types in a particular namespace <Namespace Name="DataClasses.ViewModels" Seralize="All" /> -->  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata"><Application>  
    <!-- An Assembly element with Name="*Application*" applies to all assemblies in the application package. The asterisks are not wildcards. -->  
    <Assembly Dynamic="Required All" Name="*Application*"/>  
    <!-- Add your application specific runtime directives here. -->  
    </Application></Directives>  
    ```  
  
4.  Abra a solução que contém seu aplicativo da Windows Store 8.1 existente ou um aplicativo do Windows Phone 8.1 no Visual Studio.  
  
5.  Clique em seu projeto existente para seu aplicativo no Gerenciador de soluções e, em seguida, selecione **descarregar projeto**. Depois que o projeto é descarregado, clique no arquivo de projeto novamente e escolha Editar o arquivo. csproj ou. vbproj.  
  
     ![Com o botão direito do mouse no projeto e escolha Editar](../misc/media/uap-editproject.png "UAP_EditProject")  
  
6.  Localizar o \<PropertyGroup > elemento que contém o \<TargetPlatformVersion > elemento com um valor de 8.1. Siga estas etapas para este \<PropertyGroup > elemento:  
  
    1.  Defina o valor da \<plataforma > elemento a ser: **x86**.  
  
    2.  Adicionar um \<TargetPlatformIdentifier > elemento e defina seu valor como: **UAP**.  
  
    3.  Alterar o valor existente do \<TargetPlatformVersion > elemento a ser o valor da versão de plataforma Universal do Windows que você instalou. Adicione também um \<TargetPlatformMinVersion > elemento e dê a ele o mesmo valor.  
  
    4.  Altere o valor da \<MinimumVisualStudioVersion > elemento a ser: **14**.  
  
    5.  Substitua o \<ProjectTypeGuids > elemento, conforme mostrado abaixo:  
  
         Para o C#:  
  
        ```xml  
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>  
        ```  
  
         Para VB:  
  
        ```xml  
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>  
        ```  
  
    6.  Adicionar um \<EnableDotNetNativeCompatibleProfile > elemento e defina seu valor como: **verdadeiro**.  
  
    7.  A escala do ativo padrão para aplicativos Universal Windows é 200. Se seu projeto inclui ativos não dimensionados em 200, você precisará adicionar um \<UapDefaultAssetScale > elemento com o valor da escala de seus ativos para essa PropertyGroup. Saiba mais sobre [ativos e as escalas](http://msdn.microsoft.com/library/jj679352.aspx).  
  
         Agora seu \<PropertyGroup > elemento deve ser semelhante a este exemplo:  
  
        ```xml  
        <PropertyGroup>  
            …  
             <Platform Condition=" '$(Platform)' == '' ">x86</Platform>  
             <TargetPlatformVersion>10.0.10240.0</TargetPlatformVersion>  
             <TargetPlatformMinVersion>10.0.10240.0</TargetPlatformMinVersion>  
             <TargetPlatformIdentifier>UAP</TargetPlatformIdentifier>  
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>  
             <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>  
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>  
             <UapDefaultAssetScale>100</UapDefaultAssetScale>  
             …  
        </PropertyGroup>  
        ```  
  
7.  Substitua todas as instâncias de 12.0 14.0 para refletir a versão do Visual Studio que você está usando. Como essas instâncias:  
  
    ```xml  
    <Project Tools Version="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    ```  
  
    ```  
    <PropertyGroup Condition=" '$(VisualStudioVersion)' == '' or '$(VisualStudioVersion)' < '14.0' ">  
        <VisualStudioVersion>14.0</VisualStudioVersion>  
    ```  
  
8.  Localizar \<PropertyGroup > elementos que são configurados para a plataforma AnyCPU como parte do atributo Condition. Remova esses elementos e todos os seus filhos. AnyCPU não há suporte para aplicativos do Windows 10 no Visual Studio 2015. Por exemplo, você deve remover \<PropertyGroup > elementos como esses:  
  
    ```xml  
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">  
        <PlatformTarget>AnyCPU</PlatformTarget>  
        <DebugSymbols>true</DebugSymbols>  
        <DebugType>full</DebugType>  
        <Optimize>false</Optimize>  
        <OutputPath>bin\Debug\</OutputPath>  
        <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>  
        <ErrorReport>prompt</ErrorReport>  
        <WarningLevel>4</WarningLevel>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">  
        <PlatformTarget>AnyCPU</PlatformTarget>  
        <DebugType>pdbonly</DebugType>  
        <Optimize>true</Optimize>  
        <OutputPath>bin\Release\</OutputPath>  
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>  
        <ErrorReport>prompt</ErrorReport>  
        <WarningLevel>4</WarningLevel>  
      </PropertyGroup>  
    ```  
  
9. Cada restantes \<PropertyGroup > elemento, verifique se o elemento tem um atributo de condição com uma configuração de versão. Se ele faz, mas ele não contém um \<UseDotNetNativeToolchain > elemento, em seguida, adicione um. Defina o valor para o \<UseDotNetNativeToolchain > elemento como true, como este:  
  
    ```xml  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|x64'">  
        <OutputPath>bin\x64\Release\</OutputPath>  
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>  
        <Optimize>true</Optimize>  
        <NoWarn>;2008</NoWarn>  
        <DebugType>pdbonly</DebugType>  
        <PlatformTarget>x64</PlatformTarget>  
        <UseVSHostingProcess>false</UseVSHostingProcess>  
        <ErrorReport>prompt</ErrorReport>  
        <Prefer32Bit>true</Prefer32Bit>  
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>  
      </PropertyGroup>  
    ```  
  
10. Para Windows Phone projetos apenas, remova os \<PropertyGroup > elemento que contém um \<TargetPlatformIdentifier > elemento com um valor de WindowsPhoneApp. Remova também os filhos desse elemento:  
  
    ```xml  
    <PropertyGroup Condition=" '$(TargetPlatformIdentifier)' == '' ">  
      <TargetPlatformIdentifier>WindowsPhoneApp</TargetPlatformIdentifier>  
    </PropertyGroup>  
    ```  
  
11. Localizar o \<ItemGroup > elemento que contém o \<AppxManifest > elemento. Adicione o seguinte \<None > elemento como um filho de \<ItemGroup > elemento:  
  
    ```xml  
    <None Include="project.json" />  
    ```  
  
12. Localizar o \<ItemGroup > elemento que contém outros ativos que são adicionados ao seu projeto, como arquivos. PNG de logotipo (\<Include="Assets\Logo.scale-100.png conteúdo" / >). Adicione o seguinte \<conteúdo > elemento filho a este \<ItemGroup > elemento:  
  
     **Para c#:**  
  
    ```xml  
    <Content Include="Properties\default.rd.xml" />  
    ```  
  
     **Para VB:**  
  
    ```xml  
    <Content Include="My Project\default.rd.xml" />  
    ```  
  
13. Localizar o \<ItemGroup > elemento inclui \<referência > elementos filhos para pacotes do NuGet. Anote os pacotes do NuGet que você usar porque será necessário baixá-los com o NuGet package manager depois que seu projeto é recarregado. Remover este \<ItemGroup > juntamente com seus filhos. Por exemplo, um projeto UWP poderia ter os seguintes pacotes NuGet que precisam ser removidos:  
  
    ```xml  
    <ItemGroup>  
        <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
          <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>  
          <Private>True</Private>  
        </Reference>  
        <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
          <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>  
          <Private>True</Private>  
        </Reference>  
        <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
          <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>  
          <Private>True</Private>  
        </Reference>  
        <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">  
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>  
          <Private>True</Private>  
        </Reference>  
        <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">  
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>  
          <Private>True</Private>  
        </Reference>  
      </ItemGroup>  
    ```  
  
14. Salve as alterações.  
  
15. Feche o arquivo. csproj ou. vbproj.  
  
16. Clique com botão direito no projeto no Gerenciador de soluções e escolha Recarregar projeto no menu de contexto. Todos os arquivos em seu projeto agora devem ser exibidos no Gerenciador de soluções.  
  
17. Use o Gerenciador de NuGet para adicionar os pacotes que você excluiu de volta em uma etapa anterior.  
  
     Agora, você precisa seguir as etapas para [atualizar os arquivos de manifesto de pacote](#PackageManifest) para todos os seus projetos do Windows Store 8.1 ou Windows Phone 8.1.  
  
##  <a name="MigrateCPlusPlus"></a> Migre seus aplicativos C++ Windows Store 8.1 ou Windows Phone 8.1 para usar a plataforma Universal do Windows  
  
#### <a name="migrate-your-c-project-files"></a>Migrar seus arquivos de projeto do C++  
  
1.  Para localizar qual plataforma Universal do Windows que você tiver instalado, abra essa pasta: **\Program arquivos (x86) \Windows Kits\10\Platforms\UAP**. Ela contém uma lista de pastas para cada plataforma Universal do Windows que está instalada. O nome da pasta é a versão da plataforma Universal do Windows que você instalou. Por exemplo, este dispositivo Windows 10 tem versão 10.0.10240.0 da plataforma Universal do Windows instalada.  
  
     ![Abra a pasta para exibir as versões instaladas](../misc/media/uap-uwpversions.png "UAP_UWPVersions")  
  
     Mais de uma versão da plataforma Universal do Windows pode ser instalada. É recomendável que você use a versão mais recente para seu aplicativo.  
  
2.  Abra a solução que contém seu aplicativo existente do C++ Windows Store 8.1 ou Windows Phone 8.1 no Visual Studio.  
  
     Clique em seu projeto existente no Gerenciador de soluções e selecione **descarregar projeto**. Depois que o projeto é descarregado, clique no arquivo de projeto novamente e escolha Editar o arquivo. vcxproj.  
  
     ![Direita&#45;clique em arquivo de projeto e escolha Editar](../misc/media/uap-editcplusproject.png "UAP_EditCPlusProject")  
  
3.  Localizar o \<PropertyGroup > elemento que contém o \<ApplicationTypeRevision > elemento com um valor de 8.1. Siga estas etapas para este \<PropertyGroup > elemento:  
  
    1.  Adicionar um \<WindowsTargetPlatformVersion > elemento e um \<WindowsTargetPlatformMinVersion > elemento e dê a eles o valor da versão de plataforma Universal do Windows que você instalou.  
  
    2.  Atualize o valor do elemento de ApplicationTypeRevision de 8.1 para 10.0.  
  
    3.  Altere o valor da \<MinimumVisualStudioVersion > elemento: 14.  
  
    4.  Adicionar um \<EnableDotNetNativeCompatibleProfile > elemento e defina seu valor como: true.  
  
    5.  A escala do ativo padrão para aplicativos Universal Windows é 200. Se seu projeto inclui ativos não dimensionados em 200, você precisará adicionar um \<UapDefaultAssetScale > elemento com o valor da escala de seus ativos para essa PropertyGroup. Saiba mais sobre [ativos e as escalas](http://msdn.microsoft.com/library/jj679352.aspx).  
  
    6.  Para Windows Phone projetos somente, altere o valor de \<ApplicationType > do Windows Phone para Windows Store.  
  
         Agora seu \<PropertyGroup > elemento deve ser semelhante a este exemplo:  
  
        ```xml  
        <PropertyGroup>  
            …  
                  <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>  
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>  
             <ApplicationType>Windows Store</ApplicationType>  
             <ApplicationTypeRevision>10.0</ApplicationTypeRevision>  
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>  
             <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>  
             <UapDefaultAssetScale>100</UapDefaultAssetScale>  
             …  
        </PropertyGroup>  
        ```  
  
4.  Altere todas as instâncias da \<PlatformToolset > elemento tenham o v140 de valor. Por exemplo:  
  
    ```xml  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">  
        <ConfigurationType>Application</ConfigurationType>  
        <UseDebugLibraries>false</UseDebugLibraries>  
        <WholeProgramOptimization>true</WholeProgramOptimization>  
        <PlatformToolset>v140</PlatformToolset>  
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>  
      </PropertyGroup>  
    ```  
  
5.  Cada restantes \<PropertyGroup > elemento, verifique se o elemento tem um atributo de condição com uma configuração de versão. Se ele faz, mas ele não contém um \<UseDotNetNativeToolchain > elemento, em seguida, adicione um. Defina o valor para o \<UseDotNetNativeToolchain > elemento como true, como este:  
  
    ```xml  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|X64'" Label="Configuration">  
        <ConfigurationType>Application</ConfigurationType>  
        <UseDebugLibraries>false</UseDebugLibraries>  
        <WholeProgramOptimization>true</WholeProgramOptimization>  
        <PlatformToolset>v140</PlatformToolset>  
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>  
      </PropertyGroup>  
  
    ```  
  
6.  Salve as alterações. Em seguida, feche o arquivo de projeto.  
  
7.  Clique com botão direito no arquivo de projeto no Gerenciador de soluções e escolha Recarregar projeto no menu de contexto. Todos os arquivos em seu projeto agora devem ser exibidos no Gerenciador de soluções.  
  
     Agora, você precisa seguir as etapas para [atualizar os arquivos de manifesto de pacote](#PackageManifest) para todos os seus projetos do Windows Store 8.1 ou Windows Phone 8.1.  
  
##  <a name="PackageManifest"></a> Atualize seu arquivo de manifesto de pacote para projetos de todos os Windows Store 8.1 ou Windows Phone 8.1  
 Você deve atualizar o arquivo de manifesto de pacote para cada projeto em sua solução.  
  
#### <a name="update-your-package-manifest-file"></a>Atualize seu arquivo de manifesto de pacote  
  
1. Abra o arquivo Package. appxmanifest no seu projeto. Você precisa editar o arquivo. AppX para cada um dos seus projetos da Windows Store e Windows Phone.  
  
2. Você precisa atualizar o \<pacote > elemento com os novos esquemas com base em seu tipo de projeto existente. Primeiro, remova os esquemas abaixo com base em se você tiver um projeto da Windows Store ou Windows Phone.  
  
    **ANTIGO para o projeto da Windows Store:** sua \<pacote > elemento será semelhante a esta.  
  
   ```xml  
   <Package  
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"     
       xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">  
  
   ```  
  
    **ANTIGO para o projeto do Windows Phone:** sua \<pacote > elemento será semelhante a esta.  
  
   ```xml  
   <Package  
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"     
   xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest"  
   xmlns:m3="http://schemas.microsoft.com/appx/2014/manifest"  
   xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest">  
   ```  
  
    **NOVO para a plataforma Universal do Windows:** adicione os esquemas abaixo ao seu \<pacote > elemento. Remova os prefixos de identificador de namespace associado de elementos para os esquemas que você acabou de ser removido. Atualize a propriedade IgnorableNamespaces para: uap mp. Seu novo \<pacote > elemento deve ser semelhante a esta.  
  
   ```xml  
   <Package  
       xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"  
       xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"  
       xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"  
      IgnorableNamespaces= "uap mp">  
  
   ```  
  
3. Adicionar um \<dependências > elemento filho para o \<pacote > elemento. Em seguida, adicione uma \<TargetDeviceFamily > elemento filho a este \<dependências > elemento com atributos de nome e MinVersion MaxVersionTested. Fornecer o valor de atributo de nome: universal. Conceda ao MinVersion e MaxVersionTested o valor da versão de plataforma Universal do Windows que você instalou. Esse elemento deve ser semelhante a este:  
  
   ```xml  
   <Dependencies>  
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10069.0" MaxVersionTested="10.0.10069.0" />  
   </Dependencies>  
   ```  
  
4. **Para Windows Store apenas:** você precisa adicionar uma \<mp:PhoneIdentity > elemento filho para o \<pacote > elemento. Adicione um atributo de PhoneProductId e um atributo PhonePublisherId. Defina o PhoneProductId para ter o mesmo valor que o atributo Name no \<identidade > elemento. Defina o valor de PhonePublishedId como: 00000000-0000-0000-0000-000000000000. Assim:  
  
   ```xml  
   <Identity Name="aa3815a1-2d97-4c71-8c99-578135b28cd8" Publisher="CN=xxxxxxxx" Version="1.0.0.0" />   
   <mp:PhoneIdentity PhoneProductId="aa3815a1-2d97-4c71-8c99-578135b28cd8" PhonePublisherId="00000000-0000-0000-0000-000000000000"/>  
   ```  
  
5. Encontre o \<pré-requisitos > elemento e excluir esse elemento e todos os elementos filho que ele tem.  
  
6. Adicione a **uap** namespace para o seguinte \<recursos > elementos: escala, DXFeatureLevel. Por exemplo:  
  
   ```xml  
   <Resources>  
     <Resource Language="en-us"/>  
    <Resource uap:Scale="180"/>  
    <Resource uap:DXFeatureLevel="dx11"/>  
   </Resources>  
  
   ```  
  
7. Adicione a **uap** namespace para o seguinte \<recurso > elementos: documentsLibrary, picturesLibrary, videosLibrary, musicLibrary, enterpriseAuthentication, sharedUserCertificates, removableStorage, compromissos e contatos. Por exemplo:  
  
   ```xml  
   <Capabilities>  
     <uap:Capability Name="documentsLibrary"/>  
     <uap:Capability Name="removableStorage"/>  
   </Capabilities>  
  
   ```  
  
8. Adicione a **uap** namespace para o \<VisualElements > elemento e qualquer um de seus elementos filho. Por exemplo:  
  
   ```xml  
   <uap:VisualElements  
       DisplayName="My WWA App"  
       Square150x150Logo="images/150x150.png"  
       Square44x44Logo="images/44x44.png"  
       Description="My WWA App"  
       BackgroundColor="#777777">  
     <uap:SplashScreen Image="images/splash.png"/>  
   </uap:VisualElements>  
  
   ```  
  
    **Aplica-se somente a Windows Store:** os nomes de tamanho de bloco foram alterados. Alterar os atributos no \<VisualElements > elemento para refletir a nova convergido tamanhos de bloco. 70x70 torna-se de 71 x 71, e 30 x 30 torna-se de 44 x 44.  
  
    **ANTIGO:** nomes de tamanho de bloco  
  
   ```xml  
   <m2:VisualElements  
       …  
       Square30x30Logo="Assets\SmallLogo.png"  
       …>  
    <m2:DefaultTile  
         …  
         Square70x70Logo="images/70x70.png">  
   </m2:VisualElements>  
  
   ```  
  
    **NOVO:** nomes de tamanho de bloco  
  
   ```xml  
   <uap:VisualElements  
       …  
       Square44x44Logo="Assets\SmallLogo.png"  
       …>  
    <uap:DefaultTile  
         …  
         Square71x71Logo="images/70x70.png">  
   </uap:VisualElements>  
  
   ```  
  
9. Adicione a **uap** namespace para o \<ApplicationContentUriRules > e todos os seus elementos filho. Por exemplo:  
  
    ```xml  
    <uap:ApplicationContentUriRules>  
      <uap:Rule Type="include" Match="https://www.microsoft.com/"/>  
      <uap:Rule Type="exclude" Match="*.pdf"/>  
    </uap:ApplicationContentUriRules>  
  
    ```  
  
10. Adicione a **uap** namespace para o seguinte \<extensão > elementos e todos os seus elementos filho: windows.accountPictureProvide, windows.alarm, windows.appointmentsProvider windows.autoPlayContent,  windows.autoPlayDevice, windows.cachedFileUpdate, windows.cameraSettings, windows.fileOpenPicker, windows.fileTypeAssociation, windows.fileSavePicke, windows.lockScreenCall, windows.printTaskSettings, windows.protocol, windows.search, sharetarget. Por exemplo:  
  
    ```xml  
    <Extensions>  
      <uap:Extension Category="windows.alarm"/>  
      <uap:Extension Category="windows.search" EntryPoint="MyActivateableClassId.baz"/>  
      <uap:Extension Category="windows.protocol">  
        <uap:Protocol Name="mailto" DesiredView="useHalf">  
         <uap:DisplayName>MailTo Protocol</uap:DisplayName>  
        </uap:Protocol>  
      </uap:Extension>  
    </Extensions>  
  
    ```  
  
11. Adicione a **uap** namespace para tarefas em segundo plano do tipo chatMessageNotification. Por exemplo:  
  
    ```xml  
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">  
     <BackgroundTasks ServerName="MyBackgroundTasks">  
        <uap:Task Type="chatMessageNotification"/>  
      </BackgroundTasks>  
    </Extension>  
  
    ```  
  
12. Altere as dependências de estrutura. Adicionar um nome de publicador a todos os \<PackageDependency > elementos, e especifique um MinVersion se ela já não estiver especificada.  
  
     **ANTIGO:** \<PackageDependency > elemento  
  
    ```xml  
    <Dependencies>  
     <PackageDependency Name="Microsoft.VCLibs.120.00" />  
    </Dependencies>  
  
    ```  
  
     **NOVO:** \<PackageDependency > elemento  
  
    ```xml  
    <Dependencies>  
     <PackageDependency  
          Name="Microsoft.VCLibs.120.00"  
          Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"  
          MinVersion="12.0.30113.0" />  
    </Dependencies>  
  
    ```  
  
     Use os valores apropriados do publicador e MinVersion para a estrutura real que você está usando. Lembre-se de que esses nomes poderá mudar para o Windows 10.  
  
13. Substitua as tarefas de tipo de plano de fundo gattCharacteristicNotification e rfcommConnection com uma tarefa de tipo de Bluetooth. Por exemplo:  
  
     **ANTIGO:**  
  
    ```xml  
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">  
    <BackgroundTasks ServerName="MyBackgroundTasks">  
                <Task Type="rfcommConnection"/>  
               <Task Type="gattCharacteristicNotification"/>  
    </BackgroundTasks>  
    </Extension>  
    ```  
  
     **NOVO:** com a tarefa de tipo de Bluetooth.  
  
    ```xml  
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">  
    <BackgroundTasks ServerName="MyBackgroundTasks">  
               <Task Type="bluetooth"/>  
    </BackgroundTasks>  
    </Extension>  
    ```  
  
14. Substitua o bluetooth.rfcomm de recursos do dispositivo Bluetooth e a bluetooth.genericAttributeProfile com um recurso genérico do Bluetooth. Por exemplo:  
  
     **ANTIGO:**  
  
    ```xml  
    <Capabilities>  
      <m2:DeviceCapability Name="bluetooth.rfcomm">  
        <m2:Device Id="any">  
         <m2:Function Type="serviceId:34B1CF4D-1069-4AD6-89B6-E161D79BE4D8"/>  
        </m2:Device>  
      </m2:DeviceCapability>  
      <m2:DeviceCapability Name="bluetooth.genericAttributeProfile">  
        <m2:Device Id="any">  
         <m2:Function Type="name:heartRate"/>  
        </m2:Device>  
      </m2:DeviceCapability>  
    </Capabilities>  
    ```  
  
     **NOVO:** substituído por um recurso genérico do Bluetooth.  
  
    ```xml  
    <Capabilities>  
      <uap:DeviceCapability Name="bluetooth"/>  
    </Capabilities>  
  
    ```  
  
15. Remova todos os elementos preteridos.  
  
    1. Esses atributos para \<VisualElements > foram preteridas e devem ser removidos:  
  
       - O \<VisualElements > atributos: ForegroundText, ToastCapable  
  
       - O \<DefaultTile > DefaultSize de atributo  
  
       - O \<ApplicationView > elemento  
  
         Por exemplo:  
  
       ```xml  
       <m2:VisualElements  
           …  
           ForegroundText="dark"  
           ToastCapable="true">  
       <m2:DefaultTile DefaultSize="square150x150Logo"/>  
         <m2:ApplicationView MinWidth="width320"/>  
       </m2:VisualElements>  
  
       ```  
  
    2. Remova Windows.contact e extensões de windows.contactPicker e todos os elementos sob essas extensões.  
  
16. Salve o arquivo Package. appxmanifest. Em seguida, feche o Visual Studio.  
  
17. Você precisará remover alguns arquivos ocultos, antes de poder reabrir sua solução.  
  
    1.  Abra o Explorador de arquivos, clique em **modo de exibição** na barra de ferramentas e selecione **itens ocultos** e **extensões de nome de arquivo**. Abra essa pasta em seu computador: \<caminho para o local de sua solução >\\VS\\\v14 {nome do projeto}. Se houver um arquivo com uma extensão de arquivo. suo, em seguida, excluí-lo.  
  
    2.  Agora volte para a pasta onde se encontra sua solução. Abra as pastas para projetos que existem em sua solução. Se um arquivo dentro de qualquer uma dessas pastas de projeto tiver um. csproj ou. vbproj extensão, em seguida, excluí-lo.  
  
         Agora você pode reabrir a sua solução no Visual Studio. Você está pronto para codificar, compilar e depurar seu aplicativo usando a plataforma Universal do Windows.  
  
         Saiba como [adaptar seu código](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx) podem aproveitar o que há de novo com a plataforma Universal do Windows.  
  
##  <a name="PreviousVersions"></a> Alterações necessárias para os aplicativos Universal Windows existentes criados com o Visual Studio 2015 RC  
 Se você tiver criado aplicativos universais do Windows 10 com o Visual Studio 2015 RC, você precisará redirecionar seu projeto para usar a versão da plataforma Universal do Windows instalado com a versão mais recente do Visual Studio 2015. Não há suporte para qualquer versão anterior. As alterações necessárias são diferentes dependendo do idioma usado para criar seu aplicativo:  
  
-   [Aplicativos do C em c# /VB](#RCUpdate10CSharp)  
  
-   [Aplicativos em C++](#RCUpdate10CPlusPlus)  
  
###  <a name="RCUpdate10CSharp"></a> Atualize seus projetos em c# /VB de C para usar a última plataforma Universal do Windows  
 Quando você abre a solução para seu aplicativo existente, você verá que seu aplicativo requer uma atualização:  
  
 ![Exibir o projeto no Gerenciador de soluções](../misc/media/uwp-updaterequired.png "UWP_UpdateRequired")  
  
 Se você optar por recarregar esse projeto no Gerenciador de soluções, você verá essa caixa de diálogo:  
  
 ![Redirecionar seu aplicativo para usar o SDK correto](../misc/media/missingsdkforuap.png "MissingSDKforUAP")  
  
 Porque o SDK da plataforma Windows Universal para o seu projeto está agora sem suporte, você não poderá instalá-lo. Basta clicar em Okey e, em seguida, siga as etapas abaixo.  
  
##### <a name="update-your-cvb-projects-to-use-the-latest-universal-windows-platform"></a>Atualize seus projetos em c# /VB de C para usar a última plataforma Universal do Windows  
  
1. Para localizar qual plataforma Universal do Windows que você tiver instalado, abra essa pasta: **\Program arquivos (x86) \Windows Kits\10\Platforms\UAP**. Ela contém uma lista de pastas para cada plataforma Universal do Windows que está instalada. O nome da pasta é a versão da plataforma Universal do Windows que você instalou. Por exemplo, este dispositivo Windows 10 tem versão 10.0.10240.0 da plataforma Universal do Windows instalada.  
  
    ![Abra a pasta para exibir as versões instaladas](../misc/media/uap-uwpversions.png "UAP_UWPVersions")  
  
    Mais de uma versão da plataforma Universal do Windows pode ser instalada. É recomendável que você use a versão mais recente para seu aplicativo.  
  
2. Usando o Explorador de arquivos, vá para a pasta em que o seu projeto UWP está armazenado. Exclua o arquivo Packages. config e criar um novo arquivo. JSON nesta pasta. Nomeie o arquivo: Project. JSON e, em seguida, adicione o seguinte conteúdo para este arquivo:  
  
   ```json  
  
   {  
     "dependencies": {  
       "Microsoft.ApplicationInsights": "1.0.0",  
       "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",  
       "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",  
       "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"  
     },  
     "frameworks": {  
       "uap10.0": {}  
     },  
     "runtimes": {  
       "win10-arm": {},  
       "win10-arm-aot": {},  
       "win10-x86": {},  
       "win10-x86-aot": {},  
       "win10-x64": {},  
       "win10-x64-aot": {}  
     }  
   }  
  
   ```  
  
3. Com o Visual Studio, abra a solução que contém seu aplicativo do C em c# /VB Windows Universal. Você verá que o arquivo de projeto (arquivo. csproj ou. vbproj) precisa ser atualizado. O arquivo de projeto com o botão direito e escolha Editar esse arquivo.  
  
    ![Com o botão direito do mouse no projeto e escolha Editar](../misc/media/uap-editproject.png "UAP_EditProject")  
  
4. Localizar o \<PropertyGroup > elemento que contém o \<TargetPlatformVersion > e \<TargetPlatformMinVersion > elementos. Alterar o valor existente do \<TargetPlatformVersion > e \<TargetPlatformMinVersion > elementos para ser a mesma versão da plataforma Universal do Windows que você instalou.  
  
    A escala do ativo padrão para aplicativos Universal Windows é 200. Projetos criados com ativos do Visual Studio 2015 RC incluídos dimensionados em 100, você precisará adicionar um \<UapDefaultAssetScale > elemento com um valor de 100 para este PropertyGroup. Saiba mais sobre [ativos e as escalas](http://msdn.microsoft.com/library/jj679352.aspx).  
  
5. Se você tiver adicionado todas as referências a UWP SDKs de extensão (por exemplo: o Windows Mobile SDK), você precisará atualizar a versão do SDK. Por exemplo, isso \<SDKReference > elemento:  
  
   ```xml  
   <SDKReference Include="WindowsMobile, Version=10.0.0.1">  
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>  
   </SDKReference>  
  
   ```  
  
    Deve ser alterada para isso:  
  
   ```xml  
   <SDKReference Include="WindowsMobile, Version=10.0.10240.0">  
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>  
   </SDKReference>  
  
   ```  
  
6. Encontre o \<destino > elemento com um atributo de nome que tem o valor: EnsureNuGetPackageBuildImports. Exclua este elemento e todos os seus filhos.  
  
   ```xml  
   <Target Name="EnsureNuGetPackageBuildImports" BeforeTargets="PrepareForBuild">  
       <PropertyGroup>  
         <ErrorText>This project references NuGet package(s) that are missing on this computer. Use NuGet Package Restore to download them.  For more information, see http://go.microsoft.com/fwlink/?LinkID=322105. The missing file is {0}.</ErrorText>  
       </PropertyGroup>  
       <Error Condition="!Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets'))" />  
       <Error Condition="!Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets'))" />  
   </Target>  
   ```  
  
7. Localize e exclua o \<importação > elementos com atributos de projeto e a condição que fazem referência Tracing e Microsoft. applicationinsights, como este:  
  
   ```xml  
   <Import Project="..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets" Condition="Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" />  
   <Import Project="..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets" Condition="Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" />  
  
   ```  
  
8. Localizar o \<ItemGroup > que tem \<referência > elementos filhos para pacotes do NuGet. Anote os pacotes do NuGet que são referenciados, pois você precisará dessas informações para uma etapa futura. Uma diferença significativa entre o formato de projeto do Windows 10 entre o Visual Studio 2015 RC e o Visual Studio 2015 RTM é que o usa o formato do RTM [NuGet](http://docs.nuget.org/) versão 3.  
  
    Remover o \<ItemGroup > e todos os seus filhos. Por exemplo, um projeto UWP criado com o Visual Studio RC terá os seguintes pacotes NuGet que precisam ser removidos:  
  
   ```xml  
   <ItemGroup>  
       <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
         <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>  
         <Private>True</Private>  
       </Reference>  
       <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
         <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>  
         <Private>True</Private>  
       </Reference>  
       <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">  
         <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>  
         <Private>True</Private>  
       </Reference>  
       <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">  
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>  
         <Private>True</Private>  
       </Reference>  
       <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">  
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>  
         <Private>True</Private>  
       </Reference>  
     </ItemGroup>  
  
   ```  
  
9. Localizar o \<ItemGroup > elemento que contém um \<AppxManifest > elemento. Se não houver um \<None > elemento com um atributo de inclusão definida como: Packages. config, excluí-lo. Além disso, adicione um \<None > elemento com uma inclusão de atributos e defina seu valor como: Project. JSON.  
  
10. Salve as alterações. Em seguida, feche o arquivo de projeto.  
  
11. Clique com botão direito no arquivo de projeto no Gerenciador de soluções e escolha Recarregar projeto no menu de contexto. Todos os arquivos em seu projeto agora devem ser exibidos no Gerenciador de soluções.  
  
12. Selecione o arquivo applicationinsights. config no Gerenciador de soluções e abra suas propriedades. Defina a propriedade de ação de compilação para "Conteúdo" e a cópia à propriedade de diretório de saída para "Copiar se mais recente".  
  
13. Abra o arquivo Package. appxmanifest no seu projeto.  
  
    1.  Encontre o \<TargetDeviceFamily > elemento. Altere seus atributos MinVersion e MaxVersionTested para corresponder à versão de plataforma Universal do Windows que você instalou. Assim:  
  
        ```xml  
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />  
        ```  
  
    2.  Salve as alterações.  
  
14. Use o Gerenciador de NuGet para adicionar os pacotes que você excluiu na etapa anterior. Uma diferença significativa entre o formato de projeto do Windows 10 entre o Visual Studio 2015 RC e o Visual Studio 2015 RTM é que o usa o formato do RTM [NuGet](http://docs.nuget.org/) versão 3.  
  
    Agora você pode codificar, compilar e depurar seu aplicativo.  
  
    Se você tiver projetos de teste de unidade para seus aplicativos Windows Universal, você também deve seguir [essas etapas](#MigrateUnitTest).  
  
###  <a name="RCUpdate10CPlusPlus"></a> Atualizar seus projetos do C++ para usar a última plataforma Universal do Windows  
  
1.  Para localizar qual plataforma Universal do Windows que você tiver instalado, abra essa pasta: **\Program arquivos (x86) \Windows Kits\10\Platforms\UAP**. Ela contém uma lista de pastas para cada plataforma Universal do Windows que está instalada. O nome da pasta é a versão da plataforma Universal do Windows que você instalou. Por exemplo, este dispositivo Windows 10 tem versão 10.0.10240.0 da plataforma Universal do Windows instalada.  
  
     ![Abra a pasta para exibir as versões instaladas](../misc/media/uap-uwpversions.png "UAP_UWPVersions")  
  
     Mais de uma versão da plataforma Universal do Windows pode ser instalada. É recomendável que você use a versão mais recente para seu aplicativo.  
  
2.  Abra a solução que contém seu aplicativo Universal do Windows C++. O arquivo de projeto. vcxproj com o botão direito e escolha a descarregar o arquivo de projeto. Depois que o projeto foi descarregado, clique no arquivo de projeto novamente e escolha para editá-lo.  
  
     ![Descarregue o projeto e, em seguida, edite o arquivo de projeto](../misc/media/uap-editearliercplus.png "UAP_EditEarlierCPlus")  
  
3.  Encontrar alguma \<PropertyGroup > elementos que não contêm um atributo Condition, mas contêm um \<ApplicationTypeRevision > elemento. Atualize o valor de ApplicationTypeRevision de 8.2 para 10.0. Adicionar um \<WindowsTargetPlatformVersion > e um \<WindowsTargetPlatformMinVersion > elemento e defina seus valores como o valor da versão de plataforma Universal do Windows que você instalou.  
  
     Adicionar um \<EnableDotNetNativeCompatibleProfile > elemento e defina seu valor como true se o elemento não existir.  
  
     A escala do ativo padrão para aplicativos Universal Windows é 200. Projetos criados com ativos do Visual Studio 2015 RC incluídos dimensionados em 100, você precisará adicionar um \<UapDefaultAssetScale > elemento com um valor de 100 para este PropertyGroup. Saiba mais sobre [ativos e as escalas](http://msdn.microsoft.com/library/jj679352.aspx).  
  
     Portanto, esse \<PropertyGroup > elemento agora será semelhante a esta:  
  
    ```xml  
    <PropertyGroup Label="Globals">  
        …  
        <MinimumVisualStudioVersion>14.0</MinimumVisualStudioVersion>  
        <ApplicationType>Windows Store</ApplicationType>  
        <ApplicationTypeRevision>10.0</ApplicationTypeRevision>  
        <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>  
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>  
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>  
        <UapDefaultAssetScale>100</UapDefaultAssetScale>  
      </PropertyGroup>  
  
    ```  
  
4.  Cada restantes \<PropertyGroup > elemento, verifique se o elemento tem um atributo de condição com uma configuração de versão. Se ele faz, mas ele não contém um \<UseDotNetNativeToolchain > elemento, em seguida, adicione um. Defina o valor para o \<UseDotNetNativeToolchain > elemento como true, como este:  
  
    ```xml  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">  
        <ConfigurationType>Application</ConfigurationType>  
        <UseDebugLibraries>false</UseDebugLibraries>  
        <WholeProgramOptimization>true</WholeProgramOptimization>  
        <PlatformToolset>v140</PlatformToolset>  
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>  
      </PropertyGroup>  
  
    ```  
  
5.  Você precisa atualizar o \<EnableDotNetNativeCompatibleProfile > elemento e o \<UseDotNetNativeToolchain > elemento para habilitar o .NET nativo, mas o .NET Native não está habilitado nos modelos do C++.  
  
     Salve as alterações. Em seguida, feche o arquivo de projeto.  
  
6.  Clique com botão direito no arquivo de projeto no Gerenciador de soluções e escolha Recarregar projeto no menu de contexto. Todos os arquivos em seu projeto agora devem ser exibidos no Gerenciador de soluções.  
  
7.  Abra o arquivo Package. appxmanifest no seu projeto.  
  
    1.  Encontre o \<TargetDeviceFamily > elemento. Altere seus atributos MinVersion e MaxVersionTested para corresponder à versão de plataforma Universal do Windows que você instalou. Assim:  
  
        ```xml  
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />  
        ```  
  
    2.  Salve as alterações.  
  
         Agora você pode codificar, compilar e depurar seu aplicativo.  
  
         Se você tiver projetos de teste de unidade para seus aplicativos Windows Universal, você também deve seguir [essas etapas](#MigrateUnitTest).  
  
##  <a name="MigrateUnitTest"></a> Alterações necessárias para projetos de teste de unidade existentes para aplicativos Universal Windows criados com o Visual Studio 2015 RC  
 Se você criou a unidade de projetos de teste para aplicativos universais do Windows 10 com o Visual Studio 2015 RC, você precisa fazer essas alterações adicionais ao seu projeto de teste de arquivos para usar esses projetos com a versão mais recente do Visual Studio 2015. As alterações necessárias são diferentes dependendo do idioma usado para criar seu aplicativo:  
  
-   [Aplicativos do C em c# /VB](#UnitTestRCUpdate10CSharp)  
  
-   [Aplicativos em C++](#UnitTestRCUpdate10CPlusPlus)  
  
###  <a name="UnitTestRCUpdate10CSharp"></a> Atualizar seus projetos de teste de unidade do C em c# /VB  
  
1. Com o Visual Studio, abra a solução que contém seu projeto de teste de unidade em c# /VB C. Altere o valor da \<OuttputType > elemento: AppContainerExe.  
  
   ```xml  
  
   <OutputType>AppContainerExe</OutputType>  
  
   ```  
  
2. Substitua esse elemento \<EnableCoreRuntime > false\</EnableCoreRuntime > com o seguinte elemento:  
  
   ```xml  
  
   <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>  
  
   ```  
  
3. Remova as seguintes linhas:  
  
   ```xml  
  
   <PropertyGroup>  
       <AppXPackage>True</AppXPackage>  
       <AppxPackageIncludePrivateSymbols>true</AppxPackageIncludePrivateSymbols>  
    </PropertyGroup>  
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">  
    <PlatformTarget>AnyCPU</PlatformTarget>  
    <DebugSymbols>true</DebugSymbols>  
    <DebugType>full</DebugType>  
    <Optimize>false</Optimize>  
    <OutputPath>bin\Debug\</OutputPath>  
    <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>  
    <ErrorReport>prompt</ErrorReport>  
    <WarningLevel>4</WarningLevel>  
    </PropertyGroup>  
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">  
       <PlatformTarget>AnyCPU</PlatformTarget>  
       <DebugType>pdbonly</DebugType>  
       <Optimize>true</Optimize>  
       <OutputPath>bin\Release\</OutputPath>  
       <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>  
       <ErrorReport>prompt</ErrorReport>  
       <WarningLevel>4</WarningLevel>  
    </PropertyGroup>  
  
   ```  
  
4. Adicione esse elemento \<UseDotNetNativeToolchain > true\</UseDotNetNativeToolchain > como um elemento filho a esses grupos de propriedade:  
  
   ```xml  
  
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|ARM'">  
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X86'">  
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X64'">  
  
   ```  
  
5. Excluir o seguinte \<ItemGroup > elementos:  
  
   ```xml  
  
   <ItemGroup>  
      <Compile Include="Properties\AssemblyInfo.cs" />  
      <Compile Include="UnitTest.cs" />  
   </ItemGroup>  
   <ItemGroup>  
      <AppxManifest Include="Package.appxmanifest">  
         <SubType>Designer</SubType>  
      </AppxManifest>  
      <None Include="packages.config" />  
      <None Include="UnitTestProject1_TemporaryKey.pfx" />  
   </ItemGroup>  
   <ItemGroup>  
      <Content Include="Properties\Default.rd.xml" />  
      <Content Include="Assets\Logo.scale-240.png" />  
      <Content Include="Assets\SmallLogo.scale-240.png" />  
      <Content Include="Assets\SplashScreen.scale-240.png" />  
      <Content Include="Assets\Square71x71Logo.scale-240.png" />  
      <Content Include="Assets\StoreLogo.scale-240.png" />  
      <Content Include="Assets\WideLogo.scale-240.png" />  
   </ItemGroup>  
  
   ```  
  
    Substitua-os com estes elementos:  
  
   ```xml  
  
   <ItemGroup>  
      <Compile Include="Properties\AssemblyInfo.cs" />  
      <Compile Include="UnitTestApp.xaml.cs">  
         <DependentUpon>UnitTestApp.xaml</DependentUpon>  
      </Compile>  
      <Compile Include="UnitTest.cs" />  
   </ItemGroup>  
   <ItemGroup>  
      <ApplicationDefinition Include="UnitTestApp.xaml">  
         <Generator>MSBuild:Compile</Generator>  
         <SubType>Designer</SubType>  
      </ApplicationDefinition>  
   </ItemGroup>  
   <ItemGroup>  
      <AppxManifest Include="Package.appxmanifest">  
         <SubType>Designer</SubType>  
      </AppxManifest>  
      <None Include="UnitTestProject1_TemporaryKey.pfx" />  
   </ItemGroup>  
   <ItemGroup>  
      <Content Include="Properties\UnitTestApp.rd.xml" />  
      <Content Include="Assets\LockScreenLogo.scale-200.png" />  
      <Content Include="Assets\SplashScreen.scale-200.png" />  
      <Content Include="Assets\Square150x150Logo.scale-200.png" />  
      <Content Include="Assets\Square44x44Logo.scale-200.png" />  
      <Content Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />  
      <Content Include="Assets\StoreLogo.png" />  
      <Content Include="Assets\Wide310x150Logo.scale-200.png" />  
   </ItemGroup>  
   ```  
  
6. Criar um novo projeto de teste de unidade e copie os arquivos UnitTestApp.xaml e UnitTestApp.xaml.cs desse novo projeto ao seu projeto de teste de unidade existentes que você está atualizando.  
  
7. Copie o arquivo de UnitTestApp.rd.xml da pasta propriedades do novo projeto de teste de unidade para a pasta de propriedades do seu projeto de teste de unidade existentes que você está atualizando.  
  
8. Abra o arquivo Package. appxmanifest no seu projeto. Em seguida, exclua esses elementos dela:  
  
   ```xml  
  
   <Applications>  
      <Application Id="vstest.executionengine.universal.App"  
            Executable="vstest.executionengine.appcontainer.uap.exe"  
            EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">  
         <uap:VisualElements  
            DisplayName="UnitTestProject1"  
            Square150x150Logo="Assets\Logo.png"  
            Square44x44Logo="Assets\SmallLogo.png"  
            Description="UnitTestProject1"  
            BackgroundColor="#464646">  
            <uap:SplashScreen Image="Assets\SplashScreen.png" />  
         </uap:VisualElements>  
      </Application>  
   </Applications>  
   <Capabilities>  
      <Capability Name="internetClientServer" />  
   </Capabilities>  
   ```  
  
    Substitua esses elementos excluídos com os seguintes elementos. Use o valor apropriado para ProjectName com base no nome do seu projeto, em vez de UnitTestProject1 nos elementos abaixo:  
  
   ```xml  
  
   <Applications>  
      <Application Id="vstest.executionengine.universal.App"   
            Executable="$targetnametoken$.exe"  
            EntryPoint="UnitTestProject1.App">  
         <uap:VisualElements  
               DisplayName="UnitTestProject1"  
               Square150x150Logo="Assets\Square150x150Logo.png"  
               Square44x44Logo="Assets\Square44x44Logo.png"  
               Description="UnitTestProject1"  
               BackgroundColor="transparent">  
            <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>  
            <uap:SplashScreen Image="Assets\SplashScreen.png" />  
         </uap:VisualElements>  
      </Application>  
   </Applications>  
   <Capabilities>  
      <Capability Name="internetClient" />  
   </Capabilities>  
   ```  
  
   Agora você pode executar seus testes de unidade.  
  
###  <a name="UnitTestRCUpdate10CPlusPlus"></a> Atualizar seus projetos do C++ para usar a última plataforma Universal do Windows  
  
1.  Com o Visual Studio, abra a solução que contém seu projeto de teste de unidade do C++. Remova os seguintes elementos:  
  
    ```xml  
  
    <TestApplication>true</TestApplication>  
    <AppxPackage>True</AppxPackage>  
    <CppWindowsStoreUnitTestLibraryType>true</CppWindowsStoreUnitTestLibraryType>  
    <EnableCoreRuntime>false</EnableCoreRuntime>  
  
    ```  
  
2.  Adicione o seguinte \<ProjectConfiguration > elementos abaixo desse elemento \<ItemGroup rótulo = "ProjectConfigurations" > se ainda não estiverem nesse preenchimento:  
  
    ```xml  
  
    <ProjectConfiguration Include="Debug|x64">  
       <Configuration>Debug</Configuration>  
       <Platform>x64</Platform>  
    </ProjectConfiguration>  
    <ProjectConfiguration Include="Release|x64">  
       <Configuration>Release</Configuration>  
       <Platform>x64</Platform>  
    </ProjectConfiguration>  
  
    ```  
  
3.  Substitua todas as ocorrências desse elemento:  
  
    ```xml  
  
    <ConfigurationType>DynamicLibrary</ConfigurationType>  
  
    ```  
  
     Com isso:  
  
    ```xml  
  
    <ConfigurationType>Application</ConfigurationType>  
  
    ```  
  
4.  Adicione estas \<PropertyGroup > elementos se elas não ainda estiverem no arquivo:  
  
    ```xml  
  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'" Label="Configuration">  
       <ConfigurationType>Application</ConfigurationType>  
       <UseDebugLibraries>true</UseDebugLibraries>  
       <PlatformToolset>v140</PlatformToolset>  
    </PropertyGroup>  
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'" Label="Configuration">  
       <ConfigurationType>Application</ConfigurationType>  
       <UseDebugLibraries>false</UseDebugLibraries>  
       <WholeProgramOptimization>true</WholeProgramOptimization>  
       <PlatformToolset>v140</PlatformToolset>  
       <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>  
    </PropertyGroup>  
  
    ```  
  
5.  Substitua todas as ocorrências desse elemento:  
  
    ```xml  
  
    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>  
    ```  
  
     Com isso:  
  
    ```xml  
  
    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>  
  
    ```  
  
6.  Substitua todas as ocorrências desse elemento:  
  
    ```xml  
  
    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\Lib;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>  
  
    ```  
  
     Com isso:  
  
    ```xml  
  
    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>  
  
    ```  
  
7.  Adicione estas \<ItemDefinitionGroup > elementos na seção que já contém outros \<ItemDefinitionGroup > elementos:  
  
    ```xml  
  
    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">  
       <ClCompile>  
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>  
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>  
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%     (AdditionalIncludeDirectories)</AdditionalIncludeDirectories>  
       </ClCompile>  
    <Link>  
       <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>  
    </Link>  
    </ItemDefinitionGroup>  
    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">  
       <ClCompile>  
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>  
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>  
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>  
       </ClCompile>  
       <Link>  
          <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>  
       </Link>  
    </ItemDefinitionGroup>  
  
    ```  
  
8.  Excluir o seguinte \< ItemGroup > elemento:  
  
    ```xml  
  
    <ItemGroup>  
       <Image Include="Assets\Logo.scale-100.png" />  
       <Image Include="Assets\SmallLogo.scale-100.png" />  
       <Image Include="Assets\StoreLogo.scale-100.png" />  
       <Image Include="Assets\SplashScreen.scale-100.png" />  
       <Image Include="Assets\WideLogo.scale-100.png" />  
    </ItemGroup>  
  
    ```  
  
     Substituir por isso \<ItemGroup > elemento:  
  
    ```xml  
  
    <ItemGroup>  
       <Image Include="Assets\LockScreenLogo.scale-200.png" />  
       <Image Include="Assets\SplashScreen.scale-200.png" />  
       <Image Include="Assets\Square44x44Logo.scale-200.png" />  
       <Image Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />  
       <Image Include="Assets\Square150x150Logo.scale-200.png" />  
       <Image Include="Assets\StoreLogo.png" />  
       <Image Include="Assets\Wide310x150Logo.scale-200.png" />  
    </ItemGroup>  
  
    ```  
  
9. Excluir o seguinte \< ItemGroup > elemento:  
  
    ```xml  
  
    <ItemGroup>  
       <ClInclude Include="pch.h" />  
    </ItemGroup>  
    ```  
  
     Substitua-o com essas \<ItemGroup > elementos:  
  
    ```xml  
  
    <ItemGroup>  
       <ClInclude Include="pch.h" />  
       <ClInclude Include="UnitTestApp.xaml.h">  
          <DependentUpon>UnitTestApp.xaml</DependentUpon>  
       </ClInclude>  
    </ItemGroup>  
    <ItemGroup>  
       <ApplicationDefinition Include="UnitTestApp.xaml">  
          <SubType>Designer</SubType>  
       </ApplicationDefinition>  
    </ItemGroup>  
  
    ```  
  
10. Exclua o seguinte elemento:  
  
    ```xml  
    <ClCompile Include="UnitTest.cpp"/>  
    ```  
  
     Substitua-o com essas \<CICompile > elementos:  
  
    ```xml  
  
    <ClCompile Include="UnitTestApp.xaml.cpp">  
       <DependentUpon>UnitTestApp.xaml</DependentUpon>  
    </ClCompile>  
    <ClCompile Include="UnitTest.cpp"/>  
  
    ```  
  
11. Adicione este elemento:  
  
    ```xml  
    <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />  
    ```  
  
     Acima desse elemento no arquivo:  
  
    ```xml  
  
    <ItemGroup>  
       <Xml Include="UnitTestApp.rd.xml" />  
    </ItemGroup>  
    ```  
  
12. Criar um novo projeto de C++ de teste de unidade e copie os arquivos de UnitTestApp.xaml, UnitTestApp.xaml.cpp, UnitTestApp.xaml.h e UnitTestApp.rd.xml desse projeto ao seu projeto existente que você está atualizando.  
  
13. Abra o arquivo Package. appxmanifest no seu projeto. Em seguida, exclua esses elementos dela:  
  
    ```xml  
  
    <Applications>  
       <Application Id="vstest.executionengine.universal.App"  
             Executable="vstest.executionengine.appcontainer.uap.exe"  
             EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">  
          <uap:VisualElements  
             DisplayName="UnitTestProject1"  
             Square150x150Logo="Assets\Logo.png"  
             Square44x44Logo="Assets\SmallLogo.png"  
             Description="UnitTestProject1"  
             BackgroundColor="#464646">  
             <uap:SplashScreen Image="Assets\SplashScreen.png" />  
          </uap:VisualElements>  
       </Application>  
    </Applications>  
    <Capabilities>  
       <Capability Name="internetClientServer" />  
    </Capabilities>  
  
    ```  
  
     Substitua esses elementos excluídos com os seguintes elementos. Use o valor apropriado para ProjectName com base no nome do seu projeto, em vez de UnitTestProject1 nos elementos abaixo:  
  
    ```xml  
  
    <Applications>  
       <Application Id="vstest.executionengine.universal.App"   
                Executable="$targetnametoken$.exe"  
                EntryPoint="UnitTestProject1.App">  
          <uap:VisualElements  
                DisplayName="UnitTestProject1"  
                Square150x150Logo="Assets\Square150x150Logo.png"  
                Square44x44Logo="Assets\Square44x44Logo.png"  
                Description="UnitTestProject1"  
                BackgroundColor="transparent">  
                <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>  
                <uap:SplashScreen Image="Assets\SplashScreen.png" />  
          </uap:VisualElements>  
       </Application>  
    </Applications>  
    <Capabilities>  
       <Capability Name="internetClient" />  
    </Capabilities>  
  
    ```
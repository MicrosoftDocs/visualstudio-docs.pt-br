---
title: 'Passo a passo: Criar um ambiente de build de vários computadores'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building on multiple computers
- build environment, MSBuild
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2dc88c3861adb8b1d9f239d6ceedee2b76bc2e25
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951607"
---
# <a name="walkthrough-create-a-multiple-computer-build-environment"></a>Passo a passo: Criar um ambiente de build de vários computadores

Você pode criar um ambiente de build na sua organização instalando o Visual Studio em um computador host e, em seguida, copiando vários arquivos e configurações para outro computador de modo que ele possa participar de compilações. Você não precisa instalar o Visual Studio no outro computador.

Este documento não confere direitos para redistribuir o software externamente nem para fornecer ambientes de build a terceiros.

> Aviso de isenção de responsabilidade<br /><br /> Este documento é fornecido "no estado em que se encontra". Embora tenhamos testado as etapas descritas, não é possível testar exaustivamente cada configuração. Tentaremos manter o documento atualizado com quaisquer informações adicionais que obtivermos. As informações e as exibições expressas neste documento, incluindo a URL e outras referências a sites da Internet, podem mudar sem aviso prévio. A Microsoft não oferece nenhuma garantia, explícita ou implícita, quanto às informações fornecidas aqui. Você assume o risco de utilizá-las.<br /><br /> Este documento não lhe concede nenhum direito legal à nenhuma propriedade intelectual de nenhum produto da Microsoft. Você pode copiar e usar este documento para fins internos de referência.<br /><br /> Você não tem obrigação de enviar à Microsoft nenhuma sugestão ou comentário ("Comentários") com relação a este documento. No entanto, qualquer Comentário que você forneça voluntariamente poderá ser usado em Produtos Microsoft e especificações relacionadas ou outra documentação (coletivamente, "Ofertas Microsoft"), que, por sua vez, poderão ser utilizados por terceiros para desenvolver seus próprios produtos. Portanto, ao fornecer Comentários sobre a Microsoft em qualquer versão deste documento ou das Ofertas da Microsoft aos quais elas se aplicam, você concorda que: (a) a Microsoft pode livremente usar, reproduzir, licenciar, distribuir e comercializar de outra forma seus Comentários em qualquer Oferta da Microsoft; (b) você também concede a terceiros, sem custos, somente os direitos de patente necessários para permitir que outros produtos usem ou interajam com quaisquer partes específicas de um Produto Microsoft que incorporem Seus Comentários; e (c) você não fornecerá à Microsoft nenhum Comentário (i) que você tenha motivo para acreditar que esteja sujeito a qualquer declaração ou direito de patente, direitos autorais ou outra propriedade intelectual de terceiros; ou (ii) sujeito a termos de licença que busquem exigir que qualquer Oferta da Microsoft que incorpore ou seja derivada desses Comentários, ou outra propriedade intelectual da Microsoft, seja licenciada ou compartilhada de outra forma com quaisquer terceiros.

Este passo a passo foi validado nos seguintes sistemas operacionais:

- Windows 8 (x86 e x64)
- Windows 7 Ultimate
- Windows Server 2008 R2 Standard

Depois de concluir as etapas neste passo a passo, você pode usar o ambiente de vários computadores para criar estes tipos de aplicativos:

- Aplicativos de área de trabalho em C++ que usem o SDK do Windows 8
- Aplicativos de área de trabalho em Visual Basic ou C# voltados para o .NET Framework 4.5

O ambiente de vários computadores não pode ser usado para compilar estes tipos de aplicativos:

- Aplicativos UWP. Para compilar aplicativos UWP, instale o Visual Studio no computador de build.
- Aplicativos de área de trabalho voltados para o .NET Framework 4 ou anterior. Para criar esses tipos de aplicativos, instale o Visual Studio ou Assemblies e Ferramentas do .NET Reference (do SDK do Windows 7.1) no computador de build.

## <a name="prerequisites"></a>Pré-requisitos

- O Visual Studio com a carga de trabalho instalada para **desenvolvimento de área de trabalho .NET**.

## <a name="install-software-on-the-computers"></a>Instalar o software nos computadores

Primeiro, configure o computador host e, em seguida, configure o computador de build.

Ao instalar o Visual Studio no computador host, você pode criar os arquivos e as configurações que você copiará posteriormente para o computador de build. Você pode instalar o Visual Studio em um computador x86 ou x64, mas a arquitetura do computador de build deverá corresponder à arquitetura do computador host.

1. No computador host, instale o Visual Studio.

2. No computador de compilação, instale o .NET Framework 4.5 ou posterior. Para verificar se ele está instalado, verifique se a entrada de **Versão** na subchave de registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full** tem o valor de **4.5** ou superior.

## <a name="copy-files-from-the-host-computer-to-the-build-computer"></a>Copiar arquivos do computador host para o computador de build

Esta seção aborda a cópia de arquivos específicos, compiladores, ferramentas de build, ativos do MSBuild e configurações do Registro do computador host para o computador de build. Estas instruções pressupõem que você instalou o Visual Studio no local padrão no computador host; se você tiver instalado-o em outro local, ajuste as etapas apropriadamente.

- Em um computador x86, a localização padrão é *C:\Program Files\Microsoft Visual Studio 11.0*
- Em um computador x64, a localização padrão é *C:\Program Files (x86)\Microsoft Visual Studio 11.0*

Observe que o nome da pasta *Arquivos de Programa* depende do sistema operacional instalado. Em um computador x86, o nome é *Arquivos de Programa*; em um computador x64, o nome é *Arquivos de Programa (x86)*. Independentemente da arquitetura do sistema, este passo a passo refere-se à pasta *Arquivos de Programa* como *%ProgramFiles%*.

> [!NOTE]
> No computador de build, todos os arquivos relevantes devem estar na mesma unidade; no entanto, a letra da unidade pode ser diferente da letra da unidade em que o Visual Studio está instalado no computador host. Em qualquer caso, você deve considerar o local dos arquivos ao criar entradas de Registro conforme descrito mais adiante neste documento.

### <a name="copy-the-windows-sdk-files-to-the-build-computer"></a>Copiar os arquivos do SDK do Windows para o computador de build

1. Se você tiver somente o SDK do Windows para Windows 8 instalado, copie estas pastas recursivamente do computador host para o computador de build:

   - %ProgramFiles%\Windows Kits\8.0\bin\

   - %ProgramFiles%\Windows Kits\8.0\Catalogs\

   - %ProgramFiles%\Windows Kits\8.0\DesignTime\

   - %ProgramFiles%\Windows Kits\8.0\include\

   - %ProgramFiles%\Windows Kits\8.0\Lib\

   - %ProgramFiles%\Windows Kits\8.0\Redist\

   - %ProgramFiles%\Windows Kits\8.0\References\

     Se você também tiver estes outros kits do Windows 8...

   - Kit de Avaliação e Implantação do Microsoft Windows

   - Kit de Driver do Microsoft Windows

   - Kit de Certificação de Hardware do Microsoft Windows

     ... eles poderão ter instalado arquivos nas pastas *%ProgramFiles%\Windows Kits\8.0* listadas na etapa anterior, e os termos de licença poderão não permitir direitos de servidor de build para esses arquivos. Verifique os termos de licença para cada kit do Windows instalado para determinar se os arquivos podem ser copiados para o computador de build. Se os termos de licença não permitirem direitos de servidor de build, remova os arquivos do computador de build.

2. Copie as seguintes pastas recursivamente do computador host para o computador de build:

    - %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\

    - %ProgramFiles%\Common Files\Merge Modules\

    - %ProgramFiles%\Microsoft Visual Studio 11.0\VC\

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\ProjectComponents\

    - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\V110\

    - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETCore\v4.5\

    - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETFramework\v4.5\

3. Copie estes arquivos do computador host para o computador de build:

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\msobj110.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdb110.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdbcore.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\mspdbsrv.exe

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\msvcdis110.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\makehm.exe

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\VCVarsQueryRegistry.bat

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\Tools\vsvars32.bat

4. As seguintes bibliotecas de tempo de execução do Visual C++ serão necessárias apenas se você executar saídas de build no computador de build, por exemplo, como parte do teste automatizado. Normalmente, os arquivos estão localizados em subpastas na pasta *%ProgramFiles%\Microsoft Visual Studio 11.0\VC\redist\x86* ou *%ProgramFiles%\Microsoft Visual Studio 11.0\VC\redist\x64*, dependendo da arquitetura do sistema. Em sistemas x86, copie os binários x86 para a pasta *Windows\System32*\. Em sistemas x64, copie os binários x86 para a pasta *Windows\SysWOW64* e os binários x64 para a *Windows\System32*.

    - \Microsoft.VC110.ATL\atl110.dll

    - \Microsoft.VC110.CRT\msvcp110.dll

    - \Microsoft.VC110.CRT\msvcr110.dll

    - \Microsoft.VC110.CXXAMP\vcamp110.dll

    - \Microsoft.VC110.MFC\mfc110.dll

    - \Microsoft.VC110.MFC\mfc110u.dll

    - \Microsoft.VC110.MFC\mfcm110.dll

    - \Microsoft.VC110.MFC\mfcm110u.dll

    - \Microsoft.VC110.MFCLOC\mfc110chs.dll

    - \Microsoft.VC110.MFCLOC\mfc110cht.dll

    - \Microsoft.VC110.MFCLOC\mfc110deu.dll

    - \Microsoft.VC110.MFCLOC\mfc110enu.dll

    - \Microsoft.VC110.MFCLOC\mfc110esn.dll

    - \Microsoft.VC110.MFCLOC\mfc110fra.dll

    - \Microsoft.VC110.MFCLOC\mfc110ita.dll

    - \Microsoft.VC110.MFCLOC\mfc110jpn.dll

    - \Microsoft.VC110.MFCLOC\mfc110kor.dll

    - \Microsoft.VC110.MFCLOC\mfc110rus.dll

    - \Microsoft.VC110.OPENMP\vcomp110.dll

5. Copie somente os seguintes arquivos da pasta *Debug_NonRedist\x86* ou *Debug_NonRedist\x64* para o computador de build, conforme descrito em [Preparar um computador de teste para executar um executável de depuração](/cpp/ide/preparing-a-test-machine-to-run-a-debug-executable). Nenhum outro arquivo pode ser copiado.

    - \Microsoft.VC110.DebugCRT\msvcp110d.dll

    - \Microsoft.VC110.DebugCRT\msvcr110d.dll

    - \Microsoft.VC110.DebugCXXAMP\vcamp110d.dll

    - \Microsoft.VC110.DebugMFC\mfc110d.dll

    - \Microsoft.VC110.DebugMFC\mfc110ud.dll

    - \Microsoft.VC110.DebugMFC\mfcm110d.dll

    - \Microsoft.VC110.DebugMFC\mfcm110ud.dll

    - \Microsoft.VC110.DebugOpenMP\vcomp110d.dll

## <a name="create-registry-settings"></a>Criar configurações de registro

Você deve criar entradas do Registro para definir configurações para MSBuild.

1. Identifique a pasta pai para entradas do Registro. Todas as entradas de Registro são criadas sob a mesma chave pai. Em um computador x86, a chave pai é **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft**. Em um computador x64, a chave pai é **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft**. Independentemente da arquitetura do sistema, este passo a passo refere-se à chave pai como %RegistryRoot%.

    > [!NOTE]
    > Se a arquitetura do computador host for diferente do computador de build, certifique-se de usar a chave pai apropriado em cada computador. Isso é especialmente importante se você estiver automatizando o processo de exportação.
    >
    > Além disso, se você estiver usando uma letra da unidade diferente no computador de build daquela usada no computador host, altere os valores das entradas do Registro de acordo.

2. Crie as seguintes entradas do Registro no computador de build. Todas estas entradas são cadeias de caracteres (Tipo = = "REG_SZ" no Registro). Defina os valores dessas entradas da mesma forma que os valores das entradas comparáveis no computador host.

   - **%RegistryRoot%\\.NETFramework\v4.0.30319\AssemblyFoldersEx\VCMSBuild Public Assemblies@(Default)**

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x86@InstallationFolder</strong>

   - **%RegistryRoot%\VisualStudio\11.0@Source Directories**

   - <strong>%RegistryRoot%\VisualStudio\11.0\Setup\VC@ProductDir</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir32</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir64</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer32</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer64</strong>

   - **%RegistryRoot%\VisualStudio\SxS\VC7@11.0**

   - **%RegistryRoot%\VisualStudio\SxS\VS7@11.0**

   - <strong>%RegistryRoot%\Windows Kits\Installed Roots@KitsRoot</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11</strong>

   Em um computador de build x64, crie também a seguinte entrada do Registro e consulte o computador host para determinar como configurá-la.

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x64@InstallationFolder</strong>

   Se o computador de compilação for x64 e você desejar usar a versão de 64 bits do MSBuild, ou se você estiver usando o Build Service do Team Foundation Server em um computador x64, crie as seguintes entradas no registro de 64 bits nativo. Consulte o computador host para determinar como definir estas entradas.

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\Setup\VS@ProductDir</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11</strong>

## <a name="set-environment-variables-on-the-build-computer"></a>Definir variáveis de ambiente no computador de build

Para usar o MSBuild no computador de build, é preciso definir as variáveis de ambiente PATH. Use *vcvarsall.bat* para definir as variáveis ou configure-as manualmente.

### <a name="use-vcvarsallbat-to-set-environment-variables"></a>Usar vcvarsall.bat para definir variáveis de ambiente

Abra uma janela do **Prompt de Comando** no computador de build e execute *%Program Files%\Microsoft Visual Studio 11.0\VC\vcvarsall.bat*. Você pode usar um argumento de linha de comando para especificar o conjunto de ferramentas que você deseja usar: x86, x64 nativo ou x64 de compilador cruzado. Se você não especificar um argumento de linha de comando, o conjunto de ferramentas x86 será usado.

Esta tabela descreve os argumentos compatíveis com *vcvarsall.bat*:

|Argumento Vcvarsall.bat|Compilador|Compilar uma arquitetura de computador|Arquitetura de saída de compilação|
| - |--------------| - | - |
|x86 (padrão)|Nativo de 32 bits|x86, x64|x86|
|x86_amd64|x64 Cruzado|x86, x64|X64|
|amd64|x64 Nativo|X64|X64|

Se *vcvarsall.bat* for executado com êxito – ou seja, nenhuma mensagem de erro for exibida, você poderá ignorar a próxima etapa e continuar na seção [Instalar assemblies do MSBuild para o GAC (Cache de Assembly Global) no computador de build](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#InstallingMSBuildToGAC) deste documento.

### <a name="manually-set-environment-variables"></a>Definir manualmente variáveis de ambiente

1. Para configurar manualmente o ambiente de linha de comando, adicione este caminho à variável de ambiente PATH:

    - %Program Files%\Microsoft Visual Studio 11.0\Common7\IDE

2. Opcionalmente, você também pode adicionar os seguintes caminhos à variável PATH para tornar mais fácil usar o MSBuild para compilar suas soluções.

   Se você quiser usar o MSBuild nativo de 32 bits, adicione estes caminhos à variável PATH:

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools

   - %windir%\Microsoft.NET\Framework\v4.0.30319

   Se você quiser usar o MSBuild nativo de 64 bits, adicione estes caminhos à variável PATH:

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64

   - %windir%\Microsoft.NET\Framework64\v4.0.30319

## <a name="install-msbuild-assemblies-to-the-global-assembly-cache-gac-on-the-build-computer"></a>Instalar assemblies do MSBuild para o GAC (Cache de Assembly Global) no computador de build

O MSBuild requer que alguns assemblies adicionais sejam instalados no GAC do computador de build.

1. Copie os seguintes assemblies do computador host para o computador de build. Como eles serão instalados no GAC, não importa o local em que você os coloca no computador de build.

    - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.Build.CPPTasks.Common.v110.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\CommonExtensions\Microsoft\VC\Project\Microsoft.VisualStudio.Project.VisualC.VCProjectEngine.dll

    - %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE\PublicAssemblies\Microsoft.VisualStudio.VCProjectEngine.dll

2. Para instalar os assemblies no GAC, localize *gacutil.exe* no computador de build; normalmente, ele está em %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\\. Se você não conseguir localizar essa pasta, repita as etapas na seção [Copiar arquivos do computador host para o computador de build](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CopyingFiles) deste passo a passo.

     Abra uma janela do **Prompt de Comando** que tem direitos administrativos e execute este comando para cada arquivo:

     **gacutil -i \<file>**

    > [!NOTE]
    > Uma reinicialização pode ser necessária para um assembly ser instalado totalmente no GAC.

## <a name="build-projects"></a>Criar projetos

Você pode usar o Azure Pipelines para compilar projetos e soluções do Visual Studio ou pode compilá-los na linha de comando. Ao usar o Azure Pipelines para compilar projetos, ele invoca o executável do MSBuild que corresponde à arquitetura do sistema. Na linha de comando, você pode usar o MSBuild de 32 bits ou 64 bits e escolher a arquitetura do MSBuild configurando a variável de ambiente PATH ou invocando diretamente o executável do MSBuild específico da arquitetura.

Para usar *msbuild.exe* no prompt de comando, execute o seguinte comando, em que *solution.sln* é um espaço reservado para o nome da solução.

**msbuild** *solution.sln*

Para obter mais informações sobre como usar o MSBuild na linha de comando, consulte [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md).

## <a name="create-the-build-environment-so-that-it-can-be-checked-into-source-control"></a>Criar o ambiente de build para que ele possa fazer o check-in no controle do código-fonte

Você pode criar um ambiente de build que possa ser implantado em vários computadores e que não exija arquivos de "GAC" nem a modificação das configurações do Registro. As etapas a seguir são apenas uma maneira de fazer isso. Adapte estas etapas às características exclusivas do seu ambiente de build.

> [!NOTE]
> Você precisa desabilitar o build incremental para que *tracker.exe* não gere um erro durante um build. Para desabilitar a compilação incremental, defina este parâmetro de build:
>
> **msbuild** *solution.sln* **/p:TrackFileAccess=false**

1. Crie um diretório *Depot* no computador host.

     Estas etapas referem-se ao diretório como %Depot%.

2. Copie os diretórios e arquivos, conforme descrito na seção [Copiar arquivos do computador host para o computador de build](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#CopyingFiles) deste passo a passo, mas cole-os no diretório *%Depot%* recém-criado. Por exemplo, copie de *%ProgramFiles%\Windows Kits\8.0\bin* para *%Depot%\Windows Kits\8.0\bin*.

3. Quando os arquivos forem colados em *%Depot%*, faça estas alterações:

    - Em %Depot%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPP.Targets, \Microsoft.Cpp.InvalidPlatforms.targets\\, \Microsoft.cppbuild.targets\\ e \Microsoft.CppCommon.targets\\, altere todas as instâncias de

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"

         para

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll".

         A nomenclatura anterior se baseia no assembly ao qual se está aplicando GAC.

    - Em %Depot% \MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPPClean.Targets, altere todas as instâncias de

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"

         para

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll".

4. Crie um arquivo *.props* (por exemplo, *Partner.AutoImports.props*) e coloque-o na raiz da pasta que contém os projetos. Esse arquivo é usado para definir as variáveis que são usadas pelo MSBuild para localizar vários recursos. Se as variáveis não forem definidas por esse arquivo, elas serão definidas por outros arquivos *.props* e *.targets* que dependem de valores de registro. Uma vez que não estamos configurando nenhum valor de registro, essas variáveis estariam vazias e o build falharia. Em vez disso, adicione isto a *Partner.AutoImports.props*:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <!-- This file must be imported by all project files at the top of the project file. -->
    <Project ToolsVersion="4.0"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
    <VCTargetsPath>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath>
    <VCTargetsPath11>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath11>
    <MSBuildExtensionsPath>$(DepotRoot)MSBuild</MSBuildExtensionsPath>
    <MSBuildExtensionsPath32>$(DepotRoot)MSBuild</MSBuildExtensionsPath32>
    <VCInstallDir_110>$(DepotRoot)Microsoft Visual Studio 11.0\VC\</VCInstallDir_110>
    <VCInstallDir>$(VCInstallDir_110)</VCInstallDir>
    <WindowsKitRoot>$(DepotRoot)Windows Kits\</WindowsKitRoot>
    <WindowsSDK80Path>$(WindowsKitRoot)</WindowsSDK80Path>
    <WindowsSdkDir_80>$(WindowsKitRoot)8.0\</WindowsSdkDir_80>
    <WindowsSdkDir>$(WindowsSDKDir_80)</WindowsSdkDir>
    <WindowsSdkDir_80A>$(DepotRoot)Microsoft SDKs\Windows\v8.0A\</WindowsSdkDir_80A>
    </PropertyGroup>
    </Project>
    ```

5. Em cada um dos seus arquivos de projeto, adicione a seguinte linha na parte superior, após a linha `<Project Default Targets...>`.

    ```xml
    <Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), Partner.AutoImports.props))\Partner.AutoImports.props"/>
    ```

6. Altere o ambiente da linha de comando da seguinte maneira:

    - Defina Depot=*localização do diretório Depósito criado na etapa 1*

    - Definir path=%path%;*localização do MSBuild no computador*;%Depot%\Windows\System32;%Depot%\Windows\SysWOW64;%Depot%\Microsoft Visual Studio 15.0\Common7\IDE\

       Para compilação de 64 bits nativa, aponte para o MSBuild de 64 bits.

## <a name="see-also"></a>Consulte também

- [Preparar um computador de teste para executar um executável de depuração](/cpp/ide/preparing-a-test-machine-to-run-a-debug-executable)
- [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md)
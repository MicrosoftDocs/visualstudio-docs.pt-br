---
title: Tarefa GenerateApplicationManifest | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateApplicationManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateApplicationManifest task
- HostInBrowser property (MSBuild)
- GenerateApplicationManifest task [MSBuild]
ms.assetid: a494102b-0cb2-4755-8e2a-d2c0f39fac1d
caps.latest.revision: 27
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: da5c9cb78ff4d3d9542c956a377f6342945d11a0
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49245557"
---
# <a name="generateapplicationmanifest-task"></a>Tarefa GenerateApplicationManifest
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Gera um manifesto do aplicativo ou um manifesto nativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Um manifesto nativo descreve um componente definindo uma identidade exclusiva para ele e identificando todos os assemblies e arquivos que compõem o componente. Um manifesto do aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] estende um manifesto nativo indicando o ponto de entrada do aplicativo e especificando o nível de segurança do aplicativo.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `GenerateApplicationManifest`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AssemblyName`|Parâmetro `String` opcional.<br /><br /> Especifica o campo `Name` da identidade do assembly para o manifesto gerado. Se esse parâmetro não for especificado, o nome será inferido com base nos parâmetros `EntryPoint` ou `InputManifest`. Se nenhum nome puder ser criado, a tarefa gerará um erro.|  
|`AssemblyVersion`|Parâmetro `String` opcional.<br /><br /> Especifica o campo `Version` da identidade do assembly para o manifesto gerado. Se o parâmetro não for especificado, será usado o valor padrão de “1.0.0.0”.|  
|`ClrVersion`|Parâmetro `String` opcional.<br /><br /> Especifica a versão mínima do CLR (Common Language Runtime) exigida pelo aplicativo. O valor padrão é a versão CLR em uso no sistema do build. Caso a tarefa esteja gerando um manifesto nativo, este parâmetro será ignorado.|  
|`ConfigFile`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica qual item contém o arquivo de configuração de aplicativo. Caso a tarefa esteja gerando um manifesto nativo, este parâmetro será ignorado.|  
|`Dependencies`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica uma lista de itens que define o conjunto de assemblies dependentes para o manifesto gerado. Cada item pode ser descrito com mais detalhes por metadados do item para indicar o estados de implantação adicionais e o tipo de dependência. Para obter mais informações, consulte a seção “Metadados do Item” abaixo.|  
|`Description`|Parâmetro `String` opcional.<br /><br /> Especifica a descrição do aplicativo ou componente.|  
|`EntryPoint`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica um único item que indica o ponto de entrada para o assembly do manifesto gerado.<br /><br /> Para um manifesto do aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], esse parâmetro especifica o assembly que é iniciado quando o aplicativo é executado.|  
|`ErrorReportUrl`|Opcional [String] (<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Especifica a URL da página da Web que é exibida nas caixas de diálogo durante os relatórios de erro em instalações ClickOnce.|  
|`FileAssociations`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica uma lista de um ou mais tipos de arquivo associados ao manifesto de implantação do ClickOnce.<br /><br /> As associações de arquivos são válidas somente quando voltado para o .NET Framework 3.5 ou posterior.|  
|`Files`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Os arquivos a serem incluídos no manifesto. Especifique o caminho completo para cada arquivo.|  
|`HostInBrowser`|Opcional [booliano] (<!-- TODO: review code entity reference <xref:assetId:///Boolean?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Se `true`, o aplicativo é hospedado em um navegador (assim como Aplicativos de navegador da Web WPF).|  
|`IconFile`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Indica o arquivo de ícone do aplicativo. O ícone do aplicativo é expresso no manifesto do aplicativo gerado e usado para os diálogos Menu Iniciar e Adicionar ou Remover Programas. Se essa entrada não for especificada, um ícone padrão será usado. Caso a tarefa esteja gerando um manifesto nativo, este parâmetro será ignorado.|  
|`InputManifest`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Indica um documento XML de entrada para servir como base para o gerador de manifesto. Isso permite que dados estruturados, tais como segurança de aplicativos ou definições personalizadas de manifesto, sejam refletidos no manifesto de saída. O elemento raiz do documento XML deve ser um nó de assembly no namespace asmv1.|  
|`IsolatedComReferences`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os componentes COM a serem isolados no manifesto gerado. Esse parâmetro dá suporte à capacidade de isolar os componentes COM para implantação de “COM sem Registro”. Ele funciona por meio da geração automática de um manifesto com definições padrão de registro de COM. No entanto, os componentes COM devem ser registrados no computador de build para que isso funcione corretamente.|  
|`ManifestType`|Parâmetro `String` opcional.<br /><br /> Especifica o tipo de manifesto a ser gerado. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `Native`<br />-   `ClickOnce`<br /><br /> Se esse parâmetro não for especificado, a tarefa será `ClickOnce` por padrão.|  
|`MaxTargetPath`|Parâmetro `String` opcional.<br /><br /> Especifica o comprimento máximo permitido de um caminho de arquivo em uma implantação de aplicativos [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Se esse valor for especificado, o comprimento de cada caminho de arquivo no aplicativo é verificado em relação a esse limite. Todos os itens que excedem o limite gerarão um aviso de build. Se essa entrada não for especificada ou for zero, nenhuma verificação será executada. Caso a tarefa esteja gerando um manifesto nativo, este parâmetro será ignorado.|  
|`OSVersion`|Parâmetro `String` opcional.<br /><br /> Especifica a versão mínima necessária do SO (sistema operacional) exigida pelo aplicativo. Por exemplo, o valor “5.1.2600.0” indica o sistema operacional for o Windows XP. Se esse parâmetro não for especificado, será usado o valor “4.10.0.0”, que indica o Windows 98 Second Edition, o sistema operacional mínimo com suporte no .NET Framework. Caso a tarefa esteja gerando um manifesto nativo, esta entrada será ignorada.|  
|`OutputManifest`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o nome do arquivo de manifesto de saída gerado. Se esse parâmetro não for especificado, o nome do arquivo de saída será inferido com base na identidade do manifesto gerado.|  
|`Platform`|Parâmetro `String` opcional.<br /><br /> Especifica a plataforma de destino do aplicativo. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> Se esse parâmetro não for especificado, a tarefa será `AnyCPU` por padrão.|  
|`Product`|Parâmetro `String` opcional.<br /><br /> Especifica o nome do aplicativo. Se esse parâmetro não for especificado, o nome será inferido com base na identidade do manifesto gerado. Esse nome é usado para o nome do atalho no menu Iniciar e faz parte do nome que aparece na caixa de diálogo Adicionar ou Remover Programas.|  
|`Publisher`|Parâmetro `String` opcional.<br /><br /> Especifica o editor do aplicativo. Se esse parâmetro não for especificado, o nome será inferido com base no usuário registrado ou na identidade do manifesto gerado. Esse nome é usado para o nome da pasta no menu Iniciar e faz parte do nome que aparece na caixa de diálogo Adicionar ou Remover Programas.|  
|`RequiresMinimumFramework35SP1`|Parâmetro `Boolean` opcional.<br /><br /> Se for verdadeiro, o aplicativo exigirá o .NET Framework 3.5 SP1 ou uma versão mais recente.|  
|`TargetCulture`|Parâmetro `String` opcional.<br /><br /> Identifica a cultura do aplicativo e especifica o campo `Language` da identidade do assembly para o manifesto gerado. Se esse parâmetro não for especificado, presume-se que o aplicativo não varia conforme a cultura.|  
|`TargetFrameworkMoniker`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o moniker da estrutura de destino.|  
|`TargetFrameworkProfile`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o perfil da estrutura de destino.|  
|`TargetFrameworkSubset`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o nome do subconjunto do .NET Framework de destino.|  
|`TargetFrameworkVersion`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o .NET Framework de destino do projeto.|  
|`TrustInfoFile`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Indica um documento XML que especifica a segurança do aplicativo. O elemento raiz do documento XML deve ser um nó trustInfo no namespace asmv2. Caso a tarefa esteja gerando um manifesto nativo, este parâmetro será ignorado.|  
|`UseApplicationTrust`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///Boolean?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Se for verdadeiro, as propriedades `Product`, `Publisher` e `SupportUrl` são gravadas no manifesto do aplicativo.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.GenerateManifestBase>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista dos parâmetros da classe Task, consulte [Classe base Task](../msbuild/task-base-class.md).  
  
 Para obter informações sobre como usar a tarefa `GenerateDeploymentManifest`, consulte [Tarefa GenerateApplicationManifest](../msbuild/generateapplicationmanifest-task.md).  
  
 As entradas para as dependências e os arquivos podem ser mais decorados ainda com metadados de item para especificar o estado de implantação adicional para cada item.  
  
## <a name="item-metadata"></a>Metadados de item  
  
|Nome dos metadados|Descrição|  
|-------------------|-----------------|  
|`DependencyType`|Indica se a dependência é publicada e instalada com o aplicativo ou um pré-requisito. Esses metadados são válidos para todas as dependências, mas não são usados para arquivos. Os valores disponíveis para esses metadados são:<br /><br /> -   `Install`<br />-   `Prerequisite`<br /><br /> Instala o valor padrão.|  
|`AssemblyType`|Indica se a dependência é um assembly gerenciado ou nativo. Esses metadados são válidos para todas as dependências, mas não são usados para arquivos. Os valores disponíveis para esses metadados são:<br /><br /> -   `Managed`<br />-   `Native`<br />-   `Unspecified`<br /><br /> `Unspecified` é o valor padrão, que indica que o gerador de manifesto determinará o tipo de assembly automaticamente.|  
|`Group`|Indica o grupo para baixar arquivos adicionais sob demanda. O nome do grupo é definido pelo aplicativo e pode ser qualquer cadeia de caracteres. Uma cadeia de caracteres vazia indica que o arquivo não faz parte de um grupo de download, que é o padrão. Arquivos que não estão em um grupo fazem parte do download inicial do aplicativo. Os arquivos em um grupo são baixados apenas quando explicitamente solicitado pelo aplicativo usando <xref:System.Deployment.Application>.<br /><br /> Esses metadados são válido para todos os arquivos em que `IsDataFile` é `false` e todas as dependências em que `DependencyType` é `Install`.|  
|`TargetPath`|Especifica como o caminho deve ser definido no manifesto gerado. Esse atributo é válido para todos os arquivos. Se esse atributo não for especificado, a especificação do item será usada. Esse atributo é válido para todos os arquivos e as dependências com um valor `DependencyType` de `Install`.|  
|`IsDataFile`|Um valor de metadados `Boolean` que indica se o arquivo é um arquivo de dados ou não. Um arquivo de dados é especial, pois ele é migrado entre as atualizações de aplicativos. Esses metadados só são válido para os arquivos. `False` é o valor padrão.|  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a tarefa `GenerateApplicationManifest` para gerar um manifesto do aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] e a tarefa `GenerateDeploymentManifest` para gerar um manifesto de implantação para um aplicativo com um único assembly. Em seguida, ele usa a tarefa `SignFile` para assinar os manifestos.  
  
 Isso ilustra o cenário mais simples de geração de manifesto possível, no qual manifestos [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] são gerados para um único programa. Um nome padrão e uma identidade são inferidos do assembly para o manifesto.  
  
> [!NOTE]
>  No exemplo abaixo, todos os binários do aplicativo são predefinidos para se concentrar em aspectos de geração de manifesto. Este exemplo produz uma implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] totalmente funcional.  
  
> [!NOTE]
>  Para obter mais informações sobre a propriedade `Thumbprint` usada na tarefa `SignFile` neste exemplo, consulte [Tarefa SignFile](../msbuild/signfile-task.md).  
  
```  
<Project DefaultTargets="Build"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <EntryPoint Include="SimpleWinApp.exe" />  
    </ItemGroup>  
  
    <PropertyGroup>  
        <Thumbprint>  
             <!-- Insert generated thumbprint here -->  
        </Thumbprint>  
    </PropertyGroup>  
  
    <Target Name="Build">  
  
        <GenerateApplicationManifest  
            EntryPoint="@(EntryPoint)">  
            <Output  
                ItemName="ApplicationManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateApplicationManifest>  
  
        <GenerateDeploymentManifest  
            EntryPoint="@(ApplicationManifest)">  
            <Output  
                ItemName="DeployManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateDeploymentManifest>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(ApplicationManifest)"/>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(DeployManifest)"/>  
  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa as tarefas `GenerateApplicationManifest` e `GenerateDeploymentManifest` para gerar manifestos do aplicativo e de implantação [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] para um aplicativo com um único assembly, especificando o nome e a identidade dos manifestos.  
  
 Este exemplo é semelhante ao exemplo anterior, exceto que o nome e a identidade dos manifestos são especificados explicitamente. Além disso, este exemplo é configurado como um aplicativo online em vez de um aplicativo instalado.  
  
> [!NOTE]
>  No exemplo abaixo, todos os binários do aplicativo são predefinidos para se concentrar em aspectos de geração de manifesto. Este exemplo produz uma implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] totalmente funcional.  
  
> [!NOTE]
>  Para obter mais informações sobre a propriedade `Thumbprint` usada na tarefa `SignFile` neste exemplo, consulte [Tarefa SignFile](../msbuild/signfile-task.md).  
  
```  
<Project DefaultTargets="Build"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <EntryPoint Include="SimpleWinApp.exe" />  
    </ItemGroup>  
  
    <PropertyGroup>  
        <Thumbprint>  
             <!-- Insert generated thumbprint here -->  
        </Thumbprint>  
    </PropertyGroup>  
  
    <Target Name="Build">  
  
        <GenerateApplicationManifest  
            AssemblyName="SimpleWinApp.exe"  
            AssemblyVersion="1.0.0.0"  
            EntryPoint="@(EntryPoint)"  
            OutputManifest="SimpleWinApp.exe.manifest">  
            <Output  
                ItemName="ApplicationManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateApplicationManifest>  
  
        <GenerateDeploymentManifest  
                AssemblyName="SimpleWinApp.application"  
                AssemblyVersion="1.0.0.0"  
                EntryPoint="@(ApplicationManifest)"  
                Install="false"  
                OutputManifest="SimpleWinApp.application">  
                <Output  
                    ItemName="DeployManifest"  
                    TaskParameter="OutputManifest"/>  
        </GenerateDeploymentManifest>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(ApplicationManifest)"/>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(DeployManifest)"/>  
  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa as tarefas `GenerateApplicationManifest` e `GenerateDeploymentManifest` para gerar manifestos do aplicativo e de implantação [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] para um aplicativo com vários arquivos e assemblies.  
  
> [!NOTE]
>  No exemplo abaixo, todos os binários do aplicativo são predefinidos para se concentrar em aspectos de geração de manifesto. Este exemplo produz uma implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] totalmente funcional.  
  
> [!NOTE]
>  Para obter mais informações sobre a propriedade `Thumbprint` usada na tarefa `SignFile` neste exemplo, consulte [Tarefa SignFile](../msbuild/signfile-task.md).  
  
```  
<Project DefaultTargets="Build"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <EntryPoint Include="SimpleWinApp.exe" />  
    </ItemGroup>  
  
    <PropertyGroup>  
        <Thumbprint>  
             <!-- Insert generated thumbprint here -->  
        </Thumbprint>  
        <DeployUrl>  
            <!-- Insert the deployment URL here -->  
        </DeployUrl>  
        <SupportUrl>  
            <!-- Insert the support URL here -->  
        </SupportUrl>  
    </PropertyGroup>  
  
    <Target Name="Build">  
  
    <ItemGroup>  
        <EntryPoint Include="SimpleWinApp.exe"/>  
        <Dependency Include="ClassLibrary1.dll">  
            <AssemblyType>Managed</AssemblyType>  
            <DependencyType>Install</DependencyType>  
        </Dependency>  
        <Dependency Include="ClassLibrary2.dll">  
            <AssemblyType>Managed</AssemblyType>  
            <DependencyType>Install</DependencyType>  
            <Group>Secondary</Group>  
        </Dependency>  
        <Dependency Include="MyAddIn1.dll">  
            <AssemblyType>Managed</AssemblyType>  
            <DependencyType>Install</DependencyType>  
            <TargetPath>Addins\MyAddIn1.dll</TargetPath>  
        </Dependency>  
        <Dependency Include="ClassLibrary3.dll">  
            <AssemblyType>Managed</AssemblyType>  
            <DependencyType>Prerequisite</DependencyType>  
        </Dependency>  
  
        <File Include="Text1.txt">  
            <TargetPath>Text\Text1.txt</TargetPath>  
            <Group>Text</Group>  
        </File>  
        <File Include="DataFile1.xml ">  
            <TargetPath>Data\DataFile1.xml</TargetPath>  
            <IsDataFile>true</IsDataFile>  
        </File>  
  
        <IconFile Include="Heart.ico"/>  
        <ConfigFile Include="app.config">  
            <TargetPath>SimpleWinApp.exe.config</TargetPath>  
        </ConfigFile>  
        <BaseManifest Include="app.manifest"/>  
    </ItemGroup>  
  
    <Target Name="Build">  
  
        <GenerateApplicationManifest  
            AssemblyName="SimpleWinApp.exe"  
            AssemblyVersion="1.0.0.0"  
            ConfigFile="@(ConfigFile)"  
            Dependencies="@(Dependency)"  
            Description="TestApp"  
            EntryPoint="@(EntryPoint)"  
            Files="@(File)"  
            IconFile="@(IconFile)"  
            InputManifest="@(BaseManifest)"  
            OutputManifest="SimpleWinApp.exe.manifest">  
            <Output  
                ItemName="ApplicationManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateApplicationManifest>  
  
        <GenerateDeploymentManifest  
            AssemblyName="SimpleWinApp.application"  
            AssemblyVersion="1.0.0.0"  
            DeploymentUrl="$(DeployToUrl)"  
            Description="TestDeploy"  
            EntryPoint="@(ApplicationManifest)"  
            Install="true"  
            OutputManifest="SimpleWinApp.application"  
            Product="SimpleWinApp"  
            Publisher="Microsoft"  
            SupportUrl="$(SupportUrl)"  
            UpdateEnabled="true"  
            UpdateInterval="3"  
            UpdateMode="Background"  
            UpdateUnit="weeks">  
            <Output  
                ItemName="DeployManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateDeploymentManifest>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(ApplicationManifest)"/>  
  
        <SignFile  
            CertificateThumbprint="$(Thumbprint)"  
            SigningTarget="@(DeployManifest)"/>  
  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a tarefa `GenerateApplicationManifest` para gerar um manifesto nativo para o aplicativo Test.exe, fazendo referência ao componente nativo Alpha.dll e ao componente isolado COM Bravo.dll.  
  
 Este exemplo produz Test.exe.manifest, tornando o aplicativo XCOPY implantável, aproveitando o COM Sem Registro.  
  
> [!NOTE]
>  No exemplo abaixo, todos os binários do aplicativo são predefinidos para se concentrar em aspectos de geração de manifesto. Este exemplo produz uma implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] totalmente funcional.  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <File Include="Test.exe" />  
        <Dependency Include="Alpha.dll">  
            <AssemblyType>Native</AssemblyType>  
            <DependencyType>Install</DependencyType>  
        </Dependency>  
        <ComComponent Include="Bravo.dll" />  
    </ItemGroup>  
  
    <Target Name="Build">  
        <GenerateApplicationManifest  
            AssemblyName="Test.exe"  
            AssemblyVersion="1.0.0.0"  
            Dependencies="@(Dependency)"  
            Files="@(File)"  
            IsolatedComReferences="@(ComComponent)"  
            ManifestType="Native">  
            <Output  
                ItemName="ApplicationManifest"  
                TaskParameter="OutputManifest"/>  
        </GenerateApplicationManifest>  
  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Tarefa GenerateDeploymentManifest](../msbuild/generatedeploymentmanifest-task.md)   
 [Tarefa SignFile](../msbuild/signfile-task.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)




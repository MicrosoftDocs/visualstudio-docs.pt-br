---
title: IDs de carga de trabalho e de componente do Visual Studio Enterprise 2019
titleSuffix: ''
description: Use as IDs de carga de trabalho e de componente para instalar o Visual Studio usando a linha de comando ou para especificar como uma dependência em um manifesto do VSIX
keywords: ''
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.date: 3/2/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 6a23833160c3b1c6173a605e493b979e894c1c93
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683338"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-enterprise-2019"></a>Editor principal do Visual Studio (incluído no Visual Studio Enterprise 2019)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**Descrição:** a experiência de shell do Visual Studio Core, incluindo a edição de código com reconhecimento de sintaxe, controle do código-fonte e gerenciamento de itens de trabalho.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Editor do Visual Studio Core | 16.1.28811.260 | Obrigatório
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | Página inicial do Visual Studio para usuários C++ | 16.0.28315.86 | Opcional

## <a name="azure-development"></a>Desenvolvimento do Azure

**ID:** Microsoft.VisualStudio.Workload.Azure

**Descrição:** SDKs, ferramentas e projetos do Azure para desenvolver aplicativos de nuvem e criar recursos usando o .NET Core e o .NET Framework. Também inclui ferramentas para colocar seu aplicativo em contêiner, incluindo o suporte do Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Obrigatório
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Obrigatório
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Obrigatório
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Obrigatório
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft. Componentobject. ClickOnce. publish | Publicação do ClickOnce para .NET Core  | 16.9.31004.209 | Obrigatório
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. DevelopmentTools | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Web | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 16.4.29313.120 | Obrigatório
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Obrigatório
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Pré-requisitos de desenvolvimento do Azure | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Obrigatório
Microsoft.Component.Azure.DataLake.Tools | Ferramentas Azure Data Lake e Stream Analytics | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Recomendadas
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 16.0.28516.191 | Recomendadas
Microsoft.Net.Core.Component.SDK.2.1 | Tempo de execução do .NET Core 2,1 (LTS) | 16.9.31024.58 | Recomendadas
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Kubernetes.Tools | Ferramentas do Visual Studio para Kubernetes | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. Azure. PowerShell | Azure PowerShell | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Principais ferramentas do Azure Resource Manager | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Ferramentas do Service Fabric | 16.4.29313.120 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.Snapshot | Depurador de instantâneo | 16.5.29813.82 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.TimeTravel | Depurador de Viagem no Tempo | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Ferramentas dos Serviços de Nuvem do Azure | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Ferramentas do Azure Resource Manager | 16.0.28528.71 | Recomendadas
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 16.9.31004.209 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 16.9.31004.209 | Opcional
Microsoft.Net. Component. 4.8. TargetingPack | Pacote de direcionamento do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 16.3.29207.166 | Opcional
Microsoft.Net. Componentattribute. 4.8. DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4,8 | 16.4.29318.151 | Opcional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | AzCopy do Armazenamento do Azure | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Opcional

## <a name="data-storage-and-processing"></a>Processamento e armazenamento de dados

**ID:** Microsoft.VisualStudio.Workload.Data

**Descrição:** conectar, desenvolver e testar soluções de dados com o SQL Server, Azure Data Lake ou Hadoop.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Recomendadas
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Recomendadas
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Recomendadas
Microsoft.Component.Azure.DataLake.Tools | Ferramentas Azure Data Lake e Stream Analytics | 16.9.31004.209 | Recomendadas
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Recomendadas
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Recomendadas
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Recomendadas
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Recomendadas
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Recomendadas
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 16.0.28516.191 | Recomendadas
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Recomendadas
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Recomendadas
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Recomendadas
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 16.4.29313.120 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Recomendadas
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Recomendadas
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Recomendadas
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Recomendadas
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 16.0.28315.86 | Opcional

## <a name="data-science-and-analytical-applications"></a>Aplicativos de ciência de dados e análise

**ID:** Microsoft.VisualStudio.Workload.DataScience

**Descrição:** Linguagens e ferramentas para criar aplicativos de ciência de dados, incluindo Python e F #.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.PythonTools | Suporte da linguagem Python | 16.5.29515.121 | Recomendadas
Microsoft.Component.PythonTools.Minicondax64 | Miniconda Python | 16.2.29003.222 | Recomendadas
Microsoft.Component.PythonTools.Web | Suporte Web do Python | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Ferramentas de desenvolvimento nativo do Python | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 16.5.29515.121 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK | Runtime C Universal do Windows | 16.4.29409.204 | Opcional
Microsoft. VisualStudio. Component. Windows10SDK. 19041 | SDK do Windows 10 (10.0.19041.0) | 16.9.31004.209 | Opcional

## <a name="net-desktop-development"></a>Desenvolvimento para área de trabalho com .NET

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktop

**Descrição:** Crie aplicativos WPF, Windows Forms e de console usando C#, Visual Basic e F # com .NET Core e .NET Framework.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | Ferramentas de desenvolvimento de área de trabalho do .NET | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | Recomendadas
Microsoft. Componentobject. ClickOnce. publish | Publicação do ClickOnce para .NET Core  | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Recomendadas
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 16.0.28516.191 | Recomendadas
Microsoft.Net.Core.Component.SDK.2.1 | Tempo de execução do .NET Core 2,1 (LTS) | 16.9.31024.58 | Recomendadas
Microsoft. NetCore. Component. DevelopmentTools | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. DotNetModelBuilder | Construtor de modelos ML.NET (versão prévia) | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.EntityFramework | Ferramentas do Entity Framework 6 | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Recomendadas
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Component.Dotfuscator | Proteção PreEmptive – Dotfuscator | 16.0.28528.71 | Opcional
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Opcional
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Opcional
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 16.9.31004.209 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 16.9.31004.209 | Opcional
Microsoft.Net. Component. 4.8. TargetingPack | Pacote de direcionamento do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 16.3.29207.166 | Opcional
Microsoft.Net. Componentattribute. 4.8. DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4,8 | 16.4.29318.151 | Opcional
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 16.0.28528.71 | Opcional
Microsoft.VisualStudio.Component.CodeClone | Clone de Código | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.CodeMap | Mapa de Códigos | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | Validação de dependência dinâmica | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.GraphDocument | Editor DGML | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Opcional
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Opcional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | Ferramentas de arquitetura e análise | 16.5.29514.35 | Opcional
Microsoft.VisualStudio.ComponentGroup.MSIX. Packaging | Ferramentas de empacotamento MSIX | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Opcional

## <a name="game-development-with-unity"></a>Desenvolvimento de jogos com Unity

**ID:** Microsoft.VisualStudio.Workload.ManagedGame

**Descrição:** criar jogos 2D e 3D com o Unity, um ambiente de desenvolvimento avançado de plataforma cruzada.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 3.5 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Unity | Ferramentas do Visual Studio para Unity | 16.0.28315.86 | Obrigatório
Component.UnityEngine.x64 | Unity Hub | 16.9.31004.209 | Recomendadas
Component.UnityEngine.x86 | Editor de 32 bits do Unity 5.6 | 16.1.28811.260 | Recomendadas

## <a name="linux-development-with-c"></a>Desenvolvimento de Linux com C++

**ID:** Microsoft.VisualStudio.Workload.NativeCrossPlat

**Descrição:** criar e depurar aplicativos executados em um ambiente Linux.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.MDD.Linux | Desenvolvimento do C++ para Linux | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Obrigatório
Component.Linux.CMake | Ferramentas CMake do C++ para Linux | 16.2.29003.222 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Component.MDD.Linux.GCC.arm | Ferramentas de desenvolvimento inseridas e de IoT | 16.5.29515.121 | Opcional

## <a name="desktop-development-with-c"></a>Desenvolvimento para desktop com C++

**ID:** Microsoft.VisualStudio.Workload.NativeDesktop

**Descrição:** Crie aplicativos C++ modernos para Windows usando as ferramentas de sua escolha, incluindo MSVC, Clang, CMake ou MSBuild.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 16.0.28528.71 | Obrigatório
Microsoft.VisualStudio.Component.CodeMap | Mapa de Códigos | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.GraphDocument | Editor DGML | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Atualização dos Pacotes Redistribuíveis do C++ 2019 | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Native | Ferramentas de arquitetura para o C++ | 16.0.28621.142 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Principais recursos de área de trabalho do C++ | 16.2.29012.281 | Obrigatório
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. VC. ASAN | C++ AddressSanitizer | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.VC.ATL | C++ ATL para as ferramentas de Build v142 mais recentes (x86 & x64) | 16.4.29313.120 | Recomendadas
Microsoft.VisualStudio.Component.VC.CMake.Project | Ferramentas CMake do C++ para Windows | 16.3.29103.31 | Recomendadas
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Adaptador de Teste para Boost.Test | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Adaptador de Teste para Google Test | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. Windows10SDK. 19041 | SDK do Windows 10 (10.0.19041.0) | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Componentobject. WebToolsExtensions. CMake | Editor de JSON | 16.9.31004.209 | Recomendadas
Component.Incredibuild | IncrediBuild - Aceleração de Build | 16.5.29721.120 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Opcional
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 16.0.28625.61 | Opcional
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Opcional
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 – ferramentas de build do C++ para VS 2015 (v14.00) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.ATLMFC | C++ MFC para ferramentas de Build v142 mais recentes (x86 & x64) | 16.4.29313.120 | Opcional
Microsoft.VisualStudio.Component.VC.CLI.Support | Suporte a C++/CLI para ferramentas de Build do v142 (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Llvm.Clang | Compilador C++ Clang para Windows (11.0.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset | C++ Clang-cl para ferramentas de build v142 (x64/x86) | 16.3.29207.166 | Opcional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | Módulos do C++ para ferramentas de build v142 (x64/x86 – experimental) | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 – ferramentas de build do C++ para VS 2017 x64/x86 (v14.16) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | SDK do Windows 10 (10.0.17763.0) | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | SDK do Windows 10 (10.0.18362.0) | 16.1.28829.92 | Opcional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang | C++ Clang Tools para Windows (11.0.0-x64/x86) | 16.9.31004.209 | Opcional

## <a name="game-development-with-c"></a>Desenvolvimento de jogos com C++

**ID:** Microsoft.VisualStudio.Workload.NativeGame

**Descrição:** usar todo o poder do C++ para criar jogos profissionais da plataforma DirectX, Unreal ou Cocos2d.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Atualização dos Pacotes Redistribuíveis do C++ 2019 | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Windows10SDK | Runtime C Universal do Windows | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft. VisualStudio. Component. VC. ASAN | C++ AddressSanitizer | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 16.5.29515.121 | Recomendadas
Microsoft. VisualStudio. Component. Windows10SDK. 19041 | SDK do Windows 10 (10.0.19041.0) | 16.9.31004.209 | Recomendadas
Component.Android.NDK.R16B | NDK do Android (R16B) | 16.9.31023.347 | Opcional
Component.Android.SDK25.Private | Instalação do SDK do Android (nível da API 25) (instalação local para Desenvolvimento Móvel com C++) | 16.0.28625.61 | Opcional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Opcional
Component.Cocos | Cocos | 16.0.28315.86 | Opcional
Component.Incredibuild | IncrediBuild - Aceleração de Build | 16.5.29721.120 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Opcional
Component.MDD.Android | Ferramentas de desenvolvimento do Android para C++ | 16.0.28517.75 | Opcional
Component.OpenJDK | OpenJDK (distribuição da Microsoft) | 16.1.28811.260 | Opcional
Component.Unreal | Instalador do Unreal Engine | 16.1.28810.153 | Opcional
Component.Unreal.Android | Suporte do IDE do Android para Unreal Engine | 16.1.28810.153 | Opcional
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Opcional
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Opcional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 16.0.28516.191 | Opcional
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 16.1.28829.92 | Opcional
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Opcional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | SDK do Windows 10 (10.0.17763.0) | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | SDK do Windows 10 (10.0.18362.0) | 16.1.28829.92 | Opcional

## <a name="mobile-development-with-c"></a>Desenvolvimento móvel com C++

**ID:** Microsoft.VisualStudio.Workload.NativeMobile

**Descrição:** criar aplicativos de plataforma cruzada para o iOS, Android ou Windows usando o C++.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Android.SDK25.Private | Instalação do SDK do Android (nível da API 25) (instalação local para Desenvolvimento Móvel com C++) | 16.0.28625.61 | Obrigatório
Component.OpenJDK | OpenJDK (distribuição da Microsoft) | 16.1.28811.260 | Obrigatório
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Obrigatório
Component.Android.NDK.R16B | NDK do Android (R16B) | 16.9.31023.347 | Recomendadas
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Recomendadas
Component.MDD.Android | Ferramentas de desenvolvimento do Android para C++ | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Component.Android.NDK.R16B_3264 | NDK do Android (R16B) (32 bits) | 16.9.31023.347 | Opcional
Component.Google.Android.Emulator.API25.Private | Google Android Emulator (Nível da API 25) (instalação local) | 16.1.28810.153 | Opcional
Component.HAXM.Private | Intel HAXM (Hardware Accelerated Execution Manager) (instalação local) | 16.0.28528.71 | Opcional
Component.Incredibuild | IncrediBuild - Aceleração de Build | 16.5.29721.120 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.13 | Opcional
Component.MDD.IOS | Ferramentas de desenvolvimento do iOS para C++ | 16.0.28517.75 | Opcional

## <a name="net-core-cross-platform-development"></a>Desenvolvimento multiplataforma com o .NET Core

**ID:** Microsoft.VisualStudio.Workload.NetCoreTools

**Descrição:** compile aplicativos multiplataforma usando o .NET Core, ASP.NET Core, HTML/JavaScript e contêineres incluindo suporte ao Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Obrigatório
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Obrigatório
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Obrigatório
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft. Componentobject. ClickOnce. publish | Publicação do ClickOnce para .NET Core  | 16.9.31004.209 | Obrigatório
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. DevelopmentTools | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Web | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Obrigatório
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Obrigatório
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Recomendadas
Microsoft.Net.Core.Component.SDK.2.1 | Tempo de execução do .NET Core 2,1 (LTS) | 16.9.31024.58 | Recomendadas
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 16.4.29313.120 | Recomendadas
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.Snapshot | Depurador de instantâneo | 16.5.29813.82 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.TimeTravel | Depurador de Viagem no Tempo | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. DotNetModelBuilder | Construtor de modelos ML.NET (versão prévia) | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft. VisualStudio. Component. WslDebugging | Depuração do .NET Core com WSL 2 | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Ferramentas de nuvem de desenvolvimento para a Web | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | Suporte ao IIS no tempo de desenvolvimento | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.MSIX. Packaging | Ferramentas de empacotamento MSIX | 16.9.31004.209 | Opcional

## <a name="mobile-development-with-net"></a>Desenvolvimento móvel com o .NET

**ID:** Microsoft.VisualStudio.Workload.NetCrossPlat

**Descrição:** criar aplicativos de plataforma cruzada para o iOS, Android ou Windows usando o Xamarin.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.OpenJDK | OpenJDK (distribuição da Microsoft) | 16.1.28811.260 | Obrigatório
Component.Xamarin | Xamarin | 16.9.31004.209 | Obrigatório
Component.Xamarin.RemotedSimulator | Xamarin Remoted Simulator | 16.9.31004.209 | Obrigatório
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft. Componentobject. ClickOnce. publish | Publicação do ClickOnce para .NET Core  | 16.9.31004.209 | Obrigatório
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. DevelopmentTools | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.Merq | Ferramentas internas comuns do Xamarin | 16.2.29012.281 | Obrigatório
Microsoft.VisualStudio.Component.MonoDebugger | Depurador mono | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | Mecanismo de modelagem ASP.NET | 16.9.31004.209 | Obrigatório
Component. Android. SDK30 | Instalação do SDK do Android (nível da API 30) | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas

## <a name="aspnet-and-web-development"></a>Desenvolvimento Web e ASP.NET

**ID:** Microsoft.VisualStudio.Workload.NetWeb

**Descrição:** Crie aplicativos Web usando ASP.NET Core, ASP.NET, HTML/JavaScript e contêineres, incluindo suporte a Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Obrigatório
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Obrigatório
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Obrigatório
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft. Componentobject. ClickOnce. publish | Publicação do ClickOnce para .NET Core  | 16.9.31004.209 | Obrigatório
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. DevelopmentTools | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Web | Ferramentas de desenvolvimento do .NET Core | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Obrigatório
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft. VisualStudio. Componentobject. Web. Client | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Obrigatório
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Recomendadas
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 16.0.28516.191 | Recomendadas
Microsoft.Net.Core.Component.SDK.2.1 | Tempo de execução do .NET Core 2,1 (LTS) | 16.9.31024.58 | Recomendadas
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 16.4.29313.120 | Recomendadas
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 16.0.28625.61 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.Snapshot | Depurador de instantâneo | 16.5.29813.82 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.TimeTravel | Depurador de Viagem no Tempo | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.EntityFramework | Ferramentas do Entity Framework 6 | 16.0.28315.86 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft. VisualStudio. Component. WslDebugging | Depuração do .NET Core com WSL 2 | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas do Azure WebJobs | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Ferramentas de nuvem de desenvolvimento para a Web | 16.9.31004.209 | Recomendadas
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 16.9.31004.209 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 16.9.31004.209 | Opcional
Microsoft.Net. Component. 4.8. TargetingPack | Pacote de direcionamento do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 16.3.29207.166 | Opcional
Microsoft.Net. Componentattribute. 4.8. DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4,8 | 16.4.29318.151 | Opcional
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 16.0.28528.71 | Opcional
Microsoft.VisualStudio.Component.CodeClone | Clone de Código | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.CodeMap | Mapa de Códigos | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | Validação de dependência dinâmica | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.GraphDocument | Editor DGML | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.TestTools.WebLoadTest | Ferramentas de desempenho para a Web e de teste de carga | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.ComponentGroup.AdditionalWebProjectTemplates | Modelos de projeto adicionais (versões anteriores) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | Ferramentas de arquitetura e análise | 16.5.29514.35 | Opcional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | Suporte ao IIS no tempo de desenvolvimento | 16.9.31004.209 | Opcional

## <a name="nodejs-development"></a>Desenvolvimento do Node.js

**ID:** Microsoft.VisualStudio.Workload.Node

**Descrição:** criar aplicativos de rede escaláveis usando o Node.js, um runtime JavaScript controlado por evento assíncrono. 

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Node.Tools | Ferramentas de desenvolvimento em Node.js | 16.5.29515.121 | Obrigatório
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Obrigatório
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Opcional
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Opcional

## <a name="officesharepoint-development"></a>Desenvolvimento para Office/SharePoint

**ID:** Microsoft.VisualStudio.Workload.Office

**Descrição:** criar suplementos do Office e SharePoint, soluções do SharePoint e suplementos do VSTO usando o C#, VB e JavaScript.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Obrigatório
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Obrigatório
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Obrigatório
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 16.0.28517.75 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Obrigatório
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | Ferramentas de desenvolvimento de área de trabalho do .NET | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Sharepoint.Tools | Office Developer Tools para Visual Studio | 16.4.29409.204 | Obrigatório
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Obrigatório
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 16.0.28625.61 | Obrigatório
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.TeamOffice | VSTO (Visual Studio Tools para Office) | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 16.9.31004.209 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 16.9.31004.209 | Opcional
Microsoft.Net. Component. 4.8. TargetingPack | Pacote de direcionamento do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 16.3.29207.166 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 16.3.29207.166 | Opcional
Microsoft.Net. Componentattribute. 4.8. DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4,8 | 16.4.29318.151 | Opcional
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Opcional
Microsoft.VisualStudio.ComponentGroup.Sharepoint.WIF | Windows Identity Foundation 3.5 | 16.0.28621.142 | Opcional

## <a name="python-development"></a>Desenvolvimento em Python

**ID:** Microsoft.VisualStudio.Workload.Python

**Descrição:** edição, depuração, desenvolvimento interativo e controle do código-fonte para o Python.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.PythonTools | Suporte da linguagem Python | 16.5.29515.121 | Obrigatório
Component.CPython3.x64 | Python 3 64 bits (3.7.8) | 3.7.8 | Recomendadas
Component.Microsoft.VisualStudio.LiveShare | Live Share | 1.0.3587 | Recomendadas
Microsoft.Component.PythonTools.Minicondax64 | Miniconda Python | 16.2.29003.222 | Recomendadas
Microsoft.Component.PythonTools.Web | Suporte Web do Python | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 16.4.29409.204 | Recomendadas
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Recomendadas
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Recomendadas
Microsoft. VisualStudio. Component. TypeScript. 4.1 | SDK do TypeScript 4,1 | 16.0.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 16.0.28517.75 | Recomendadas
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento Web e ASP.NET | 16.9.31004.209 | Recomendadas
Component.CPython2.x64 | Python 2 64 bits (2.7.18) | 2.7.18.1 | Opcional
Component.CPython2.x86 | Python 2 32 bits (2.7.18) | 2.7.18.1 | Opcional
Component.CPython3.x86 | Python 3 32 bits (3.7.8) | 3.7.8 | Opcional
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 16.9.31004.209 | Opcional
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 16.9.31004.209 | Opcional
Componente. Microsoft. WebTools. BrowserLink. WebLivePreview | Visualização dinâmica da Web | 0.4.12.14637 | Opcional
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Opcional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Ferramentas de desenvolvimento nativo do Python | 16.9.31004.209 | Opcional
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Opcional
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Opcional
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Opcional
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Opcional
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Opcional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 16.4.29313.120 | Opcional
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 16.9.31019.194 | Opcional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 16.9.31019.194 | Opcional
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 16.4.29318.151 | Opcional
Microsoft.VisualStudio.Component.MSODBC.SQL | Driver ODBC do SQL Server | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | Utilitários de linha de comando do SQL Server | 16.0.28707.177 | Opcional
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Opcional
Microsoft.VisualStudio.Component.SQL.ADAL | runtime do SQL ADAL | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 16.0.28315.86 | Opcional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 16.3.29207.166 | Opcional
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 16.5.29515.121 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK | Runtime C Universal do Windows | 16.4.29409.204 | Opcional
Microsoft. VisualStudio. Component. Windows10SDK. 19041 | SDK do Windows 10 (10.0.19041.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 16.9.31004.209 | Opcional

## <a name="universal-windows-platform-development"></a>Desenvolvimento para a Plataforma Universal do Windows

**ID:** Microsoft.VisualStudio.Workload.Universal

**Descrição:** Crie aplicativos para o Plataforma Universal do Windows com C#, VB ou, opcionalmente, C++.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.NetFX.Native | .NET Nativo | 16.5.29515.121 | Obrigatório
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 16.0.28315.86 | Obrigatório
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 16.0.28517.75 | Obrigatório
Microsoft. NetCore. Component. Runtime. 3.1 | Tempo de execução do .NET Core 3,1 (LTS) | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. Runtime. 5.0 | Tempo de execução do .NET 5,0 | 16.9.31024.58 | Obrigatório
Microsoft. NetCore. Component. SDK | SDK .NET | 16.9.31024.58 | Obrigatório
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Obrigatório
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.Graphics | Editores de imagens e modelos 3D | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 16.0.28315.86 | Obrigatório
Microsoft. VisualStudio. Component. Windows10SDK. 19041 | SDK do Windows 10 (10.0.19041.0) | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.MSIX. Packaging | Ferramentas de empacotamento MSIX | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET Native e .NET Standard | 16.3.29102.218 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.UWP.Support | Ferramentas da Plataforma Universal do Windows | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Ferramentas da Plataforma Universal do Windows para Xamarin | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Opcional
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 16.0.28528.71 | Opcional
Microsoft.VisualStudio.Component.CodeClone | Clone de Código | 16.4.29409.204 | Opcional
Microsoft.VisualStudio.Component.CodeMap | Mapa de Códigos | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | Validação de dependência dinâmica | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.GraphDocument | Editor DGML | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 16.0.28625.61 | Opcional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | Suporte da Plataforma Universal do Windows do C++ para ferramentas de build v142 (ARM64) | 16.3.29207.166 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Funcionalidades principais do C++ | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM | Ferramentas de compilação ARM do MSVC v142-VS 2019 C++ (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (mais recente) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 – ferramentas de build do C++ para VS 2017 ARM (v14.16) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 – ferramentas de build do C++ para VS 2017 ARM64 (v14.16) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 – ferramentas de build do C++ para VS 2017 x64/x86 (v14.16) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | SDK do Windows 10 (10.0.17763.0) | 16.0.28517.75 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.18362 | SDK do Windows 10 (10.0.18362.0) | 16.1.28829.92 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | Conectividade de dispositivos USB | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | Ferramentas de arquitetura e análise | 16.5.29514.35 | Opcional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | Ferramentas da Plataforma Universal do Windows do C++ (v142) | 16.9.31004.209 | Opcional
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141 | Ferramentas da Plataforma Universal do Windows do C++ (v141) | 16.1.28810.153 | Opcional

## <a name="visual-studio-extension-development"></a>Desenvolvimento de extensões do Visual Studio

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtension

**Descrição:** criar complementos e extensões para o Visual Studio, incluindo novos comandos, analisadores de código e janelas de ferramentas.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 16.5.29515.121 | Obrigatório
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 16.0.28517.75 | Obrigatório
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 16.9.31004.209 | Obrigatório
Microsoft. net. Component. 4.8. SDK | SDK do .NET Framework 4,8 | 16.4.29313.120 | Obrigatório
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 16.3.29207.166 | Obrigatório
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 16.1.28829.92 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 16.0.28714.129 | Obrigatório
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.VSSDK | SDK do Visual Studio | 16.0.28315.86 | Obrigatório
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Pré-requisitos para o desenvolvimento de extensões do Visual Studio | 16.9.31004.209 | Obrigatório
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 16.9.31004.209 | Recomendadas
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 16.9.31019.194 | Recomendadas
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 16.5.29515.121 | Recomendadas
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 16.0.28625.61 | Recomendadas
Microsoft.Component.CodeAnalysis.SDK | SDK da Plataforma do Compilador .NET | 16.2.29003.222 | Opcional
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 16.5.29515.121 | Opcional
Microsoft.VisualStudio.Component.DslTools | SDK de Modelagem | 16.0.28315.86 | Opcional

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
Component.GitHub.VisualStudio | Extensão do GitHub para Visual Studio | 2.5.9.5485
Component.Xamarin.Profiler | Criador de perfil do Xamarin | 16.0.28315.86
Microsoft.Component.ClickOnce | Publicação ClickOnce | 16.4.29409.204
Microsoft.Component.HelpViewer | Visualizador da Ajuda | 16.0.28625.61
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 16.4.29409.204
Microsoft.Net.Component.4.6.2.SDK | SDK do .NET Framework 4.6.2 | 16.4.29409.204
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 16.4.29409.204
Microsoft.Net.Component.4.7.2.SDK | SDK do .NET Framework 4.7.2 | 16.4.29409.204
Microsoft.Net.Component.4.7.SDK | SDK do .NET Framework 4.7 | 16.4.29409.204
Microsoft.Net.Core.Component.SDK.2.2 | Tempo de execução do .NET Core 2,2 (sem suporte) | 16.9.31024.58
Microsoft. net. Core. Component. SDK. 3.0 | Tempo de execução do .NET Core 3,0 (sem suporte) | 16.9.31024.58
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | Ferramentas de desenvolvimento mais .NET Core 2,1 | 16.9.31004.209
Microsoft.NetCore.ComponentGroup.Web.2.1 | Ferramentas de desenvolvimento para a Web e .NET Core 2,1 | 16.9.31004.209
Microsoft.VisualStudio.Component.AzureDevOps.OfficeIntegration | Integração do Azure DevOps ao Office | 16.0.28625.61
Microsoft. VisualStudio. Component. Debugger. VSOnline | Depurador para Codespaces do GitHub | 16.9.31004.209
Microsoft.VisualStudio.Component.Git | Git para Windows | 16.0.28625.61
Microsoft.VisualStudio.Component.LinqToSql | Ferramentas do LINQ to SQL | 16.0.28625.61
Microsoft.VisualStudio.Component.TestTools.CodedUITest | Teste de interface do usuário codificado | 16.0.28327.66
Microsoft.VisualStudio.Component.VC.14.20.ARM | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM (v14.20) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.20.ARM.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ARM64 | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM64 (v14.20) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.20.ARM64.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM64 (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL | ATL do C++ v14.20 para ferramentas de build v142 (x86 e x64) | 16.1.28829.92
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM | ATL do C++ v14.20 para ferramentas de build v142 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM.Spectre | ATL do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64 | ATL do C++ v14.20 para ferramentas de build v142 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.ARM64.Spectre | ATL do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.ATL.Spectre | ATL do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (x86 e x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.CLI.Support | Suporte do C++/CLI para ferramentas de build v142 (14.20) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.20.MFC | MFC do C++ v14.20 para ferramentas de build v142 (x86 e x64) | 16.2.29003.222
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM | MFC do C++ v14.20 para ferramentas de build v142 (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM.Spectre | MFC do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64 | MFC do C++ v14.20 para ferramentas de build v142 (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.ARM64.Spectre | MFC do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.MFC.Spectre | MFC do C++ v14.20 para ferramentas de build v142 com Mitigações de Espectro (x86 e x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.20.x86.x64 | MSVC v142 – ferramentas de build do C++ para VS 2019 x64/x86 (v14.20) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.20.x86.x64.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 x64/x86 (v14.20) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ARM | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM (v14.21) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.21.ARM.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM (v14.21) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ARM64 | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM64 (v14.21) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.21.ARM64.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM64 (v14.21) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ATL | ATL do C++ v14.21 para ferramentas de build v142 (x86 e x64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM | ATL do C++ v14.21 para ferramentas de build v142 (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM.Spectre | ATL do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64 | ATL do C++ v14.21 para ferramentas de build v142 (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.ATL.ARM64.Spectre | ATL do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.ATL.Spectre | ATL do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (x86 e x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.CLI.Support | Suporte do C++/CLI para ferramentas de build v142 (14.21) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.14.21.MFC | MFC do C++ v14.21 para ferramentas de build v142 (x86 e x64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM | MFC do C++ v14.21 para ferramentas de build v142 (ARM) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM.Spectre | MFC do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (ARM) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64 | MFC do C++ v14.21 para ferramentas de build v142 (ARM64) | 16.2.29019.55
Microsoft.VisualStudio.Component.VC.14.21.MFC.ARM64.Spectre | MFC do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (ARM64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.MFC.Spectre | MFC do C++ v14.21 para ferramentas de build v142 com Mitigações de Espectro (x86 e x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.14.21.x86.x64 | MSVC v142 – ferramentas de build do C++ para VS 2019 x64/x86 (v14.21) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.14.21.x86.x64.Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 x64/x86 (v14.21) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. ARM | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM (v14.22) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.22. ARM. Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM (v14.22) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. ARM64 | MSVC v142 – ferramentas de build do C++ para VS 2019 ARM64 (v14.22) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.22. ARM64. Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 ARM64 (v14.22) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. ATL | C++ v 14.22 ATL para ferramentas de Build v142 (x86 & x64) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. ATL. ARM | C++ v 14.22 ATL para ferramentas de Build v142 (ARM) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. ATL. ARM. Spectre | C++ v 14.22 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.22. ATL. ARM64 | C++ v 14.22 ATL para ferramentas de Build v142 (ARM64) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. ATL. ARM64. Spectre | C++ v 14.22 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. ATL. Spectre | C++ v 14.22 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. CLI. support | Suporte do C++/CLI para ferramentas de build v142 (14.22) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.22. MFC | C++ v 14.22 MFC para v142 ferramentas de compilação (x86 & x64) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. MFC. ARM | C++ v 14.22 MFC para ferramentas de Build do v142 (ARM) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. MFC. ARM. Spectre | C++ v 14.22 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. MFC. ARM64 | C++ v 14.22 MFC para ARM64 (ferramentas de Build do v142) | 16.4.29313.120
Microsoft. VisualStudio. Component. VC. 14.22. MFC. ARM64. Spectre | C++ v 14.22 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. MFC. Spectre | C++ v 14.22 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.22. x86. x64 | MSVC v142 – ferramentas de build do C++ para VS 2019 x64/x86 (v14.22) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.22. x86. x64. Spectre | MSVC v142 – bibliotecas com mitigação de Espectro do C++ para VS 2019 x64/x86 (v14.22) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.23) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.23. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.23) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (v 14.23) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.23. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.23) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ATL | C++ v 14.23 ATL para ferramentas de Build v142 (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ATL. ARM | C++ v 14.23 ATL para ferramentas de Build v142 (ARM) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ATL. ARM. Spectre | C++ v 14.23 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.23. ATL. ARM64 | C++ v 14.23 ATL para ferramentas de Build v142 (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ATL. ARM64. Spectre | C++ v 14.23 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. ATL. Spectre | C++ v 14.23 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14,23) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.23. MFC | C++ v 14.23 MFC para v142 ferramentas de compilação (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. MFC. ARM | C++ v 14.23 MFC para ferramentas de Build do v142 (ARM) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. MFC. ARM. Spectre | C++ v 14.23 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. MFC. ARM64 | C++ v 14.23 MFC para ARM64 (ferramentas de Build do v142) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. MFC. ARM64. Spectre | C++ v 14.23 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. MFC. Spectre | C++ v 14.23 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.23. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.23) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.23. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.23) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. 14.24. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.24) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.24) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (v 14.24) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.24) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL | C++ v 14.24 ATL para ferramentas de Build v142 (x86 & x64) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL. ARM | C++ v 14.24 ATL para ferramentas de Build v142 (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL. ARM. Spectre | C++ v 14.24 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL. ARM64 | C++ v 14.24 ATL para ferramentas de Build v142 (ARM64) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL. ARM64. Spectre | C++ v 14.24 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. ATL. Spectre | C++ v 14.24 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14,24) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. MFC | C++ v 14.24 MFC para v142 ferramentas de compilação (x86 & x64) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. MFC. ARM | C++ v 14.24 MFC para ferramentas de Build do v142 (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. MFC. ARM. Spectre | C++ v 14.24 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. MFC. ARM64 | C++ v 14.24 MFC para ARM64 (ferramentas de Build do v142) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.24. MFC. ARM64. Spectre | C++ v 14.24 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. MFC. Spectre | C++ v 14.24 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.24) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.24. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.24) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. 14.25. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL | C++ v 14.25 ATL para ferramentas de Build v142 (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL. ARM | C++ v 14.25 ATL para ferramentas de Build v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL. ARM. Spectre | C++ v 14.25 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL. ARM64 | C++ v 14.25 ATL para ferramentas de Build v142 (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL. ARM64. Spectre | C++ v 14.25 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. ATL. Spectre | C++ v 14.25 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14,25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC | C++ v 14.25 MFC para v142 ferramentas de compilação (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC. ARM | C++ v 14.25 MFC para ferramentas de Build do v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC. ARM. Spectre | C++ v 14.25 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC. ARM64 | C++ v 14.25 MFC para ARM64 (ferramentas de Build do v142) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC. ARM64. Spectre | C++ v 14.25 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. MFC. Spectre | C++ v 14.25 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.25. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.25) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL | C++ v 14.26 ATL para ferramentas de Build v142 (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL. ARM | C++ v 14.26 ATL para ferramentas de Build v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL. ARM. Spectre | C++ v 14.26 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL. ARM64 | C++ v 14.26 ATL para ferramentas de Build v142 (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL. ARM64. Spectre | C++ v 14.26 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. ATL. Spectre | C++ v 14.26 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14,26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC | C++ v 14.26 MFC para v142 ferramentas de compilação (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC. ARM | C++ v 14.26 MFC para ferramentas de Build do v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC. ARM. Spectre | C++ v 14.26 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC. ARM64 | C++ v 14.26 MFC para ARM64 (ferramentas de Build do v142) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC. ARM64. Spectre | C++ v 14.26 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. MFC. Spectre | C++ v 14.26 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.26. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.26) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ARM64 | MSVC v142-VS 2019 C++ ARM64 Build Tools (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL | C++ v 14.27 ATL para ferramentas de Build v142 (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL. ARM | C++ v 14.27 ATL para ferramentas de Build v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL. ARM. Spectre | C++ v 14.27 ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL. ARM64 | C++ v 14.27 ATL para ferramentas de Build v142 (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL. ARM64. Spectre | C++ v 14.27 ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. ATL. Spectre | C++ v 14.27 ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14,27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC | C++ v 14.27 MFC para v142 ferramentas de compilação (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC. ARM | C++ v 14.27 MFC para ferramentas de Build do v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC. ARM. Spectre | C++ v 14.27 MFC para v142 ferramentas de Build com mitigações Spectres (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC. ARM64 | C++ v 14.27 MFC para ARM64 (ferramentas de Build do v142) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC. ARM64. Spectre | C++ v 14.27 MFC para v142 ferramentas de Build com mitigações Spectres (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. MFC. Spectre | C++ v 14.27 MFC para v142 ferramentas de Build com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.27. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.27) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ARM | Ferramentas de Build do ARM MSVC v142-VS 2019 C++ (v 14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ARM. Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (v 14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ARM64 | Ferramentas de Build do MSVC v142-VS 2019 C++ ARM64 (v 14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ARM64. Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (v 14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL. ARM | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL. ARM. Spectre | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL. ARM64 | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL. ARM64. Spectre | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. ATL. Spectre | C++ v 14.28 (16,8) ATL para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. CLI. support | Suporte a C++/CLI para ferramentas de Build do v142 (14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC | C++ v 14.28 (16,8) MFC para ferramentas de Build do v142 (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC. ARM | C++ v 14.28 (16,8) MFC para ferramentas de Build do v142 (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC. ARM. Spectre | C++ v 14.28 (16,8) MFC para ferramentas de Build v142 com mitigações Spectre (ARM) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC. ARM64 | C++ v 14.28 (16,8) MFC para ARM64 (ferramentas de Build do v142) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC. ARM64. Spectre | C++ v 14.28 (16,8) MFC para ferramentas de Build v142 com mitigações Spectre (ARM64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. MFC. Spectre | C++ v 14.28 (16,8) MFC para ferramentas de Build v142 com mitigações Spectre (x86 & x64) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. x86. x64 | Ferramentas de Build MSVC v142-VS 2019 C++ x64/x86 (v 14.28-16.8) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. 14.28. x86. x64. Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (v 14.28-16.8) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.ATL.ARM | C++ ATL para as ferramentas de Build v142 mais recentes (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | C++ ATL para as ferramentas de Build v142 mais recentes com mitigações de Spectre (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | C++ ATL para as ferramentas de Build v142 mais recentes (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | C++ ATL para as ferramentas de Build v142 mais recentes com mitigações de Spectre (ARM64) | 16.5.29515.121
Microsoft. VisualStudio. Component. VC. ATL. ARM64EC | C++ ATL para as ferramentas de Build v142 mais recentes (ARM64EC-experimental) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. ATL. ARM64EC. Spectre | C++ ATL para as ferramentas de Build v142 mais recentes com mitigações Spectres (ARM64EC-experimental) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.ATL.Spectre | C++ ATL para as ferramentas de Build v142 mais recentes com atenuações do Spectre (x86 & x64) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | C++ MFC para ferramentas de Build v142 mais recentes com atenuações do Spectre (x86 & x64) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.MFC.ARM | C++ MFC para as ferramentas de Build v142 mais recentes (ARM) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | C++ MFC para ferramentas de Build v142 mais recentes com mitigações de Spectre (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | MFC do C++ para as ferramentas de Build do v142 mais recentes (ARM64) | 16.4.29313.120
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | C++ MFC para ferramentas de Build v142 mais recentes com mitigações Spectre (ARM64) | 16.5.29721.120
Microsoft. VisualStudio. Component. VC. MFC. ARM64EC | C++ MFC para as ferramentas de Build v142 mais recentes (ARM64EC – experimental) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. MFC. ARM64EC. Spectre | C++ MFC para ferramentas de Build v142 mais recentes com mitigações Spectres (ARM64EC-experimental) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.Redist.MSM | MSMs dos Pacotes Redistribuíveis do C++ 2019 | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v142-VS 2019 C++ ARM Spectre-mitigated bibliotecas (mais recente) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | MSVC v142-VS 2019 C++ ARM64 Spectre-mitigated bibliotecas (mais recente) | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. Runtimes. ARM64EC. Spectre | MSVC v142-VS 2019 C++ ARM64EC Spectre-mitigated bibliotecas (mais recente-experimental) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | MSVC v142-VS 2019 C++ x64/x86 Spectre-mitigated bibliotecas (mais recente)  | 16.9.31004.209
Microsoft. VisualStudio. Component. VC. Tools. ARM64EC | MSVC v142-VS 2019 C++ ARM64EC Build Tools (mais recente – experimental) | 16.9.31004.209
Microsoft.VisualStudio.Component.VC.v141.ARM.Spectre | MSVC v141 – bibliotecas com mitigação de Espectro do C++ para VS 2017 ARM (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.v141.ARM64.Spectre | MSVC v141 – bibliotecas com mitigação de Espectro do C++ para VS 2017 ARM64 (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VC.v141.ATL | ATL do C++ para ferramentas de build v141 (x86 e x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM | ATL do C++ para ferramentas de build v141 (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM.Spectre | ATL do C++ para ferramentas de build v141 com Mitigações de Espectro (ARM) | 16.5.29721.120
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64 | ATL do C++ para ferramentas de build v141 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64.Spectre | ATL do C++ para ferramentas de build v141 com Mitigações de Espectro (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.ATL.Spectre | ATL do C++ para ferramentas de build v141 com Mitigações de Espectro (x86 e x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.CLI.Support | Suporte do C++/CLI para ferramentas de build v141 (14.16) | 16.3.29207.166
Microsoft.VisualStudio.Component.VC.v141.MFC | MFC do C++ para ferramentas de build v141 (x86 e x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM | MFC do C++ para ferramentas de build v141 (ARM) | 16.2.28915.88
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM.Spectre | MFC do C++ para ferramentas de build v141 com Mitigações de Espectro (ARM) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64 | MFC do C++ para ferramentas de build v141 (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64.Spectre | MFC do C++ para ferramentas de build v141 com Mitigações de Espectro (ARM64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.MFC.Spectre | MFC do C++ para ferramentas de build v141 com Mitigações de Espectro (x86 e x64) | 16.0.28625.61
Microsoft.VisualStudio.Component.VC.v141.x86.x64.Spectre | MSVC v141 – bibliotecas com mitigação de Espectro do C++ para VS 2017 x64/x86 (v14.16) | 16.5.29515.121
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 16.0.28707.177
Microsoft.VisualStudio.Component.WinXP | Suporte do Windows XP do C++ para ferramentas do VS 2017 (v141) [Preterido] | 16.9.31004.209
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 16.9.31004.209

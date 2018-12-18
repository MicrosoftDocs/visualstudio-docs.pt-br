---
title: IDs de carga de trabalho e de componente do Visual Studio Community 2017
description: Use as IDs de carga de trabalho e de componente para instalar o Visual Studio usando a linha de comando ou para especificar como uma dependência em um manifesto do VSIX
keywords: ''
author: TerryGLee
ms.author: tglee
manager: douge
ms.date: 11/13/2018
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.service: ''
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.assetid: 58494fc3-12de-4761-bd4a-74b54f72bfb3
ms.workload:
- multiple
ms.openlocfilehash: 5bf5e1487910156dfd547ae563451bd2f2d428d9
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607959"
---
# <a name="visual-studio-community-2017-component-directory"></a>Diretório de componentes do Visual Studio Community 2017

As tabelas desta página listam as IDs que podem ser usadas para instalar o Visual Studio usando a linha de comando ou que podem ser especificadas como uma dependência em um manifesto do VSIX. Observe que adicionaremos outros componentes conforme atualizações forem liberadas para o Visual Studio.

Além disso, observe o seguinte sobre a página:

* Cada carga de trabalho tem sua própria seção, seguida pela ID da carga de trabalho e por uma tabela dos componentes que estão disponíveis para a carga de trabalho.
* Por padrão, os componentes **Obrigatórios** serão instalados durante a instalação da carga de trabalho.
* Se preferir, também será possível instalar os componentes **Recomendados** e **Opcionais**.
* Também adicionamos uma seção que lista os componentes adicionais que não são afiliados a nenhuma carga de trabalho.

Ao definir dependências no manifesto do VSIX, é necessário especificar somente IDs de Componente. Use as tabelas desta página para determinar nossas dependências mínimas de componente. Em alguns cenários, isso pode significar que somente um componente de uma carga de trabalho é especificado. Em outros cenários, isso pode significar que vários componentes de uma única carga de trabalho ou que vários componentes de várias cargas de trabalho são especificados. Para obter mais informações, consulte a página [Como migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

Para obter mais informações sobre como usar essas IDs, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md). Além disso, para obter uma lista de IDs de carga de trabalho e de componente para outros produtos, consulte a página [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md).

## <a name="visual-studio-core-editor-included-with-visual-studio-community-2017"></a>Principal editor do Visual Studio (incluído no Visual Studio Community 2017)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**Descrição:** a experiência de shell do Visual Studio Core, incluindo a edição de código com reconhecimento de sintaxe, controle do código-fonte e gerenciamento de itens de trabalho.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Editor do Visual Studio Core | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | Página inicial do Visual Studio para usuários C++ | 15.0.27128.1 | Opcional

## <a name="azure-development"></a>Desenvolvimento do Azure

**ID:** Microsoft.VisualStudio.Workload.Azure

**Descrição:** SDKs do Azure, ferramentas e projetos para desenvolver aplicativos na nuvem, criar recursos e criação de Contêineres incluindo suporte a Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Necessária
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Necessária
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Necessária
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Component.NetFX.Core.Runtime | Tempo de execução do .NET Core | 15.0.26208.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.Web.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 15.0.26621.2 | Necessária
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | Necessária
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 15.8.27705.0 | Necessária
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Necessária
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Pré-requisitos de desenvolvimento do Azure | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.Component.Azure.DataLake.Tools | Ferramentas Azure Data Lake e Stream Analytics | 15.9.28107.0 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.MobileAppsSdk | SDK dos Aplicativos Móveis do Azure | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Principais ferramentas do Azure Resource Manager | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Ferramentas do Service Fabric | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Ferramentas dos Serviços de Nuvem do Azure | 15.0.26504.0 | Recomendado
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Ferramentas do Azure Resource Manager | 15.0.27005.2 | Recomendado
Microsoft.Net.Component.4.6.2.SDK | SDK do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.2.SDK | SDK do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.SDK | SDK do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional
Microsoft.NetCore.1x.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 1.0 – 1.1 para Web | 15.6.27406.0 | Opcional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.8.27729.1 | Opcional
Microsoft.NetCore.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.Azure.Storage.AzCopy | AzCopy do Armazenamento do Azure | 15.0.26906.1 | Opcional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Opcional

## <a name="data-storage-and-processing"></a>Armazenamento de dados e processamento

**ID:** Microsoft.VisualStudio.Workload.Data

**Descrição:** conectar, desenvolver e testar soluções de dados com o SQL Server, Azure Data Lake ou Hadoop.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Recomendado
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Recomendado
Component.Redgate.SQLSearch.VSExtension | Redgate SQL Search | 3.1.7.2062 | Recomendado
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Recomendado
Microsoft.Component.Azure.DataLake.Tools | Ferramentas Azure Data Lake e Stream Analytics | 15.9.28107.0 | Recomendado
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Recomendado
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 15.0.26621.2 | Recomendado
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | Recomendado
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Recomendado
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Recomendado
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Recomendado
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Recomendado
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 15.8.27825.0 | Opcional

## <a name="data-science-and-analytical-applications"></a>Ciência de dados e aplicativos analíticos

**ID:** Microsoft.VisualStudio.Workload.DataScience

**Descrição:** linguagens e ferramentas para criar aplicativos de ciência de dados, incluindo Python, R e F#.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Anaconda3.x64 | Anaconda3 64 bits (5.2.0) | 5.2.0 | Recomendado
Microsoft.Component.CookiecutterTools | Suporte do modelo Cookiecutter | 15.0.26621.2 | Recomendado
Microsoft.Component.PythonTools | Suporte da linguagem Python | 15.0.26823.1 | Recomendado
Microsoft.Component.PythonTools.Web | Suporte Web do Python | 15.9.28107.0 | Recomendado
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Recomendado
Microsoft.VisualStudio.Component.R.Open | Microsoft R Client (3.3.2) | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.RHost | Suporte de tempo de execução para ferramentas de desenvolvimento do R | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.RTools | Suporte à linguagem R | 15.0.26919.1 | Recomendado
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Recomendado
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Component.Anaconda2.x64 | Anaconda2 64 bits (5.2.0) | 5.2.0 | Opcional
Component.Anaconda2.x86 | Anaconda2 32 bits (5.2.0) | 5.2.0 | Opcional
Component.Anaconda3.x86 | Anaconda3 32 bits (5.2.0) | 5.2.0 | Opcional
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 15.6.27309.0 | Opcional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Ferramentas de desenvolvimento nativo do Python | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Graphics.Win81 | SDK das Ferramentas de Gráficos do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.140 | Conjunto de ferramentas do VC++ 2015.3 v14.00 (v140) para área de trabalho | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 15.0.26823.1 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK | Tempo de execução C Universal do Windows | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.Component.Windows81SDK | SDK do Windows 8.1 | 15.6.27406.0 | Opcional

## <a name="net-desktop-development"></a>Desenvolvimento de área de trabalho do .NET

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktop

**Descrição:** criar aplicativos do WPF, do Windows Forms e de console usando C#, Visual Basic e F#.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | Ferramentas de desenvolvimento de área de trabalho do .NET | 15.7.27625.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 15.0.27005.2 | Recomendado
Microsoft.VisualStudio.Component.EntityFramework | Ferramentas do Entity Framework 6 | 15.6.27406.0 | Recomendado
Component.Dotfuscator | Proteção PreEmptive – Dotfuscator | 15.0.26208.0 | Opcional
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Opcional
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Opcional
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Opcional
Microsoft.Net.Component.4.6.2.SDK | SDK do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.2.SDK | SDK do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.SDK | SDK do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Opcional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.8.27729.1 | Opcional
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Opcional
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.FSharp.Desktop | Suporte à linguagem F# da área de trabalho | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Opcional
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Opcional
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Opcional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Opcional
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Opcional
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Opcional

## <a name="game-development-with-unity"></a>Desenvolvimento de jogos com Unity

**ID:** Microsoft.VisualStudio.Workload.ManagedGame

**Descrição:** criar jogos 2D e 3D com o Unity, um ambiente de desenvolvimento avançado de plataforma cruzada.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Component.3.5.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 3.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.Unity | Ferramentas do Visual Studio para Unity | 15.7.27617.1 | Necessária
Component.UnityEngine.x64 | Editor de 64 bits do Unity 2018.1 | 15.8.27924.0 | Recomendado
Component.UnityEngine.x86 | Editor de 32 bits do Unity 5.6 | 15.6.27406.0 | Recomendado

## <a name="linux-development-with-c"></a>Desenvolvimento de Linux com C++

**ID:** Microsoft.VisualStudio.Workload.NativeCrossPlat

**Descrição:** criar e depurar aplicativos executados em um ambiente Linux.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.MDD.Linux | Desenvolvimento do Visual C++ para Linux | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK | Tempo de execução C Universal do Windows | 15.6.27406.0 | Necessária
Component.Linux.CMake | Ferramentas do Visual C++ para CMake e Linux | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Recomendado
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Component.MDD.Linux.GCC.arm | Desenvolvimento Incorporado e de IoT | 15.6.27309.0 | Opcional

## <a name="desktop-development-with-c"></a>Desenvolvimento de área de trabalho com o C++

**ID:** Microsoft.VisualStudio.Workload.NativeDesktop

**Descrição:** compile aplicativos de área de trabalho do Windows usando o conjunto de ferramentas Microsoft C++, o ATL ou o MFC.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Atualização Redistribuível do Visual C++ 2017 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | Principais recursos de área de trabalho do Visual C++ | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Debugger.JustInTime | Depurador Just-In-Time | 15.0.27005.2 | Recomendado
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Graphics.Win81 | SDK das Ferramentas de Gráficos do Windows 8.1 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Recomendado
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.VC.ATL | Visual C++ ATL para x86 e x64 | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.VC.CMake.Project | Ferramentas do Visual C++ para CMake | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 15.0.26823.1 | Recomendado
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Adaptador de Teste para Boost.Test | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Adaptador de Teste para Google Test | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Recomendado
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Component.Incredibuild | IncrediBuild - Aceleração de Build | 15.7.27617.1 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Opcional
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 15.6.27309.0 | Opcional
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.140 | Conjunto de ferramentas do VC++ 2015.3 v14.00 (v140) para área de trabalho | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.VC.ATLMFC | Visual C++ MFC para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.CLI.Support | Suporte ao C++/CLI | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | Módulos de Biblioteca Padrão (experimental) | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | SDK do Windows 10 (10.0.10240.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | SDK do Windows 10 (10.0.10586.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | SDK do Windows 10 (10.0.14393.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | SDK do Windows 10 (10.0.15063.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | SDK do Windows 10 (10.0.15063.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | SDK do Windows 10 (10.0.15063.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [ARM e ARM64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | SDK do Windows 10 (10.0.16299.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | SDK do Windows 10 (10.0.16299.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows81SDK | SDK do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.WinXP | Suporte do Windows XP para C++ | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | SDK do Windows 8.1 e SDK do UCRT | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.WinXP | Suporte do Windows XP para C++ | 15.8.27705.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | SDK do Windows 10 (10.0.15063.0) | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 15.8.27825.0 | Opcional

## <a name="game-development-with-c"></a>Desenvolvimento de jogos com C++

**ID:** Microsoft.VisualStudio.Workload.NativeGame

**Descrição:** usar todo o poder do C++ para criar jogos profissionais da plataforma DirectX, Unreal ou Cocos2d.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Atualização Redistribuível do Visual C++ 2017 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK | Tempo de execução C Universal do Windows | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Graphics.Win81 | SDK das Ferramentas de Gráficos do Windows 8.1 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 15.0.26823.1 | Recomendado
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Recomendado
Component.Android.NDK.R12B | NDK do Android (R12B) | 12.1.10 | Opcional
Component.Android.SDK23.Private | Instalação do SDK do Android (nível 23 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Opcional
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Opcional
Component.Cocos | Cocos | 15.0.26906.1 | Opcional
Component.Incredibuild | IncrediBuild - Aceleração de Build | 15.7.27617.1 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Opcional
Component.JavaJDK | Java SE Development Kit (8.0.1120.15) | 15.6.27406.0 | Opcional
Component.MDD.Android | Ferramentas de desenvolvimento do Android para C++ | 15.0.26606.0 | Opcional
Component.OpenJDK | OpenJDK de distribuição da Microsoft | 15.9.28125.51 | Opcional
Component.Unreal | Instalador do Unreal Engine | 15.8.27729.1 | Opcional
Component.Unreal.Android | Suporte ao Visual Studio Android para Unreal Engine | 15.0.27005.2 | Opcional
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 15.6.27309.0 | Opcional
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Opcional
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Opcional
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | SDK do Windows 10 (10.0.10240.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | SDK do Windows 10 (10.0.10586.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | SDK do Windows 10 (10.0.14393.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | SDK do Windows 10 (10.0.15063.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | SDK do Windows 10 (10.0.15063.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | SDK do Windows 10 (10.0.15063.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [ARM e ARM64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | SDK do Windows 10 (10.0.16299.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | SDK do Windows 10 (10.0.16299.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows81SDK | SDK do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 | SDK do Windows 8.1 e SDK do UCRT | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | SDK do Windows 10 (10.0.15063.0) | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 15.8.27825.0 | Opcional

## <a name="mobile-development-with-c"></a>Desenvolvimento móvel com C++

**ID:** Microsoft.VisualStudio.Workload.NativeMobile

**Descrição:** criar aplicativos de plataforma cruzada para o iOS, Android ou Windows usando o C++.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Android.SDK19.Private | Instalação do SDK do Android (nível 19 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28107.0 | Necessária
Component.Android.SDK21.Private | Instalação do SDK do Android (nível 21 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Necessária
Component.Android.SDK22.Private | Instalação do SDK do Android (nível 22 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Necessária
Component.Android.SDK23.Private | Instalação do SDK do Android (nível 23 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Necessária
Component.Android.SDK25.Private | Instalação do SDK do Android (nível 25 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Necessária
Component.OpenJDK | OpenJDK de distribuição da Microsoft | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Necessária
Component.Android.NDK.R15C | NDK do Android (R15C) | 15.2.1 | Recomendado
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | Recomendado
Component.MDD.Android | Ferramentas de desenvolvimento do Android para C++ | 15.0.26606.0 | Recomendado
Component.Android.NDK.R12B | NDK do Android (R12B) | 12.1.10 | Opcional
Component.Android.NDK.R12B_3264 | NDK do Android (R12B) (32 bits) | 12.1.11 | Opcional
Component.Android.NDK.R13B | NDK do Android (R13B) | 13.1.7 | Opcional
Component.Android.NDK.R13B_3264 | NDK do Android (R13B) (32 bits) | 13.1.8 | Opcional
Component.Android.NDK.R15C_3264 | NDK do Android (R15C) (32 bits) | 15.2.1 | Opcional
Component.Google.Android.Emulator.API23.Private | Emulador do Google Android (API Nível 23) (instalação local) | 15.6.27413.0 | Opcional
Component.HAXM.Private | Intel HAXM (Hardware Accelerated Execution Manager) (instalação local) | 15.6.27413.0 | Opcional
Component.Incredibuild | IncrediBuild - Aceleração de Build | 15.7.27617.1 | Opcional
Component.IncredibuildMenu | IncrediBuildMenu | 1.5.0.2 | Opcional
Component.MDD.IOS | Ferramentas de desenvolvimento do iOS para C++ | 15.0.26621.2 | Opcional

## <a name="net-core-cross-platform-development"></a>Desenvolvimento de plataforma cruzada do .NET Core

**ID:** Microsoft.VisualStudio.Workload.NetCoreTools

**Descrição:** compile aplicativos multiplataforma usando o .NET Core, ASP.NET Core, HTML/JavaScript e contêineres incluindo suporte ao Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Necessária
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Necessária
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.Web.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 15.8.27705.0 | Necessária
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Necessária
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 15.0.26621.2 | Recomendado
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | Recomendado
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Ferramentas de nuvem de desenvolvimento para a Web | 15.8.27729.1 | Recomendado
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional
Microsoft.NetCore.1x.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 1.0 – 1.1 para Web | 15.6.27406.0 | Opcional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.8.27729.1 | Opcional
Microsoft.NetCore.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | Suporte ao IIS no tempo de desenvolvimento | 15.9.28219.51 | Opcional

## <a name="mobile-development-with-net"></a>Desenvolvimento móvel com o .NET

**ID:** Microsoft.VisualStudio.Workload.NetCrossPlat

**Descrição:** criar aplicativos de plataforma cruzada para o iOS, Android ou Windows usando o Xamarin.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Xamarin | Xamarin | 15.8.27906.1 | Necessária
Component.Xamarin.RemotedSimulator | Xamarin Remoted Simulator | 15.6.27323.2 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Necessária
Microsoft.NetCore.ComponentGroup.DevelopmentTools | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Merq | Ferramentas internas comuns do Xamarin | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.MonoDebugger | Depurador mono | 15.0.26720.2 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | Mecanismo de modelagem ASP.NET | 15.8.27729.1 | Necessária
Component.Android.SDK27 | Instalação do SDK do Android (nível 27 da API) | 15.9.28016.0 | Recomendado
Component.Google.Android.Emulator.API27 | Google Android Emulator (nível 27 da API) | 15.9.28016.0 | Recomendado
Component.HAXM | Intel HAXM (Hardware Accelerated Execution Manager) (instalação global) | 15.6.27413.0 | Recomendado
Component.OpenJDK | OpenJDK de distribuição da Microsoft | 15.9.28125.51 | Recomendado
Component.Xamarin.Inspector | Xamarin Workbooks | 15.0.26606.0 | Opcional
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Opcional
Microsoft.Component.NetFX.Native | .NET Nativo | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.Graphics | Editores de imagens e modelos 3D | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Ferramentas da Plataforma Universal do Windows para Xamarin | 15.7.27617.1 | Opcional

## <a name="aspnet-and-web-development"></a>Desenvolvimento do ASP.NET e para a Web

**ID:** Microsoft.VisualStudio.Workload.NetWeb

**Descrição:** compile aplicativos Web usando ASP.NET, ASP.NET Core, HTML/JavaScript e contêineres incluindo suporte ao Docker.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Necessária
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Necessária
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.ComponentGroup.Web.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.FSharp | Suporte à linguagem F# | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.FSharp.WebTemplates | Suporte à linguagem F# para projetos Web | 15.8.27705.0 | Necessária
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Necessária
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Component.Microsoft.VisualStudio.Web.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 15.0.26621.2 | Recomendado
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.CloudExplorer | Cloud Explorer | 15.9.28230.55 | Recomendado
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.EntityFramework | Ferramentas do Entity Framework 6 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Ferramentas Microsoft Azure WebJobs | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | Ferramentas de nuvem de desenvolvimento para a Web | 15.8.27729.1 | Recomendado
Microsoft.Net.Component.4.6.2.SDK | SDK do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.2.SDK | SDK do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.SDK | SDK do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional
Microsoft.NetCore.1x.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 1.0 – 1.1 para Web | 15.6.27406.0 | Opcional
Microsoft.NetCore.ComponentGroup.DevelopmentTools | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.8.27729.1 | Opcional
Microsoft.NetCore.ComponentGroup.Web | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | Suporte ao IIS no tempo de desenvolvimento | 15.9.28219.51 | Opcional
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 15.6.27406.0 | Opcional

## <a name="nodejs-development"></a>Desenvolvimento do Node.js

**ID:** Microsoft.VisualStudio.Workload.Node

**Descrição:** criar aplicativos de rede escaláveis usando o Node.js, um tempo de execução JavaScript controlado por evento assíncrono. 

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.Node.Build | Suporte ao MSBuild do Node.js | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Node.Tools | Suporte ao desenvolvimento em Node.js | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.TestTools.Core | Principais recursos das ferramentas de teste | 15.7.27520.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional

## <a name="officesharepoint-development"></a>Desenvolvimento para Office/SharePoint

**ID:** Microsoft.VisualStudio.Workload.Office

**Descrição:** criar suplementos do Office e SharePoint, soluções do SharePoint e suplementos do VSTO usando o C#, VB e JavaScript.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Necessária
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Necessária
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | Ferramentas de desenvolvimento de área de trabalho do .NET | 15.7.27625.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Sharepoint.Tools | Office Developer Tools para Visual Studio | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Necessária
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.TeamOffice | VSTO (Visual Studio Tools para Office) | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.Net.Component.4.6.2.SDK | SDK do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.2.SDK | SDK do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.Component.4.7.SDK | SDK do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.TargetingPack | Pacote de direcionamento do .NET Framework 4.7 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.6.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.6.2 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.1.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.1 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.2.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7.2 | 15.8.27825.0 | Opcional
Microsoft.Net.ComponentGroup.4.7.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 4.7 | 15.6.27406.0 | Opcional

## <a name="python-development"></a>Desenvolvimento do Python

**ID:** Microsoft.VisualStudio.Workload.Python

**Descrição:** edição, depuração, desenvolvimento interativo e controle do código-fonte para o Python.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.PythonTools | Suporte da linguagem Python | 15.0.26823.1 | Necessária
Component.CPython3.x64 | Python 3 64 bits (3.6.6) | 3.6.6 | Recomendado
Microsoft.Component.CookiecutterTools | Suporte do modelo Cookiecutter | 15.0.26621.2 | Recomendado
Microsoft.Component.PythonTools.Web | Suporte Web do Python | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Recomendado
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Recomendado
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Recomendado
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Recomendado
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Recomendado
Component.Anaconda2.x64 | Anaconda2 64 bits (5.2.0) | 5.2.0 | Opcional
Component.Anaconda2.x86 | Anaconda2 32 bits (5.2.0) | 5.2.0 | Opcional
Component.Anaconda3.x64 | Anaconda3 64 bits (5.2.0) | 5.2.0 | Opcional
Component.Anaconda3.x86 | Anaconda3 32 bits (5.2.0) | 5.2.0 | Opcional
Component.CPython2.x64 | Python 2 64 bits (2.7.14) | 2.7.14 | Opcional
Component.CPython2.x86 | Python 2 32 bits (2.7.14) | 2.7.14 | Opcional
Component.CPython3.x86 | Python 3 32 bits (3.6.6) | 3.6.6 | Opcional
Component.Microsoft.VisualStudio.RazorExtension | Razor Language Services | 15.0.26720.2 | Opcional
Component.Microsoft.Web.LibraryManager | Gerenciador de Biblioteca | 15.8.27705.0 | Opcional
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Opcional
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Opcional
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Opcional
Microsoft.Component.NetFX.Native | .NET Nativo | 15.0.26208.0 | Opcional
Microsoft.Component.PythonTools.UWP | Suporte ao Python IoT | 15.0.26606.0 | Opcional
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 15.6.27309.0 | Opcional
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Ferramentas de desenvolvimento nativo do Python | 15.8.27729.1 | Opcional
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Opcional
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Emulador de Computação do Azure | 15.0.26621.2 | Opcional
Microsoft.VisualStudio.Component.Azure.Storage.Emulator | Emulador de Armazenamento do Azure | 15.9.28125.51 | Opcional
Microsoft.VisualStudio.Component.Azure.Waverton | Principais ferramentas dos Serviços de Nuvem do Azure | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.DockerTools | Ferramentas de desenvolvimento de contêiner | 15.8.27906.1 | Opcional
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.Graphics | Editores de imagens e modelos 3D | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Graphics.Win81 | SDK das Ferramentas de Gráficos do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.ManagedDesktop.Core | Núcleo da carga de trabalho de área de trabalho gerenciada | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Opcional
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.SQL.ADAL | Tempo de execução do SQL ADAL | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.SQL.CMDUtils | Utilitários de linha de comando do SQL Server | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.SQL.DataSources | Fontes de dados para suporte do SQL Server | 15.0.26621.2 | Opcional
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2016 LocalDB | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.SQL.NCLI | SQL Server Native Client | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.SQL.SSDT | Ferramentas de dados do SQL Server | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.VC.140 | Conjunto de ferramentas do VC++ 2015.3 v14.00 (v140) para área de trabalho | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.DiagnosticTools | Ferramentas de criação de perfil do C++ | 15.0.26823.1 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional
Microsoft.VisualStudio.Component.Web | Ferramentas de desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK | Tempo de execução C Universal do Windows | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | SDK do Windows 10 (10.0.10586.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.Component.Windows81SDK | SDK do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Web | Pré-requisitos de ferramentas de desenvolvimento do ASP.NET e para a Web | 15.9.28219.51 | Opcional

## <a name="universal-windows-platform-development"></a>Desenvolvimento na Plataforma Universal do Windows

**ID:** Microsoft.VisualStudio.Workload.Universal

**Descrição:** criar aplicativos para a Plataforma Universal do Windows com o C#, VB, JavaScript ou, opcionalmente, o C++.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.NetFX.Native | .NET Nativo | 15.0.26208.0 | Necessária
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Graphics | Editores de imagens e modelos 3D | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Component.UWP.Support | Ferramentas da Plataforma Universal do Windows | 15.9.28119.51 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | Ferramentas da Plataforma Universal do Windows para Cordova | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET Native e .NET Standard | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | Ferramentas da Plataforma Universal do Windows para Xamarin | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Microsoft.Component.VC.Runtime.OSSupport | Tempo de execução Visual C++ para UWP | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Graphics.Tools | Depurador de gráficos e criador de perfil de GPU do DirectX | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Graphics.Win81 | SDK das Ferramentas de Gráficos do Windows 8.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Emulador móvel do Windows 10 (Fall Creators Update) | 15.0.27406.0 | Opcional
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | Ferramentas da Plataforma Universal do Windows para ARM64 | 15.0.28125.51 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM | Compiladores e bibliotecas do Visual C++ para o ARM | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | Compiladores e bibliotecas do Visual C++ para ARM64 | 15.9.28230.55 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10240 | SDK do Windows 10 (10.0.10240.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.10586 | SDK do Windows 10 (10.0.10586.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.14393 | SDK do Windows 10 (10.0.14393.0) | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop | SDK do Windows 10 (10.0.15063.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP | SDK do Windows 10 (10.0.15063.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.15063.UWP.Native | SDK do Windows 10 (10.0.15063.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [x86 e x64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm | SDK do Windows 10 (10.0.16299.0) para Desktop C++ [ARM e ARM64] | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP | SDK do Windows 10 (10.0.16299.0) para UWP: C#, VB, JS | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.16299.UWP.Native | SDK do Windows 10 (10.0.16299.0) para UWP: C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17763 | SDK do Windows 10 (10.0.17763.0) | 15.9.28218.60 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | Conectividade de dispositivos USB | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.UWP.VC | Ferramentas da Plataforma Universal do Windows para C++ | 15.9.28107.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | SDK do Windows 10 (10.0.15063.0) | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 15.8.27825.0 | Opcional

## <a name="visual-studio-extension-development"></a>Desenvolvimento de extensões do Visual Studio

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtension

**Descrição:** criar complementos e extensões para o Visual Studio, incluindo novos comandos, analisadores de código e janelas de ferramentas.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.PortableLibrary | Pacote de direcionamento da Biblioteca Portátil do .NET | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VSSDK | SDK do Visual Studio | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Pré-requisitos para o desenvolvimento de extensões do Visual Studio | 15.7.27625.0 | Necessária
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.TextTemplating | Transformação de modelo de texto | 15.0.26208.0 | Recomendado
Component.Dotfuscator | Proteção PreEmptive – Dotfuscator | 15.0.26208.0 | Opcional
Microsoft.Component.CodeAnalysis.SDK | SDK da Plataforma do Compilador .NET | 15.0.27729.1 | Opcional
Microsoft.Component.VC.Runtime.OSSupport | Tempo de execução Visual C++ para UWP | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.ClassDesigner | Designer de Classe | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.DslTools | SDK de Modelagem | 15.0.27005.2 | Opcional
Microsoft.VisualStudio.Component.VC.ATL | Visual C++ ATL para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.ATLMFC | Visual C++ MFC para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.CoreIde | Principais recursos do Visual Studio C++ | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional

## <a name="mobile-development-with-javascript"></a>Desenvolvimento móvel com JavaScript

**ID:** Microsoft.VisualStudio.Workload.WebCrossPlat

**Descrição:** criar aplicativos Android, iOS e UWP usando as Ferramentas para Apache Cordova.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Component.CordovaToolset.6.3.1 | Conjunto de ferramentas do Cordova 6.3.1 | 15.7.27625.0 | Necessária
Component.WebSocket | WebSocket4Net | 15.0.26606.0 | Necessária
Microsoft.VisualStudio.Component.Cordova | Desenvolvimento móvel com os principais recursos do JavaScript | 15.0.26606.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | Diagnóstico do JavaScript | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.JavaScript.ProjectSystem | JavaScript ProjectSystem e Ferramentas Compartilhadas | 15.0.26606.0 | Necessária
Microsoft.VisualStudio.Component.JavaScript.TypeScript | Suporte às linguagens JavaScript e TypeScript | 15.9.28125.51 | Necessária
Microsoft.VisualStudio.Component.TypeScript.2.3 | SDK do TypeScript 2.3 | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | Desenvolvimento do ASP.NET e para a Web | 15.8.27825.0 | Necessária
Component.Android.SDK23.Private | Instalação do SDK do Android (nível 23 da API) (instalação local para desenvolvimento móvel com JavaScript/C++) | 15.9.28016.0 | Opcional
Component.Google.Android.Emulator.API23.Private | Emulador do Google Android (API Nível 23) (instalação local) | 15.6.27413.0 | Opcional
Component.HAXM.Private | Intel HAXM (Hardware Accelerated Execution Manager) (instalação local) | 15.6.27413.0 | Opcional
Component.JavaJDK | Java SE Development Kit (8.0.1120.15) | 15.6.27406.0 | Opcional
Component.OpenJDK | OpenJDK de distribuição da Microsoft | 15.9.28125.51 | Opcional
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Opcional
Microsoft.Component.NetFX.Native | .NET Nativo | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.AppInsights.Tools | Ferramentas de Análise do Desenvolvedor | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.DiagnosticTools | Ferramentas de criação de perfil do .NET | 15.8.27729.1 | Opcional
Microsoft.VisualStudio.Component.Git | Git para Windows | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.Graphics | Editores de imagens e modelos 3D | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Phone.Emulator.15254 | Emulador móvel do Windows 10 (Fall Creators Update) | 15.0.27406.0 | Opcional
Microsoft.VisualStudio.Component.SQL.CLR | Tipos de dados CLR do SQL Server | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.UWP.Cordova | Ferramentas da Plataforma Universal do Windows para Cordova | 15.7.27617.1 | Opcional

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
Component.Android.Emulator | Emulador do Visual Studio para Android | 15.6.27413.0
Component.Android.NDK.R11C | NDK do Android (R11C) | 11.3.14
Component.Android.NDK.R11C_3264 | NDK do Android (R11C) (32 bits) | 11.3.16
Component.Android.SDK23 | Instalação do SDK do Android (API nível 23) (instalação global) | 15.9.28107.0
Component.Android.SDK25 | Instalação do SDK do Android (API nível 25) | 15.9.28107.0
Component.GitHub.VisualStudio | Extensão do GitHub para Visual Studio | 2.5.2.2500
Component.Google.Android.Emulator.API23.V2 | Emulador do Google Android (API Nível 23) (instalação global) | 15.6.27413.0
Component.Google.Android.Emulator.API25 | Emulador de Google Android (API Nível 25) | 15.7.27604.0
Microsoft.Component.Blend.SDK.WPF | SDK do Blend for Visual Studio para .NET | 15.6.27406.0
Microsoft.Component.HelpViewer | Visualizador da Ajuda | 15.6.27323.2
Microsoft.VisualStudio.Component.DependencyValidation.Community | Validação de dependência | 15.0.26208.0
Microsoft.VisualStudio.Component.GraphDocument | Editor DGML | 15.0.27005.2
Microsoft.VisualStudio.Component.LinqToSql | Ferramentas do LINQ to SQL | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator | Emulador do Windows 10 Mobile (Edição de Aniversário) | 15.6.27406.0
Microsoft.VisualStudio.Component.Phone.Emulator.15063 | Emulador móvel do Windows 10 (atualização dos criadores) | 15.6.27406.0
Microsoft.VisualStudio.Component.Runtime.Node.x86.6.4.0 | Tempo de execução para componentes com base no Node.js v6.4.0 (x86) | 15.7.27617.1
Microsoft.VisualStudio.Component.Runtime.Node.x86.7.4.0 | Tempo de execução para componentes com base no Node.js v7.4.0 (x86) | 15.7.27617.1
Microsoft.VisualStudio.Component.TypeScript.2.0 | SDK do TypeScript 2.0 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.1 | SDK do TypeScript 2.1 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.2 | SDK do TypeScript 2.2 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.5 | SDK do TypeScript 2.5 | 15.6.27406.0
Microsoft.VisualStudio.Component.TypeScript.2.6 | SDK do TypeScript 2.6 | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.7 | SDK do TypeScript 2.7 | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.8 | SDK do TypeScript 2.8 | 15.0.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.9 | SDK do TypeScript 2.9 | 15.0.27924.0
Microsoft.VisualStudio.Component.TypeScript.3.0 | SDK do TypeScript 3.0 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.ATL.ARM | ATL do Visual C++ para ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | ATL do Visual C++ para ARM com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | ATL do Visual C++ para ARM64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | ATL do Visual C++ para ARM64 com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATL.Spectre | ATL do Visual C++ (x86/x64) com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | MFC do Visual C++ para x86/x64 com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.ClangC2 | Clang/C2 (experimental) | 15.7.27520.0
Microsoft.VisualStudio.Component.VC.MFC.ARM | MFC do Visual C++ para ARM | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | MFC do Visual C++ para ARM com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | MFC do Visual C++ para ARM64 | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | Suporte do MFC do Visual C++ para ARM64 com mitigações de Spectre | 15.7.27625.0
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | Bibliotecas do VC++ 2017 versão 15.9 v14.16 para Spectre (ARM) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | Bibliotecas do VC++ 2017 versão 15.9 v14.16 para Spectre (ARM64) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | Bibliotecas do VC++ 2017 versão 15.9 v14.16 para Spectre (x86 e x64) | 15.9.28230.55
Microsoft.VisualStudio.Component.VC.Tools.14.11 | Conjunto de ferramentas do VC++ 2017 versão 15.4 v14.11 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.12 | Conjunto de ferramentas do VC++ 2017 versão 15.5 v14.12 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.13 | Conjunto de ferramentas do VC++ 2017 versão 15.6 v14.13 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.14 | Conjunto de ferramentas do VC++ 2017 versão 15.7 v14.14 | 15.0.27924.0
Microsoft.VisualStudio.Component.VC.Tools.14.15 | Conjunto de ferramentas do VC++ 2017 versão 15.8 v14.15 | 15.0.28230.55

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Carga de trabalho do Visual Studio e IDs do componente](workload-and-component-ids.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)

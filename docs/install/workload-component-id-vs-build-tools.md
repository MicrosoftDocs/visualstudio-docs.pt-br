---
title: IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio 2017
description: Usar IDs de carga de trabalho e de componente do Visual Studio para criar aplicativos clássicos baseados no Windows
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
ms.assetid: b99298df-0280-47fc-af73-44cd7a8ac553
ms.workload:
- multiple
ms.openlocfilehash: 958e4e842468e871cd9aa65f0a20b87a84aeb4ca
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607855"
---
# <a name="visual-studio-build-tools-2017-component-directory"></a>Diretório de componentes das Ferramentas de Build do Visual Studio 2017

As tabelas desta página listam as IDs que podem ser usadas para instalar o Visual Studio usando a linha de comando ou que podem ser especificadas como uma dependência em um manifesto do VSIX. Observe que adicionaremos outros componentes conforme atualizações forem liberadas para o Visual Studio.

Além disso, observe o seguinte sobre a página:

* Cada carga de trabalho tem sua própria seção, seguida pela ID da carga de trabalho e por uma tabela dos componentes que estão disponíveis para a carga de trabalho.
* Por padrão, os componentes **Obrigatórios** serão instalados durante a instalação da carga de trabalho.
* Se preferir, também será possível instalar os componentes **Recomendados** e **Opcionais**.
* Também adicionamos uma seção que lista os componentes adicionais que não são afiliados a nenhuma carga de trabalho.

Ao definir dependências no manifesto do VSIX, é necessário especificar somente IDs de Componente. Use as tabelas desta página para determinar nossas dependências mínimas de componente. Em alguns cenários, isso pode significar que somente um componente de uma carga de trabalho é especificado. Em outros cenários, isso pode significar que vários componentes de uma única carga de trabalho ou que vários componentes de várias cargas de trabalho são especificados. Para obter mais informações, consulte a página [Como migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

Para obter mais informações sobre como usar essas IDs, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md). Além disso, para obter uma lista de IDs de carga de trabalho e de componente para outros produtos, consulte a página [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md).

## <a name="azure-development-build-tools"></a>Ferramentas de build de desenvolvimento do Azure

**ID:** Microsoft.VisualStudio.Workload.AzureBuildTools

**Descrição:** tarefas e destinos do MSBuild para o build de aplicativos do Azure.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Ferramentas de Criação do Azure | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Azure.ClientLibs | Bibliotecas do Azure para .NET | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Ferramentas de build dos Serviços de Nuvem do Azure | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento do WCF | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento para a Web | 15.8.27729.1 | Necessária
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.Net.Component.3.5.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 3.5 | 15.6.27406.0 | Opcional
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

## <a name="data-storage-and-processing-build-tools"></a>Ferramentas de build de processamento e armazenamento de dados

**ID:** Microsoft.VisualStudio.Workload.DataBuildTools

**Descrição:** Criar Projetos de Banco de Dados do SQL Server

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Recomendado
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# e Visual Basic | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Component.SQL.SSDTBuildSku | SQL Server Data Tools – Ferramentas de Build | 15.8.27825.0 | Recomendado
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Recomendado

## <a name="net-desktop-build-tools"></a>Ferramentas de build de área de trabalho do .NET

**ID:** Microsoft.VisualStudio.Workload.ManagedDesktopBuildTools

**Descrição:** ferramentas para o build de aplicativos de console, Windows Forms e WPF usando C#, Visual Basic e F#.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.Component.ClickOnce.MSBuild | Ferramentas de build do ClickOnce | 15.7.27617.1 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Recomendado
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.Component.TestTools.BuildTools | Recursos principais de ferramentas de teste – Ferramentas de Build | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento do WCF | 15.6.27309.0 | Recomendado
Microsoft.Net.Component.3.5.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 3.5 | 15.6.27406.0 | Opcional
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
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.FSharp.MSBuild | compilador F# | 15.8.27825.0 | Opcional

## <a name="msbuild-tools"></a>Ferramentas do MSBuild

**ID:** Microsoft.VisualStudio.Workload.MSBuildTools

**Descrição:** fornece as ferramentas necessárias para criar aplicativos baseados em MSBuild.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.VisualStudio.Component.CoreBuildTools | Principais Ferramentas de Build do Visual Studio | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária

## <a name="net-core-build-tools"></a>Ferramentas de compilação do .NET Core

**ID:** Microsoft.VisualStudio.Workload.NetCoreBuildTools

**Descrição:** ferramentas para criar aplicativos usando .NET Core, ASP.NET Core, HTML/JavaScript e Contêineres.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Necessária
Microsoft.NetCore.BuildTools.ComponentGroup | Ferramentas de compilação do .NET Core | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.Net.Core.Component.SDK | Ferramentas de desenvolvimento do .NET Core 2.0 | 15.6.27406.0 | Opcional
Microsoft.Net.Core.Component.SDK.1x | Ferramentas de desenvolvimento do .NET Core 1.0 a 1.1 | 15.6.27406.0 | Opcional

## <a name="nodejs-build-tools"></a>Ferramentas de compilação do Node.js

**ID:** Microsoft.VisualStudio.Workload.NodeBuildTools

**Descrição:** tarefas e destinos do MSBuild para criar aplicativos de rede escalonáveis usando o Node.js, um tempo de execução JavaScript controlado por eventos assíncronos.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Node.Build | Suporte ao MSBuild do Node.js | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária

## <a name="officesharepoint-build-tools"></a>Ferramentas de build do Office/SharePoint

**ID:** Microsoft.VisualStudio.Workload.OfficeBuildTools

**Descrição:** crie suplementos do Office, do SharePoint e do VSTO.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.ClickOnce.MSBuild | Ferramentas de build do ClickOnce | 15.7.27617.1 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Sharepoint.BuildTools | Ferramentas de build de desenvolvimento do Office/SharePoint | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.Workflow.BuildTools | Ferramentas de Build do Windows Workflow Foundation | 15.8.27906.1 | Necessária
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento do WCF | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento para a Web | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.TeamOffice.BuildTools | Ferramentas de build do VSTO (Ferramentas do Visual Studio para Office) | 15.7.27617.1 | Recomendado
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

## <a name="universal-windows-platform-build-tools"></a>Ferramentas de build da Plataforma Universal do Windows

**ID:** Microsoft.VisualStudio.Workload.UniversalBuildTools

**Descrição:** fornece as ferramentas necessárias para criar aplicativos da Plataforma Universal do Windows.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Component.NetFX.Native | .NET Nativo | 15.0.26208.0 | Necessária
Microsoft.Component.VC.Runtime.OSSupport | Tempo de execução Visual C++ para UWP | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.ARM | Compiladores e bibliotecas do Visual C++ para o ARM | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Necessária
Microsoft.VisualStudio.ComponentGroup.UWP.BuildTools | Pré-requisitos de build da Plataforma Universal do Windows | 15.8.27705.0 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Recomendado
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
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.15063 | SDK do Windows 10 (10.0.15063.0) | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.ComponentGroup.Windows10SDK.16299 | SDK do Windows 10 (10.0.16299.0) | 15.8.27825.0 | Opcional

## <a name="visual-c-build-tools"></a>Ferramentas de build do Visual C++

**ID:** Microsoft.VisualStudio.Workload.VCTools

**Descrição:** compile aplicativos de área de trabalho do Windows usando o conjunto de ferramentas Microsoft C++, o ATL ou o MFC.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Necessária
Microsoft.VisualStudio.Component.VC.CoreBuildTools | Principais recursos das Ferramentas de Build do Visual C++ | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | Atualização Redistribuível do Visual C++ 2017 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK | Tempo de execução C Universal do Windows | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.TestTools.BuildTools | Recursos principais de ferramentas de teste – Ferramentas de Build | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.VC.CMake.Project | Ferramentas do Visual C++ para CMake | 15.8.27906.1 | Recomendado
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Recomendado
Microsoft.Component.VC.Runtime.UCRTSDK | SDK do CRT Universal do Windows | 15.6.27309.0 | Opcional
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.VC.140 | Conjunto de ferramentas do VC++ 2015.3 v14.00 (v140) para área de trabalho | 15.7.27617.1 | Opcional
Microsoft.VisualStudio.Component.VC.ATL | Visual C++ ATL para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.ATLMFC | Visual C++ MFC para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.CLI.Support | Suporte ao C++/CLI | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | Módulos de Biblioteca Padrão (experimental) | 15.6.27309.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM | Compiladores e bibliotecas do Visual C++ para o ARM | 15.8.27825.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | Compiladores e bibliotecas do Visual C++ para ARM64 | 15.9.28230.55 | Opcional
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

## <a name="visual-studio-extension-development"></a>Desenvolvimento de extensões do Visual Studio

**ID:** Microsoft.VisualStudio.Workload.VisualStudioExtensionBuildTools

**Descrição:** ferramentas para criar complementos e extensões para Visual Studio, inclusive novos comandos, analisadores de código e janelas de ferramentas.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.VSSDKBuildTools | Núcleo de Ferramentas de Build do SDK do Visual Studio | 15.8.27924.0 | Necessária
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtensionBuildTools.Prerequisites | Pré-requisitos para o desenvolvimento de extensões do Visual Studio | 15.8.27729.1 | Necessária
Component.Dotfuscator | Proteção PreEmptive – Dotfuscator | 15.0.26208.0 | Opcional
Microsoft.Component.VC.Runtime.OSSupport | Tempo de execução Visual C++ para UWP | 15.6.27406.0 | Opcional
Microsoft.VisualStudio.Component.Static.Analysis.Tools | Ferramentas de análise estática | 15.0.26208.0 | Opcional
Microsoft.VisualStudio.Component.VC.ATL | Visual C++ ATL para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.ATLMFC | Visual C++ MFC para x86 e x64 | 15.7.27625.0 | Opcional
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | Ferramentas mais recentes da v141 do VC++ 2017 versão 15.9 v14.16 | 15.9.28230.55 | Opcional

## <a name="web-development-build-tools"></a>Ferramentas de build de desenvolvimento para a Web

**ID:** Microsoft.VisualStudio.Workload.WebBuildTools

**Descrição:** tarefas e destinos do MSBuild para a compilação de aplicativos Web.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.TypeScript.3.1 | SDK do TypeScript 3.1 | 15.0.28218.60 | Necessária
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento para a Web | 15.8.27729.1 | Necessária
Microsoft.Component.ClickOnce.MSBuild | Ferramentas de build do ClickOnce | 15.7.27617.1 | Recomendado
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Recomendado
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Recomendado
Microsoft.Net.Core.Component.SDK.2.1 | Ferramentas de desenvolvimento do .NET Core 2.1 | 15.8.27924.0 | Recomendado
Microsoft.VisualStudio.Component.AspNet45 | Recursos avançados do ASP.NET | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.DockerTools.BuildTools | Ferramentas de desenvolvimento de contêiner – Ferramentas de Build | 15.7.27617.1 | Recomendado
Microsoft.VisualStudio.Component.TestTools.BuildTools | Recursos principais de ferramentas de teste – Ferramentas de Build | 15.7.27625.0 | Recomendado
Microsoft.VisualStudio.Component.WebDeploy | Implantação da Web | 15.8.27729.1 | Recomendado
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Ferramentas de build de desenvolvimento do WCF | 15.6.27309.0 | Recomendado
Microsoft.Net.Component.3.5.DeveloperTools | Ferramentas de desenvolvimento do .NET Framework 3.5 | 15.6.27406.0 | Opcional
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

## <a name="mobile-development-with-net"></a>Desenvolvimento móvel com .NET

**ID:** Microsoft.VisualStudio.Workload.XamarinBuildTools

**Descrição:** ferramentas para criar aplicativos multiplataforma para iOS, Android e Windows usando C# e F#.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.NuGet.BuildTools | Os destinos e as tarefas de compilação do NuGet | 15.9.28016.0 | Necessária
Microsoft.VisualStudio.Component.Roslyn.Compiler | Compiladores Roslyn do C# e Visual Basic | 15.6.27309.0 | Necessária
Component.Android.SDK25 | Instalação do SDK do Android (API nível 25) | 15.9.28107.0 | Opcional
Component.OpenJDK | OpenJDK de distribuição da Microsoft | 15.9.28125.51 | Opcional

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
Microsoft.VisualStudio.Component.TypeScript.2.0 | SDK do TypeScript 2.0 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.1 | SDK do TypeScript 2.1 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.2 | SDK do TypeScript 2.2 | 15.8.27729.1
Microsoft.VisualStudio.Component.TypeScript.2.3 | SDK do TypeScript 2.3 | 15.8.27729.1
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

* [Ferramentas de build do Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017#build-tools-for-visual-studio-2017)
* [Carga de trabalho do Visual Studio e IDs do componente](workload-and-component-ids.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)

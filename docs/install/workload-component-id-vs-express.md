---
title: IDs decomponente e carga de trabalho do Visual Studio 2017 Desktop Express
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
ms.assetid: a3c0cc76-e3ce-435c-a1af-a6318b5a4dbe
ms.workload:
- multiple
ms.openlocfilehash: 48c478986ba79d84bb4cc93e7437a9a8a6aac33a
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607647"
---
# <a name="visual-studio-2017-desktop-express-component-directory"></a>Diretório de componentes do Visual Studio 2017 Desktop Express

As tabelas desta página listam as IDs que podem ser usadas para instalar o Visual Studio usando a linha de comando ou que podem ser especificadas como uma dependência em um manifesto do VSIX. Observe que adicionaremos outros componentes conforme atualizações forem liberadas para o Visual Studio.

Além disso, observe o seguinte sobre a página:

* Cada carga de trabalho tem sua própria seção, seguida pela ID da carga de trabalho e por uma tabela dos componentes que estão disponíveis para a carga de trabalho.
* Por padrão, os componentes **Obrigatórios** serão instalados durante a instalação da carga de trabalho.
* Se preferir, também será possível instalar os componentes **Recomendados** e **Opcionais**.
* Também adicionamos uma seção que lista os componentes adicionais que não são afiliados a nenhuma carga de trabalho.

Ao definir dependências no manifesto do VSIX, é necessário especificar somente IDs de Componente. Use as tabelas desta página para determinar nossas dependências mínimas de componente. Em alguns cenários, isso pode significar que somente um componente de uma carga de trabalho é especificado. Em outros cenários, isso pode significar que vários componentes de uma única carga de trabalho ou que vários componentes de várias cargas de trabalho são especificados. Para obter mais informações, consulte a página [Como migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

Para obter mais informações sobre como usar essas IDs, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md). Além disso, para obter uma lista de IDs de carga de trabalho e de componente para outros produtos, consulte a página [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md).

## <a name="express-for-windows-desktop"></a>Express para Windows Desktop

**ID:** Microsoft.VisualStudio.Workload.WDExpress

**Descrição:** Compile aplicativos Gerenciados e Nativos como WPF, WinForms e Win32 com edição de código com reconhecimento de sintaxe, controle do código-fonte e gerenciamento de item de trabalho. Inclui suporte para o C#, Visual Basic e Visual C++.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.Component.ClickOnce | Publicação ClickOnce | 15.8.27825.0 | Necessária
Microsoft.Component.HelpViewer | Visualizador da Ajuda | 15.6.27323.2 | Necessária
Microsoft.Component.MSBuild | MSBuild | 15.7.27520.0 | Necessária
Microsoft.Component.VC.Runtime.OSSupport | Tempo de execução Visual C++ para UWP | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.2.TargetingPack | Pacote de direcionamento do .NET Framework 4.5.2 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.5.TargetingPack | Pacote de direcionamento do .NET Framework 4.5 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.SDK | SDK do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.1.TargetingPack | Pacote de direcionamento do .NET Framework 4.6.1 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.6.TargetingPack | Pacote de direcionamento do .NET Framework 4.6 | 15.6.27406.0 | Necessária
Microsoft.Net.Component.4.TargetingPack | Pacote de direcionamento do .NET Framework 4 | 15.6.27406.0 | Necessária
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | Ferramentas de desenvolvimento do .NET Framework 4.6.1 | 15.8.27825.0 | Necessária
Microsoft.Net.ComponentGroup.TargetingPacks.Common | Ferramentas de desenvolvimento do .NET Framework 4 a 4.6 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Common.Azure.Tools | Ferramentas de conectividade e publicação | 15.9.28107.0 | Necessária
Microsoft.VisualStudio.Component.CoreEditor | Editor do Visual Studio Core | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.EntityFramework | Ferramentas do Entity Framework 6 | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.NuGet | Gerenciador de pacotes NuGet | 15.9.28016.0 | Necessária
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
Microsoft.VisualStudio.Component.VC.CLI.Support | Suporte ao C++/CLI | 15.6.27309.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.ARM | Compiladores e bibliotecas do Visual C++ para o ARM | 15.8.27825.0 | Necessária
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | Compiladores e bibliotecas do Visual C++ para ARM64 | 15.9.28230.55 | Necessária
Microsoft.VisualStudio.Component.VisualStudioData | Fontes de dados e referências de serviço | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK.14393 | SDK do Windows 10 (10.0.14393.0) | 15.6.27406.0 | Necessária
Microsoft.VisualStudio.Component.Windows10SDK.17134 | SDK do Windows 10 (10.0.17134.0) | 15.8.27924.0 | Necessária

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
N/D | N/D | N/D

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Carga de trabalho do Visual Studio e IDs do componente](workload-and-component-ids.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)

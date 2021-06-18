---
title: APIs removidas no Visual Studio 2022 Preview
description: Saiba mais sobre as APIs do SDK do VS removidas no Visual Studio 2022 Preview, para os autores de extensão que atualizam suas extensões para funcionar com o Visual Studio 2022 Preview.
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: bed8d0a261f70acb5e842ebeaf0059faae3fc478
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308658"
---
# <a name="visual-studio-2022-sdk-removed-apis"></a>APIs removidas do SDK do Visual Studio 2022

[!INCLUDE [preview-note](../includes/preview-note.md)]

As APIs a seguir foram removidas do SDK do Visual Studio e não podem mais ser usadas. consulte cada seção para obter detalhes sobre como atualizar seu código.

* [`IVsImageService`](#ivsimageservice)
* [`IBlockContextProvider`](#iblockcontextprovider)
* [`IToolTipProvider`](#itooltipprovider)
* [`IVsTextScanner` e `IVsFullTextScanner`](#ivstextscanner-and-ivsfulltextscanner)
* [Carregamento de solução assíncrona e carregamento de solução leve](#asynchronous-solution-load-and-lightweight-solution-load)
* [`IVsDummy`](#ivsdummy)
* [`Microsoft.VisualStudio.Shell.Task`](#microsoftvisualstudioshelltask)
* [Abrir do código-fonte seguro](#open-from-source-safe)
* [Novos Designer XAML do WPF para .NET Framework](#new-wpf-xaml-designer-for-net-framework)

## <a name="ivsimageservice"></a>IVsImageService

O `IVsImageService` está sendo removido no Visual Studio 2022. Todos os usuários do `IVsImageService` devem mudar para o `IVsImageService2` em vez disso.

### <a name="recommended-updates"></a>Atualizações recomendadas

Se você usar `IVsImageService` , substitua chamadas para seus métodos com chamadas para métodos equivalentes em `IVsImageService2` :

| **Método IVsImageService** | **Método IVsImageService2 equivalente** |
|----------------------------|----------------------------------------|
| Adicionar                        | AddCustomImage                         |
| Obter                        | GetImage                               |
| GetIconForFile             | GetImageMonikerForFile                 |
| GetIconForFileEx           | GetImageMonikerForFile                 |

`IVsImageService`os métodos Add e Get referenciados para imagens personalizadas por nome (uma cadeia de caracteres), em vez de um moniker.  É preferível que você alterne seu código para usar apenas monikers para referir-se a imagens personalizadas, mas se esse prova impraticável `IVsImageService2` tiver alguns métodos que lhe permitirão associar um nome a um moniker:

* `TryAssociateNameWithMoniker`
* `GetImageMonikerForName`

Usando esses dois métodos, você pode continuar a referenciar imagens por nome.

## <a name="iblockcontextprovider"></a>IBlockContextProvider

O `IBlockContextProvider` e os tipos relacionados estão sendo removidos no Visual Studio 2022. Todos os usuários do `IBlockContextProvider` devem mudar para o `IStructureContextSourceProvider` em vez disso.

### <a name="recommended-updates"></a>Atualizações recomendadas

Os usuários do `IBlockContextProvider` devem usar o `IStructureContextSourceProvider` em vez disso ([documentação](/dotnet/api/microsoft.visualstudio.text.adornments.istructurecontextsourceprovider)).

## <a name="itooltipprovider"></a>IToolTipProvider

O `IToolTipProvider` e os tipos relacionados estão sendo removidos no Visual Studio 2022. Todos os usuários do `IToolTipProvider` devem mudar para o `IToolTipService` em vez disso.

### <a name="recommended-updates"></a>Atualizações recomendadas

Os usuários do `IToolTipProvider` devem usar o `IToolTipService` em vez disso ([documentação](/dotnet/api/microsoft.visualstudio.text.adornments.itooltipservice)).

## <a name="ivstextscanner-and-ivsfulltextscanner"></a>IVsTextScanner e IVsFullTextScanner

O `IVsTextScanner` e o `IVsFullTextScanner` estão sendo removidos no Visual Studio 2022. Todos os usuários do `IVsTextScanner` ou do `IVsFullTextScanner` devem mover para o `IVsTextLines` em vez disso.

### <a name="recommended-updates"></a>Atualizações recomendadas

Os usuários do `IVsTextScanner` ou do `IVsFullTextScanner` devem usar o `IVsTextLines` em vez disso ([documentação](/dotnet/apimicrosoft.visualstudio.textmanager.interop.ivstextlines.getlinetext)).

## <a name="asynchronous-solution-load-and-lightweight-solution-load"></a>Carregamento de solução assíncrona e carregamento de solução leve

Os recursos do ASL (carregamento de solução assíncrona) e LSL (carregamento de solução leve) estão sendo removidos no Visual Studio 2022, já que os seguintes métodos estão sendo removidos:

### <a name="interfaces"></a>Interfaces

* `IVsSolution4` -Métodos: `IsBackgroundSolutionLoadEnabled` , `EnsureProjectsAreLoaded` , `EnsureProjectIsLoaded` , `EnsureSolutionIsLoaded`
* `IVsSolutionLoadEvents` -Métodos: `OnBeforeBackgroundSolutionLoadBegins` , `OnQueryBackgroundLoadProjectBatch` , `OnBeforeLoadProjectBatch` , `OnAfterLoadProjectBatch`
* `IVsSolutionLoadManagerSupport` -Interface inteira
* `IVsSolutionLoadManager` -Interface inteira
* `IVsSccManager3`  -Interface inteira
* `IVsAsynchronousProjectCreate` -Interface inteira
* `IVsAsynchronousProjectCreateUI` -Interface inteira

### <a name="enums-properties-and-ui-contexts"></a>Enumerações, propriedades e contextos de interface do usuário

* `VSHPROPID_ProjectUnloadStatus` Enumera `UNLOADSTATUS_LoadPendingIfNeeded`
* `VSHPROPID_DemandLoadDependencies`
* `VSHPROPID_IsProjectProvisioned`
* `VSPROPID_IsInBackgroundIdleLoadProjectBatch`
* `VSPROPID_IsInSyncDemandLoadProjectBatch`
* `VSPROPID_ActiveSolutionLoadManager`
* `UICONTEXT_BackgroundProjectLoad`

### <a name="recommended-updates"></a>Atualizações recomendadas

Nenhum.

## <a name="ivsdummy"></a>IVsDummy

O `IVsDummy` está sendo removido no Visual Studio 2022 e não será substituído. 

### <a name="recommended-updates"></a>Atualizações recomendadas

Nenhum. Mas ele não deve ter nenhum impacto, pois a API não fez nada.

## <a name="microsoftvisualstudioshelltask"></a>Microsoft. VisualStudio. Shell. Task

A `Microsoft.VisualStudio.Shell.Task` classe foi renomeada para `Microsoft.VisualStudio.Shell.TaskListItem` não entrar em conflito com a classe muito popular `System.Threading.Tasks.Task` .

## <a name="open-from-source-safe"></a>Abrir do código-fonte seguro

O suporte para abrir uma solução da origem segura está sendo removido, pois os seguintes métodos, eventos e constantes estão sendo removidos.

## <a name="interfaces"></a>Interfaces

* `IVsSCCProvider3` -Interface inteira

### <a name="recommended-updates"></a>Atualizações recomendadas

Nenhum.

## <a name="new-wpf-xaml-designer-for-net-framework"></a>Novos Designer XAML do WPF para .NET Framework

O Designer XAML do WPF atual para .NET Framework foi preterido e será substituído por um novo Designer XAML do WPF para .NET Framework, com base na mesma arquitetura usada para o WPF Designer XAML para .NET (.NET Core). Isso também significa que o modelo de extensibilidade de controle do WPF .NET Framework baseado em .design.dll e Microsoft. Windows. Design. Extensibility não é mais suportado. O novo Designer XAML do WPF para .NET Framework fornecerá o mesmo modelo de extensibilidade que o WPF Designer XAML para .NET (.NET Core). Se você já tiver criado uma extensão de .designtools.dll para .NET (.NET Core), essa mesma extensão funcionará para o novo Designer XAML do WPF para .NET Framework. Consulte o link de migração abaixo para obter mais informações sobre como migrar para o novo modelo de extensibilidade para plataformas do WPF (.NET Framework e .NET Core) e plataformas UWP avançando. 

### <a name="recommended-updates"></a>Atualizações recomendadas

Consulte [migração de extensibilidade do designer XAML](https://github.com/microsoft/xaml-designer-extensibility/blob/main/documents/xaml-designer-extensibility-migration.md).

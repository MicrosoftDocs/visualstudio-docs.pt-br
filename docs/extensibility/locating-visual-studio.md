---
title: Localizando Visual Studio | Microsoft Docs
description: Você pode instalar várias instâncias da mesma versão do Visual Studio. Saiba como usar uma API de consulta COM para encontrar a instância que você deseja.
ms.custom: SEO-VS-2020
ms.date: 08/21/2017
ms.topic: conceptual
helpviewer_keywords:
- deployment, VSIX
ms.assetid: 680c3b25-7901-4768-8363-6d1fcd1ea636
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: cd0fcd294983d6a6567676f06703b4bd1dd376c4
ms.sourcegitcommit: b4cc3dee59421f7089112becf128a369acadaf61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2021
ms.locfileid: "112990500"
---
# <a name="locate-visual-studio"></a>Localizar o Visual Studio

A partir do Visual Studio 2017, você pode instalar várias instâncias da mesma versão ou até mesmo da edição. Isso é útil quando você deseja visualizar novas funcionalidades em seu computador de desenvolvimento primário enquanto mantém a instalação anterior. Devido a essas alterações, não há nenhuma variável de ambiente única ou valor do Registro que você possa usar para localizar uma instância. Em vez disso, você pode usar uma [API de consulta COM](/dotnet/api/microsoft.visualstudio.setup.configuration) para encontrar instâncias com base em critérios relevantes para sua extensão.

Essa é uma API rápida e somente leitura com pacotes NuGet disponíveis para código nativo e gerenciado.

| Código | Pacote |
| ---- | --- |
| Nativo | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Native |
| Gerenciado | https://nuget.org/packages/Microsoft.VisualStudio.Setup.Configuration.Interop |

Você pode localizar uma única instância considerando um caminho ou o processo atual ou enumerar todas as instâncias. Consulte [nossos exemplos](https://github.com/Microsoft/vs-setup-samples) para ver exemplos completos de como localizar Visual Studio.

## <a name="tools"></a>Ferramentas

Para encontrar Visual Studio ferramentas em ambientes de build, scripts do PowerShell, instaladores e mais cenários, há várias ferramentas de software livre que você pode usar diretamente ou redistribuir junto com seus próprios scripts.

| Projeto | Descrição |
| ------- | ----------- |
| [vswhere](https://github.com/Microsoft/vswhere) | Executável nativo de arquivo único para localizar os critérios de reunião de instâncias, como versão ou pré-lançamento, qual produto está instalado e quais cargas de trabalho estão instaladas. Também dá suporte à Visual Studio 2010 e mais recente, embora menos informações retornem isso para Visual Studio 2017 e mais recente. Consulte o [wiki](https://github.com/Microsoft/vswhere/wiki) para ver exemplos. |
| [Cmdlets vsSetup](https://github.com/Microsoft/vssetup.powershell) | Cmdlets do PowerShell com suporte 2.0 e mais recente que retornam informações rich como objetos que você pode usar para encontrar instâncias com base nos mesmos critérios que _vswhere_ e para descobrir ainda mais propriedades sobre instâncias. Consulte o [wiki](https://github.com/Microsoft/vssetup.powershell/wiki) para ver exemplos. |
| [VSIXBootstrapper](https://github.com/Microsoft/vsixbootstrapper) | Localiza automaticamente _o VSIXInstaller_ e passa a linha de comando para instalar um arquivo **.vsix.* Esse recurso pode ser útil em instaladores que não têm suporte direto para as APIs de consulta. Consulte o [wiki](https://github.com/Microsoft/vsixbootstrapper/wiki) para ver exemplos. |

## <a name="see-also"></a>Confira também

* [Alterações na Visual Studio 2017](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup/)
* [Iniciar o Visual Studio usando DTE](launch-visual-studio-dte.md)

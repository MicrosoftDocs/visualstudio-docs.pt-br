---
title: Ferramentas para detectar e gerenciar instâncias do Visual Studio
titleSuffix: ''
description: Saiba mais sobre as ferramentas que você pode usar para detectar e gerenciar instalações do Visual Studio em computadores cliente.
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 85686707-14C0-4860-9B7A-66485D43D241
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 914449fe1db792614af1f9ed22464cb9fdb91481
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306885"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>Ferramentas para detectar e gerenciar instâncias do Visual Studio

Há várias ferramentas que você pode usar para detectar Visual Studio em máquinas cliente e gerenciar as instalações.

## <a name="detecting-existing-visual-studio-instances"></a>Detectando instâncias existentes do Visual Studio

As seguintes ferramentas e utilitários ajudarão você a detectar e gerenciar instâncias Visual Studio instaladas em máquinas cliente:

* [**vswhere**](https://github.com/microsoft/vswhere): um executável integrado Visual Studio ou disponível para distribuição separada que ajuda você a encontrar o local de todas as Visual Studio instâncias em um computador específico.
* [**VSSetup.PowerShell:**](https://github.com/microsoft/vssetup.powershell)scripts do PowerShell que usam a API de Configuração de Instalação para identificar instâncias instaladas do Visual Studio.
* [**VS-Setup-Samples: exemplos**](https://github.com/microsoft/vs-setup-samples)de C# e C++ que demonstram como usar a API de Configuração de Configuração para consultar uma instalação existente.
* [**Instrumentação de Gerenciamento do Windows (WMI)**](/windows/win32/wmisdk/wmi-start-page): Visual Studio de instância pode ser consultada por meio da classe Visual Studio MSFT_VSInstance.
* A [**API de Configuração de**](<xref:Microsoft.VisualStudio.Setup.Configuration>) Configuração fornece interfaces para desenvolvedores que querem criar seus próprios utilitários para interrogação Visual Studio instâncias.
* [**Microsoft Endpoint Configuration Manager inventário de software:**](/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory)pode ser usado para coletar informações sobre Visual Studio instâncias em dispositivos cliente.

## <a name="using-vswhereexe"></a>Usar o vswhere.exe

`vswhere.exe` é incluído automaticamente no Visual Studio 2017 e posterior, ou você pode baixá-lo na página de [versões do vswhere](https://github.com/Microsoft/vswhere/releases). Use o `vswhere -?` para obter informações de ajuda sobre a ferramenta. Por exemplo, esse comando mostra todas as versões do Visual Studio, incluindo versões anteriores do produto e pré-lançamentos, e exibe os resultados no formato JSON:

```shell
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

## <a name="using-windows-management-instrumentation-wmi"></a>Usando Instrumentação de Gerenciamento do Windows (WMI)

Se o Visual Studio do Detector de Cliente estiver instalado no computador, você poderá consultar informações Visual Studio instância usando o WMI. O Utilitário do Detector de Cliente do Visual Studio é instalado por padrão com cada atualização do Visual Studio 2017, Visual Studio 2019 e Visual Studio 2022 lançada em ou após 12 de maio de 2020. Ele também estará disponível no catálogo [Microsoft Update se](https://catalog.update.microsoft.com/) você quiser instalá-lo independentemente.  Para obter um exemplo de como usar o utilitário para retornar Visual Studio de instância, abra o PowerShell como administrador no computador cliente e digite o seguinte comando:

```shell
Get-CimInstance MSFT_VSInstance
```

## <a name="using-microsoft-endpoint-configuration-manager"></a>Usando Microsoft Endpoint Configuration Manager

[Microsoft Endpoint Configuration Manager recursos de inventário de software](/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory) podem ser usados para consultar e coletar informações sobre Visual Studio instâncias em dispositivos cliente. Por exemplo, a consulta a seguir retornará o nome de exibição, a versão e o nome do dispositivo em que o Visual Studio está instalado para todas as instâncias do Visual Studio 2017 e 2019:

```WQL
select distinct SMS_G_System_COMPUTER_SYSTEM.Name, SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName, SMS_G_System_ADD_REMOVE_PROGRAMS.Version from SMS_R_System inner join SMS_G_System_COMPUTER_SYSTEM on SMS_G_System_COMPUTER_SYSTEM.ResourceID = SMS_R_System.ResourceId inner join SMS_G_System_ADD_REMOVE_PROGRAMS on SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceID = SMS_R_System.ResourceId where SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Visual Studio %[a-z]% 201[7,9]" 
```

::: moniker range="vs-2017"

> [!TIP]
> Para obter mais informações sobre a instalação do Visual Studio 2017, confira [Arquivos de Instalação do Visual Studio](https://devblogs.microsoft.com/setup/tag/vs2017/).

::: moniker-end

## <a name="editing-the-registry-for-a-visual-studio-instance"></a>A edição do Registro para uma instância do Visual Studio

No Visual Studio, configurações do Registro são armazenadas em um local privado, o que permite várias instâncias lado a lado no mesmo computador com a mesma versão do Visual Studio.

Como essas entradas não são armazenadas no Registro global, há instruções especiais para usar o Editor do Registro para fazer alterações nas configurações do Registro:

1. Se você tiver uma instância do Visual Studio aberta, feche-a.

1. Inicie o `regedit.exe`.

1. Selecione o nó `HKEY_LOCAL_MACHINE`.

1. No menu principal Regedit, selecione Carregar Arquivo Hive... e, em seguida, selecione o arquivo de Registro privado, que é armazenado na pasta  >   **AppData\Local.** Por exemplo:

   ```shell
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` corresponde à instância do Visual Studio que você deseja procurar.

Você precisará fornecer um nome de hive, que se tornará o nome do hive isolado. Depois de fazer isso, você poderá pesquisar o Registro no hive isolado que criou.

> [!IMPORTANT]
> Antes de iniciar o Visual Studio novamente, você deve descarregar a seção isolada que criou. Para fazer isso, selecione **Descarregar**  >  **Arquivo hive** no menu principal Regedit. (Se você não fizer isso, o arquivo permanecerá bloqueado e o Visual Studio não poderá ser iniciado.)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)

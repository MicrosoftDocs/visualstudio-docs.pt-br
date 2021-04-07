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
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 2b6b641081c9b969cadd2c9517967adb8cc4cb1e
ms.sourcegitcommit: 56060e3186086541d9016d4185e6f1bf3471e958
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106547434"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>Ferramentas para detectar e gerenciar instâncias do Visual Studio

Há várias ferramentas que você pode usar para detectar instalações do Visual Studio em computadores cliente e para gerenciar as instalações.

## <a name="detecting-existing-visual-studio-instances"></a>Detectando instâncias existentes do Visual Studio

As ferramentas e os utilitários a seguir ajudarão você a detectar e gerenciar as instâncias do Visual Studio instaladas em computadores cliente:

* [**vswhere**](https://github.com/microsoft/vswhere): um executável interno do Visual Studio ou disponível para distribuição separada que ajuda a localizar o local de todas as instâncias do Visual Studio em um determinado computador.
* [**Vssetup. PowerShell**](https://github.com/microsoft/vssetup.powershell): scripts do PowerShell que usam a API de configuração da instalação para identificar as instâncias instaladas do Visual Studio.
* [**Vs-setup-Samples**](https://github.com/microsoft/vs-setup-samples): exemplos de C# e C++ que demonstram como usar a API de configuração de instalação para consultar uma instalação existente.
* [**Instrumentação de gerenciamento do Windows (WMI)**](https://docs.microsoft.com/windows/win32/wmisdk/wmi-start-page): as informações da instância do Visual Studio podem ser consultadas por meio do MSFT_VSInstance de classe do Visual Studio. 
* A [**API de configuração de instalação**](<xref:Microsoft.VisualStudio.Setup.Configuration>) fornece interfaces para desenvolvedores que desejam criar seus próprios utilitários para interrogar instâncias do Visual Studio.
* [**Microsoft Endpoint Configuration Manager software Inventory**](https://docs.microsoft.com/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory): pode ser usado para coletar informações sobre instâncias do Visual Studio em dispositivos cliente. 

## <a name="using-vswhereexe"></a>Usar o vswhere.exe

`vswhere.exe` é incluído automaticamente no Visual Studio 2017 e posterior, ou você pode baixá-lo na [página de versões do vswhere](https://github.com/Microsoft/vswhere/releases). Use o `vswhere -?` para obter informações de ajuda sobre a ferramenta. Por exemplo, esse comando mostra todas as versões do Visual Studio, incluindo versões anteriores do produto e pré-lançamento, e gera os resultados no formato JSON:

```cmd
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

## <a name="using-windows-management-instrumentation-wmi"></a>Usando Instrumentação de Gerenciamento do Windows (WMI)

Se o utilitário detector de cliente do Visual Studio estiver instalado no computador, você poderá consultar as informações de instância do Visual Studio usando o WMI. O utilitário detector de cliente do Visual Studio é instalado por padrão com todas as atualizações do Visual Studio 2017 e do Visual Studio 2019 lançadas no ou após 12 de maio de 2020. Ele também estará disponível no [catálogo Microsoft Update](https://catalog.update.microsoft.com/) se você quiser instalá-lo de forma independente.  Para obter um exemplo de como usar o utilitário para retornar as informações da instância do Visual Studio, abra o PowerShell como administrador no computador cliente e digite o seguinte comando:

```cmd
Get-CimInstance MSFT_VSInstance
```

## <a name="using-microsoft-endpoint-configuration-manager"></a>Usando o Microsoft Endpoint Configuration Manager 

Os recursos de [inventário de software do Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory) podem ser usados para consultar e coletar informações sobre instâncias do Visual Studio em dispositivos cliente. Por exemplo, a consulta a seguir retornará o nome de exibição, a versão e o nome do dispositivo em que o Visual Studio está instalado para todas as instâncias do Visual Studio 2017 e 2019 instaladas: 

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

1. No menu principal do regedit, selecione **arquivo**  >  **Carregar Hive...** e, em seguida, selecione o arquivo de registro privado, que é armazenado na pasta **AppData\Local** Por exemplo:

   ```
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` corresponde à instância do Visual Studio que você deseja procurar.

Você precisará fornecer um nome de hive, que se tornará o nome do hive isolado. Depois de fazer isso, você poderá pesquisar o Registro no hive isolado que criou.

> [!IMPORTANT]
> Antes de iniciar o Visual Studio novamente, você deve descarregar a seção isolada que criou. Para fazer isso, selecione **arquivo**  >  **Descarregar Hive** no menu principal do regedit. (Se você não fizer isso, o arquivo permanecerá bloqueado e o Visual Studio não poderá ser iniciado.)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)

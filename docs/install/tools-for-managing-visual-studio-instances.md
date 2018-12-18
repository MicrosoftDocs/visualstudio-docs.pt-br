---
title: Ferramentas para detectar e gerenciar instâncias do Visual Studio
description: Saiba mais sobre as ferramentas que você pode usar para detectar e gerenciar instalações do Visual Studio em computadores cliente.
ms.date: 08/14/2017
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 85686707-14C0-4860-9B7A-66485D43D241
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 160d0f283542445335496e3cbb7b98955df02b05
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672607"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>Ferramentas para detectar e gerenciar instâncias do Visual Studio

Há várias ferramentas que você pode usar para detectar instalações do Visual Studio em computadores cliente, bem como para gerenciar as instalações.

## <a name="detecting-existing-visual-studio-instances"></a>Detectando instâncias existentes do Visual Studio

Tornamos várias ferramentas disponíveis que ajudarão você a detectar e gerenciar instâncias do Visual Studio instaladas em computadores cliente:

* [VSWhere](https://github.com/microsoft/vswhere): um executável integrado ao Visual Studio ou disponível para distribuição separada que ajuda a encontrar o local de todas as instâncias do Visual Studio em um computador específico.
* [VSSetup.PowerShell](https://github.com/microsoft/vssetup.powershell): scripts do PowerShell que usam a API de Configuração de Instalação para identificar instâncias instaladas do Visual Studio.
* [VS-Setup-Samples](https://github.com/microsoft/vs-setup-samples): amostras do C# e C++ que demonstram como usar a API de Configuração de Instalação para consultar uma instalação existente.

Além disso, a [API de Configuração de Instalação](<xref:Microsoft.VisualStudio.Setup.Configuration>) fornece interfaces para desenvolvedores que desejam criar seus próprios utilitários para interrogar instâncias do Visual Studio.

## <a name="using-vswhereexe"></a>Usar o vswhere.exe

`vswhere.exe` é incluído automaticamente no Visual Studio 2017 versão 15.2 ou superior, ou pode ser baixado da [página de versões](https://github.com/Microsoft/vswhere/releases). Use o `vswhere -?` para obter informações de ajuda sobre a ferramenta. Como exemplo, este comando mostra todas as versões do Visual Studio, incluindo versões mais antigas do produto e pré-lançamentos e gera os resultados no formato JSON:

```cmd
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

>[!TIP]
>Para obter mais informações sobre a instalação do Visual Studio 2017, consulte [artigos de blog de Heath Stewart](https://blogs.msdn.microsoft.com/heaths/tag/vs2017/).


## <a name="editing-the-registry-for-a-visual-studio-instance"></a>A edição do Registro para uma instância do Visual Studio

No Visual Studio de 2017, configurações do Registro são armazenadas em um local privado, o que permite várias instâncias lado a lado no mesmo computador com a mesma versão do Visual Studio.

Como essas entradas não são armazenadas no Registro global, há instruções especiais para usar o Editor do Registro para fazer alterações nas configurações do Registro:

1. Se você tiver uma instância do Visual Studio 2017 aberta, feche-a.
2. Inicie o `regedit.exe`.
3. Selecione o nó `HKEY_LOCAL_MACHINE`.
4. No menu principal do Regedit, selecione **Arquivo -> Carregar Hive...** e selecione o arquivo de Registro privado, que é armazenado na pasta **AppData\Local**. Por exemplo:
   ```
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` corresponde à instância do Visual Studio que você deseja procurar.

Você precisará fornecer um nome de hive, que se tornará o nome do hive isolado. Depois de fazer isso, você poderá pesquisar o Registro no hive isolado que criou.

> [!IMPORTANT]
> Antes de iniciar o Visual Studio novamente, você deve descarregar a seção isolada que criou. Para fazer isso, selecione Arquivo -> Descarregar Hive no menu principal do Regedit. (Se você não fizer isso, o arquivo permanecerá bloqueado e o Visual Studio não poderá ser iniciado.)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Guia de Administradores do Visual Studio](visual-studio-administrator-guide.md)

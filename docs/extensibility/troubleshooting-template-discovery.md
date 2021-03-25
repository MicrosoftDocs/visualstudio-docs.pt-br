---
title: Solucionar problemas de descoberta de modelo no Visual Studio | Microsoft Docs
description: Saiba como habilitar o log de diagnóstico para solucionar problemas de implantação de projetos e modelos personalizados no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: troubleshooting
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 82b7b3f5eced4c8e24830fba34e47d224186949d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072943"
---
# <a name="troubleshooting-template-installation"></a>Solução de problemas de instalação do modelo

Se você tiver problemas para implantar seus modelos de projeto ou item, poderá habilitar o log de diagnósticos.

::: moniker range="vs-2017"

1. Crie um arquivo pkgdef na pasta *Common7\IDE\CommonExtensions* para sua instalação. Por exemplo, *c:\Arquivos de programas (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef*.

::: moniker-end

::: moniker range=">=vs-2019"

1. Crie um arquivo pkgdef na pasta *Common7\IDE\CommonExtensions* para sua instalação. Por exemplo, *c:\Arquivos de programas (x86) \Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\EnablePkgDefLogging.pkgdef*.

::: moniker-end

2. Adicione o seguinte ao arquivo pkgdef:

    ```
    [$RootKey$\VsTemplate]
    "EnableTemplateDiscoveryLog"=dword:00000001
    ```

3. Abra um [prompt de comando do desenvolvedor](../ide/reference/command-prompt-powershell.md) para sua instalação e execução `devenv /updateConfiguration` .

::: moniker range="vs-2017"

4. Abra o Visual Studio e inicie as caixas de diálogo novo projeto e novo item para inicializar as duas árvores de modelo.

   O log de modelo agora aparece em **%LocalAppData%\Microsoft\VisualStudio\15.0_ [InstanceId] \VsTemplateDiagnosticsList.csv** (InstanceId corresponde à ID de instalação da sua instância do Visual Studio). Cada inicialização de árvore de modelo acrescenta entradas a esse log.

::: moniker-end

::: moniker range=">=vs-2019"

4. Abra o Visual Studio e inicie as caixas de diálogo **criar um novo projeto** e **novo item** para inicializar as duas árvores de modelo.

   O log de modelo agora aparece em **%LocalAppData%\Microsoft\VisualStudio\16.0_ [InstanceId] \VsTemplateDiagnosticsList.csv** (InstanceId corresponde à ID de instalação da sua instância do Visual Studio). Cada inicialização de árvore de modelo acrescenta entradas a esse log.

::: moniker-end

O arquivo de log contém as seguintes colunas:

- **FullPathToTemplate**, que tem os seguintes valores:

  - 1 para implantação baseada em manifesto

  - 0 para implantação baseada em disco

- **TemplateFileName**

- Outras propriedades de modelo

> [!NOTE]
> Para desabilitar o registro em log, remova o arquivo pkgdef ou altere o valor de `EnableTemplateDiscoveryLog` para `dword:00000000` e execute `devenv /updateConfiguration` novamente.

## <a name="see-also"></a>Confira também

- [Criando modelos personalizados de projeto e item](creating-custom-project-and-item-templates.md)
- [Solução de problemas do Visual Studio](/troubleshoot/visualstudio/welcome-visual-studio/)

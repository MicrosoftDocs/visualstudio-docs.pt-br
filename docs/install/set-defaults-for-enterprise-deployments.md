---
title: Definir padrões para implantações empresariais
description: Saiba mais sobre as políticas de domínio e outras operações de configuração de implantação corporativa do Visual Studio.
ms.date: 04/13/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- gpo
- policy
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9B7B4608-7A3F-4FF4-BDCE-42D9F7CE6DBA
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: b32c56e418631bfc8f5435d0eb113c9da2296ae9
ms.sourcegitcommit: 3985d0ae8d6332f4682c82a10897763173d52961
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107385993"
---
# <a name="set-defaults-for-enterprise-deployments-of-visual-studio"></a>Definir padrões para implantações empresariais do Visual Studio

Você pode definir políticas de Registro que afetam a implantação do Visual Studio. Essas políticas são globais para Machine e afetam:

- Quando alguns pacotes compartilhados com outras versões ou instâncias estão instalados
- Onde e se os pacotes são armazenados em cache
- Como as atualizações do administrador devem ser aplicadas

Você pode definir algumas dessas políticas usando as [opções de linha de comando](use-command-line-parameters-to-install-visual-studio.md), definir valores de registro no computador ou até mesmo distribuí-los usando a Política de Grupo em toda a organização.

## <a name="registry-keys"></a>Chaves do Registro

Há vários locais em que você pode definir os padrões da empresa para habilitar seu controle por meio de Política de Grupo ou diretamente no registro. O Visual Studio procura sequencialmente para verificar se políticas empresariais foram definidas. Assim que um valor de política é descoberto na ordem abaixo, as chaves restantes são ignoradas.

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`
3. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\Setup` (em sistemas operacionais de 64 bits)

Alguns valores de registro são definidos automaticamente na primeira vez em que são usados, caso ainda não estejam definidos. Isso garante que as instalações subsequentes usem os mesmos valores. Esses valores são armazenados na segunda chave do Registro, `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`.

Você pode definir os valores de registro a seguir:

::: moniker range="vs-2017"
| **Nome** | **Tipo** | **Padrão** | **Descrição** |
| -------- | -------- | ----------- | --------------- |
| `CachePath` | `REG_SZ` ou `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages | O diretório em que os manifestos de pacote e opcionalmente, as cargas são armazenados. Para obter mais informações, consulte [desabilitar ou mover a página de cache do pacote](disable-or-move-the-package-cache.md) . |
| `KeepDownloadedPayloads` | `REG_DWORD` | 1 | Manter cargas de pacote, mesmo após a instalação. Você pode alterar o valor a qualquer momento. Desabilitar a política removerá quaisquer payloads de pacote em cache para a instância que você reparar ou modificar. Para obter mais informações, consulte [desabilitar ou mover a página de cache do pacote](disable-or-move-the-package-cache.md) . |
| `SharedInstallationPath` | `REG_SZ` ou `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared | O diretório em que alguns pacotes compartilhados entre versões de instâncias do Visual Studio estão instalados. Você pode alterar o valor a qualquer momento, mas ele só afetará as instalações futuras. Todos os produtos já instalados no local antigo não devem ser movidos ou poderão não funcionar corretamente. |
| `BackgroundDownloadDisabled` |`REG_DWORD` | 0 | Impedir que a instalação baixe atualizações automaticamente para todos os produtos instalados do Visual Studio. Você pode alterar o valor a qualquer momento. |
| `AdministratorUpdatesEnabled` | `REG_DWORD` | 0 | Permite que as atualizações do administrador sejam aplicadas ao computador cliente. Se esse valor estiver ausente ou estiver definido como 0, as atualizações do administrador serão bloqueadas. Esse valor é para uso administrativo. Para obter mais informações, consulte [habilitando atualizações do administrador](enabling-administrator-updates.md). | 
| `AdministratorUpdatesOptOut` | `REG_DWORD` | 0 | Indica que o usuário não deseja receber atualizações do administrador para o Visual Studio. A ausência do valor do registro ou um valor definido de 0 significa que o usuário do Visual Studio deseja receber atualizações do administrador para o Visual Studio. Isso é para o usuário do desenvolvedor (se eles tiverem permissões de administrador no computador cliente). Para obter mais informações, consulte [aplicando atualizações do administrador](../install/applying-administrator-updates.md#understanding-configuration-options). | 
| `UpdateConfigurationFile` | `REG_SZ` ou `REG_EXPAND_SZ` | % ProgramData% \Microsoft\VisualStudio\updates.config | O caminho do arquivo para configurar atualizações administrativas. Para obter mais informações, consulte [métodos para configurar uma atualização de administrador](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update). | 
::: moniker-end

::: moniker range="vs-2019"
| **Nome** | **Tipo** | **Padrão** | **Descrição** |
| -------- | -------- | ----------- | --------------- |
| `CachePath` | `REG_SZ` ou `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages | O diretório em que os manifestos de pacote e opcionalmente, as cargas são armazenados. Para obter mais informações, consulte [desabilitar ou mover a página de cache do pacote](disable-or-move-the-package-cache.md) . |
| `KeepDownloadedPayloads` | `REG_DWORD` | 1 | Manter cargas de pacote, mesmo após a instalação. Você pode alterar o valor a qualquer momento. Desabilitar a política removerá quaisquer payloads de pacote em cache para a instância que você reparar ou modificar. Para obter mais informações, consulte [desabilitar ou mover a página de cache do pacote](disable-or-move-the-package-cache.md) . |
| `SharedInstallationPath` | `REG_SZ` ou `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared | O diretório em que alguns pacotes compartilhados entre versões de instâncias do Visual Studio estão instalados. Você pode alterar o valor a qualquer momento, mas ele só afetará as instalações futuras. Todos os produtos já instalados no local antigo não devem ser movidos ou poderão não funcionar corretamente. |
| `BackgroundDownloadDisabled` |`REG_DWORD` | 0 | Impedir que a instalação baixe atualizações automaticamente para todos os produtos instalados do Visual Studio. Você pode alterar o valor a qualquer momento. |
| `AdministratorUpdatesEnabled` | `REG_DWORD` | 0 | Permite que as atualizações do administrador sejam aplicadas ao computador cliente. Se esse valor estiver ausente ou estiver definido como 0, as atualizações do administrador serão bloqueadas. Esse valor é para uso administrativo. Para obter mais informações, consulte [habilitando atualizações do administrador](enabling-administrator-updates.md). | 
| `AdministratorUpdatesOptOut` | `REG_DWORD` | 0 | Indica que o usuário não deseja receber atualizações do administrador para o Visual Studio. A ausência do valor do registro ou um valor definido de 0 significa que o usuário do Visual Studio deseja receber atualizações do administrador para o Visual Studio. Isso é para o usuário do desenvolvedor (se eles tiverem permissões de administrador no computador cliente). Para obter mais informações, consulte [aplicando atualizações do administrador](../install/applying-administrator-updates.md#understanding-configuration-options). | 
| `UpdateConfigurationFile` | `REG_SZ` ou `REG_EXPAND_SZ` | % ProgramData% \Microsoft\VisualStudio\updates.config | O caminho do arquivo para configurar atualizações administrativas. Para obter mais informações, consulte [métodos para configurar uma atualização de administrador](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update). | 
| `BaselineStickinessVersions2019` | `REG_SZ` ou `REG_EXPAND_SZ` | `16.7.0` | A versão secundária de linha de base de serviço em que o cliente deve permanecer. Para obter mais informações, consulte a página [aplicando atualizações do administrador](../install/applying-administrator-updates.md#understanding-configuration-options) . | 
::: moniker-end

> [!IMPORTANT]
> Se você alterar a política do Registro `CachePath` após qualquer instalação, deverá mover o pacote de cache para o novo local e verificar se ele está protegido para que `SYSTEM` e `Administrators` tenham controle total e `Everyone` tenha acesso de leitura.
> A falha ao mover o cache existente ou protegê-lo pode causar problemas com instalações futuras.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

- [Instalar o Visual Studio](install-visual-studio.md)
- [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
- [Aplicando atualizações do administrador](applying-administrator-updates.md)
- [Desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md)
- [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)

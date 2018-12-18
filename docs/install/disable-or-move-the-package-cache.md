---
title: Desabilitar ou mover o cache do pacote
description: Saiba como desabilitar, habilitar ou mover o cache do pacote para implantações do Visual Studio.
ms.date: 04/14/2017
ms.technology: vs-acquisition
ms.custom: seodec18
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- cache
- nocache
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 2429993A-3F0E-41C5-9562-FEA6AE994440
author: heaths
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 006e7112a2b6c7b990fb412c6a9a2c458bc9e8b2
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159536"
---
# <a name="disable-or-move-the-package-cache"></a>Desabilitar ou mover o cache do pacote

O cache do pacote fornece uma origem de pacotes instalados, caso você precise reparar o Visual Studio ou outros produtos relacionados, em casos em não há conexão com a Internet. Com algumas unidades ou configurações de sistema, no entanto, não convém manter todos os pacotes.
O instalador os baixará quando necessário. Portanto, se você deseja salvar ou recuperar espaço em disco, pode desabilitar ou mover o cache do pacote.

## <a name="disable-the-package-cache"></a>Desabilitar o cache do pacote

Antes de instalar, modificar ou reparar o Visual Studio ou outros produtos com o novo instalador, você pode iniciar o instalador com a opção `--nocache` para o instalador.

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vs_installer.exe" --nocache
```

Qualquer operação que você fizer em qualquer produto removerá quaisquer pacotes existentes para o produto e evitará salvar pacotes após a instalação. Se você modificar ou reparar o Visual Studio e pacotes forem necessários, serão baixados automaticamente e removidos após a instalação.

Se você quiser reabilitar o cache, passe `--cache` em vez disso. Somente os pacotes que são necessários serão armazenados. Portanto, se você precisar restaurar todos os pacotes, deverá reparar o Visual Studio antes de se desconectar da rede.

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vs_installer.exe" repair --passive --norestart --cache
```

Você também pode definir a `KeepDownloadedPayloads` [política do Registro](set-defaults-for-enterprise-deployments.md) para desabilitar o cache antes de instalar, modificar ou reparar o Visual Studio.

## <a name="move-the-package-cache"></a>Mover o cache do pacote

Uma configuração comum do sistema é ter o Windows instalado em um SSD com um disco rígido maior (ou mais) para necessidades de desenvolvimento, como código-fonte, binários de programa e muito mais. Se quiser trabalhar offline em vez disso, você poderá mover o cache do pacote.

No momento, você só poderá fazer isso se definir a `CachePath`[política do Registro](set-defaults-for-enterprise-deployments.md) antes de instalar, modificar ou reparar o Visual Studio.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Definir padrões para implantações corporativas](set-defaults-for-enterprise-deployments.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)

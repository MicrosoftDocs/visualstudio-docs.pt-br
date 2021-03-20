---
title: OpenCV
description: Exemplo de personalização usando o devinit para o Linux e o Windows para o repositório OpenCV.
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 319f560e4661f12acbef941692e5fd2c257c25ee
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672463"
---
# <a name="opencv"></a>OpenCV

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

Este exemplo ilustra como personalizar o [GitHub Codespaces](https://github.com/features/codespaces) para desenvolver com projetos de várias plataformas, como [OpenCV/OpenCV](https://github.com/opencv/opencv).

As personalizações a seguir já estão aplicadas na bifurcação [Microsoft/OpenCV](https://github.com/microsoft/opencv) e permitem criar o direcionamento para o Windows e o Ubuntu.

## <a name="customization-with-devcontainerjson-and-devinitjson"></a>Personalização com devcontainer.jse devinit.jsem

O `.devcontainer` diretório precisa conter os seguintes arquivos:

* devcontainer.json
* devinit.jsem

### <a name="devcontainerjson"></a>devcontainer.json

Veja a seguir o conteúdo do _devcontainer.jsno_ arquivo.

```json
{
  "postCreateCommand": "devinit init"
}
```

O `postCreateCommand` inicia a ferramenta  [devinit](devinit-and-codespaces.md) , que consome _devinit.jsem_.

### <a name="devinitjson"></a>devinit.jsem

Veja a seguir o conteúdo do [_devinit.jsno_](devinit-json.md) arquivo.

```json
{
    "run": [
        {
            "comments": "Example that will install Ubuntu 20.04 using WSL2, and configure it with various packages useful for C++ development.",
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```

O _devinit.jsno_ é o arquivo consumido pela ferramenta [devinit](devinit-and-codespaces.md) e deve estar no mesmo diretório de _devcontainer.jsem_.

Neste exemplo, a ferramenta [WSL-install](tool-wsl-install.md) é usada para criar uma instância WSL que executa o Ubuntu 20, 4 e o provisionamento com ferramentas essenciais de desenvolvimento em C++.
## <a name="targeting-windows-or-linux"></a>Direcionamento para Windows ou Linux

Uma configuração de compilação padrão direcionada ao Windows sempre é criada com o nome `x64-Debug` .

Ao adicionar os arquivos mencionados acima, na criação da instância do codespace, o Visual Studio provisiona uma nova conexão SSH no [Gerenciador de conexões](/cpp/linux/connect-to-your-remote-linux-computer)e cria uma nova configuração no seletor de configuração que tem como alvo a instância do Ubuntu por meio da conexão SSH.

![Configuração de direcionamento para Ubuntu](media/wsl-ssh-linux-configuration.png).

Ao selecionar a configuração realçada que se destina a WSL, é possível criar e depurar os destinos de compilação do OpenCV.

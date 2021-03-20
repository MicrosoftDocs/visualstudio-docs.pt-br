---
title: wsl-install
description: devinit ferramenta WSL-install.
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4dff121d7866918d5c30986dc9bd4c3cab039ac5
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672421"
---
# <a name="wsl-install"></a>wsl-install

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `wsl-install` ferramenta é usada para instalar o Linux distribuições para o [subsistema do Windows para Linux](/windows/wsl/) (WSL).

> [!IMPORTANT]
> A `wsl-install` ferramenta requer que o WSL 2 já esteja habilitado no Windows. Se, por algum motivo, o WSL 2 não estiver habilitado, você poderá seguir a [documentação de instalação do WSL](https://docs.microsoft.com/windows/wsl/install-win10). Você também pode usar a ferramenta de [habilitação de WindowsFeature](tool-windowsfeature-enable.md) para habilitar todos os recursos do Windows necessários.

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                             |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                             |
| [**entrada**](#input)                              | string | Sim      | O distribuição a ser instalado. Consulte a [entrada](#input) abaixo para obter detalhes.     |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.  |

### <a name="input"></a>Entrada

O URI para o pacote de distribuição de aplicativo AppX ( `.appx` ) que contém o distribuição a ser implantado. O URI deve apontar para um `.appx` arquivo que contém um único `install.tar.gz` na raiz do arquivo ou dentro de um arquivo interno `.appx` . Exemplos de distribuições com suporte incluem:

| Distribuição                          | Uri                                                           |
|---------------------------------|---------------------------------------------------------------|
| Ubuntu 20.04                    | https://aka.ms/wslubuntu2004                                  |
| Ubuntu 18.04                    | https://aka.ms/wsl-ubuntu-1804                                |
| Ubuntu 16.04                    | https://aka.ms/wsl-ubuntu-1604                                |
| Debian GNU/Linux                | https://aka.ms/wsl-debian-gnulinux                            |
| Kali Linux                      | https://aka.ms/wsl-kali-linux-new                             |
| OpenSUSE Leap 42                | https://aka.ms/wsl-opensuse-42                                |
| SUSE Linux Enterprise Server 12 | https://aka.ms/wsl-sles-12                                    |

> [!NOTE]
> No momento, não há suporte para distribuições do ARM Linux no Codespaces do GitHub.

### <a name="additional-options"></a>Opções adicionais

Há suporte para várias opções adicionais:

| Nome                      | Type      | Obrigatório | Valor                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --WSL-versão             | Cadeia de caracteres    | No       | Versão do WSL a ser usada. O valor padrão é 2.                                                                                                                                  |
| --pós-criação-comando     | Cadeia de caracteres    | No       | O comando a ser executado dentro do distribuição do Linux quando a instalação for concluída. O comando deve ser formatado como uma única palavra ou encapsulado entre aspas. O padrão é nenhum comando.  |

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `wsl-install` ferramenta é erro como a `input` propriedade, o distribuição a ser instalado, é necessário.

## <a name="example-usage"></a>Exemplo de uso
Abaixo estão exemplos de como executar `wsl-install` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-ubuntu-2004"></a>.devinit.jsem que o Ubuntu 20, 4 será instalado:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command"></a>.devinit.jsem que o Ubuntu 20, 4 será instalado e executará um comando post Create:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'echo Hello from Ubuntu!'"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command-that-configures-the-packages-listed"></a>.devinit.jsem que o Ubuntu 20, 4 será instalado e executará um comando post Create que configurará os pacotes listados:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```

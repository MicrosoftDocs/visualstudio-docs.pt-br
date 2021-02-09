---
title: choco-upgrade
description: devinit Tool choco-upgrade.
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
ms.openlocfilehash: fab2a3f2893ba79874b6909b3d19ccf939f8b14a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906315"
---
# <a name="choco-upgrade"></a>choco-upgrade

A `choco-upgrade` ferramenta pode ser usada para instalar e atualizar pacotes de [Chocolatey](https://chocolatey.org/docs/commandsupgrade) .

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta não fará nada.

| Nome                                             | Tipo   | Obrigatório  | Valor                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No        | Propriedade de comentários opcional. Não usado.                                                                          |
| [**entrada**](#input)                              | string | Sim       | O pacote a ser atualizado. Consulte a [entrada](#input) abaixo para obter detalhes.                                                 |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No        | Opções adicionais a serem passadas para a ferramenta. Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.       |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar o nome do pacote a ser atualizado (por exemplo, ' MongoDB ') ou o caminho para um arquivo de configuração dos seguintes formatos _packages.config_, _. nuspec_ e _. nupkg_. O valor de `input` será acrescentado a um `choco upgrade` comando (por exemplo `choco upgrade mongodb` ), juntamente com quaisquer argumentos específicos no [`additionalOptions`](#additional-options) e as `choco` Opções internas (definidas [abaixo](#built-in-options)). Os pacotes podem ser encontrados na [Galeria de pacotes de chocolate](https://chocolatey.org/packages). Ao usar um arquivo de configuração, você pode passar o caminho para esse arquivo na `input` propriedade, por exemplo: `"input":"packages.config"` .

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de `additionalOptions` . Esses argumentos são passagem direta para os argumentos usados pelo [`choco upgrade`](https://chocolatey.org/docs/commands-upgrade) e são definidos na documentação de Chocolatey.

### <a name="built-in-options"></a>Opções internas

A `choco-upgrade` ferramenta define um número de `choco` argumentos de linha de comando para garantir que o `choco` possa ser executado sem periféricos. Esses argumentos estão listados abaixo e a documentação sobre eles pode ser encontrada na [documentação do Chocolatey](https://chocolatey.org/docs/).

| Nome                  | Descrição                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--Sim**             | Confirmar todos os prompts – escolha a resposta afirmativo em vez de solicitar. Implica `--accept-license` . |
| **--sem progresso**     | Não mostrar o progresso-as porcentagens de progresso não serão mostradas.                                         |
| **--Skip-PowerShell** | Ignorar PowerShell-chocolateyInstall.ps1 não será executado.                                              |

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `choco-upgrade` ferramenta é erro, pois a `input` propriedade é necessária.

## <a name="example-usage"></a>Exemplo de uso
Abaixo estão exemplos de como executar `choco-upgrade` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-update-packages-listed-in-packagesconfig"></a>.devinit.jsno que atualizarão os pacotes listados em packages.config:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "packages.config",
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-mongodb"></a>.devinit.jsno que irá atualizar o MongoDB:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb"
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-to-a-specific-version-of-mongodb"></a>.devinit.jsno que será atualizado para uma versão específica do MongoDB:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb",
            "additionalOptions": "--version 4.2.7"
        }
    ]
}
```
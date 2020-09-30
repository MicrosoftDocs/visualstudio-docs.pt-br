---
title: dotnet-toolinstall
description: ferramenta devinit dotnet-toolinstall.
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: cb19cab0c03b87894029a18f682f05def6a2197c
ms.sourcegitcommit: 09d1f5cef5360cdc1cdfd4b22a1a426b38079618
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91005541"
---
# <a name="dotnet-toolinstall"></a>dotnet-toolinstall

A `dotnet-toolinstall` ferramenta é usada para instalar as [Ferramentas do .NET Core](https://dotnet.microsoft.com/) por meio do `dotnet tool update` comando.

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Tipo   | Obrigatório | Valor                                                                 |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                 |
| [**entrada**](#input)                              | string | Sim      | A ferramenta .NET Core a ser instalada. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.      |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar a instalação da ferramenta .NET Core. Há uma lista não oficial de ferramentas em [https://github.com/natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) .

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de `additionalOptions` . Esses argumentos são uma passagem direta para os argumentos usados pelo [`dotnet tool update`](https://docs.microsoft.com/dotnet/core/tools/global-tools#update-a-tool) comando. 

O `dotnet tool update` comando é usado para lidar com segurança com o caso em que uma ferramenta já está instalada.

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `dotnet-toolinstall` ferramenta é erro, conforme `input` necessário.

## <a name="example-usage"></a>Exemplo de uso

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-2.0",
    "run": [
        {
            "comments": "Example that will install the dotnet-trace tool.",
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace"
        },
        {
            "comments": "Example that will install the dotnet-trace tool as a global tool.",
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace",
            "additionalOptions": "--global"
        }
    ]
}
```
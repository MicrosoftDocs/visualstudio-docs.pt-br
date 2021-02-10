---
title: require-nuget
description: ferramenta devinit require-NuGet.
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
ms.openlocfilehash: 38a8ab363fffe1f13651afb4065833cfd3eb840f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99950445"
---
# <a name="require-nuget"></a>require-nuget

A `require-nuget` ferramenta baixa a CLI do NuGet e a adiciona ao `PATH` . A CLI do NuGet fornece a extensão completa da funcionalidade do NuGet para instalar, criar, publicar e gerenciar pacotes sem fazer alterações nos arquivos do projeto. Leia mais sobre a CLI do NuGet [aqui](/nuget/reference/nuget-exe-cli-reference).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                                |
| [**entrada**](#input)                              | Cadeia de caracteres | No       | Versão da CLI do NuGet para instalar. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                     |

### <a name="input"></a>Entrada

O `input` é uma propriedade opcional usada para especificar a versão do NUGET CLI a ser instalada. Se `input` for omitido, a versão mais recente da CLI será instalada.

### <a name="additional-options"></a>Opções adicionais

Não usado.

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-nuget` ferramenta é instalar a versão mais recente da CLI do NuGet.

## <a name="example-usage"></a>Exemplo de uso
Veja abaixo um exemplo de como executar `require-nuget` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-a-specified-version-of-nuget"></a>.devinit.js, que instalará uma versão especificada do NuGet:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nuget",
            "input": "5.5.1",
        }
    ]
}
```
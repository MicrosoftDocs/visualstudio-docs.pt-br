---
title: require-dotnetframeworksdk
description: a ferramenta devinit requer-dotnetframeworksdk.
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
ms.openlocfilehash: 4de8daf4b57d4775e4f1ede57392bb594bae53ea
ms.sourcegitcommit: 09d1f5cef5360cdc1cdfd4b22a1a426b38079618
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91005106"
---
# <a name="require-dotnetframeworksdk"></a>require-dotnetframeworksdk

A `require-dotnetframeworksdk` ferramenta é usada para instalar o [SDK do .NET Framework](https://dotnet.microsoft.com/) por meio dos [instaladores fornecidos](https://dotnet.microsoft.com/download/visual-studio-sdks).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Tipo   | Obrigatório  | Valor                                                                                    |
|--------------------------------------------------|--------|-----------|------------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No        | Propriedade de comentários opcional. Não usado.                                                    |
| [**entrada**](#input)                              | Cadeia de caracteres | No        | A versão do SDK do .NET Framework para instalar. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No        | Não usado. Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.               |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar a versão .NET Framework SDK a ser instalada. Uma lista de versões pode ser encontrada no [site DOTNET-Framework](https://dotnet.microsoft.com/download/visual-studio-sdks).

### <a name="additional-options"></a>Opções adicionais

Não usado.

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-dotnetframeworksdk` ferramenta é instalar a versão mais recente. Consulte os [instaladores fornecidos](https://dotnet.microsoft.com/download/visual-studio-sdks) para obter a versão mais recente.

## <a name="example-usage"></a>Exemplo de uso

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-2.0",
    "run": [
        {
            "comments": "Example that will install a specific version of the .NET Framework SDK.",
            "tool": "require-dotnetframeworksdk",
            "input": "4.8.0"
        },
        {
            "comments": "Example that will install the latest version of the .NET Framework SDK.",
            "tool": "require-dotnetframeworksdk"
        }
    ]
}
```
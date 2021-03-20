---
title: require-dotnetframeworksdk
description: a ferramenta devinit requer-dotnetframeworksdk.
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
ms.openlocfilehash: 0c40ebfd2a8b665a1421ba70c0f785774e97d3df
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672147"
---
# <a name="require-dotnetframeworksdk"></a>require-dotnetframeworksdk

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `require-dotnetframeworksdk` ferramenta é usada para instalar o [SDK do .NET Framework](https://dotnet.microsoft.com/) por meio dos [instaladores fornecidos](https://dotnet.microsoft.com/download/visual-studio-sdks).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório  | Valor                                                                                    |
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
Abaixo estão exemplos de como executar `require-dotnetframeworksdk` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-the-latest-net-framework"></a>.devinit.jsque instalará o .NET Framework mais recente:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-the-net-framework"></a>.devinit.js, que instalará uma versão específica do .NET Framework:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk",
            "input": "4.8.0"
        }
    ]
}
```
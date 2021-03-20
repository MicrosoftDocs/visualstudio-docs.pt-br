---
title: require-dotnetcoresdk
description: a ferramenta devinit requer-dotnetcoresdk.
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
ms.openlocfilehash: 1963ad8dfe1bd31eb3f98ec6fdf57524a274cfb6
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671787"
---
# <a name="require-dotnetcoresdk"></a>require-dotnetcoresdk

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `require-dotnetcoresdk` ferramenta é usada para instalar o [SDK do .NET Core](https://dotnet.microsoft.com/) e o tempo de execução compartilhado por meio do script [dotnet-install](/dotnet/core/tools/dotnet-install-script) .

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                               |
| [**entrada**](#input)                              | Cadeia de caracteres | No       | A versão do SDK do .NET Core a ser instalada. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                    |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar a versão de SDK do .NET Core a ser instalada. Uma lista de versões pode ser encontrada no [site dotnet-Core](https://dotnet.microsoft.com/download/dotnet-core).

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de `additionalOptions` . Esses argumentos são uma passagem direta para os argumentos usados no script [dotnet-install](/dotnet/core/tools/dotnet-install-script) . Para obter mais informações sobre os parâmetros disponíveis, consulte a [documentação](/dotnet/core/tools/dotnet-install-script) do script [dotnet-install](/dotnet/core/tools/dotnet-install-script) . Ao usar `additionalOptions` o, certifique-se de usar os nomes e o formato do argumento do PowerShell.

> [!NOTE]
> Qualquer valor adicional para um argumento que inclua um espaço deve incluir um par adicional de aspas de escape (usando barra invertida). Um exemplo pode ser visto no [uso de exemplo](#example-usage) usando `-InstallDir` .

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-dotnetcoresdk` ferramenta é instalar a versão do SDK do .NET Core especificado em um `global.json` arquivo [(documentação)](/dotnet/core/tools/global-json?tabs=netcore3x) no diretório de trabalho atual. Se nenhum `global.json` arquivo for encontrado, `require-dotnetcoresdk` o instalará a versão atual mais recente do SDK do .NET Core e o tempo de execução compartilhado.

## <a name="example-usage"></a>Exemplo de uso
Abaixo estão exemplos de como executar `require-dotnetcoresdk` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-the-latest-version-of-net-core"></a>.devinit.js, que instalará a versão mais recente do .NET Core:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core"></a>.devinit.jsno que instalará uma versão específica do .NET Core:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core-and-aspnet-core"></a>.devinit.jsno que instalará uma versão específica do .NET Core e ASP.NET Core:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0",
            "additionalOptions": "-Runtime aspnetcore"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-net-core-in-a-specific-directory"></a>.devinit.js, que instalará o .NET Core em um diretório específico:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "additionalOptions": "-InstallDir \"C:\\Program Files\\dotnet\""
        }
    ]
}
```
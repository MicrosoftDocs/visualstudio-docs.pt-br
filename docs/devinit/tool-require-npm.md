---
title: require-npm
description: a ferramenta devinit requer-NPM.
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
ms.openlocfilehash: 93723ee50fd718c5abb7c86f0f3b986ed9832abd
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672292"
---
# <a name="require-npm"></a>require-npm

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `require-npm` ferramenta é usada para instalar o [NPM](https://www.npmjs.com/).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                                                       |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                                       |
| [**entrada**](#input)                              | string | Sim      | Especifica a versão do NPM. Consulte a [entrada](#input) abaixo para obter detalhes.                           |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Não usado. Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                  |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar a versão NPM.

### <a name="additional-options"></a>Opções adicionais

Não utilizado.

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-nodejs` ferramenta é instalar a versão mais recente do LTS do NPM.

## <a name="example-usage"></a>Exemplo de uso
Abaixo estão exemplos de como executar `require-npm` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-the-lts-of-npm"></a>.devinit.js, que instalará o LTS do NPM:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-npm"></a>.devinit.js, que instalará uma versão específica do NPM:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm",
            "input": "6.14.6"
        }
    ]
}
```
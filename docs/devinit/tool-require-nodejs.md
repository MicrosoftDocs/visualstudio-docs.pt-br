---
title: require-nodejs
description: a ferramenta devinit requer-NodeJS.
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
ms.openlocfilehash: 75690f85fb627140226242b476d70bfc4dac6ed2
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672299"
---
# <a name="require-nodejs"></a>require-nodejs

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `require-nodejs` ferramenta é usada para instalar o [Node.js](https://nodejs.org/) por meio de um MSI distribuído pela organização do Node.js.

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                                     |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                     |
| [**entrada**](#input)                              | Cadeia de caracteres | No       | A versão do Node.JS a ser instalada. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.          |

### <a name="input"></a>Entrada

A `input` propriedade é usada para especificar a versão de Node.js. Uma lista de versões pode ser encontrada na [ página de downloadNode.js](https://nodejs.org/en/download/). O número de versão completo é obrigatório. Minor. caminho (por exemplo 14.4.0) se algum for omitido, a instalação falhará.

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de `additionalOptions` . Esses argumentos são passagem direta para o instalador MSI para Node.js.  

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-nodejs` ferramenta é instalar a versão mais recente do LTS do nó, conforme detalhado no [site](https://nodejs.org/en/download/)Node.JS.

## <a name="example-usage"></a>Exemplo de uso
Abaixo estão exemplos de como executar `require-nodejs` o usando um `.devinit.json` . 

#### <a name="devinitjson-that-will-install-the-lts-of-nodejs"></a>.devinit.js, que instalará o LTS de Node.js:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-nodejs"></a>.devinit.js, que instalará uma versão específica do Node.js:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs",
            "input": "14.4.0"
        }
    ]
}
```

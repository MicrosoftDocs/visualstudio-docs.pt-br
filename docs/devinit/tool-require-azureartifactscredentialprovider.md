---
title: require-azureartifactscredentialprovider
description: a ferramenta devinit requer-azureartifactscredentialprovider.
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
ms.openlocfilehash: e5ba9847b09f06f853f48a0885de5e0d63664fac
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671605"
---
# <a name="require-azureartifactscredentialprovider"></a>require-azureartifactscredentialprovider

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `require-azureartifactscredentialprovider` ferramenta instala o provedor de credenciais Azure Artifacts. O provedor de credenciais Azure Artifacts automatiza a aquisição de credenciais necessárias para restaurar os pacotes NuGet como parte do seu fluxo de trabalho de desenvolvimento do .NET. Leia mais sobre Azure Artifacts provedor de credenciais [aqui](https://github.com/microsoft/artifacts-credprovider/blob/master/README.md).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta seguirá o comportamento [padrão](#default-behavior) detalhado abaixo.

| Nome                                             | Type   | Obrigatório | Valor                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **feitos**                                     | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                                |
| [**entrada**](#input)                              | Cadeia de caracteres | No       | Não usado. Consulte a [entrada](#input) abaixo para obter detalhes. |
| [**additionalOptions**](#additional-options)     | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                     |

### <a name="input"></a>Entrada

Não usado. Ignora qualquer entrada, se mencionada.

### <a name="additional-options"></a>Opções adicionais

As opções adicionais são passadas como estão para o comando do provedor de credenciais.

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `require-azureartifactscredentialprovider` ferramenta é instalar a versão mais recente do provedor de credenciais Azure Artifacts.

## <a name="example-usage"></a>Exemplo de uso
Veja abaixo um exemplo de como executar `require-azureartifactscredentialprovider` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-azure-artifacts-credential-provider"></a>.devinit.js, que instalará Azure Artifacts provedor de credenciais:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-azureartifactscredentialprovider",
        }
    ]
}
```

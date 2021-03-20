---
title: Winget-instalar
description: ferramenta devinit para Winget.
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4a2ad1ef30692d7d23f2d450f0ba32d6f38f8262
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672620"
---
# <a name="winget-install"></a>Winget-instalar

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Como parte desse `devinit` e as ferramentas associadas não estarão mais disponíveis. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

A `winget-install` ferramenta é usada para instalar [pacotes do Winget](https://docs.microsoft.com/windows/package-manager/winget/).

## <a name="usage"></a>Uso

Se as `input` Propriedades e `additionalOptions` forem omitidas ou vazias, a ferramenta gerará um erro.

| Nome                                         | Type   | Obrigatório | Valor                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **feitos**                                 | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                             |
| [**entrada**](#input)                          | Cadeia de caracteres | No       | O pacote a instalar. Consulte a [entrada](#input) abaixo para obter detalhes.                    |
| [**additionalOptions**](#additional-options) | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                  |

### <a name="input"></a>Entrada

A propriedade de entrada é usada para especificar o `Id` ou `Name` o pacote a ser instalado (por exemplo, ' MongoDB. Server '). O valor de entrada será acrescentado a um `winget install` comando (por exemplo, `winget install MongoDB.Server` ). Se o nome do pacote não for exclusivo e corresponder a outros pacotes, você poderá especificar o `Id` do pacote e adicionar o `--exact` sinalizador ao `additionalOptions` para garantir que a identidade do pacote corresponda exatamente. O `Id` de um pacote pode ser encontrado executando o `winget search` comando e usando o `Id` parâmetro para um pacote.  

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de AdditionalOptions. Esses argumentos são passagem direta para os argumentos usados pelo `winget install` e são definidos na `winget install` [documentação](https://docs.microsoft.com/windows/package-manager/winget/install)do.

#### <a name="manifests"></a>Manifestos

Um opcional adicional com `winget` suporte é a capacidade de fornecer um [arquivo de manifesto](https://docs.microsoft.com/windows/package-manager/winget/install#local-install) para detalhar o pacote a ser instalado. Para usar esse recurso com devinit `input` , o parâmetro deve estar vazio e a `additionalOptions` propriedade deve incluir a `--manifest` opção seguida pelo caminho para o manifesto (por exemplo, `--manifest path.to.manifest.yml` ).

### <a name="built-in-options"></a>Opções internas

A ferramenta Winget-install define um número de argumentos de linha de comando Winget para garantir que o Winget possa ser executado sem periféricos. Esses argumentos estão listados abaixo e a documentação sobre eles pode ser encontrada na `winget install` [documentação](https://docs.microsoft.com/windows/package-manager/winget/install)do.

| Nome     | Descrição                                                                                                                       |
|----------|-----------------------------------------------------------------------------------------------------------------------------------|
| --silencioso | Executa o instalador no modo sem confirmação. Isso suprime todas as interfaces do usuário. A experiência padrão mostra o progresso do instalador.                       | 

## <a name="example-usage"></a>Exemplo de uso

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-6.0",
    "run": [
        {
            "comments": "Installs Microsoft PowerToys.",
            "tool": "winget-install",
            "input": "Microsoft.PowerToys",
            "additionalOptions": "--version 0.15.2",
        },
        {
            "comments": "Installs PostgreSQL.",
            "tool": "winget-install",
            "input": "PostgreSQL.PostgreSQL",
            "additionalOptions": "--exact"
        },
        {
            "comments": "Installs the package defined in winget-manifest.yml.",
            "tool": "winget-install",
            "additionalOptions": "--manifest winget-manifest.yml"
        }
    ]
}
```

---
title: msi-install
description: ferramenta devinit para msiexec.
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
ms.openlocfilehash: 9b177d63ceabd8162c5ddd77e87c68d4a820b00a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896234"
---
# <a name="msi-install"></a>msi-install

A `msi-install` ferramenta é usada para instalar `.msi` formatos de arquivo de pacote usando [msiexec](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec).

## <a name="usage"></a>Uso

Se o `input` for omitido ou ficar vazio, a ferramenta produzirá um erro.

| Nome                                         | Type   | Obrigatório | Valor                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **feitos**                                 | Cadeia de caracteres | No       | Propriedade de comentários opcional. Não usado.                                             |
| [**entrada**](#input)                          | string | Sim      | O `msi` a instalar. Consulte a [entrada](#input) abaixo para obter detalhes.                      |
| [**additionalOptions**](#additional-options) | Cadeia de caracteres | No       | Consulte [as opções adicionais](#additional-options) abaixo para obter detalhes.                  |

### <a name="input"></a>Entrada

A propriedade de entrada é usada para especificar um caminho ou uma URL para um `.msi` arquivo que será instalado. Se o caminho para o `.msi` estiver incorreto ou a URL não apontar para um `.msi` diretamente, `msi-install` o observará que o pacote de instalação não pode ser aberto.

### <a name="additional-options"></a>Opções adicionais

Opções de configuração adicionais podem ser passadas como um valor de AdditionalOptions. Esses argumentos são uma passagem direta para os argumentos usados pelo `msiexec` e são definidos na `msiexec` [documentação](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)do.

### <a name="built-in-options"></a>Opções internas

A ferramenta MSI-install define um número de `msiexec` argumentos de linha de comando para garantir que o MSI possa ser executado sem periféricos. Esses argumentos estão listados abaixo e a documentação sobre eles pode ser encontrada na `msiexec` [documentação](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)do.

| Nome          | Descrição                                                                                                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /i            | Executa uma instalação normal                                                                                                                                                                    |
| /quiet        | Especifica o modo silencioso sem interação do usuário necessária                                                                                                                                        |
| /qn           | Especifica que não há interface do usuário durante o processo de instalação                                                                                                                                           |
| /passive      | Especifica o modo autônomo em que a instalação mostra apenas uma barra de progresso                                                                                                                    |
| /l * V          | Ativa o registro em log e registra todas as informações, incluindo informações detalhadas, em um `devinit.log` arquivo na pasta temporária local da máquina. Se a ferramenta falhar, o caminho do arquivo de log será exibido.      |
| /norestart    | Interrompe a reinicialização da máquina após a conclusão da instalação, mas retornará um código de saída 3010 se for necessária uma reinicialização                                                                  |

### <a name="default-behavior"></a>Comportamento padrão

O comportamento padrão da `msi-install` ferramenta é erro, pois a `input` propriedade é necessária.

## <a name="example-usage"></a>Exemplo de uso
Veja abaixo um exemplo de como executar `msi-install` o usando um `.devinit.json` .

#### <a name="devinitjson-that-will-install-the-7-zip-msi"></a>.devinit.js, que instalará o MSI 7-zip:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-4.0",
    "run": [
        {
            "tool": "msi-install",
            "input": "https://www.7-zip.org/a/7z1900.msi"
        }
    ]
}
```

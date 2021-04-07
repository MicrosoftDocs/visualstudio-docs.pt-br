---
title: Migrar testsettings para RunSettings
description: Saiba como migrar testsettings para RunSettings
ms.custom: SEO-VS-2020
ms.date: 03/18/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab1cfe921777fa75d4f69251668934e8d78d9bec
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106087179"
---
# <a name="upgrade-from--testsettings-to-runsettings"></a>Atualizar de  *. testsettings* para *. RunSettings*

Você pode atualizar o arquivo de configuração de teste de *. testsettings* para *. RunSettings* com a ferramenta SettingsMigrator que é instalada juntamente com o Visual Studio. Dependendo do local de instalação do Visual Studio, você pode encontrar a ferramenta Settings Migrator no seguinte caminho: `C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Extensions\TestPlatform\SettingsMigrator.exe`

No local correto do diretório, você pode executar a ferramenta com o formato abaixo:

```console
SettingsMigrator.exe <Full path to testsettings file to be migrated>
SettingsMigrator.exe <Full path to testsettings file to be migrated> <Full path to runsettings file to be created>
```

## <a name="examples"></a>Exemplos
```console
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings E:\MyTest\MyNewRunSettings.runsettings
```

Se você estiver interessado em ler mais sobre como as opções *. testsettings* são convertidas em *. RunSettings* , você pode encontrar mais detalhes de implementação no [repositório da plataforma de teste](https://github.com/microsoft/vstest-docs/blob/master/RFCs/0023-TestSettings-Deprecation.md#migration) de software livre no github.

## <a name="see-also"></a>Confira também

- [Configurar execuções de teste com `.runsettings`](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [Atualizar do MSTestv1 para o MSTestv2](../test/mstest-update-to-mstestv2.md)
- [Teste de unidade em seu código](../test/unit-test-your-code.md)
- [Depurar testes de unidade com o Gerenciador de Testes](../test/debug-unit-tests-with-test-explorer.md)

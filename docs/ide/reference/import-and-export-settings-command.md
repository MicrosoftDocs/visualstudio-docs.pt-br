---
description: Importa, exporta ou redefine as configurações do Visual Studio. Extensão de arquivo vssettings
title: Comando Importar e Exportar Configurações
ms.date: 05/28/2021
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dba50cf598c3c74f6c9407fbef5d55f938941a11
ms.sourcegitcommit: 63cb90e8cea112aa2ce8741101b309dbc709e393
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2021
ms.locfileid: "110687645"
---
# <a name="import-and-export-settings-command-vssettings-file"></a>Comando Importar e Exportar Configurações (arquivo .vssettings)

Importa, exporta ou redefine Visual Studio arquivo de configurações, `.vssettings` .

O esquema do arquivo está aberto. Normalmente, o esquema segue uma estrutura XML em que cada categoria é uma marca, que pode conter marcas de subcategoria. Essas marcas de subcategoria podem conter marcas de valor de propriedade. Embora a maioria dos pacotes use a estrutura comum, qualquer pacote no Visual Studio pode contribuir com XML arbitrário para o arquivo com o esquema escolhido.

## <a name="syntax"></a>Sintaxe

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>Comutadores

/export:`filename`

Opcional. Exporta as configurações atuais para o arquivo especificado.

/import:`filename`

Opcional. Importa as configurações no arquivo especificado.

/reset

Opcional. Redefine as configurações atuais.

## <a name="remarks"></a>Comentários

Executar esse comando sem nenhuma opção abre o assistente **Importar e Exportar Configurações**. Para obter mais informações, confira [Sincronizar as configurações](../synchronized-settings-in-visual-studio.md) e [Configurações do ambiente](../environment-settings.md).

## <a name="example"></a>Exemplo

O seguinte comando exporta as configurações atuais para o arquivo `MyFile.vssettings`:

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```



## <a name="see-also"></a>Confira também

- [Configurações do ambiente](../../ide/environment-settings.md)
- [Sincronizar as configurações](../../ide/synchronized-settings-in-visual-studio.md)
- [Personalizar o IDE do Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)

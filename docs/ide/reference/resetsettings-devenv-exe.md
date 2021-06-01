---
title: -ResetSettings (devenv.exe)
description: Saiba como usar a opção de linha de comando ResetSettings devenv para restaurar Visual Studio configurações padrão e iniciar automaticamente o Visual Studio IDE.
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /ResetSettings switch
- ResetSettings switch
- /ResetSettings Devenv switch
- settings [Visual Studio], resetting
ms.assetid: 1d41021c-6f58-4bd5-b122-d1c995812192
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e523738ff23b40c80b5df21d90b582d94c59087f
ms.sourcegitcommit: a8031c1387d2090129ed33e063744f9f31653dcd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2021
ms.locfileid: "110724532"
---
# <a name="resetsettings-devenvexe"></a>/ResetSettings (devenv.exe)

Restaura as configurações padrão do Visual Studio e inicia automaticamente o IDE do Visual Studio. Opcionalmente, essa opção redefine as configurações para um arquivo de configurações especificado ( `*.vssettings` ).

As configurações padrão derivam do perfil selecionado quando o Visual Studio foi iniciado pela primeira vez.

> [!TIP]
> Para saber como redefinir configurações usando o IDE (ambiente de desenvolvimento integrado), confira [Reset settings](../environment-settings.md#reset-settings) (Redefinir configurações).

## <a name="syntax"></a>Sintaxe

```shell
devenv /ResetSettings [SettingsFile|DefaultCollectionSpecifier]
```

## <a name="arguments"></a>Argumentos

- *SettingsFile*

  Opcional. O caminho completo e o nome do `.vssettings` arquivo a ser aplicado Visual Studio.

- *DefaultCollectionSpecifier*

  Opcional. Um especificador que representa uma coleção padrão de configurações a restaurar. Escolha um dos especificadores de coleção padrão listados na tabela.

  | Nome da coleção padrão | Especificador da coleção |
  | --- | --- |
  | **Geral** | `General` |
  | **JavaScript** | `JavaScript` |
  | **Visual Basic** | `VB` |
  | **Visual C #** | `CSharp` |
  | **Visual C++** | `VC` |
  | **Desenvolvimento para a Web** | `Web` |
  | **Desenvolvimento para a Web (Somente Código)** | `WebCode` |

## <a name="remarks"></a>Comentários

Se nenhum *SettingsFile* for especificado, o IDE abrirá usando as configurações existentes. 


## <a name="example"></a>Exemplo

O primeiro exemplo aplica as configurações armazenadas no arquivo `MySettings.vssettings`.

O segundo exemplo restaura o perfil padrão do Visual C#.

O terceiro exemplo também fechará Visual Studio depois de aplicar as configurações. Você pode anexar `/Command "File.Exit"` .

```shell
devenv /ResetSettings "%USERPROFILE%\MySettings.vssettings"

devenv /ResetSettings CSharp

devenv /NoSplash /ResetSettings General /Command Exit 
```

## <a name="see-also"></a>Confira também

- [Configurações do ambiente](../environment-settings.md)
- [Personalizar o IDE do Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)
- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)

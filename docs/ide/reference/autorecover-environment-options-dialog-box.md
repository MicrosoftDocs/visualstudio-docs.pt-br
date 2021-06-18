---
title: AutoRecover, Caixa de diálogo Opções, Ambiente
description: Saiba mais sobre a caixa de diálogo recuperação automática, ambiente, opções e como ela é usada para especificar se o backup automático dos arquivos deve ou não ser feito.
ms.custom: SEO-VS-2020
ms.date: 08/14/2020
ms.topic: reference
f1_keywords:
- VS.DialogAutoRestore
- VS.ToolsOptionsPages.Environment.AutoRecover
- VS.ToolsOptionsPages.Environment.Auto_Save_and_Restore
helpviewer_keywords:
- files, recovering
- AutoRecover page
- saving files, automatically
- files, saving automatically
ms.assetid: 397e5e44-4bbe-4289-94d1-642b466c9111
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 007e82ee7c1c2839ba266794432605f1f92a1669
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307785"
---
# <a name="autorecover-environment-options-dialog-box"></a>Caixa de diálogo AutoRecuperação, Ambiente, Opções

Use essa página da caixa de diálogo **Opções** para especificar se o backup automático dos arquivos deve ser feito ou não. Especifique também se deseja restaurar os arquivos modificados caso o Visual Studio seja desligado inesperadamente.

Para acessar essa caixa de diálogo, acesse **ferramentas**  >  **Opções**  >  **ambiente** de  >  **recuperação automática**.

:::image type="content" source="media/autorecover-options.png" alt-text="Captura de tela da seção AutoRecuperação na caixa de diálogo opções":::

**Salvar informações de AutoRecuperação a cada [n] minutos**

::: moniker range=">=vs-2022"

Use esta opção para personalizar a frequência com que um arquivo é salvo automaticamente no editor. Para arquivos salvos anteriormente, o Visual Studio salva uma cópia do arquivo em ***%LocalAppData%\Microsoft\VisualStudio\BackupFiles \\ [ProjectName]***. Se o arquivo for novo e você ainda não o tiver salvo, o Visual Studio o salvará automaticamente usando um nome de arquivo gerado aleatoriamente.

::: moniker-end

::: moniker range="vs-2019"

Use esta opção para personalizar a frequência com que um arquivo é salvo automaticamente no editor. Para arquivos salvos anteriormente, o Visual Studio 2019 versão 16,2 e posterior salva uma cópia do arquivo em ***%LocalAppData%\Microsoft\VisualStudio\BackupFiles \\ [ProjectName]***. Se o arquivo for novo e você ainda não o tiver salvo, o Visual Studio o salvará automaticamente usando um nome de arquivo gerado aleatoriamente.

> [!NOTE]
> Se você estiver usando o Visual Studio 2019 versão 16,1 ou anterior, o local do arquivo será *%USERPROFILE%\Documents\Visual Studio [Version] \backup files \\ [ProjectName]*. Para obter mais informações, consulte a página [histórico das notas de versão do Visual Studio 2019](/visualstudio/releases/2019/release-notes-history/) .

::: moniker-end

::: moniker range="vs-2017"

Use esta opção para personalizar a frequência com que um arquivo é salvo automaticamente no editor. Para arquivos salvos anteriormente, o Visual Studio 2017 salva uma cópia do arquivo no *%USERPROFILE%\Documents\Visual Studio [Version] \backup files \\ [ProjectName]*. Se o arquivo for novo e você ainda não o tiver salvo, o Visual Studio o salvará automaticamente usando um nome de arquivo gerado aleatoriamente.

::: moniker-end

**Manter informações de AutoRecuperação por [n] dias**

Use esta opção para especificar por quanto tempo o Visual Studio manterá arquivos criados para AutoRecuperação.

### <a name="see-also"></a>Confira também

- [caixa de diálogo Opções](../../ide/reference/options-dialog-box-visual-studio.md)

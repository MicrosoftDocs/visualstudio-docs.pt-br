---
title: AutoRecover, Caixa de diálogo Opções, Ambiente
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
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
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 804ea0baa47925e35a282a615598ea66c843b911
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388790"
---
# <a name="autorecover-environment-options-dialog-box"></a>Caixa de diálogo AutoRecuperação, Ambiente, Opções

Use essa página da caixa de diálogo **Opções** para especificar se o backup automático dos arquivos deve ser feito ou não. Especifique também se deseja restaurar os arquivos modificados caso o Visual Studio seja desligado inesperadamente.

Acesse essa caixa de diálogo selecionando o menu **Ferramentas**, escolhendo **Opções** e, em seguida, clicando em **Ambiente** > **AutoRecuperação**. Se essa página não aparecer na lista, selecione **Mostrar todas as configurações** na caixa de diálogo **Opções**.

**Salvar informações de AutoRecuperação a cada [n] minutos**

Use esta opção para personalizar a frequência com que um arquivo é salvo automaticamente no editor. Para arquivos já salvos, uma cópia do arquivo é salva em *%USERPROFILE%\Documents\Visual Studio\\[versão]\Backup Files\\[nomedoprojeto]*. Se o arquivo for novo e você ainda não o tiver salvado, ele será salvo automaticamente com um nome de arquivo gerado aleatoriamente.

**Manter informações de AutoRecuperação por [n] dias**

Use esta opção para especificar por quanto tempo o Visual Studio manterá arquivos criados para AutoRecuperação.

### <a name="see-also"></a>Consulte também

- [Caixa de diálogo de opções](../../ide/reference/options-dialog-box-visual-studio.md)
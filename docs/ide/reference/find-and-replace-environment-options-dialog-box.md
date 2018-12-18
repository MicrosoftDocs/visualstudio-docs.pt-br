---
title: Caixa de diálogo Localizar e Substituir, Ambiente, Opções
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.FindReplace
- VS.ToolsOptionsPages.Environment.FindandReplace
helpviewer_keywords:
- Find and Replace, Options dialog box
- Find and Replace, customizing
ms.assetid: f804d6d5-6309-46e4-8294-b83e880b5ec9
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7481f7d374d3958245cc7d506b0e0cccf1b5dbcb
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389196"
---
# <a name="find-and-replace-environment-options-dialog-box"></a>Caixa de diálogo Localizar e Substituir, Ambiente, Opções

Use esta página da caixa de diálogo **Opções** para controlar caixas de mensagem e outros aspectos de uma operação de localizar e substituir. Você pode acessar essa caixa de diálogo no menu **Ferramentas**, clicando em **Opções**, expandindo **Ambiente** e, em seguida, clicando em **Localizar e Substituir**. Se essa página não aparecer na lista, selecione **Mostrar todas as configurações** na caixa de diálogo **Opções**.

## <a name="uielement-list"></a>Lista UIElement

**Exibir mensagens informativas**

Selecione esta opção para exibir todas as mensagens informativas de Localizar e Substituir que têm a opção **Sempre mostrar esta mensagem**. Por exemplo, se você tiver optado por não exibir a mensagem "A localização atingiu o ponto inicial da pesquisa.", selecionar essa opção faria com que essa mensagem informativa aparecesse novamente quando você usasse Localizar e Substituir.

Se não quiser ver nenhuma mensagem informativa para Localizar e Substituir, desmarque essa opção.

Quando você desmarcar a opção **Sempre mostrar esta mensagem** em algumas, mas não em todas as mensagens informativas de **Localizar e Substituir**, a caixa de seleção **Exibir mensagens informativas** parecerá estar preenchida, mas não selecionada. Para restaurar todas as mensagens opcionais de **Localizar e Substituir**, desmarque essa opção e selecione-a novamente.

> [!NOTE]
> Essa opção não afeta nenhuma mensagem informativa de **Localizar e Substituir** que não exibe a opção **Sempre mostrar esta mensagem**.

**Exibir mensagens de aviso**

Selecione esta opção para exibir todas as mensagens de aviso de Localizar e Substituir que têm a opção **Sempre mostrar esta mensagem**. Por exemplo, se você optar por não exibir a mensagem de aviso de **Substituir tudo** que aparece quando você tenta fazer substituições em arquivos que não estão abertos para edição, selecionar esta opção faria com que a mensagem de aviso aparecesse novamente quando você tentasse substituir tudo.

Se não quiser ver nenhuma mensagem de aviso para Localizar e Substituir, desmarque essa opção.

Quando você desmarcar a opção **Sempre mostrar esta mensagem** em algumas, mas não em todas as mensagens de aviso de **Localizar e Substituir**, a caixa de seleção **Exibir mensagens de aviso** parecerá estar preenchida, mas não selecionada. Para restaurar todas as mensagens opcionais de **Localizar e Substituir**, desmarque essa opção e selecione-a novamente.

> [!NOTE]
> Essa opção não afeta nenhuma mensagem de aviso de **Localizar e Substituir** que não exibe a opção **Sempre mostrar esta mensagem**.

**Preencher automaticamente a opção Localizar no editor**

Selecione esta opção para colar o texto de um dos lados do ponto de inserção atual do editor no campo **Localizar** quando você selecionar qualquer modo de exibição da janela **Localizar e Substituir** no menu **Editar**. Desmarque esta opção para usar o último padrão de pesquisa da pesquisa anterior como a cadeia de caracteres para **Localizar**.

## <a name="see-also"></a>Consulte também

- [Localizando e substituindo texto](../../ide/finding-and-replacing-text.md)
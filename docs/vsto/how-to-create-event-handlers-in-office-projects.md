---
title: 'Como: criar manipuladores de eventos em projetos do Office'
description: Saiba mais sobre as várias maneiras que você pode criar manipuladores de eventos padrão para controles em Visual Basic e C#.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Basic [Office development in Visual Studio], event handlers
- event handlers [Office development in Visual Studio]
- Visual C# [Office development in Visual Studio], event handlers
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b2aed6102b6aed5938ecfab826363e62dcfac48a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889415"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>Como: criar manipuladores de eventos em projetos do Office
  Há várias maneiras de criar manipuladores de eventos em Visual Basic e C#. No modo Design, você pode criar os manipuladores de eventos padrão para controles clicando duas vezes no controle ou usando o painel eventos da janela **Propriedades** para criar manipuladores para qualquer evento no controle. No entanto, se você estiver no modo de exibição de código, talvez não queira alternar para modo de exibição de Design para criar um manipulador de eventos.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>Para criar um manipulador de eventos no Visual Basic

1. Na lista suspensa **nome da classe** na parte superior do editor de código, selecione o objeto para o qual você deseja criar um manipulador de eventos.

    > [!NOTE]
    > Se você quiser criar manipuladores de eventos para `ThisDocument` o ou `ThisWorkbook` , deverá selecionar **(eventos ThisDocument)** ou **(eventos ThisWorkbook)** na lista suspensa **nome da classe**

2. Na lista suspensa **nome do método** na parte superior do editor de código, selecione o evento.

     O Visual Studio cria o manipulador de eventos e move o ponto de inserção para o manipulador de eventos recém-criado. Se o manipulador de eventos já existir, o ponto de inserção será movido para o manipulador de eventos existente.

### <a name="to-create-an-event-handler-in-c"></a>Para criar um manipulador de eventos em C\#

1. Crie o delegado de evento no evento **Startup** da classe digitando o nome do evento qualificado seguido por um espaço e, em seguida, digitando **+=** sem espaço depois. Por exemplo:

     `this.<object name>.<event name> +=`

2. No final da linha de código, pressione a tecla TAB duas vezes.

     O Visual Studio conclui automaticamente a linha de código, cria o manipulador de eventos e move o ponto de inserção para o manipulador de eventos recém-criado.

## <a name="see-also"></a>Confira também
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
- [Walkthrough: programa em relação a eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)

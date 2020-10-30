---
title: Converter entre literais de cadeia de caracteres regulares e textuais
ms.custom: SEO-VS-2020
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: f411c0ac56adeb30370cbfc6f0f908ffd25bed05
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93045909"
---
# <a name="convert-between-regular-string-and-verbatim-string-literals-refactoring"></a>Converter entre cadeia de caracteres regular e refatoração de literais de cadeia de caracteres textual

Esta refatoração aplica-se a:

- C#

**O que:** Permite converter entre cadeias de caracteres regulares e literais de cadeia de caracteres textuais.

**Quando:** Você quer economizar espaço ou fornecer mais clareza em seu código.

**Por que:** Converter um literal de cadeia de caracteres textual em um literal de cadeia de caracteres regular pode ajudar a economizar espaço. Converter um literal de cadeia de caracteres regular em um literal de cadeia de caracteres textual pode fornecer mais clareza.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor sobre a cadeia de caracteres regular ou literal de cadeia de caracteres textual:

2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas** .

3. Selecione uma das seguintes opções:

    Selecione **Converter em cadeia de caracteres regular** .

    ![Converter em cadeia de caracteres regular](media/convert-to-regular-string.png)

    Selecione **Converter em cadeia de caracteres verbatim** .

    ![Converter em cadeia de caracteres textual](media/convert-to-verbatim-string.png)

## <a name="see-also"></a>Veja também

- [Refatoração](../refactoring-in-visual-studio.md)
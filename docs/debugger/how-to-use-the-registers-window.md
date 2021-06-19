---
title: Exibir valores de registro no | Microsoft Docs
description: Exibir valores de registro na janela Registros no Visual Studio. Durante a depuração, os valores de registro mudam conforme o código é executado em seu aplicativo.
ms.custom: SEO-VS-2020
ms.date: 11/19/2018
ms.topic: how-to
f1_keywords:
- vs.debug.registers
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- registers, debugging
- register contents
- flags, Registers window
- register groups
- debugging [Visual Studio], Registers window
- Registers window
ms.assetid: 2918ffa2-562f-40d6-9053-ef321bbeb767
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e2648f74453f51cd8d655ccb0c2344eb1030c1ed
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385390"
---
# <a name="view-register-values-in-the-registers-window-c-c-visual-basic-f"></a>Exibir valores de registro na janela Registros (C#, C++, Visual Basic, F#)

A **janela Registros** exibe o conteúdo do registro durante Visual Studio depuração. Para obter uma introdução aos conceitos por trás de registros de alto nível e o **registra** janela, consulte [Noções básicas de depuração: janela Registros](../debugger/debugging-basics-registers-window.md).

> [!NOTE]
> As informações de registro não estão disponíveis para scripts ou aplicativos SQL.

Durante a depuração, os valores de registro mudam conforme o código é executado em seu aplicativo. Os valores que foram alterados recentemente aparecem em vermelho na **janela Registros.**

Para reduzir a desordem, a janela **Registros** organiza registros em grupos, que variam de acordo com a plataforma e o tipo de processador. Você pode exibir ou ocultar grupos de registro. Para obter mais informações, confira [Como exibir e ocultar grupos de registros](../debugger/how-to-display-and-hide-register-groups.md).

Para obter informações sobre os sinalizadores que você vê na janela **Registros,** consulte [Sobre a janela Registros](../debugger/debugging-basics-registers-window.md)

Você pode editar valores do registro. Para obter mais informações, [consulte Como editar um valor de registro](../debugger/how-to-edit-a-register-value.md).

**Para abrir a janela Registros**

1. Habilita a depuração no nível do endereço selecionando Habilitar depuração no nível do endereço em **Ferramentas** (ou **Depurar** ) > **Opções** de   >  **Depuração .**

1. Enquanto a depuração estiver em execução ou em um ponto de interrupção, selecione **Depurar**  >  **Registros** do Windows  >  ou pressione **Alt** + **5.**

>[!NOTE]
>Caixas de diálogo e comandos de menu podem ser diferentes dependendo de sua Visual Studio edição ou configurações. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu Visual Studio **Ferramentas.** Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

### <a name="see-also"></a>Confira também

- [Noções básicas de depuração: janela Registros](../debugger/debugging-basics-registers-window.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)

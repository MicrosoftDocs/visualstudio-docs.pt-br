---
title: Exibir valores de registro no depurador | Microsoft Docs
description: Exiba os valores de registro na janela de registros no Visual Studio. Durante a depuração, os valores de registro mudam conforme o código é executado em seu aplicativo.
ms.custom: SEO-VS-2020, seodec18
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
ms.openlocfilehash: ea0275a5186b58c9b9a07934b95351b597a816f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99845003"
---
# <a name="view-register-values-in-the-registers-window-c-c-visual-basic-f"></a>Exibir valores de registro na janela de registros (C#, C++, Visual Basic, F #)

A janela de **registros** exibe o conteúdo do registro durante a depuração do Visual Studio. Para obter uma introdução aos conceitos por trás de registros de alto nível e o **registra** janela, consulte [Noções básicas de depuração: janela Registros](../debugger/debugging-basics-registers-window.md).

> [!NOTE]
> Informações de registro não estão disponíveis para scripts ou aplicativos SQL.

Durante a depuração, os valores de registro mudam conforme o código é executado em seu aplicativo. Os valores que foram alterados recentemente aparecem em vermelho na janela de **registros** .

Para reduzir a desordem, a janela **Registros** organiza registros em grupos, que variam de acordo com a plataforma e o tipo de processador. Você pode exibir ou ocultar grupos de registros. Para obter mais informações, confira [Como exibir e ocultar grupos de registros](../debugger/how-to-display-and-hide-register-groups.md).

Para obter informações sobre os sinalizadores que você vê na janela de **registros** , consulte [sobre a janela de registros](../debugger/debugging-basics-registers-window.md)

Você pode editar valores do registro. Para obter mais informações, consulte [como: editar um valor de registro](../debugger/how-to-edit-a-register-value.md).

**Para abrir a janela de registros**

1. Habilite a depuração no nível de endereço selecionando **Habilitar depuração no nível de endereço** em **ferramentas** (ou **depurar**) > depuração de **Opções**  >  .

1. Enquanto a depuração estiver em execução ou em um ponto de interrupção, selecione **depurar**  >    >  **registros** do Windows ou pressione **ALT** + **5**.

>[!NOTE]
>Caixas de diálogo e comandos de menu podem diferir dependendo da edição ou das configurações do Visual Studio. Para alterar as configurações, selecione **importar e exportar configurações** no menu **ferramentas** do Visual Studio. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

### <a name="see-also"></a>Confira também

- [Noções básicas de depuração: janela de registros](../debugger/debugging-basics-registers-window.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)

---
title: Como exibir e ocultar grupos de registros | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.registergroups
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Registers window, displaying and hiding register groups
- register groups, displaying and hiding
ms.assetid: 6be5dfb4-4cfe-4daf-b538-60405640857d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f08e31f67f9626c15dee0b6b4b8202a0370c976b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349894"
---
# <a name="how-to-display-and-hide-register-groups-c-c-visual-basic-f"></a>Como exibir e ocultar grupos de registros (C#, C++, Visual Basic, F #)

A janela **Registros** estará disponível apenas se a depuração do nível de endereços estiver habilitada na caixa de diálogo **Opções**, nó **Depuração**, categoria **Geral**.

Para reduzir a confusão, a janela **Registros** organiza os registros em grupos. Se você clicar com o botão direito do mouse na janela **Registros**, verá um menu de atalho contendo esses grupos, que você poderá exibir ou ocultar como achar melhor seguindo o procedimento abaixo.

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** . Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

## <a name="display-or-hide-register-groups"></a>Exibir ou ocultar grupos de registros

1. Clique com o botão direito do mouse na janela **Registros**.

2. No menu de atalho, selecione os grupos de registro que você deseja mostrar ou ocultar.

     Os grupos de registro que não têm suporte pelo hardware no qual você está depurando estão desabilitados no menu de atalho, e não podem ser selecionados.

## <a name="see-also"></a>Veja também

- [Como usar a janela Registros](../debugger/how-to-use-the-registers-window.md)
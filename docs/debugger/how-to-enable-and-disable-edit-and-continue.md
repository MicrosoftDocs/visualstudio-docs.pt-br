---
title: Como habilitar e desabilitar editar e continuar | Microsoft Docs
ms.custom: seodec18
ms.date: 10/04/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 1907a67412a787148da7a6679e173383e2bb7423
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349660"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>Como habilitar e desabilitar editar e continuar (C#, VB, C++)

Você pode desabilitar ou habilitar **Editar e continuar** na caixa de diálogo **Opções** do Visual Studio em tempo de design. **Editar e continuar** funciona somente em compilações de depuração. Para obter mais informações, confira [Editar e Continuar](../debugger/edit-and-continue.md).

Para C++ nativo, **Editar e continuar** requer o uso da `/INCREMENTAL` opção. Para obter mais informações sobre os requisitos de recursos em C++, consulte esta [postagem de blog](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/) e [Editar e continuar (C++)](../debugger/edit-and-continue-visual-cpp.md).

**Para habilitar ou desabilitar editar e continuar:**

1. Se você estiver em uma sessão de depuração, pare a depuração (**depurar**  >  **parar depuração** ou **Shift** + **F5**).

1. Em **ferramentas**  >  **Opções** > (ou **Debug**  >  **Opções**de depuração) > **depuração**  >  **geral**, selecione **Editar e continuar** no painel direito.

    > [!NOTE]
    > Se IntelliTrace estiver habilitado e você coletar eventos de IntelliTrace e informações de chamada, Editar e Continuar estará desabilitado. Para obter mais informações, consulte [IntelliTrace](../debugger/intellitrace.md).

1. Para código C++, verifique se **Habilitar edição nativa e continuar** está selecionado e defina as opções adicionais:
    - **Aplicar alterações ao continuar (somente nativo)**

      Se selecionado, o Visual Studio compila automaticamente e aplica alterações de código quando você continua a depuração de um estado de interrupção. Caso contrário, você pode optar por aplicar alterações usando **depurar**  >  **aplicar alterações de código**.

    - **Avisar sobre o código obsoleto (somente nativo)**

      Se selecionado, fornecerá avisos sobre o código obsoleto.

1. Clique em **OK**.

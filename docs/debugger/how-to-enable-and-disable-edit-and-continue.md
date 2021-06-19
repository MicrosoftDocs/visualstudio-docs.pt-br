---
title: Habilitar e desabilitar Editar e Continuar | Microsoft Docs
description: Saiba como desabilitar e habilitar Editar e Continuar em Visual Studio opções em tempo de design. Editar e Continuar só funciona em compilações de depuração.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 261963cbc1aee63374d6a9c147f42678208c39ec
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384701"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>Como habilitar e desabilitar Editar e Continuar (C#, VB, C++)

Você pode desabilitar ou **habilitar Editar e Continuar** na caixa de diálogo Visual Studio **Opções** em tempo de design. **Editar e Continuar** só funciona em builds de depuração. Para obter mais informações, confira [Editar e Continuar](../debugger/edit-and-continue.md).

Para O C++nativo, **Editar e Continuar** requer o uso da opção `/INCREMENTAL` . Para obter mais informações sobre os requisitos de recursos no C++, consulte esta [postagem no blog](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/) [e Editar e continuar (C++)](../debugger/edit-and-continue-visual-cpp.md).

**Para habilitar ou desabilitar Editar e Continuar:**

1. Se você estiver em uma sessão de depuração, pare a depuração (**Depurar**  >  **Parar Depuração** ou **Shift** + **F5**).

1. Em **Opções**  >  **de Ferramentas** > (ou Opções de **Depuração**) > Geral de  >   **Depuração,** selecione Editar e  >  Continuar no painel direito. 

    > [!NOTE]
    > Se IntelliTrace estiver habilitado e você coletar eventos de IntelliTrace e informações de chamada, Editar e Continuar estará desabilitado. Para obter mais informações, consulte [IntelliTrace](../debugger/intellitrace.md).

1. Para código C++, certifique-se de **habilitar Edição Nativa** e Continuar está selecionado e de definir as opções adicionais:
    - **Aplicar alterações em continuar (somente nativo)**

      Se selecionado, Visual Studio compila e aplica automaticamente as alterações de código quando você continua a depuração de um estado de quebra. Caso contrário, você pode optar por aplicar alterações usando **Depurar**  >  **Aplicar Alterações de Código**.

    - **Avisar sobre código stale (somente nativo)**

      Se selecionado, fornece avisos sobre código desaplicável.

1. Clique em **OK**.

---
title: Obsoleto de caixa de diálogo de aviso de código | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.stalecode
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Stale Code Warning dialog box
- code, stale code warning
- warnings, Stale Code Warning dialog box
- Edit and Continue, stale code
ms.assetid: 594b894c-e652-4e13-a980-9909473d5712
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f1e212602b317127cfd14adcd246a23cdd92ed86
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44281787"
---
# <a name="stale-code-warning-dialog-box"></a>Caixa de diálogo Aviso de Código Obsoleto
Essa caixa de diálogo aparece quando você tiver feito alterações no código nativo que **editar e continuar** não pôde aplicar imediatamente. Como resultado, alguns códigos nativos no quadro de pilhas atual agora está expirado, ou seja, obsoleto. Para obter mais informações, consulte [como: trabalhar com código obsoleto](/visualstudio/debugger/edit-and-continue-visual-cpp#bkmk_how_to_work_with_stale_code).  
  
 **Não mostrar esta caixa de diálogo novamente**  
 Se você marcar essa caixa de seleção, Editar e Continuar aplicará as alterações de código sem solicitar permissão no futuro. Você pode ativar esse aviso novamente indo para o **opções** caixa de diálogo, abrindo o **depuração** pasta, clicando no **editar e continuar** da página e selecionando **Avisar sobre código obsoleto**.  
  
## <a name="see-also"></a>Consulte também  
 [Alterações de código suportadas (C++)](../debugger/supported-code-changes-cpp.md)   
 [Caixa de diálogo Editar e Continuar, Depuração, Opções](/visualstudio/debugger/edit-and-continue)
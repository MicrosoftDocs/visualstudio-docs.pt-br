---
title: Caixa de diálogo Selecionar tipo de código | Microsoft Docs
ms.date: 06/12/2020
ms.topic: reference
f1_keywords:
- vs.debug.selectengines
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- debugging [Visual Studio], engine selection
- debugger, engine selection
- debugging engine selection dialog box
no-loc:
- Blazor WebAssembly
ms.assetid: 932269fe-94e3-43cb-8931-078f31afd177
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ccfe636cd8981c2f9dcc1375fb795d6c026b572
ms.sourcegitcommit: 5e82a428795749c594f71300ab03a935dc1d523b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211572"
---
# <a name="select-code-type-dialog-box"></a>Caixa de diálogo Selecionar Tipo de Código

Para abrir essa caixa de diálogo, abra a caixa de diálogo **Anexar ao Processo** e clique no botão **Selecionar**.

**Determinar automaticamente o tipo de código a ser depurado** O depurador apropriado será selecionado com base no tipo de código que está em execução.

**Depurar esses tipos de código:** Na lista fornecida, escolha os tipos de código que você deseja depurar. Isso pode ser útil ao [solucionar problemas de uma falha ao anexar](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md#BKMK_Troubleshoot_attach_errors). Essa opção restringe a detecção para apenas os tipos de código que você deseja depurar.

   ::: moniker range=">=vs-2019"
   - Blazor WebAssembly-Lado do clienteBlazor WebAssembly
   - GPU-emulador de software-código C++ em execução em um emulador de software de GPU
   - JavaScript (Chrome)-JavaScript em execução no Chrome
   - JavaScript (Microsoft Edge-Chromium)-JavaScript em execução no Microsoft Edge baseado em Chromium para Windows 10
   - Depurador de CDP do JavaScript (v3)-Chrome DevTools Protocol versão 3, usado para depuração em um cliente de CDP
   - Gerenciado (CoreCLR)-.NET Core
   - Gerenciado (compilação nativa)-código do C++/CLR
   - Gerenciado (v 3.5, v 3.0, v 2.0)-código de .NET Framework para .NET Framework 2,0 e superior (até 3,5)
   - Gerenciado (v. 4.6, v 4.5, v 4.0)-código de .NET Framework para .NET Framework 4,0 e superior
   - Nativo-C/C++
   - Node.js depuração – código hospedado pelo Node.js Runtime
   - Python-python 
   - Script – especifica o depurador de script geral para JavaScript. Use opções mais restritivas se elas se aplicarem ao seu cenário, como o JavaScript (Chrome).
   - T-SQL-Transact-SQL
   - Unity-Unity
   - Modo de compatibilidade gerenciado – especifica o depurador herdado para código gerenciado, para uso normalmente na depuração de modo misto com o código C++/CLR (permite editar e continuar para o modo misto) ou para dar suporte a extensões que direcionam o depurador herdado. Na maioria dos cenários de depuração de modo misto, selecione **nativo** e os tipos de código **gerenciado** apropriados em vez do modo de compatibilidade gerenciado.
   ::: moniker-end

   Para a maioria dos cenários, não há suporte para a anexação de vários depuradores na mesma sessão de depuração. Você pode fazer isso usando uma segunda instância do Visual Studio.

## <a name="see-also"></a>Confira também
- [Segurança do depurador](../debugger/debugger-security.md)
- [Anexar aos processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)

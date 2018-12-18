---
title: Editar e continuar a caixa de diálogo de mensagem de erro | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.ENC.SupportedButNotAvaiable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ba573a6b6bffdfeebf37c5f46f1f774d699a1131
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388695"
---
# <a name="edit-and-continue-error-message"></a>Editar e continuar a mensagem de erro 

O **editar e continuar** caixa de mensagem de erro aparece quando você estiver depurando em uma linguagem de código que dá suporte a editar e continuar, mas editar e continuar não está disponível para as alterações de código que você fez. A mensagem de erro fornece uma explicação mais detalhada. Para responder à caixa de diálogo, selecione **Okey** para fechar a caixa de diálogo e cancelar a tentativa de editar.  

As possíveis razões para essa mensagem de erro incluem:  

-   Tentativa de editar o código do SQL Server.
-   Tentativa de editar o código otimizado. Talvez você precise alternar de um build de versão para um build de depuração.
-   Tentativa de editar o código enquanto ele está em execução, em vez de enquanto está em pausa no depurador. Tente [definindo um ponto de interrupção](../debugger/using-breakpoints.md)e a edição do código enquanto está em pausa.
-   Tentativa de editar o código gerenciado quando a depuração não gerenciada só está habilitada. Editar e continuar não funciona com [depuração de modo misto](../debugger/how-to-debug-in-mixed-mode.md).
-   Fazer com que um código de alteração que não há suporte para editar e continuar em sua linguagem de programação. Para obter mais informações, consulte os artigos [suporte para alterações de código em C# ](supported-code-changes-csharp.md), [sem suporte a edições no Visual Basic Edit and Continue](unsupported-edits-in-visual-basic-edit-and-continue.md), e [suporte para alterações de código C++](supported-code-changes-cpp.md).
-   Tentativa de editar o código em um aplicativo que você estiver associada, em vez de iniciar a depuração a partir de **depurar** menu.  
-   Tentativa de editar o código durante a depuração de uma recuperação de desastre. Watson.  
-   Tentativa de editar o código após uma exceção não tratada ocorre e a opção **desenrolar a pilha de chamadas em exceções não tratadas** não estiver selecionada.  
-   Tentando editar código durante a depuração de um aplicativo de tempo de execução incorporado.
-   Tentativa de editar o código gerenciado usando uma versão do .NET Framework anteriores à 4.5.1 com um destino de aplicativo de 64 bits. Para usar Editar e continuar para o .NET Framework anteriores à 4.5.1, defina o destino como **x86** na  **\<ProjectName >** > **propriedades**  >  **Compile** guia **avançado compilador** configuração.  
-   Tentativa de editar o código em um assembly que foi modificado durante a depuração e foi recarregado.  
-   Tentativa de editar o código em um assembly que não foi carregado.  
-   Começar a depurar uma versão antiga de um aplicativo, porque a versão mais recente tem erros de compilação.
  
Para obter mais informações, consulte:
- [Postagem de C++ Edit e Continue blog](https://blogs.msdn.microsoft.com/vcblog/2016/07/01/c-edit-and-continue-in-visual-studio-2015-update-3/)  
- [Alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md)
- [Editar e continuar](../debugger/edit-and-continue.md)
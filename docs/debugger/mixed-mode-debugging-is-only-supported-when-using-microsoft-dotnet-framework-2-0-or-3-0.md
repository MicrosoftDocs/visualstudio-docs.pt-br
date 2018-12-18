---
title: Depuração de modo misto é suportado apenas quando o Microsoft .NET Framework 2.0 ou 3.0 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_to_old
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: f607af6f-57fe-472a-a32e-b6202067aa96
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 9d51a0ca72840b20e23eaaa9db3a82382a3fa012
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44284062"
---
# <a name="mixed-mode-debugging-is-only-supported-when-using-microsoft-net-framework-20-or-30"></a>A depuração de modo misto só é suportada quando o Microsoft .NET Framework 2.0 ou 3.0 é usado
As versões do Microsoft .NET Framework anteriores à versão 2.0 não fornecem suporte à depuração de modo misto de processos de 64 bits. Isso significa que, durante a depuração, você não pode depurar de código gerenciado para código nativo e vice-versa.  
  
 Para resolver esse problema, você pode:  
  
-   Atualize seu projeto para usar o Microsoft .NET Framework 2.0 ou 3.0.  
  
-   Depure seu código gerenciado e nativo em sessões separadas de depuração.  
  
-   Depure seu código misto como um processo de 32 bits, como descrito nos procedimentos a seguir.  
  
### <a name="to-change-the-operating-system-to-32-bit-visual-basic-or-c"></a>Para alterar o sistema operacional para 32 bits (Visual Basic ou C#)  
  
1.  Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **propriedades** no menu de atalho.  
  
2.  Nas páginas de propriedade, clique o **Compile** ou **depurar** guia.  
  
3.  Clique em **plataforma**e, em seguida, selecione **x86** da lista de plataformas.  
  
     Por padrão, os compiladores do Visual Basic e do C# produzem código para ser executado em qualquer CPU. Em um computador de 64 bits, esses binários são executados como processos de 64 bits. Para executar em um processo de 32 bits, você deve escolher **Win32**, e não **AnyCPU**.  
  
### <a name="to-change-the-operating-system-to-32-bit-cc"></a>Para alterar o sistema operacional para 32 bits (C/C++)  
  
1.  Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **propriedades** no menu de atalho.  
  
     Nas páginas de propriedades, clique em **plataforma**e, em seguida, selecione **Win32** da lista de plataformas.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Ver [Configurando a depuração SQL](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100)).  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos de 64 bits](../debugger/debug-64-bit-applications.md)
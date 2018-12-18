---
title: Especifique uma versão do .NET Framework para depuração | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- .NET Framework, specifying version for debugging
- debugging [Visual Studio], specifying .NET Framework version
ms.assetid: 7a4893ba-4620-4774-893f-378d4ca28893
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 86289c9a93a0bb9e0f7756443d79f4a1a6dd38a6
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056002"
---
# <a name="how-to-specify-a-net-framework-version-for-debugging-c-visual-basic-f"></a>Como: Especificar uma versão do .NET Framework para depuração (C#, Visual Basic, F#)

O depurador do Visual Studio dá suporte à depuração de versões mais antigas do Microsoft [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] , bem como a versão atual. Se você iniciar um aplicativo do Visual Studio, o depurador sempre poderá identificar a versão correta do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] para o aplicativo que você está depurando. No entanto, se o aplicativo já está em execução e você iniciar a depuração usando **anexar**, o depurador pode não ser capaz de identificar uma versão anterior da [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. Se isso ocorrer, você receberá uma mensagem de erro, que indica  

``` cmd 
The debugger has made an incorrect assumption about the [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] version your application is going to use.  
```

Nos raros casos em que esse erro aparecer, você pode definir uma chave do registro para indicar ao depurador a qual versão usar.  
  
### <a name="to-specify-a-net-framework-version-for-debugging"></a>Para especificar uma versão do .NET Framework para depuração  
  
1. Examine no diretório Windows\Microsoft.NET\Framework para localizar as versões do .NET Framework instaladas no computador. Os números de versão devem ser semelhantes a:  
  
    `V1.1.4322`  
  
    Identifique o número de versão correta e anote.  
  
2. Inicie o **Editor do Registro** (regedit).  
  
3. Em **Editor do Registro**, abra a pasta HKEY_LOCAL_MACHINE.  
  
4. Navegar Para. HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449EC4CC-30D2-4032-9256-EE18EB41B62B}  
  
    Se a chave não existir, clique com o botão direito do mouse em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine e clique em **Nova Chave**. Nomeie a nova chave `{449EC4CC-30D2-4032-9256-EE18EB41B62B}`.  
  
5. Depois de navegar até {449EC4CC-30D2-4032-9256-EE18EB41B62B}, examine a coluna **Nome** e localize a chave CLRVersionForDebugging.  
  
   1.  Se a chave não existir, clique com o botão direito do mouse em {449EC4CC-30D2-4032-9256-EE18EB41B62B} e clique em **Novo Valor de Cadeia de Caracteres**. Clique com o novo valor de cadeia de caracteres, clique em **renomeie**e o tipo `CLRVersionForDebugging`.  
  
6. Clique duas vezes em **CLRVersionForDebugging**.  
  
7. Na caixa **Editar Cadeia de Caracteres**, digite o número de versão do .NET Framework na caixa **Valor**. Por exemplo: V1.1.4322  
  
8. Clique em **OK**.  
  
9. Feche o **Editor de Registro**.  
  
     Se você ainda receber uma mensagem de erro quando começar a depuração, verifique se inseriu o número de versão corretamente no Registro. Além disso, verifique se está usando uma versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] com suporte pelo Visual Studio. O depurador é compatível com a versão atual e a anterior do .NET Framework, mas não é compatível com versões futuras.  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)
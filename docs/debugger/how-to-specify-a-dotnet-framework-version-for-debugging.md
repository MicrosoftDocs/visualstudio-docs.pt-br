---
title: Especificar uma versão de .NET Framework para depuração | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 3ae48670fceb78ff85f395852f0a31414f37e8cf
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349062"
---
# <a name="specify-an-older-net-framework-version-for-debugging-c-visual-basic-f"></a>Especificar uma versão mais antiga do .NET Framework para depuração (C#, Visual Basic, F #)

O depurador do Visual Studio dá suporte à depuração de versões mais antigas do Microsoft .NET Framework, bem como à versão atual. Se você iniciar um aplicativo do Visual Studio, o depurador poderá sempre identificar a versão correta do .NET Framework para o aplicativo que você está depurando. No entanto, se o aplicativo já estiver em execução e você iniciar a depuração usando **Attach to**, o depurador poderá nem sempre ser capaz de identificar uma versão mais antiga do .NET Framework. Se isso ocorrer, você receberá uma mensagem de erro, que indica

``` cmd
The debugger has made an incorrect assumption about the .NET Framework version your application is going to use.
```

Nos casos raros em que esse erro aparece, você pode definir uma chave do registro para indicar ao depurador qual versão usar.

### <a name="to-specify-a-net-framework-version-for-debugging"></a>Para especificar uma versão do .NET Framework para depuração

1. Examine no diretório Windows\Microsoft.NET\Framework para localizar as versões do .NET Framework instaladas no computador. Os números de versão devem ser semelhantes a:

    `V1.1.4322`

    Identifique o número de versão correta e anote.

2. Inicie o **Editor do Registro** (regedit).

3. Em **Editor do Registro**, abra a pasta HKEY_LOCAL_MACHINE.

4. Navegue até: HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449EC4CC-30D2-4032-9256-EE18EB41B62B}

    Se a chave não existir, clique com o botão direito do mouse em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine e clique em **Nova Chave**. Nomeie a nova chave `{449EC4CC-30D2-4032-9256-EE18EB41B62B}` .

5. Depois de navegar até {449EC4CC-30D2-4032-9256-EE18EB41B62B}, examine a coluna **Nome** e localize a chave CLRVersionForDebugging.

   1. Se a chave não existir, clique com o botão direito do mouse em {449EC4CC-30D2-4032-9256-EE18EB41B62B} e clique em **Novo Valor de Cadeia de Caracteres**. Clique com o botão direito do mouse no novo valor de cadeia de caracteres, clique em **renomear**e digite `CLRVersionForDebugging` .

6. Clique duas vezes em **CLRVersionForDebugging**.

7. Na caixa **Editar Cadeia de Caracteres**, digite o número de versão do .NET Framework na caixa **Valor**. Por exemplo: V1.1.4322

8. Clique em **OK**.

9. Feche o **Editor do registro**.

     Se você ainda receber uma mensagem de erro quando começar a depuração, verifique se inseriu o número de versão corretamente no Registro. Verifique também se você está usando uma versão do .NET Framework com suporte pelo Visual Studio. O depurador é compatível com a versão atual e a anterior do .NET Framework, mas não é compatível com versões futuras.

## <a name="see-also"></a>Veja também
- [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)
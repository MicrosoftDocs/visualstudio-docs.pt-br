---
title: Erro-o servidor Web não está configurado corretamente | Microsoft Docs
ms.date: 09/20/2017
ms.topic: error-reference
f1_keywords:
- vs.debug.remote.projnotconfigured
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 711297ef00c064c482ed3a86b896566b6e019534
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460319"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>Erro: o servidor Web não foi configurado corretamente

Depois de executar as etapas detalhadas aqui para resolver o problema e antes de tentar depurar novamente, talvez você também precise redefinir o IIS. Você pode fazer isso abrindo um prompt de comando de administrador e digitando `iisreset` .

Siga estas etapas para resolver esse problema:

1. Se o aplicativo Web hospedado no servidor estiver configurado como uma compilação de versão, Republique-o como uma compilação de depuração e verifique se o arquivo de web.config contém `debug=true` no elemento Compilation. Redefina o IIS e tente novamente.

    Por exemplo, se você estiver usando um perfil de publicação para uma compilação de versão, altere-o para depurar e republicar. Caso contrário, o atributo de depuração será definido como `false` quando você publicar.

2. IIS Verifique se o caminho físico está correto. No IIS, você encontra essa configuração em **configurações básicas > caminho físico** (ou **Configurações avançadas** em versões anteriores do IIS).

    O caminho físico poderá estar incorreto se o aplicativo Web tiver sido copiado para um computador diferente, manualmente renomeado ou movido. Redefina o IIS e tente novamente.

3. Se você estiver Depurando localmente no Visual Studio, verifique se o servidor correto está selecionado nas propriedades. (Abra **propriedades > servidores ou propriedades de > da Web** **> depurar** , dependendo do tipo de projeto. Para um projeto Web Forms, abra **páginas de propriedades > opções de início > servidor**).

    Se você estiver usando um servidor externo (personalizado), como o IIS, a URL deverá estar correta. Caso contrário, selecione IIS Express e tente novamente.

4. IIS Verifique se a versão correta do ASP.NET está instalada no servidor.

    As versões incompatíveis do ASP.NET no IIS e no seu projeto do Visual Studio podem causar esse problema. Talvez seja necessário definir a versão do Framework no web.config. Para instalar o ASP.NET no IIS, use o [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx). Além disso, consulte [iis 8,0 usando ASP.NET 3,5 e ASP.NET 4,5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) ou, para ASP.NET Core, [host no Windows com IIS](https://docs.asp.net/en/latest/publishing/iis.html).

4. Se o `maxConnection` limite no IIS for muito baixo e você tiver muitas conexões, talvez seja necessário [aumentar o limite de conexão](/iis/configuration/system.applicationhost/sites/sitedefaults/limits).

## <a name="see-also"></a>Veja também
- [Depuração remota do ASP.NET em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
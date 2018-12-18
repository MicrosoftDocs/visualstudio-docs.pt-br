---
title: 'Erro: O servidor web não é configurado corretamente | Microsoft Docs'
ms.custom: ''
ms.date: 09/20/2017
ms.technology: vs-ide-debug
ms.topic: troubleshooting
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c9ff79148af491ee27aeae20b66b4d7b742bef6b
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31471847"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>Erro: o servidor Web não foi configurado corretamente

Depois de fazer as etapas descritas aqui para resolver o problema e antes de tentar novamente depurar, você talvez precise redefinir o IIS. Você pode fazer isso, abra um prompt de comando do administrador e digitando `iisreset`.

Siga estas etapas para resolver esse problema:

1. Se o aplicativo web hospedado no servidor está configurado como uma versão de compilação, republicar como uma compilação de depuração e verifique se o arquivo Web. config contém `debug=true` no elemento de compilação. Redefinir o IIS e tente novamente.

    Por exemplo, se você estiver usando um perfil de publicação para uma compilação de versão, alterá-la para depurar e publicar novamente. Caso contrário, o atributo de depuração será definido `false` quando você publica.

2. (IIS) Verifique se o caminho físico está correto. No IIS, você encontrar essa configuração em **configurações básicas > caminho físico** (ou **configurações avançadas** em versões anteriores do IIS).

    O caminho físico pode estar incorreto, se o aplicativo web foi copiado para um computador diferente, manualmente renomeado ou movido. Redefinir o IIS e tente novamente.

3. Se você estiver depurando localmente no Visual Studio, verifique se o servidor correto está selecionado nas propriedades. (Abra **Propriedades > Web > servidores** ou **Propriedades > Depurar** dependendo do tipo de projeto. Para um projeto de formulários da Web, abra **páginas de propriedade > Iniciar Opções > servidor**).

    Se você estiver usando um servidor externo (personalizado) como o IIS, a URL deve estar correta. Caso contrário, selecione o IIS Express e tente novamente.

4. (IIS) Certifique-se de que a versão correta do ASP.NET está instalada no servidor.

    Versões incompatíveis do ASP.NET no IIS e no projeto do Visual Studio podem causar esse problema. Talvez seja necessário definir a versão do framework no Web. config. Para instalar o ASP.NET no IIS, use o [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx). Além disso, consulte [IIS 8.0 usando ASP.NET 3.5 e o ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) ou, para o ASP.NET Core [Host no Windows com o IIS](https://docs.asp.net/en/latest/publishing/iis.html).
  
4. Se o `maxConnection` limite no IIS é muito baixo e você tem muitas conexões, talvez você precise [aumentar o limite de conexão](/iis/configuration/system.applicationhost/sites/sitedefaults/limits).
  
## <a name="see-also"></a>Consulte também  
 [ASP.NET em um computador remoto do IIS a depuração remota](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)   
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
---
title: Autorização de proxy necessária | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2d24ae1-9902-460e-b72a-0299eed9ee82
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 2650dadddefe3be18a4406eb4fd07c5599622212
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49259195"
---
# <a name="proxy-authorization-required"></a>Autorização de proxy necessária
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Esse erro geralmente ocorre quando usuários estão conectados ao Visual Studio Online por meio de um servidor proxy e este bloqueia as chamadas. O Visual Studio Online é usado para manter o usuário conectado ao IDE.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Reinicie o Visual Studio. Uma caixa de diálogo de autenticação de proxy deverá aparecer. Insira suas credenciais na caixa de diálogo.  
  
-   Se a etapa acima não resolver o problema, pode ser porque o servidor proxy não solicita credenciais para endereços http://go.microsoft.com, mas sim para endereços *.visualStudio.com. Para esses servidores, você precisa colocar os seguintes itens na lista de permissões para desbloquear todos os cenários de credenciais no Visual Studio:  
  
    -   *.windows.net  
  
    -   *.microsoftonline.com  
  
    -   *.visualstudio.com  
  
    -   *.microsoft.com  
  
    -   *.live.com  
  
-   Caso contrário, você pode remover o http://go.microsoft.com de endereços da lista de permissões para que a caixa de diálogo de autenticação de proxy apareça para ambos o http://go.microsoft.com endereço e os pontos de extremidade do servidor quando o Visual Studio for reiniciado.  
  
-   OU  
  
-   Se você quiser usar suas credenciais padrão com o proxy, poderá fazer o seguinte:  
  
    1.  Localize devenv.exe.config (o arquivo de configuração devenv.exe) em: **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** (ou **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**).  
  
    2.  No arquivo de configuração, localize o bloco `<system.net>` e adicione esse código:  
  
        ```xml  
        <defaultProxy enabled="true" useDefaultCredentials="true">  
            <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>  
        </defaultProxy>  
  
        ```  
  
         Você deve inserir o endereço de proxy correto para sua rede na `proxyaddress="<http://<yourproxy:port#>`.  
  
-   OU  
  
-   Você também pode seguir as instruções [nesta postagem](http://blogs.msdn.com/b/rido/archive/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy.aspx) para adicionar o código que permitirá o uso do proxy.




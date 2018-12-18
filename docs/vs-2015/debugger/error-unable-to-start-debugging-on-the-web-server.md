---
title: 'Erro: Não é possível iniciar a depuração no servidor Web | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- IIS, debugging DLLs
- debugger, Web application errors
- unable to start debugging error
- security [debugger], Web applications
- debugging [Visual Studio], errors
- HTTP servers, debugging error
- security settings, checking for default Web sites
- errors [debugger], unable to start debugging
- debugging ASP.NET Web applications, unable to start debugging error
- remote debugging, errors
ms.assetid: f62e378a-3a99-4f78-9d97-8bb63a4da181
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 168aaff6e7165c0566b198dab22174b14dad9949
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779288"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>Erro: não foi possível iniciar a depuração no servidor Web
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você tenta depurar um aplicativo ASP.NET em execução em um servidor Web, você pode receber essa mensagem de erro: não é possível iniciar a depuração no servidor Web.
  
Em muitos casos, esse erro ocorre porque o IIS não está configurado corretamente.

##  <a name="vxtbshttpservererrorsthingstocheck"></a> Verifique a configuração do IIS

Após executar etapas para resolver um problema detalhado aqui e antes de tentar novamente a depuração, talvez também precise redefinir o IIS. Você pode fazer isso abrindo um prompt de comando do administrador e digitando `iisreset`, ou você pode fazer isso no Gerenciador do IIS. 

* Parar e reiniciar seus Pools de aplicativos e tente novamente.

    O Pool de aplicativos pode ter sido interrompido ou outra alteração de configuração que você fez pode exigir que você parar e reiniciar o Pool de aplicativos.
    
    > [!NOTE]
    > Se o Pool de aplicativos mantém parando, você precisa desinstalar o módulo de reescrita de URL do painel de controle e, em seguida, reinstalá-lo usando o Web Platform Installer (WPI). Isso pode ser um problema após uma atualização do sistema significativos.

* Verifique a configuração do Pool de aplicativos, corrigi-lo se necessário e, em seguida, tente novamente.

    Se as credenciais de senha foram alterados, você precisa atualizá-los em seu Pool de aplicativos. Além disso, se você tiver instalado recentemente o ASP.NET, o Pool de aplicativos pode ser configurado da versão errada do ASP.NET. Corrija o problema e reinicie o Pool de aplicativos.
    
* Verifique se sua pasta de aplicativo Web tem as permissões corretas.

    Certifique-se de que você dê IIS_IUSRS ou IUSR (ou o usuário específico associado com o Pool de aplicativos) de leitura e direitos de execução para a pasta de aplicativo da Web. Corrija o problema e reinicie o Pool de aplicativos.

* Se você estiver usando um arquivo de HOSTS com endereços locais, tente usar o endereço de loopback em vez do endereço IP da máquina.

* Abra a página de localhost no navegador.

     Se o IIS não está instalado corretamente, você receberá um erro quando você digita `http://localhost` em um navegador.
     
     Para obter informações sobre como implantar o IIS, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) ou, para o ASP.NET Core [publicando para IIS](https://docs.asp.net/en/latest/publishing/iis.html)).

* Certifique-se de que a versão correta do ASP.NET é instalada no IIS.  Ver [implantar um aplicativo ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md#BKMK_deploy_asp_net) ou, para o ASP.NET Core [publicando para IIS](https://docs.asp.net/en/latest/publishing/iis.html)).

* Crie um aplicativo básico ASP.NET no servidor.

     Se você não pode receber o seu aplicativo para trabalhar com o depurador, tente criar um aplicativo básico ASP.NET localmente no servidor e tentar depurar o aplicativo básico. Se você pode depurar um aplicativo básico, que podem ajudá-lo a identificar qual é a diferença entre as duas configurações.
  
* Resolver erros de autenticação, se você estiver usando apenas o endereço IP

     Por padrão, os endereços IP devem fazer parte da Internet e a autenticação NTLM não é feita pela Internet. Se seu site estiver configurado no IIS para exigir autenticação, essa autenticação falhará. Para corrigir esse problema, você pode especificar o nome do computador remoto em vez do endereço IP.
     
## <a name="other-causes"></a>Outras causas

Se você estiver usando uma versão mais antiga do Visual Studio:

- Reinicie o Visual Studio com privilégios elevados e tente novamente.

    Um bug nas versões mais antigas (corrigidos mais tarde) necessários privilégios elevados em alguns cenários de depuração de ASP.NET.
    
- Se estiver executando várias instâncias do Visual Studio, abra novamente o seu projeto em uma instância do Visual Studio e tente novamente.
   
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)




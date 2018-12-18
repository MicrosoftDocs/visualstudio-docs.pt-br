---
title: 'Como: executar o processo de trabalho em uma conta de usuário | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- user accounts, aspnet_wp.exe
- ASP.NET, debugging Web applications
- tools, aspnet_wp.exe
- ASP.NET, tools
- aspnet_wp.exe
ms.assetid: b58e97b1-e62a-4318-aea4-52276ea20735
caps.latest.revision: 35
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d5d9e9cbadd2b7154eeb84bad99239e0b026eecd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734445"
---
# <a name="how-to-run-the-worker-process-under-a-user-account"></a>Como executar o processo de trabalho em uma conta de usuário
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para configurar o computador de modo que você possa executar o processo de trabalho do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] (aspnet_wp.exe ou w3wp.exe) em uma conta de usuário, siga estas etapas.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-run-aspnetwpexe-under-a-user-account"></a>Para executar aspnet_wp.exe em uma conta de usuário  
  
1.  Abra o arquivo machine.config, localizado no computador na pasta CONFIGURATION no caminho onde você instalou o tempo de execução.  
  
2.  Localizar o &lt;processModel&gt; seção e altere os atributos de usuário e senha para o nome e a senha da conta de usuário que você deseja aspnet_wp.exe para ser executado em.  
  
3.  Salve o arquivo machine.config.  
  
4.  No [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)], o IIS 6.0 está instalado por padrão. O processo de trabalho correspondente é w3wp.exe. Para executar no modo do IIS 6.0 com o aspnet_wp.exe como o processo de trabalho, siga estas etapas:  
  
    1.  Clique em **inicie**, clique em **ferramentas administrativas** e, em seguida, escolha **serviços de informações da Internet**.  
  
    2.  No **serviços de informações da Internet** caixa de diálogo, clique com botão direito a **Sites da Web** pasta e escolha **propriedades**.  
  
    3.  No **propriedades de Sites da Web** diálogo caixa, escolha **serviço**.  
  
    4.  Selecione **executar serviço WWW no modo de isolamento do IIS6.0**.  
  
    5.  Fechar o **propriedades** caixa de diálogo e **Gerenciador de serviços de Internet**.  
  
5.  Abra um prompt de comando do Windows e redefina o servidor executando:  
  
    ```  
    iisreset  
    ```  
    – ou —  
  
    ```  
    net stop iisadmin /y  
    net start w3svc  
    ```  
  
6.  Localize a pasta de arquivos temporários do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], que deve estar no mesmo caminho que a pasta CONFIG. Clique com botão direito temporários [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] pasta de arquivos e escolha **propriedades** no menu de atalho.  
  
7.  No **propriedades de arquivos temporários do ASP.NET** caixa de diálogo, clique o **segurança** guia.  
  
8.  Clique em **Avançadas**.  
  
9. No **configurações de segurança avançadas para arquivos temporários do ASP.Net** caixa de diálogo, clique em **Add**.  
  
    O **caixa de diálogo Selecionar usuário, computador ou grupo** é exibida.  
  
10. Digite o nome de usuário na **insira o nome do objeto para selecionar** caixa e, em seguida, clique em **Okey**. O nome de usuário deve seguir este formato: NomedeDomínio\NomedeUsuário.  
  
11. No **entrada de permissão para arquivos temporários do ASP.NET** diálogo caixa, dar ao usuário **controle total**e, em seguida, clique em **Okey** para fechar o **entrada para o ASP temporário Arquivos do .NET** caixa de diálogo.  
  
12. Um **segurança** caixa de diálogo será exibida e perguntará se você realmente quer alterar as permissões em uma pasta do sistema. Clique em **Sim**.  
  
13. Clique em **Okey** para fechar o **propriedades de arquivos temporários do ASP.NET** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
[Depuração do ASP.NET: requisitos do sistema](../debugger/aspnet-debugging-system-requirements.md)  
  





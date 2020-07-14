---
title: Executar um processo de trabalho em uma conta de usuário | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- user accounts, aspnet_wp.exe
- ASP.NET, debugging Web applications
- tools, aspnet_wp.exe
- ASP.NET, tools
- aspnet_wp.exe
ms.assetid: b58e97b1-e62a-4318-aea4-52276ea20735
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ac5bee0ffa05aa275782c57fc9b7b1c369bf65d
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349400"
---
# <a name="how-to-run-the-worker-process-under-a-user-account"></a>Como executar o processo de trabalho em uma conta de usuário
Para configurar o computador de modo que você possa executar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] (aspnet_wp.exe ou w3wp.exe) em uma conta de usuário, siga estas etapas.

 > [!IMPORTANT]
 > A partir do Windows Server 2008 R2, recomendamos o uso do [ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities) como a identidade de cada pool de aplicativos.

## <a name="procedure"></a>Procedimento

#### <a name="to-run-aspnet_wpexe-under-a-user-account"></a>Para executar aspnet_wp.exe em uma conta de usuário

1. Abra o arquivo machine.config, localizado no computador na pasta CONFIGURATION no caminho onde você instalou o runtime.

2. Localize a seção &lt;processModel&gt; e altere os atributos de usuário e de senha para o nome e a senha da conta de usuário com a qual você deseja que o aspnet_wp.exe seja executado.

3. Salve o arquivo machine.config.

4. No [!INCLUDE[winxpsvr](../debugger/includes/winxpsvr_md.md)], o IIS 6.0 está instalado por padrão. O processo de trabalho correspondente é w3wp.exe. Para executar no modo do IIS 6.0 com o aspnet_wp.exe como o processo de trabalho, siga estas etapas:

   1. Clique em **Iniciar**, clique em **Ferramentas Administrativas** e, em seguida, escolha **Serviços de Informações da Internet**.

   2. Na caixa de diálogo **Serviços de Informações da Internet**, clique com o botão direito do mouse na pasta **Sites** e escolha **Propriedades**.

   3. Na caixa de diálogo **Propriedades de Sites**, escolha **Serviço**.

   4. Selecione **Executar serviço WWW no modo de isolamento do IIS6.0**.

   5. Feche a caixa de diálogo **Propriedades** e o **Gerenciador de Serviços de Internet**.

5. Abra um prompt de comando do Windows e redefina o servidor executando:

   ```cmd
   iisreset
   ```

   — ou —

   ```cmd
   net stop iisadmin /y
   net start w3svc
   ```

6. Localize a pasta de arquivos temporários do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], que deve estar no mesmo caminho que a pasta CONFIG. Clique com o botão direito do mouse na pasta de arquivos temporários do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e escolha **Propriedades** no menu de atalho.

7. Na caixa de diálogo **Propriedades de arquivos temporários do ASP.NET**, clique na guia **Segurança**.

8. Clique em **Avançado**.

9. Na caixa de diálogo **Configurações de segurança avançadas para arquivos temporários do ASP.Net**, clique em **Adicionar**.

    A **caixa de diálogo Selecionar usuário, computador ou grupo** é exibida.

10. Digite o nome de usuário na caixa **Inserir o nome do objeto a ser selecionado** e, em seguida, clique em **OK**. O nome de usuário deve seguir este formato: NomedeDomínio\NomedeUsuário.

11. Na caixa de diálogo **Entrada de permissão para arquivos temporários do ASP.NET**, dê ao usuário **Controle Total** e, em seguida, clique em **OK** para fechar a caixa de diálogo **Entrada para arquivos temporários do ASP.NET**.

12. Uma caixa de diálogo **Segurança** aparecerá e perguntará se você realmente quer alterar as permissões em uma pasta do sistema. Clique em **Sim**.

13. Clique em **OK** para fechar a caixa de diálogo **Propriedades de arquivos temporários do ASP.NET**.

## <a name="see-also"></a>Veja também
- [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [Depuração ASP.NET: requisitos do sistema](../debugger/aspnet-debugging-system-requirements.md)

---
title: 'Erro: Falha na depuração porque a autenticação integrada do Windows não está habilitada. | Microsoft Docs'
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
- vs.debug.error.webdbg_ntlm_authn_not_enabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 6027cd94-74cf-470f-b7ce-6f6b68bc56ba
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0b922e8e8fde8b185207810d107afb9a9c5a6e05
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757255"
---
# <a name="error-debugging-failed-because-integrated-windows-authentication-is-not-enabled"></a>Erro: falha na depuração porque a autenticação integrada do Windows não está habilitada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A autenticação do usuário que solicitou a depuração foi impedida por um erro de autenticação. Isso pode ocorrer ao tentar entrar em um aplicativo Web ou serviço Web XML. Uma causa desse erro é que a autenticação integrada do Windows não está habilitada. Para habilitá-la, siga as etapas em “Para habilitar a autenticação integrada do Windows”.  
  
 Se você tiver habilitado a autenticação integrada do Windows e esse erro ainda aparecer, é possível que esse erro seja causado porque **autenticação de resumo para o Windows Domain Servers** está habilitado. Nessa situação, você deverá entrar em contato com o administrador da rede.  
  
### <a name="to-enable-integrated-windows-authentication"></a>Para habilitar a autenticação integrada do Windows  
  
1.  Faça logon no servidor Web com uma conta de administrador.  
  
2.  Clique em **inicie** e, em seguida, clique em **painel de controle**.  
  
3.  Na **painel de controle**, clique duas vezes em **ferramentas administrativas**.  
  
4.  Clique duas vezes em **serviços de informações da Internet**.  
  
5.  Clique no nó do servidor Web.  
  
     Um **Sites da Web** pasta é aberta abaixo do nome do servidor.  
  
6.  Você pode configurar a autenticação para todos os sites ou para sites individuais. Para configurar a autenticação para todos os sites da Web, clique com botão direito do **Sites da Web** pasta e clique **propriedades**. Para configurar a autenticação para um site individual, abra o **Sites da Web** pasta, clique com botão direito no site individual e, em seguida, clique em **propriedades**.  
  
     O **propriedades** caixa de diálogo é exibida.  
  
7.  Clique o **segurança de diretório** guia.  
  
8.  No **controle de acesso e autenticação anônima** seção, clique em **editar**.  
  
     O **métodos de autenticação** caixa de diálogo é exibida.  
  
9. Sob **acesso autenticado**, selecione **autenticação do Windows integrada**.  
  
10. Clique em **Okey** para fechar o **métodos de autenticação** caixa de diálogo.  
  
11. Clique em **Okey** para fechar o **propriedades** caixa de diálogo.  
  
12. Fechar o **serviços de informações da Internet** janela.  
  
### <a name="to-enable-integrated-windows-authentication-in-windows-vistaiis-7"></a>Para habilitar a autenticação integrada do Windows no Windows Vista/IIS 7  
  
1.  Faça logon no servidor Web com uma conta de administrador.  
  
2.  Ative a Autenticação do Windows e a Compatibilidade de Gerenciamento do II6, se você ainda não tiver feito isso anteriormente, seguindo estas etapas:  
  
    1.  Clique em **inicie**, clique em **painel de controle** e, em seguida, clique em **programas**.  
  
    2.  Sob **programas e recursos**, clique em **ativar ou desativar recursos do Windows ativar**.  
  
         A caixa de diálogo Controle de Acesso do Usuário aparecerá e solicitará para que a permissão continue.  
  
    3.  Clique em **Continue**.  
  
         A caixa de diálogo Recursos do Windows é exibida.  
  
    4.  Na lista de recursos, expanda o **serviços de informações da Internet** nó.  
  
    5.  Sob **serviços de informações da Internet**, expanda o **serviços da World Wide Web** nó.  
  
    6.  Sob **serviços da World Wide Web**, clique em **segurança**.  
  
    7.  Clique em **autenticação do Windows**.  
  
    8.  Sob **serviços de informações da Internet**, expanda o **ferramentas de gerenciamento da Web** nó.  
  
    9. Sob **as ferramentas de gerenciamento da Web**, expanda o **compatibilidade com gerenciamento do IIS 6** nó e selecione o **Metabase do IIS 6 e compatibilidade de configuração do IIS 6** caixa de seleção.  
  
    10. Sob **as ferramentas de gerenciamento da Web**, selecione **Console de gerenciamento do IIS** e clique em **Okey.**  
  
    11. Reinicie o computador para que essas alterações tenham efeito.  
  
3.  Clique em **inicie** e, em seguida, clique em **painel de controle**.  
  
4.  Clique em **modo de exibição clássico**e, em seguida, clique duas vezes em **ferramentas administrativas**.  
  
5.  No **nome** coluna e clique duas vezes em **serviços de informações da Internet (IIS) Manager**.  
  
6.  No **conexões** coluna, expanda o nó para o servidor.  
  
     Um **Sites da Web** pasta é aberta abaixo do nome do servidor.  
  
7.  Expanda o **Sites da Web** nó e clique no site da Web para o qual você deseja habilitar a autenticação integrada do Windows.  
  
8.  O título do painel central altera o nome do site que você selecionou. Nesse painel, sob o **IIS** título, clique duas vezes em **autenticação**.  
  
     O título do painel é alterado para **autenticação**.  
  
9. No **autenticação** painel, no **nome** coluna, clique com botão direito **autenticação do Windows** e, em seguida, clique em **habilitar**.  
  
10. Fechar o **serviços de informações da Internet (IIS) Manager** janela.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: Erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)   
 [Autenticação Digest da Microsoft](http://go.microsoft.com/fwlink/?LinkId=77938)   
 [Executando aplicativos da Web no Windows Vista com o IIS 7.0 e Visual Studio](http://msdn.microsoft.com/library/262a82ac-dd0e-4096-86c6-fb463e88be66)




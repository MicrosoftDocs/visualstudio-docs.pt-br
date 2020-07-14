---
title: Erro-falha na depuração porque a autenticação integrada do Windows não está habilitada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.webdbg_ntlm_authn_not_enabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
- aspx
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9c4f0e25449b0e108ac39662ec52a0ba9abc217
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460832"
---
# <a name="error-debugging-failed-because-integrated-windows-authentication-is-not-enabled"></a>Erro: falha na depuração porque a autenticação integrada do Windows não está habilitada
A autenticação do usuário que solicitou a depuração foi impedida por um erro de autenticação. Isso pode ocorrer ao tentar entrar em um aplicativo Web ou serviço Web XML. Uma causa desse erro é que a autenticação integrada do Windows não está habilitada. Para habilitá-la, siga as etapas em “Para habilitar a autenticação integrada do Windows”.

 Se você habilitou a autenticação integrada do Windows e esse erro ainda aparece, é possível que ele seja causado porque a **Autenticação Digest para servidores de domínio do Windows** está habilitada. Nessa situação, você deverá entrar em contato com o administrador da rede.

### <a name="to-enable-integrated-windows-authentication"></a>Para habilitar a autenticação integrada do Windows

1. Faça logon no servidor Web com uma conta de administrador.

2. Clique em **Iniciar** e em **painel de controle**.

3. No **Painel de Controle**, clique duas vezes em **Ferramentas Administrativas**.

4. Clique duas vezes em **Serviços de Informações da Internet**.

5. Clique no nó do servidor Web.

     Uma pasta **Sites** é aberta abaixo do nome do servidor.

6. Você pode configurar a autenticação para todos os sites ou para sites individuais. Para configurar a autenticação para todos os sites, clique com o botão direito do mouse na pasta **Sites** e clique em **Propriedades**. Para configurar a autenticação para um site individual, abra a pasta **Sites**, clique com o botão direito do mouse no site individual e clique em **Propriedades**.

     A caixa de diálogo **Propriedades** é exibida.

7. Clique na guia **Segurança de Diretório**.

8. Na seção **Acesso anônimo e controle de autenticação**, clique em **Editar**.

     A caixa de diálogo **Métodos de Autenticação** é exibida.

9. Em **Acesso autenticado**, selecione **Autenticação integrada do Windows**.

10. Clique em **OK** para fechar a caixa de diálogo **Métodos de Autenticação**.

11. Clique em **OK** para fechar a caixa de diálogo **Propriedades**.

12. Feche a janela **Serviços de Informações da Internet**.

### <a name="to-enable-integrated-windows-authentication-in-windows-vistaiis-7"></a>Para habilitar a autenticação integrada do Windows no Windows Vista/IIS 7

1. Faça logon no servidor Web com uma conta de administrador.

2. Ative a Autenticação do Windows e a Compatibilidade de Gerenciamento do II6, se você ainda não tiver feito isso anteriormente, seguindo estas etapas:

    1. Clique em **Iniciar**, em **painel de controle** e em **programas**.

    2. Em **Programas e Recursos**, clique em **Ativar ou desativar recursos do Windows**.

         A caixa de diálogo Controle de Acesso do Usuário aparecerá e solicitará para que a permissão continue.

    3. Clique em **Continue**.

         A caixa de diálogo Recursos do Windows é exibida.

    4. Na lista de funcionalidades, expanda o nó **Serviços de Informações da Internet**.

    5. Em **Serviços de Informações da Internet**, expanda o nó **Serviços da World Wide Web**.

    6. Em **Serviços da World Wide Web**, clique em **Segurança**.

    7. Clique em **Autenticação do Windows**.

    8. Em **Serviços de Informações da Internet**, expanda o nó **Ferramentas de Gerenciamento da Web**.

    9. Expanda **Ferramentas de Gerenciamento da Web**, expanda o nó **Compatibilidade com Gerenciamento do IIS 6** e selecione a caixa de seleção **Compatibilidade com Metabase do IIS 6 e configuração do IIS 6**.

    10. Em **Ferramentas de Gerenciamento da Web**, selecione **Console de Gerenciamento do IIS** e clique em **OK**.

    11. Reinicie o computador para que essas alterações tenham efeito.

3. Clique em **Iniciar** e em **Painel de Controle**.

4. Clique em **Exibição clássica** e clique duas vezes em **Ferramentas Administrativas**.

5. Clique na coluna **Nome** e clique duas vezes em **Gerenciador do IIS (Serviços de Informações da Internet)**.

6. Na coluna **Conexões**, expanda o nó para o servidor.

     Uma pasta **Sites** é aberta abaixo do nome do servidor.

7. Expanda o nó **Sites** e clique no site para a qual você deseja habilitar a autenticação integrada do Windows.

8. O título do painel central altera o nome do site que você selecionou. Neste painel, no título **IIS**, clique duas vezes em **Autenticação**.

     O título do painel é alterado para **Autenticação**.

9. No painel **Autenticação**, na coluna **Nome**, clique com o botão direito do mouse em **Autenticação do Windows** e clique em **Habilitar**.

10. Feche a janela **Gerenciador do IIS (Serviços de Informações da Internet)**.

## <a name="see-also"></a>Veja também
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
- [Autenticação do Microsoft Digest](/windows/win32/secauthn/microsoft-digest-authentication)
- [Executando aplicativos Web no Windows Vista com o IIS 7,0 e o Visual Studio](https://msdn.microsoft.com/Library/262a82ac-dd0e-4096-86c6-fb463e88be66)
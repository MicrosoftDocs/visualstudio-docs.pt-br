---
title: Solucionando problemas de referências de serviço
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 471b62c35cbe7098d52e9cbeb08be29cd39c7d58
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39180419"
---
# <a name="troubleshoot-service-references"></a>Solucionar problemas de referências de serviço

Este tópico lista problemas comuns que podem ocorrer quando você estiver trabalhando com o Windows Communication Foundation (WCF) ou referências de WCF Data Services no Visual Studio.

## <a name="error-returning-data-from-a-service"></a>Erro retornando dados de um serviço

Quando você retornar um `DataSet` ou `DataTable` de um serviço, você poderá receber uma exceção de "a cota de tamanho máximo para mensagens de entrada foi excedida". Por padrão, o `MaxReceivedMessageSize` propriedade para algumas associações é definida como um valor relativamente pequeno para limitar a exposição a ataques de negação de serviço. Você pode aumentar esse valor para evitar a exceção. Para obter mais informações, consulte <xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A>.

Para corrigir esse erro:

1.  Na **Gerenciador de soluções**, clique duas vezes o *App. config* arquivo para abri-lo.

2.  Localize o `MaxReceivedMessageSize` propriedade e alterá-lo para um valor maior.

## <a name="cannot-find-a-service-in-my-solution"></a>Não é possível localizar um serviço na minha solução

Quando você clica o **Discover** botão na **adicionar referências de serviço** caixa de diálogo, um ou mais projetos de biblioteca de serviço WCF na solução não aparecem na lista de serviços. Isso pode ocorrer se uma biblioteca de serviço foi adicionada à solução, mas ainda não foram compilada.

Para corrigir esse erro:

-   Na **Gerenciador de soluções**, o projeto de biblioteca de serviços WCF com o botão direito e clique em **Build**.

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>Erro ao acessar um serviço em uma área de trabalho remota

Quando um usuário acessa um serviço WCF hospedado na Web sobre uma conexão de área de trabalho remota e o usuário não tem permissões administrativas, autenticação NTLM será usada. Se o usuário não tem permissões administrativas, o usuário pode receber a seguinte mensagem de erro: "a solicitação HTTP é autorizada no esquema de autenticação de cliente 'Anonymous'. O cabeçalho de autenticação recebido do servidor foi 'NTLM' ".

Para corrigir esse erro:

1.  No projeto do site, abra o **propriedades** páginas.

2.  Sobre o **opções de inicialização** guia, desmarque a **autenticação NTLM** caixa de seleção.

    > [!NOTE]
    > Você deve desativar a autenticação NTLM somente para sites que contêm exclusivamente os serviços WCF. Segurança para serviços do WCF é gerenciada por meio da configuração na *Web. config* arquivo. Isso torna a autenticação NTLM desnecessários.

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>Nível de acesso para classes geradas configuração não tem nenhum efeito

Definindo o **nível para as classes geradas de acesso** opção a **configurar referências de serviço** caixa de diálogo para **interno** ou **amigo** Talvez não funcionem sempre. Mesmo que a opção parece estar definida na caixa de diálogo, as classes de suporte resultante são geradas com um nível de acesso de `Public`.

Isso é uma limitação conhecida de determinados tipos, como aqueles serializado usando o <xref:System.Xml.Serialization.XmlSerializer>.

## <a name="error-debugging-service-code"></a>Código de serviço de depuração de erro

Quando você entrar no código para um serviço WCF no código do cliente, você poderá receber um erro relacionado a ausência de símbolos. Isso pode ocorrer quando um serviço que fazia parte de sua solução foi movido ou removido da solução.

Quando você primeiro adiciona uma referência a um serviço WCF que faz parte da solução atual, uma dependência de compilação explícita é adicionada entre o projeto de serviço e o projeto de cliente de serviço. Isso garante que o cliente sempre acessa binários de serviço atualizado, que é especialmente importante para cenários como de depuração do código do cliente em código de serviço de depuração.

Se o projeto de serviço é removido da solução, essa dependência de compilação explícita é invalidada. Visual Studio não pode mais garantir que o projeto de serviço é recriado conforme necessário.

Para corrigir esse erro, você deve recriar manualmente o projeto de serviço:

1.  No menu **Ferramentas**, clique em **Opções**.

2.  No **opções** diálogo caixa, expanda **projetos e soluções**e, em seguida, selecione **geral**.

3.  Certifique-se de que o **configurações de build Show advanced** caixa de seleção está selecionada e, em seguida, clique em **Okey**.

4.  Carregar o projeto de serviço do WCF.

5.  No **Configuration Manager** caixa de diálogo, defina as **configuração da solução ativa** para **depurar**. Para obter mais informações, consulte [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md).

6.  Na **Gerenciador de soluções**, selecione o projeto de serviço do WCF.

7.  Sobre o **compilar** menu, clique em **recompilar** para recompilar o projeto de serviço do WCF.

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>WCF Data Services não são exibidos no navegador

Quando ele tenta exibir uma representação XML dos dados em um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)], Internet Explorer pode interpretar incorretamente os dados como um RSS feed. Certifique-se de que a opção para exibir RSS feeds está desabilitada.

Para corrigir esse erro, desabilite os feeds RSS:

1.  No Internet Explorer, sobre o **ferramentas** menu, clique em **opções da Internet**.

2.  Sobre o **conteúdo** guia da **Feeds** seção, clique em **configurações**.

3.  No **configurações do Feed** caixa de diálogo, desmarque a **ativar o modo de exibição de leitura de feed** caixa de seleção e, em seguida, clique em **Okey**.

4.  Clique em **Okey** para fechar o **opções da Internet** caixa de diálogo.

## <a name="see-also"></a>Consulte também

- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
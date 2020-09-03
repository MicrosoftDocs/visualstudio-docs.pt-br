---
title: 'Solucionando problemas de exceções: System. ServiceModel. Security. MessageSecurityException | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: troubleshooting
helpviewer_keywords:
- System.ServiceModel.Security.MessageSecurityException exception
- MessageSecurityException exception
ms.assetid: 61ad69a1-ac50-49de-9a7c-8454a84ec5bd
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9b8ce3f16c1439d62cfa1e2cff344b70e6724c42
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655360"
---
# <a name="troubleshooting-exceptions-systemservicemodelsecuritymessagesecurityexception"></a>Exceções de solução de problemas: System.ServiceModel.Security.MessageSecurityException
Uma <xref:System.ServiceModel.Security.MessageSecurityException> exceção é gerada quando [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] o determina que uma mensagem não está protegida corretamente ou foi violada. O erro ocorre com mais frequência quando todas as seguintes condições forem verdadeiras:

- Você usa uma referência de serviço WCF sobre uma conexão remota, por exemplo, Conexão de Área de Trabalho Remota ou Serviços de Terminal para se comunicar com um serviço WCF (.svc) em um projeto do site ou aplicativo Web.

- Você não tem permissões de administrador no site remoto.

- As solicitações para o host local no site remoto estão sendo tratadas pelo [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Development Server.

## <a name="associated-tips"></a>Dicas relacionadas
 **Resolva os problemas de autenticação NTLM ao usar o Development Server ASP.Net.**
O [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Development Server normalmente tem a segurança do Desafio/Resposta do Windows NT (NTLM) desativada, o que permite o acesso anônimo. Por padrão, quando você executa uma sessão dos Serviços de Terminal ou usa uma conexão remota, a segurança NTLM é habilitada. Quando a autenticação NTLM é habilitada, todas as solicitações do host local são validadas em relação às credenciais do usuário ou processo que iniciou o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Development Server. Isso reduz ameaças de segurança. No entanto, o WCF também realiza sua própria autenticação e não permite que uma conta de administrador consuma serviços WCF.

 Se um usuário remoto puder executar o site usando o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Development Server e também trabalhar com um serviço Web ou serviço WCF, você poderá criar uma associação de serviço personalizada ou desativar a segurança NTLM.

> [!IMPORTANT]
> Desativar a segurança NTLM não é recomendado e poderia constituir uma ameaça à segurança.

 Se você criar uma associação de serviço personalizada, ainda estará protegido pela autenticação NTLM.

 Use as etapas a seguir para criar uma associação de serviço personalizada para o serviço WCF.

#### <a name="to-create-a-custom-service-binding-for-the-wcf-service-hosted-inside-the-aspnet-development-server"></a>Para criar uma associação de serviço personalizada para o serviço WCF hospedado dentro do ASP.NET Development Server

1. Abra o arquivo Web.config do serviço WCF que está gerando a exceção.

2. Insira as informações a seguir no arquivo Web.config.

   ```
   <bindings>
     <customBinding>
       <binding name="Service1Binding">
         <transactionFlow />
         <textMessageEncoding />
         <httpTransport authenticationScheme="Ntlm" />
       </binding>
     </customBinding>
   </bindings>
   ```

3. Salve e feche o arquivo Web.config.

4. No código para WCF ou serviço Web, altere o valor do ponto de extremidade para o seguinte:

   ```
   <endpoint address="" binding="customBinding" bindingConfiguration="Service1Binding" contract="IService1" />
   ```

    Isso garante que o serviço use a associação personalizada.

5. Adicione uma referência ao serviço no aplicativo Web que acessa o serviço. (Na caixa de diálogo **Adicionar referência de serviço** , adicione uma referência ao serviço como você fez com o serviço original que estava gerando a exceção.)

   Siga estas etapas para desabilitar a segurança NTLM quando você estiver trabalhando com uma referência de serviço WCF.

> [!IMPORTANT]
> Desativar a segurança NTLM não é recomendado e poderia constituir uma ameaça à segurança.

#### <a name="to-turn-off-ntlm-security"></a>Para desativar a segurança NTLM

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nome do site e clique em **páginas de propriedades**.

2. Selecione **Opções de inicialização**e desmarque a caixa de seleção **autenticação NTLM** .

3. Clique em **OK**.

## <a name="see-also"></a>Consulte Também
 <xref:System.ServiceModel.Security.MessageSecurityException> [Usar o Assistente de Exceção](https://msdn.microsoft.com/library/e0a78c50-7318-4d54-af51-40c00aea8711)
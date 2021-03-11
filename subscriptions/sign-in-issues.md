---
title: Problemas ao entrar nas assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 176c7f11-b19d-49e9-a6dd-b2e5da5e8480
ms.date: 02/19/2021
ms.topic: conceptual
description: Saiba mais sobre problemas que podem surgir ao entrar em assinaturas do Visual Studio
ms.openlocfilehash: 5735e0c4178e6866539fff2edac6155642a1ba73
ms.sourcegitcommit: f9ed9c4c6c166ef9826feb21dcb9c4d47ed14e1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607191"
---
# <a name="issues-signing-in-to-visual-studio-subscriptions"></a>Problemas ao entrar em assinaturas do Visual Studio
Para usar sua Assinatura do Visual Studio, primeiro é necessário entrar.  Dependendo da sua assinatura, talvez você a tenha configurado com uma identidade da MSA (conta Microsoft) ou do AAD (Azure Active Directory).  Este artigo discute alguns problemas que podem ser encontrados ao entrar em sua assinatura.

## <a name="microsoft-accounts-msa-cannot-be-created-using-workschool-email-addresses"></a>MSA (Contas Microsoft) não podem ser criadas usando endereços de email de trabalho/estudante
A capacidade de criar uma nova MSA (Conta Microsoft) pessoal usando um endereço de email de trabalho/estudante não é mais permitida quando o domínio do email é configurado no Azure AD. O que isso significa? Se sua organização usa Microsoft 365 ou outros serviços corporativos da Microsoft que dependem do Azure AD e, se você tiver adicionado um nome de domínio ao seu locatário do Azure AD, os usuários não poderão mais criar um novo conta Microsoft pessoal usando um endereço de email em seu domínio.

### <a name="why-was-this-change-made"></a>Por que essa alteração foi feita?
Ter uma conta Microsoft pessoal com endereço de trabalho como nome de usuário é bem problemático para usuários finais e departamentos de TI semelhantes. Por exemplo:
- Os usuários podem achar que sua conta Microsoft pessoal está em conformidade com a empresa e que eles estão em conformidade quando salvam o documento de negócios no OneDrive
- Os usuários que saem de uma organização geralmente perdem o acesso ao seu email de trabalho. Quando eles fazem isso, talvez não consigam voltar para sua conta Microsoft pessoal se esquecerem sua senha. Por outro lado, o departamento de TI poderia redefinir a senha deles e entrar na conta pessoal de antigos funcionários.
- Os departamentos de TI têm uma falsa sensação de segurança e de propriedade da conta. Mas os usuários precisam apenas que o código vá e volte para o email de trabalho uma vez e poderão renomear sua conta a qualquer momento no futuro.

A situação é especialmente confusa para usuários que têm duas contas com o mesmo endereço de email (uma no Azure AD e outra na conta Microsoft).

### <a name="what-does-this-experience-look-like"></a>Qual é a aparência dessa experiência?
Se você tentar se inscrever em um aplicativo de consumidor da Microsoft com um endereço de email de trabalho ou de estudante, verá a mensagem abaixo.

   > [!div class="mx-imgBorder"]
   > ![Não é possível criar uma conta com o email de trabalho](_img/sign-in-issues/cannot-use-work-email.png "Forneça um nome de usuário e uma senha para criar sua conta.")

No entanto, se tentar se inscrever em um aplicativo da Microsoft compatível com contas pessoais e corporativas/de estudante, você deverá ver esta mensagem:

   > [!div class="mx-imgBorder"]
   > ![Contas corporativas/de estudante com suporte](_img/sign-in-issues/existing-account.png "Você não pode se inscrever aqui com um endereço de email corporativo ou de estudante...")

### <a name="are-existing-accounts-affected"></a>As contas existentes são afetadas?
O bloco de inscrição descrito aqui impede apenas a criação de novas contas. Ele não tem impacto sobre usuários que já têm uma Conta Microsoft com um endereço de email de trabalho/estudante. Caso já esteja nessa situação, facilitamos a renomeação de uma conta Microsoft pessoal. Esse [artigo de suporte](https://windows.microsoft.com/en-US/Windows/rename-personal-microsoft-account) fornece orientações passo a passo simples. Renomear seus conta Microsoft pessoais significa alterar o nome de usuário e não afeta seu email de trabalho ou como você entra nos serviços corporativos, como Microsoft 365. Isso também não afeta suas coisas pessoais. Só muda a maneira como você entra nela. É possível usar outro endereço de email (pessoal), obter um novo endereço de email @outlook.com da Microsoft ou usar seu número de telefone como um novo nome de usuário.

> [!NOTE]
> Se o departamento de TI desejar que você crie uma conta Microsoft pessoal com seu email de trabalho/estudante, por exemplo, para acessar serviços empresariais da Microsoft como o Suporte Premier, converse com sua equipe de administração antes de renomear sua conta.

## <a name="deleting-a-sign-in-address-may-prevent-access-to-a-subscription"></a>Excluir um endereço de entrada pode impedir o acesso a uma assinatura
Se você excluir uma ou mais identidades (MSA ou AAD) associadas a sua assinatura, suas informações de assinante, incluindo seu nome de usuário e ID de entrada, poderão ser tornadas anônimas, resultando na perda de acesso à sua assinatura.

Para evitar impactos no acesso da sua assinatura, use uma dessas técnicas.
- Implante um sistema de gerenciamento de identidades único, MSA ou AAD, mas não ambos.
- Associe as identidades do AAD e MSA por meio do locatário.

## <a name="signing-in-may-fail-when-using-aliases"></a>A entrada pode falhar ao usar aliases
Dependendo do tipo de conta usado para entrar, as assinaturas disponíveis podem não ser exibidas corretamente ao entrar no [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) . Uma possível causa é o uso de "alias" ou "nomes amigáveis" em vez da identidade à qual a assinatura foi atribuída. Isso é chamado de "alias".

### <a name="what-is-aliasing"></a>O que é um alias?
O termo "alias" refere-se a usuários com identidades diferentes para entrar no Windows (ou no Active Directory) e para acessar o email.

Os aliases podem ser encontrados quando a empresa tem um Serviço Online da Microsoft para a entrada no diretório, como JohnD@contoso.com, mas os usuários acessam as contas de email usando aliases ou nomes amigáveis, como John.Doe@contoso.com. Para muitos clientes que gerenciam as assinaturas por VLSC (Volume Licensing Service Center), isso pode resultar em uma experiência de logon malsucedida, pois o endereço de email fornecido (John.Doe@contoso.com) não coincide com o endereço do diretório (JohnD@contoso.com) necessário para a autenticação bem-sucedida por meio da opção "Conta corporativa ou de estudante".

### <a name="what-options-do-i-have"></a>Quais as opções disponíveis?
Do ponto de vista de um assinante, é importante trabalhar primeiro com seu administrador para entender a configuração de identidade da sua empresa. Se necessário, seu administrador pode ter que atualizar as configurações de conta do portal de administração ou você pode precisar criar uma conta da Microsoft (MSA) usando seu endereço de email corporativo. Antes de executar as etapas para criar um MSA, fale com seu administrador em relação a quaisquer políticas ou problemas com a realização desta ação.

## <a name="resources"></a>Recursos
- Para obter assistência com vendas, assinaturas, contas e cobrança para assinaturas do Visual Studio, consulte [suporte a assinaturas](https://aka.ms/vssubscriberhelp)do Visual Studio. 

## <a name="see-also"></a>Consulte também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Saiba como [vincular contas MSA e AAD](/azure/active-directory/b2b/add-users-administrator) dentro do AAD.
- Saiba mais sobre a [anonimização](anonymization.md).
---
title: Como usar identidades conectadas em assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: lank
ms.assetid: 50ce0445-ef1a-4e92-b9d0-aebb2155a111
ms.date: 02/19/2021
ms.topic: conceptual
robots: noindex, nofollow
description: Saiba como trabalhar com contas da Microsoft conectadas e Azure Active Directory identidades
ms.openlocfilehash: 9625774cbf5338750034f1f288bd2ada0aa9fc33
ms.sourcegitcommit: f9ed9c4c6c166ef9826feb21dcb9c4d47ed14e1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607113"
---
# <a name="how-to-use-connected-identities-in-visual-studio-subscriptions"></a>Como usar identidades conectadas em assinaturas do Visual Studio
Se você receber uma assinatura do Visual Studio por meio de seu trabalho ou escola e usar o conta Microsoft (MSA) para entrar, seu administrador de assinaturas poderá conectar seu MSA à sua identidade no Azure Active Directory do AD (Azure Active Directory) da sua organização.  Isso alterará o modo como você acessa alguns dos benefícios incluídos na sua assinatura. 

## <a name="overview-of-connected-ids"></a>Visão geral das IDs conectadas
As organizações estão cada vez mais mudando para identidades baseadas no Azure AD para fornecer segurança e suporte aprimorados para o gerenciamento automatizado de assinaturas.  Se sua assinatura usar um MSA como um @outlook.com ou outro endereço de email pessoal, seu administrador poderá alterar seu email de entrada para sua identidade do Azure AD.  Isso alterará como entrar no portal do assinante em https://my.visualstudio.com , mas pode não alterar o modo como você acessa todos os seus benefícios.  

Se seu administrador conectar suas identidades MSA e Azure AD, você receberá um email informando que você saberá como começar a acessar sua assinatura do Visual Studio com sua identidade do Azure AD, em vez de seu MSA. 

## <a name="how-to-access-benefits-using-azure-ad-identities"></a>Como acessar benefícios usando identidades do Azure AD
Depois que o administrador conectar o MSA à sua identidade do Azure AD, você precisará entrar no portal do assinante em https://my.visualstudio.com com sua identidade do Azure ad para acessar os benefícios que dependem do Azure AD.  Elas incluem:
- Visual Studio IDE
- Azure DevOps
- Crédito individual do Azure DevTest

## <a name="how-to-access-benefits-using-your-msa"></a>Como acessar os benefícios usando o MSA
Para muitos dos benefícios oferecidos nas assinaturas do Visual Studio como Pluralsight, LinkedIn, CloudPilot e outros, você realmente cria contas de usuário nos sites dos parceiros.  Para essas contas, você deve continuar a usar a identidade usada quando criou a conta.  Por exemplo, se você ativou o benefício da Pluralsight usando sua MSA, você deve continuar a usar o MSA ao fazer o treinamento da Pluralsight, independentemente da identidade usada para entrar no portal do Assinante.  

## <a name="use-an-alternate-identity-to-access-your-subscription"></a>Usar uma identidade alternativa para acessar sua assinatura
Adicionar uma conta alternativa à sua Assinatura do Visual Studio permite que você acesse os benefícios da assinatura, como o Azure DevOps e o Azure, com uma identidade diferente daquela à qual a assinatura está atribuída. No passado, essa funcionalidade estava disponível somente se a sua assinatura do VS (Visual Studio) fosse atribuída a uma conta da Microsoft (MSA). Nós estendemos essa funcionalidade para contas corporativas ou de estudante no Azure AD (Azure Active Directory).  Para obter mais informações sobre como usar contas alternativas, confira nosso artigo sobre [identidades alternativas](vs-alternate-identity.md) . 

## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="q-how-can-i-contact-my-admin-about-this"></a>P: como posso contatar meu administrador sobre isso?
R: consulte nosso artigo de [administrador de assinaturas em contato](contact-my-admin.md) para obter informações sobre como contatar seu administrador.  

### <a name="q-im-an-admin--how-do-i-use-this"></a>P: sou um administrador.  Como fazer usar isso?
R: A implementação de identidades conectadas é simples.  Confira [este artigo](personal-email-sign-ins.md) para saber mais. 

## <a name="resources"></a>Recursos
- Para obter assistência com vendas, assinaturas, contas e cobrança para assinaturas do Visual Studio, consulte [suporte a assinaturas](https://aka.ms/vssubscriberhelp)do Visual Studio.

## <a name="see-also"></a>Consulte também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Depois que o administrador conecta suas contas do Azure AD e MSA, recomendamos verificar se você pode entrar com êxito no [portal de assinatura](https://my.visualstudio.com?wt.mc_id=o~msft~docs) e acessar os benefícios como o Azure DevOps, o Visual Studio e seu crédito individual do Azure DevTest.
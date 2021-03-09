---
title: Identidades para assinantes do Visual Studio
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 86f2856c-8adf-4085-9962-f4136679e5ed
ms.date: 02/19/2021
ms.topic: conceptual
description: Como adicionar uma identidade alternativa à sua Assinatura do Visual Studio para ser usada com o Azure DevOps e o Azure
ms.openlocfilehash: 4d00e6808a71522f95d8580056556f5a502ecbde
ms.sourcegitcommit: 35fa920126b34c8d3839da53e3a4c2c6f509968f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102473303"
---
# <a name="identities-for-visual-studio-subscribers"></a>Identidades para assinantes do Visual Studio
Quando você ativar sua assinatura do Visual Studio, será vinculada a identidade (ou o logon) que você usou durante a ativação com a assinatura do Visual Studio. Dessa forma, você poderá ser reconhecido no [portal do assinante do Visual Studio](https://my.visualstudio.com?wt.mc_id=o~msft~docs), no Azure DevOps e no Azure.

No Azure DevOps, o status da sua Assinatura do Visual Studio é verificado sempre que você faz logon e você recebe automaticamente as funcionalidades de cada organização da qual é membro.
Como essas funcionalidades são incluídas como um benefício do assinante, você pode ser adicionado gratuitamente como membro de qualquer organização do Azure DevOps ao usar uma identidade vinculada à sua Assinatura do Visual Studio.

No Azure, verificamos seu status de assinatura do Visual Studio quando você ativa o [crédito individual do Azure DevTest mensal](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/) que é um benefício do Assinante.

No [portal do assinante do Visual Studio](https://my.visualstudio.com?wt.mc_id=o~msft~docs), talvez você possa adicionar uma **alternativa identidade**, além da identidade usada durante a ativação. É permitido adicionar uma identidade alternativa quando uma conta da Microsoft é usada para ativar a assinatura. Dessa forma, você também pode adicionar uma conta corporativa ou de estudante (que você usa ao fazer logon no Visual Studio, Microsoft 365, ou em sua rede empresarial ou de estudante), permitindo que você acesse o Azure DevOps usando sua conta pessoal e sua conta de trabalho ou escolar.

## <a name="add-an-alternate-account-to-your-subscription"></a>Adicionar uma conta alternativa à sua assinatura
Adicionar uma conta alternativa à sua assinatura do Visual Studio permite que você acesse determinados benefícios de assinatura, como o Azure DevOps e o Azure, ou entre no IDE do Visual Studio com uma identidade diferente da à qual a assinatura está atribuída. No passado, essa funcionalidade estava disponível somente se a sua assinatura do VS (Visual Studio) fosse atribuída a uma conta da Microsoft (MSA). Nós estendemos essa funcionalidade para contas corporativas ou de estudante no Azure AD (Azure Active Directory).

> [!NOTE]
> Uma ID alternativa só permite que você use essa segunda ID para ativar créditos do Azure e DevOps do Azure, e para entrar no IDE do Visual Studio.  Ele não pode ser usado para entrar no portal de assinatura em <https://my.visualstudio.com> .  Você ainda precisa usar a ID à qual a assinatura é atribuída para entrar no Portal. 

Para todas as assinaturas, é possível adicionar uma "conta corporativa ou de estudante" para que você possa usar essa conta com benefícios que exigem um logon (VS IDE, Azure DevOps e Azure).

### <a name="add-the-alternate-account"></a>Adicionar a conta alternativa
1. Entre no portal do Assinante do Visual Studio com sua Conta Microsoft (https://my.visualstudio.com).
2. Selecione a guia **Assinaturas** .
3. Escolha **adicionar conta alternativa**.
4. Adicione sua conta corporativa ou de estudante.
    > [!div class="mx-imgBorder"]
    > ![Adicionar conta corporativa ou de estudante](_img/vs-alternate-identity/enter-alternate-account-my-visual-studio-com-portal.png "Adicionar uma conta corporativa ou de estudante como uma conta alternativa em sua assinatura.")

5. Use sua conta corporativa ou de estudante para entrar no Azure DevOps (https://{suaconta}.visualstudio.com).

Sua conta alternativa é adicionada à Assinatura do Visual Studio, permitindo que as duas identidades utilizem os benefícios da assinatura que exigem que você entre com a conta alternativa (IDE, Azure DevOps e Azure).

## <a name="faq"></a>Perguntas frequentes

### <a name="q--why-doesnt-azure-devops-recognize-me-as-a-visual-studio-subscriber"></a>P: Por que o Azure DevOps não me reconhece como um assinante do Visual Studio?

R: O Azure DevOps deverá reconhecer sua assinatura automaticamente quando você entrar usando sua identidade principal ou alternativa. Caso contrário, você poderá tentar algumas coisas:

* Verifique se você tem uma assinatura ativa do Visual Studio que inclui o [Azure DevOps](vs-azure-devops.md#eligibility) como um benefício.

* Confirme se você está usando um logon ou uma identidade que seja a identidade principal ou alternativa da sua assinatura do Visual Studio.

* Visite o [portal do assinante do Visual Studio](https://my.visualstudio.com?wt.mc_id=o~msft~docs) pelo menos uma vez antes de entrar no Azure DevOps.

Se o Azure DevOps ainda não reconhecer sua assinatura, contate o [suporte do Azure DevOps](https://azure.microsoft.com/support/devops/).

## <a name="resources"></a>Recursos
[Suporte a assinaturas do Visual Studio](https://aka.ms/vssubscriberhelp)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas 
Para obter mais informações sobre como usar o Azure, o Azure DevOps ou o IDE do Visual Studio, confira estes recursos:
- [Azure](vs-azure.md)
- [Azure DevOps](vs-azure-devops.md)
- [Visual Studio](vs-ide-benefit.md)
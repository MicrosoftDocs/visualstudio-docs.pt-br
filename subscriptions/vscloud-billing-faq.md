---
title: Perguntas frequentes de cobrança para assinaturas do Visual Studio Visual Cloud | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 21e0471d-ad59-4d21-9c6f-13f7147569af
ms.date: 03/05/2021
ms.topic: conceptual
description: Perguntas sobre cobrança para assinaturas de nuvem.
ms.openlocfilehash: 2c03871d11279b7c368ebd0c7012670fc92c9ee0
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249723"
---
# <a name="visual-studio-cloud-subscriptions-billing-faq"></a>Perguntas frequentes sobre cobrança de assinaturas de nuvem do Visual Studio
[Compare os benefícios e os preços das assinaturas de nuvem](https://visualstudio.microsoft.com/vs/pricing/) para entender os benefícios de cada assinatura do Visual Studio, com comparações entre as assinaturas de nuvem e padrão do Visual Studio, detalhes sobre os benefícios do assinante e muito mais.

## <a name="general-purchasing-questions"></a>Perguntas gerais sobre compras
### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-using-a-purchase-order"></a>P: Posso comprar assinaturas de nuvem do Visual Studio usando uma ordem de compra?
R: Não. Todas as assinaturas de nuvem do Visual Studio precisam ser compradas usando uma assinatura do Azure. (Considere isso como sua conta de cobrança do Azure.)

### <a name="q-what-types-of-azure-subscriptions-can-be-used-to-buy-visual-studio-cloud-subscriptions"></a>P: Quais tipos de assinaturas do Azure podem ser usadas para comprar assinaturas de nuvem do Visual Studio?
R: A maioria das assinaturas do Azure podem ser usadas – damos suporte a assinaturas do Azure conectadas ao seu [EA (Enterprise Agreement)](https://azure.microsoft.com/pricing/enterprise-agreement/), assinaturas do Azure configuradas por CSPs (provedores de solução de nuvem), assinaturas do Azure configuradas por meio de revendedores Microsoft Open License e assinaturas do Azure pagas conforme o uso.

Alguns tipos de assinaturas do Azure, incluindo a [avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/) e as assinaturas incluídas como benefícios do assinante nas assinaturas do Visual Studio, não podem ser usadas.

### <a name="q-am-i-required-to-buy-other-azure-services"></a>P: É necessário comprar outros serviços do Azure?
R: Não. Se você quiser comprar somente assinaturas de nuvem do Visual Studio por meio do Azure, você poderá fazer isso.

### <a name="q-where-can-i-view-my-billing-and-usage-data"></a>P: onde posso exibir meus dados de cobrança e de uso?
R: Obtenha informações sobre como [exibir sua fatura e uso](https://docs.microsoft.com/azure/cost-management-billing/manage/download-azure-invoice-daily-usage-date).

## <a name="enterprise-agreement-ea-customers"></a>Clientes do EA (Contrato Enterprise)
### <a name="q-can-i-use-an-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>P: Posso usar um Contrato Enterprise para comprar assinaturas de nuvem do Visual Studio?
R: Sim, você pode. Você precisará ser um colaborador ou uma função mais alta para uma assinatura do Azure que foi criada para seu EA. Faça suas compras de assinaturas de nuvem do Visual Studio diretamente no Visual Studio Marketplace. Não é possível comprar assinaturas de nuvem do Visual Studio usando uma ordem de compra.

### <a name="q-how-can-i-tell-whether-i-have-the-necessary-privileges-to-buy-services-in-the-visual-studio-marketplace-through-my-organizations-enterprise-agreement"></a>P: Como posso saber se tenho os privilégios necessários para comprar serviços no Visual Studio Marketplace por meio Contrato Enterprise da minha organização?
R: a abordagem mais fácil para determinar se você tem os privilégios certos é selecionar o botão **comprar** para um serviço oferecido na Visual Studio Marketplace.
Você precisa selecionar uma assinatura do Azure (que é uma conta de cobrança) em uma lista apresentada de assinaturas do Azure que estão vinculadas ao seu logon no momento.
Como o nome da assinatura do Azure assume como padrão o tipo de conta de cobrança ("Pago Conforme o Uso", "Contrato Enterprise", etc.), geralmente fica claro se a assinatura do Azure faz parte do Contrato Enterprise.

Outro método é tentar visitar o [Azure Enterprise Portal](https://ea.azure.com).  Se você conseguir acessá-lo com êxito, significará que você já tem a função de admin corporativo ou de proprietário da conta. Somente os proprietários da conta podem configurar novas contas de cobrança do Azure em um Contrato Enterprise. Se você não conseguir acessar o Azure Enterprise Portal, descubra na sua organização quem é o admin corporativo e solicite que ele o adicione como proprietário da conta no Azure Enterprise Portal.  Se não for possível encontrar essa pessoa, [envie um tíquete de suporte](https://support.microsoft.com/supportrequestform/cf791efa-485b-95a3-6fad-3daf9cd4027c) e solicite as informações de contato.  É necessário o nome da sua organização e o número de registro do Contrato Enterprise para o tíquete de suporte.

### <a name="q-can-i-use-the-azure-monetary-commitment-funds-from-my-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>P: Posso usar os fundos do compromisso monetário do Azure do meu Contrato Enterprise para comprar assinaturas de nuvem do Visual Studio?
R: Não, esses fundos pré-pagos não são qualificados para comprar as assinaturas de nuvem do Visual Studio. Quando você escolher uma assinatura do Azure criada para o EA para comprar assinaturas de nuvem do Visual Studio, os encargos serão exibidos na sua próxima fatura "excedente". Normalmente, isso ocorre mensalmente, mas devido às regras do histórico de alguns clientes do EA, é possível que uma fatura excedente não seja emitida por vários meses. Consulte um especialista em licenciamento do EA se você precisar saber qual valor de compras adicionais (compras que não são qualificadas para o compromisso monetário do Azure) emitirá uma fatura excedente.

## <a name="how-charges-are-processed"></a>Como os encargos são processados
### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>P: Como os encargos **mensais** da assinatura de nuvem são processados?
R: Na primeira compra, vamos cobrar uma quantidade proporcional para cobrir os dias restantes do mês em questão. Por exemplo, se uma compra de 10 assinaturas de nuvem mensais do Visual Studio Professional for feita em 15 de abril, serão cobradas 5 unidades porque resta 50% do mês (15 dias de um mês de 30 dias).
Em primeiro de maio e a cada mês seguinte até o cancelamento, será cobrado o total de 10 unidades.

Mais tarde, quando você aumentar a quantidade paga, o aumento de unidades também será cobrado proporcionalmente para cobrir os dias restantes do mês em questão. Ou seja, se você comprar uma assinatura de nuvem do Visual Studio Professional a mais em 10 de maio, serão cobradas aproximadamente 0,677 unidades (21 dias restantes no dia 31 do mês de maio).

### <a name="q-how-are-annual-cloud-subscription-charges-processed"></a>P: Como os encargos **anuais** da assinatura de nuvem são processados?
R: A cada compra, a quantidade comprada será cobrada imediatamente. Os encargos não são distribuídos ao longo do ano e não há cobrança proporcional. Se você comprar assinaturas de nuvem anuais em diferentes momentos no ano, você terá assinaturas que se renovarão em meses diferentes. Nós não fazemos com que todas as assinaturas de nuvem anuais do cliente coincidam como é comum nas compras do contrato de licenciamento por volume da Microsoft.

### <a name="q-how-do-cancellations-work"></a>P: Como os cancelamentos funcionam?
R: Ao cancelar uma assinatura de nuvem do Visual Studio, você está cancelando a renovação automática. A assinatura continuará até a data de renovação normal e, em seguida, simplesmente expirará.
Após a expiração, o assinante do Visual Studio não poderá mais usar o Visual Studio nem os outros benefícios da assinatura.

Com as assinaturas de nuvem mensais, os cancelamentos entram em vigor no primeiro dia do mês seguinte. Ao cancelar apenas algumas das assinaturas de nuvem mensais, você deverá remover os usuários no primeiro dia do próximo mês para garantir que as pessoas certas continuem com as assinaturas atribuídas ativas.

Para assinaturas de nuvem anuais, os cancelamentos entram em vigor no primeiro dia do mês após 12 meses da compra original ou 12 meses do último encargo de renovação anual. Por exemplo, se você comprou uma assinatura na nuvem anual do Visual Studio Professional em 3 de janeiro de 2018, ela permanece ativa até 1º de fevereiro de 2019, quando será renovada automaticamente por mais um ano. Se você cancelar em algum momento entre esse período e primeiro de fevereiro de 2020 a assinatura expirará em primeiro de fevereiro de 2020. Não há nenhum reembolso para cancelamentos durante o ano da assinatura para as assinaturas de nuvem anuais.

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>P: Que tipos de desconto por volume estão disponíveis para as assinaturas do Visual Studio?
R: Você recebe um desconto de 5% na sexta assinatura e em todas as próximas *dentro de cada tipo* de assinatura:

* Visual Studio Professional mensal
* Visual Studio Professional anual
* Visual Studio Enterprise mensal
* Visual Studio Enterprise anual

Por exemplo, se você comprar seis assinaturas mensais do Visual Studio Professional e cinco assinaturas mensais do Visual Studio Enterprise, você pagará o preço normal nas cinco do Professional, receberá um desconto de 5% na sexta do Professional e pagará o preço normal nas cinco assinaturas do Enterprise.

Além disso, o desconto aplica-se somente aos encargos em um determinado período de cobrança mensal. Então, se você comprar cinco assinaturas anuais do Visual Studio Professional em um mês e, em seguida, comprar mais cinco no próximo mês, você pagará o preço normal nas 10 assinaturas.

> [!NOTE]
> A Microsoft não oferece mais assinaturas anuais do Visual Studio Professional e do Visual Studio Enterprise nas Assinaturas na Nuvem. Não haverá nenhuma alteração na experiência dos clientes existentes nem na capacidade de renovar, aumentar, diminuir ou cancelar suas assinaturas. Novos clientes são incentivados a ir para [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) a fim de explorar diferentes opções para comprar o Visual Studio.

## <a name="other-questions"></a>Outras perguntas
### <a name="q-can-i-use-the-monthly-azure-devtest-individual-credit-as-a-visual-studio-subscriber-to-buy-more-visual-studio-cloud-subscriptions"></a>P: posso usar o crédito individual do Azure DevTest mensal como um assinante do Visual Studio para comprar mais assinaturas de nuvem do Visual Studio?
R: não, você não pode usar seu [crédito individual do Azure DevTest mensalmente](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/) como um assinante do Visual Studio para pagar Visual Studio Marketplace compras. Nenhuma compra de assinatura de nuvem do Visual Studio será cobrada em seu cartão de crédito.
Antes de fazer compras, você precisará [remover seu limite de gastos](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="q-whats-the-difference-between-annual-and-monthly-cloud-subscriptions"></a>P: Qual é a diferença entre as assinaturas de nuvem anuais e mensais?
R: As assinaturas de nuvem mensais incluem o Visual Studio mais o uso do Azure DevOps Services e do TFS. As assinaturas de nuvem anuais também têm isso, mas incluem benefícios para o Assinante, incluindo o uso do Windows e de outros softwares da Microsoft para instalação e execução para desenvolvimento e teste, um crédito individual DevTest do Azure mensal para ser usado para experimentar os serviços do Azure e fazer desenvolvimento e testes na nuvem, treinamento, suporte e muito mais.
[Compare os benefícios e os preços da assinatura na nuvem](https://visualstudio.microsoft.com/vs/pricing/)

### <a name="q-do-i-get-new-versions-of-visual-studio-if-i-buy-a-visual-studio-cloud-subscription"></a>P: Posso obter as novas versões do Visual Studio se eu comprar uma assinatura de nuvem do Visual Studio?
R: Sim. Quando novas versões são lançadas, você pode baixar e executá-las. Além disso, você também pode continuar a executar as versões anteriores.

### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-from-my-software-reseller"></a>P: Posso comprar assinaturas de nuvem do Visual Studio do meu revendedor de software?
R: Sim, você pode, se o revendedor participar do programa CSP (provedor de soluções na nuvem). Pergunte isso a ele.

### <a name="q-where-can-i-find-information-about-azure-invoices"></a>P: onde posso encontrar informações sobre as faturas do Azure?
R: Confira o artigo [entender sua fatura do Azure](https://docs.microsoft.com/azure/cost-management-billing/understand/understand-invoice) na [documentação do Azure](/azure/).

## <a name="related-resources"></a>Recursos relacionados
- [Portal de administração de assinaturas do Visual Studio](https://manage.visualstudio.com/)
- [Suporte de assinatura do Visual Studio](https://visualstudio.microsoft.com/vs/support/)
- [Compra de assinatura de nuvem do Visual Studio para CSPs](vscloud-csp.md)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Comprar assinaturas de nuvem agora
- [Visual Studio Professional mensalmente](https://marketplace.visualstudio.com/items?itemName=ms.vs-professional-monthly)
- [Visual Studio Enterprise mensalmente](https://marketplace.visualstudio.com/items?itemName=ms.vs-enterprise-monthly)
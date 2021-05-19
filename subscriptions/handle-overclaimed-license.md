---
title: Manipular licenças Superalocadas em assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: a747100c-6f08-41a4-aaad-05099741742b
ms.date: 05/18/2021
ms.topic: conceptual
description: Saiba como os administradores podem resolver assinaturas Superalocadas
ms.openlocfilehash: 533ce71e8795e89bcb21fd437da6bea91db291f4
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973390"
---
# <a name="over-allocated-subscriptions"></a>Assinaturas Superalocadas
Às vezes, os pedidos são alterados após os assinantes serem adicionados, o que pode resultar em um número maior de assinaturas atribuídas que licenças pertencentes à empresa. Isso é chamado de "sobrealocação".  

Para ver suas alocações de assinatura, clique no ícone superior à esquerda para abrir o painel alocações.  

> [!NOTE]
> Não são permitidas sobrelocalidades em programas de licença aberta.  Além disso, outros programas podem exibir essas informações no portal de maneira diferente.
>
> [!div class="mx-imgBorder"]
> ![Aviso de assinaturas solicitadas em excesso](_img/over-claimed/over-claimed-alert.png "O número de sobrealocações é listado na visão geral e é representado pela barra com hash no grafo para cada tipo de assinatura.")

Observe que a exibição usa uma barra com hash para indicar assinaturas Superalocadas.  O número de sobrealocações em todos os tipos de assinatura está incluído na seção de visão geral na parte superior e cada nível de assinatura também exibe seu próprio status de alocação.  

## <a name="receive-notifications-when-over-allocations-occur"></a>Receber notificações quando houver excesso de alocações
Você pode designar um endereço de email para receber notificações quando ocorrerem sobrealocações, bem como definir um limite que deve ser excedido antes que as notificações sejam enviadas.  Saiba mais sobre como [definir preferências para seus contratos](admin-preferences.md) no portal de administração.

## <a name="resolve-over-allocated-subscriptions"></a>Resolver assinaturas Superalocadas
Há várias maneiras de resolver sobrelocalidades:
- Entre em contato com seu revendedor para comprar assinaturas adicionais.
- Aguarde até que o período de realidade anual e pague pelas assinaturas Superalocadas nesse ponto. 
- Exclua algumas atribuições de assinatura.  (Isso não evitará a necessidade de pagamento na adequação ("true-up") anual, pois essa adequação é baseada no número máximo de assinaturas atribuídas em qualquer momento durante o ano.)

## <a name="billing-and-true-up"></a>Adequação ("true-up") e cobrança
Se sua organização tiver um EA (Contrato Enterprise), os administradores poderão atribuir assinaturas sem comprá-las e pagar por elas mais tarde por meio de um processo de reconciliação, conhecido como adequação ("true-up").  Quando você sobrealocar, sua organização será cobrada pelo número máximo de assinaturas atribuídas aos usuários durante a "verdadeira".  Isso acontecerá mesmo se você não tiver o número máximo de assinaturas atribuído no momento em que ocorrer a adequação ("true-up").  Para saber mais sobre como monitorar seu uso máximo, acesse o tópico [Uso máximo](maximum-usage.md).


## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre como gerenciar [assinaturas do Visual Studio com o GitHub Enterprise](assign-github.md).
- Para obter assistência com vendas, assinaturas, contas e cobrança para Assinaturas do Visual Studio, entre em contato com o [Suporte a Assinaturas](https://aka.ms/vsadminhelp) do Visual Studio.
---
title: Compra de assinatura de nuvem do Visual Studio para CSPs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/15/2018
ms.topic: Get-Started-Article
description: Informações para Provedores de Soluções na Nuvem como comprar e gerenciar assinaturas de nuvem do Visual Studio para seus clientes.
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: 50f4cfeaa6d0f530a70729155f0e81065359281d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49899455"
---
# <a name="buy-and-manage-visual-studio-cloud-subscriptions-for-your-customers"></a>Comprar e gerenciar assinaturas de nuvem do Visual Studio para seus clientes

Os parceiros do programa [CSP (Provedores de Soluções na Nuvem)](https://partner.microsoft.com/cloud-solution-provider) podem comprar assinaturas de nuvem do Visual Studio Enterprise e do Visual Studio Professional para seus clientes.

[Comparar opções de assinatura de nuvem](https://visualstudio.microsoft.com/vs/pricing)

## <a name="prerequisites"></a>Pré-requisitos

Primeiro você precisa configurar o locatário do cliente no Partner Center e criar uma assinatura do Azure para esse locatário.

[Saiba mais](/azure/devops/organizations/billing/csp/set-up-csp-customer)

## <a name="who-can-buy-visual-studio-subscriptions"></a>Quem pode comprar assinaturas do Visual Studio?
Qualquer pessoa que tenha [acesso de proprietário ou colaborador](https://na01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvsts%2Forganizations%2Fbilling%2Fadd-backup-billing-managers%3Fview%3Dvsts%2520%2520sa&data=02%7C01%7C%7Cb9e717e8abff47b0cd7e08d618edd860%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636723807145220358&sdata=aIaamEXHhx94KCYVY%2FFibqFzNBEqKPntpql867xAMgU%3D&reserved=0) à assinatura do Azure pode comprar assinaturas do Visual Studio. 

## <a name="how-to-buy"></a>Como comprar

<iframe src="//channel9.msdn.com/Shows/Visual-Studio-for-CSP-Partners/CSP-How-to-buy-Visual-Studio-Subscriptions/player" width="600" height="315" allowFullScreen="true" frameBorder="0"></iframe>

0. Faça logon no [Microsoft Partner Center](https://partnercenter.microsoft.com).
0. Escolha **Clientes** e selecione o cliente para o qual deseja comprar.
0. Escolha **Gerenciamento de Serviço**.
0. Escolha **Visual Studio Marketplace**.
0. Verifique se o nome do cliente está no canto superior direito.
0. Escolha **Assinaturas**.
0. Escolha Enterprise ou Professional e escolha mensal ou anual para Visual Studio.
0. Escolha **Comprar**.
0. Escolha a assinatura do Azure a ser cobrada pela compra.
0. Insira o número de usuários que o cliente precisa.
0. Examine a ordem e **Confirme**.

>[!NOTE]
> Você precisará seguir estas etapas sempre que comprar assinaturas do Visual Studio como CSP. Ainda não existe uma API para automatizar a compra.

Depois de confirmar a compra, escolha **Gerenciar** para atribuir assinaturas aos usuários finais do cliente.  Você também pode acessar o portal de administração de assinatura do Partner Center escolhendo **Gerenciamento de serviço**.  A partir daí, veja as etapas ou o vídeo abaixo.

## <a name="how-to-manage-visual-studio-cloud-subscriptions-for-your-customer"></a>Como gerenciar assinaturas de nuvem do Visual Studio para o cliente

<iframe src="//channel9.msdn.com/Shows/Visual-Studio-for-CSP-Partners/CSP-How-to-manage-Visual-Studio-Subscriptions/player" width="600" height="315" allowFullScreen="true" frameBorder="0"></iframe>

0. Faça logon no [Microsoft Partner Center](https://partnercenter.microsoft.com).
0. Escolha **Clientes** e o nome do cliente.
0. Escolha **Gerenciamento de Serviço**.
0. Escolha **Gerenciar assinaturas do Visual Studio**.

Se você tiver mais de uma assinatura do Azure para este cliente, use o menu suspenso para escolher a assinatura do Azure que foi usada para fazer as compras.  O **Resumo de Licenças** mostra o número de assinaturas que foram atribuídas e quantas estão disponíveis para cada opção de assinatura de nuvem do Visual Studio.  O resumo também permite comprar assinaturas adicionais ou reduzir o número de assinaturas.

Escolha **Adicionar** para atribuir uma assinatura a um novo usuário.  A contagem exibida é atualizada e o usuário final recebe uma notificação por email.
Em seguida, o usuário final poderá entrar usando o endereço de email que você forneceu para ativar a assinatura do Visual Studio no [portal do assinante do Visual Studio](https://my.visualstudio.com?wt.mc_id=o~msft~docs).

Para reatribuir uma assinatura do Visual Studio a um usuário diferente, você pode excluir o assinante atual e adicionar um novo assinante.

Se algum assinante não tiver ativado sua assinatura do Visual Studio, o motivo poderá ser que ele não encontrou o email de convite.  Nesse caso, você também pode solicitar um novo envio do convite de ativação para o usuário por meio do portal de administração do Visual Studio.

## <a name="view-visual-studio-pricing-for-csp-partners"></a>Exibir os preços do Visual Studio para parceiros CSP

Para exibir os preços do Visual Studio para parceiros CSP, faça logon no [Partner Center](https://partnercenter.microsoft.com).  Escolha **Preços e ofertas** no painel de navegação esquerdo.  Escolha o arquivo de preços do mês atual em **serviços baseados em uso** no canto superior direito. Depois de baixar a planilha do Excel, acesse a planilha **Lista de preços do Azure** e filtre a folha **Categoria do Medidor** para **Visual Studio**.

Aqui está a maneira de interpretar os dados dessa planilha:

| Categoria do medidor    |   Nome                 |  Unidades                                |           O que é isso                          |
|-------------------|------------------------|---------------------------------------|-------------------------------------------------|
| Visual Studio     | Enterprise             |  Assinatura                         | Assinatura mensal do Visual Studio Enterprise   |
| Visual Studio     | Enterprise (anual)    |  Assinaturas Anuais                 | Assinatura anual do Visual Studio Enterprise    |
| Visual Studio     | Professional           |  Assinatura                         | Assinatura mensal do Visual Studio Professional |
| Visual Studio     | Professional (anual)  |  Assinaturas Anuais                 | Assinatura anual do Visual Studio Professional  |

Oferecemos um desconto de 5% para a compra da sexta unidade (para um determinado cliente) a cada mês da assinatura do Visual Studio. É por isso que aparecem duas linhas para cada opção de assinatura. Uma linha mostra um "Valor Mínimo" igual a 0, que você deve interpretar como o preço base da primeira à quinta unidade. A outra linha mostra um "Valor Mínimo" igual a 5, que é o preço com 5% de desconto aplicado à sexta unidade e às próximas.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>P: Como os encargos **mensais** da assinatura de nuvem são processados?

R: Na primeira compra, vamos cobrar uma quantidade proporcional para cobrir os dias restantes do mês em questão. Por exemplo, se uma compra de 10 assinaturas de nuvem mensais do Visual Studio Professional for feita no dia 15 de abril, serão cobradas cinco unidades porque há 15 dias restantes do mês de 30 dias ou 50%, e será cobrada a proporção de 50% das unidades.
Em primeiro de maio e a cada mês seguinte até o cancelamento, será cobrado o total de 10 unidades.

Mais tarde, quando você aumentar a quantidade paga, o aumento de unidades também será cobrado proporcionalmente para cobrir os dias restantes do mês em questão. Ou seja, se você comprar uma assinatura de nuvem do Visual Studio Professional a mais em 10 de maio, serão cobradas aproximadamente 0,677 unidades (21 dias restantes no dia 31 do mês de maio).

### <a name="q-how-are-annual-cloud-subscription-charges-processed"></a>P: Como os encargos **anuais** da assinatura de nuvem são processados?

R: A cada compra, a quantidade comprada será cobrada imediatamente. Os encargos não são distribuídos ao longo do ano e não há cobrança proporcional. Se você comprar assinaturas de nuvem anuais em diferentes momentos no ano, você terá assinaturas que se renovarão em meses diferentes. Nós não fazemos com que todas as assinaturas de nuvem anuais do cliente coincidam como é comum nas compras do contrato de licenciamento por volume da Microsoft.

### <a name="q-how-do-cancellations-work"></a>P: Como os cancelamentos funcionam?

R: Ao cancelar uma assinatura de nuvem do Visual Studio, você está cancelando a renovação automática. A assinatura continuará até a data de renovação normal e, em seguida, simplesmente expirará.
Após a expiração, o assinante do Visual Studio não poderá mais usar o Visual Studio nem os outros benefícios da assinatura.

Com as assinaturas de nuvem mensais, os cancelamentos entram em vigor no primeiro dia do mês seguinte. Ao cancelar apenas algumas das assinaturas de nuvem mensais do cliente, você deverá remover os usuários no primeiro dia do próximo mês para garantir que as pessoas certas continuem com as assinaturas atribuídas ativas.

Para assinaturas de nuvem anuais, os cancelamentos entram em vigor no primeiro dia do mês após 12 meses da compra original ou 12 meses do último encargo de renovação anual. Por exemplo, se você comprou uma assinatura de nuvem anual do Visual Studio Enterprise em 3 de janeiro de 2018, ela ficará ativa até primeiro de fevereiro de 2019, quando será renovada automaticamente por mais um ano. Se você cancelar em algum momento entre esse período e primeiro de fevereiro de 2020 a assinatura expirará em primeiro de fevereiro de 2020. Não há nenhum reembolso para cancelamentos durante o ano da assinatura para as assinaturas de nuvem anuais.

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>P: Que tipos de desconto por volume estão disponíveis para as assinaturas do Visual Studio?

R: Você recebe um desconto de 5% na sexta assinatura e em todas as próximas *dentro de cada tipo* de assinatura:

* Visual Studio Professional mensal
* Visual Studio Professional anual
* Visual Studio Enterprise mensal
* Visual Studio Enterprise anual

Por exemplo, se você comprar seis assinaturas mensais do Visual Studio Professional e cinco assinaturas mensais do Visual Studio Enterprise, você pagará o preço normal nas cinco do Professional, receberá um desconto de 5% na sexta do Professional e pagará o preço normal nas cinco assinaturas do Enterprise.

Além disso, o desconto aplica-se somente aos encargos em um determinado período de cobrança mensal. Então, se você comprar cinco assinaturas anuais do Visual Studio Professional em um mês e, em seguida, comprar mais cinco no próximo mês, você pagará o preço normal nas 10 assinaturas.

Esses descontos são refletidos nos dados de preços dentro do [Partner Center](https://partnercenter.microsoft.com).

### <a name="q-are-there-renewal-discounts"></a>P: Há descontos para renovação?

R: Não, os preços para assinaturas do Visual Studio são fixos. O mesmo preço é oferecido para novas assinaturas e para a continuação de assinaturas.

### <a name="q-are-there-azure-devtest-pricing-options-for-csps"></a>P: Há opções de preços de Desenvolvimento/Teste do Azure para os CSPs?

R: Não no momento. Seus clientes podem usufruir dos [preços do Azure para Desenvolvimento/Teste](http://aka.ms/azuredevtestpricing), mas não há nada específico para os CSPs.
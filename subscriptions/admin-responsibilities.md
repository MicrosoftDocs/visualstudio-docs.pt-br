---
title: Responsabilidades do administrador | Visual Studio Marketplace
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/13/2018
ms.topic: Get-Started-Article
description: Saiba mais sobre as responsabilidades dos administradores de assinaturas.
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: 9fdefa652a368c344f11fdaf70dbf5db9b172fbf
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39638092"
---
# <a name="overview-of-administrator-responsibilities"></a>Visão geral das responsabilidades do administrador
Como administrador, você tem a capacidade de gerenciar as assinaturas da organização.  A função de administrador também tem a responsabilidade de garantir que as assinaturas sejam gerenciadas de acordo com os termos de licença. Este artigo descreve as responsabilidades, os benefícios e as limitações da função de administrador.

## <a name="roles--responsibilities"></a>Funções e responsabilidades
Um administrador do Visual Studio tem quatro responsabilidades principais:
1.  **Entender os benefícios e as restrições das assinaturas do Visual Studio.** O entendimento correto sobre os benefícios permite que você reduza os custos de hardware através do uso de serviços de nuvem e reduza os custos de software com licenças por usuário para ambientes de pré-produção. 
2.  **Atribuir assinaturas do Visual Studio a pessoas específicas e determinadas e incentivar o uso.** O contrato requer que as assinaturas do Visual Studio sejam atribuídas a pessoas específicas e determinadas. Faça o acompanhamento das pessoas que receberam assinaturas para garantir que elas acessem e aproveitem ao máximo os benefícios incluídos nas assinaturas do Visual Studio.
3.  **Fazer inventário de seu ambiente de pré-produção com precisão.** Isso é essencial para garantir que todos os usuários que interagem com software licenciado do Visual Studio estejam adequadamente licenciados com suas respectivas assinaturas do Visual Studio. 
4.  **Controlar as alterações de atribuição dos usuários e adquirir licenças adicionais de acordo com um agendamento.** Os contratos de VL (Licenciamento por Volume) e MPSA da Microsoft oferecem flexibilidade para usar e atribuir assinaturas do Visual Studio. Em troca, é esperado que você controle as alterações em relação ao uso do software e atribuições de usuário, e também processe os pedidos de licenças adicionais de acordo com o agendamento descrito no contrato.

## <a name="benefits-and-limitations"></a>Benefícios e limitações
As assinaturas do Visual Studio permitem aos membros da equipe de desenvolvimento instalar e usar o software para projetar, desenvolver, testar, avaliar e demonstrar outro software. As assinaturas de software do Visual Studio não estão licenciadas para ambientes de produção. 

|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Licenciamento baseado no usuário                     | As Plataformas MSDN e todos os níveis de assinaturas do Visual Studio são licenciados por usuário. Cada membro da equipe de desenvolvimento que interagir (instalar, configurar ou acessar) com o software que acompanha esses produtos e serviços, exigirá sua própria assinatura do Visual Studio.                                                                                                                                                                                                                                                                                                                                  |
| Instalações ilimitadas                  | Cada usuário licenciado poderá instalar e usar o software em qualquer número de dispositivos para projetar, desenvolver, testar, avaliar e demonstrar o software. A exceção é o Microsoft Office, que é licenciado para uma área de trabalho. O software licenciado do Visual Studio pode ser instalado e usado no trabalho, em casa, na escola e em dispositivos no escritório de um cliente ou também em hardware dedicado hospedado por terceiros.                                                                                                                                                                                                                                  |
| Não destinado a ambientes de produção | O software das assinaturas do Visual Studio não está licenciado para ambientes de produção, incluindo qualquer ambiente acessado por usuários finais para finalidades diferentes de testes de aceitação ou comentários, um ambiente em conexão com um banco de dados de produção, para dar suporte à recuperação de desastres ou backup de produção ou ser usado para a produção durante períodos de pico de atividade. As exceções incluem benefícios específicos para determinados níveis de assinatura, descritos no [White Paper de licenciamento do Visual Studio](http://aka.ms/vslicensing).                                                                                            |
| Reatribuição de licença                     | Quando um usuário sair de uma equipe e não precisar mais de uma licença, você poderá reatribuir a licença depois de 90 dias. Quando você reatribuir uma licença, as chaves do produto (Product Keys) que já tiverem sido usadas ainda ficarão disponíveis, mas não serão substituídas. Para organizações que têm contratos EA (Contrato Enterprise), todos os benefícios que já tiverem sido usados pelo usuário original, como treinamentos do Pluralsight, serão redefinidos.                                                                                                                                                                                                                                                 |
| Exceção para usuários finais                  | Ao final de um projeto de desenvolvimento de software, os usuários finais normalmente examinam um aplicativo e determinam se ele atende aos critérios necessários para o lançamento. Esse processo é chamado de UAT (teste de aceitação do usuário). Os membros da equipe, como um responsável pela empresa ou um gerente de produto, podem agir como proxies para os usuários finais. Os usuários finais que não tiverem uma assinatura do Visual Studio poderão acessar o software para realizar o UAT se o uso do software estiver em conformidade com todos os termos de licenciamento do Visual Studio. É raro que alguém cuja função principal é projetar, desenvolver ou testar o software também seja qualificado como um "usuário final". |

## <a name="inventory-of-pre-production-environment"></a>Inventário do ambiente de pré-produção
As assinaturas do Visual Studio simplificam o gerenciamento de ativos ao contar usuários em vez de dispositivos.

Os administradores do Visual Studio devem atribuir assinaturas do Visual Studio a **pessoas específicas e determinadas**. As convenções de nomenclatura como Dev1, Dev2 ou Dev3 **não são permitidas**.

Aqui estão algumas maneiras para simplificar a realização do inventário do ambiente de pré-produção:
- Examine as atribuições de usuário. A Microsoft oferece um site chamado [Portal de administração do Visual Studio](https://manage.visualstudio.com/) para ajudá-lo a rastrear as atribuições de assinaturas do Visual Studio.
- Use seu Active Directory local ou baseado em nuvem para listar os usuários. Se você usa o Active Directory para gerenciar o acesso de usuários, talvez seja possível identificar usuários de desenvolvimento e teste de acordo com as respectivas associações de diretório.
- Use ferramentas automatizadas para inventariar sistemas. Talvez também seja necessário usar uma ferramenta de inventário de software para ajudá-lo a gerenciar os ativos de software e distinguir ambientes de pré-produção dos ambientes de produção. Muitos clientes com o Microsoft System Center criam convenções de nomenclatura para ajudar a automatizar essa parte do processo de inventário.
- Obter ajuda com a reconciliação manual. Inscreva a sua equipe para ajudar a reconciliar os usuários de desenvolvimento e teste com seu ambiente de desenvolvimento e teste. 

## <a name="large-teams-and-external-contractors"></a>Equipes grandes e prestadores de serviço externos
Os administradores de assinaturas do Visual Studio são responsáveis por garantir que cada usuário que interage com software licenciado do Visual Studio seja licenciado adequadamente com sua própria assinatura do Visual Studio.

### <a name="internal-teams"></a>Equipes internas
Normalmente, as empresas de software modernas incluem stakeholders de vários grupos. Identifique os contatos de cada grupo que podem ajudá-lo a manter o controle sobre alterações e inventário de usuário. Cada organização é diferente, mas uma lista típica de equipes envolvidas no desenvolvimento pode incluir:
- Equipes de engenharia de software. 
- Equipes de negócios, incluindo os proprietários de produto e analistas de negócios.
- Equipes de gerenciamento de projeto. 
- Equipes de qualidade, incluindo a equipe de garantia de qualidade e testadores manuais.
- Operações de TI, incluindo gerentes de infraestrutura de pré-produção e laboratório.

### <a name="external-contractors-and-partners"></a>Parceiros e prestadores de serviço externos
Os prestadores de serviço externos podem trazer licenças para se relacionar com seu ambiente licenciado do Visual Studio. Os Microsoft Certified Partners podem receber algumas assinaturas gratuitas do Visual Studio para uso interno. No entanto, essas assinaturas não abrangem atividades de geração de receita, como o desenvolvimento de software personalizado para um cliente. Peça aos parceiros para que enviem uma carta certificada, explicando as licenças que eles estão fornecendo e aquelas que eles necessitam que você adquira.

## <a name="track-user-assignment-and-process-orders"></a>Rastrear atribuição de usuário e processar pedidos
Os administradores de assinaturas do Visual Studio devem controlar o uso do Visual Studio e processar pedidos de qualquer aumento no uso conforme o prazo descrito no contrato de Licenciamento por Volume ou no Contrato de produtos e serviços da Microsoft. O novo Portal de administração de assinaturas do Visual Studio tornou isso mais simples com um rastreador útil que mostra as licenças usadas e disponíveis.

### <a name="high-water-mark-of-usage"></a>Marca d'água alta de uso
**A obrigação da sua empresa de comprar assinaturas do Visual Studio entra em vigor imediatamente quando:**
- Uma licença é atribuída a um usuário.
- Um usuário interage com software do Visual Studio.

Sua obrigação de compra completa é determinada pela **marca d'água alta de uso**. Esta marca-d'água é o ponto alto em atribuições de usuário diário ou em usuários interagindo com software do Visual Studio, o que for maior.
1.  Os administradores de assinaturas do Visual Studio podem aumentar a marca d'água alta de uso atribuindo assinaturas do Visual Studio a indivíduos.
2.  Os administradores de assinaturas do Visual Studio podem reatribuir assinaturas de um assinante a outro após 90 dias do momento da atribuição original. Para evitar uma marca d'água alta artificialmente, sempre faça isso removendo primeiro a assinatura existente e, em seguida, adicionando a nova.
3.  Os administradores de assinaturas do Visual Studio podem alterar o nível de assinatura atribuído para um indivíduo, o que constituiria na diminuição em uma atribuição e no aumento em outra. Ao diminuir o nível de assinatura atribuído de um assinante, a pessoa deve imediatamente parar de usar e desinstalar tudo o que está somente na assinatura de nível mais alto. 

### <a name="cloud-subscriptions-open-license-or-open-value"></a>Assinaturas de nuvem, Open License ou Open Value
É possível que você esteja atribuindo assinaturas por meio de um programa, como assinaturas do Microsoft Cloud, Open License ou Open Value. Nesse caso, você deve processar seu pedido de usuários adicionais durante o mês no qual os usuários (funcionários ou prestadores de serviço externos) começam a interagir com o software licenciado do Visual Studio.

### <a name="enterprise-mpsa-and-select-agreements"></a>Contratos Enterprise, MPSA e Select
Os Microsoft EAs (Contratos Enterprise), o MPSA e os Select Plus Agreements oferecem flexibilidade em como usar e licenciar software do Visual Studio ao longo do tempo. Os administradores do Visual Studio devem fazer um pedido adequação ("true-up") anual para colocar suas licenças de software de acordo com a marca d'água alta de uso estabelecida durante o período do contrato.
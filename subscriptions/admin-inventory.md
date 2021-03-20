---
title: Inventário de pré-produção na assinatura do Visual Studio | Visual Studio Marketplace
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 7d74e113-8fb2-490e-8502-48cce7b1327a
ms.date: 03/19/2021
ms.topic: conceptual
description: Saiba mais sobre a responsabilidade dos administradores de realizar inventários de pré-produção
ms.openlocfilehash: f6b1e1ebc02a986be86fb48578a4be47ccc3dfaa
ms.sourcegitcommit: d8d230791890cda532c263d04288dc13d2261c7f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104757666"
---
# <a name="inventory-of-pre-production-environment"></a>Inventário do ambiente de pré-produção
As assinaturas do Visual Studio simplificam o gerenciamento de ativos ao contar usuários em vez de dispositivos.

Os administradores do Visual Studio devem atribuir assinaturas do Visual Studio a **indivíduos específicos e nomeados**. As convenções de nomenclatura como Dev1, Dev2 ou o uso de nomes de equipe, como “FeatureTeam”, **não são permitidos**.

Aqui estão algumas maneiras para simplificar a realização do inventário do ambiente de pré-produção:
- Examine as atribuições de usuário. A Microsoft oferece um site chamado [Portal de administração do Visual Studio](https://manage.visualstudio.com/) para ajudá-lo a rastrear as atribuições de assinaturas do Visual Studio.
- Use seu Active Directory local ou baseado em nuvem para listar os usuários. Se você usa o Active Directory para gerenciar o acesso de usuários, talvez seja possível identificar usuários de desenvolvimento e teste de acordo com as respectivas associações de diretório.
- Use ferramentas automatizadas para inventariar sistemas. Talvez também seja necessário usar uma ferramenta de inventário de software para ajudá-lo a gerenciar os ativos de software e distinguir ambientes de pré-produção dos ambientes de produção. Muitos clientes com o Microsoft System Center criam convenções de nomenclatura para ajudar a automatizar essa parte do processo de inventário.
- Obter ajuda com a reconciliação manual. Inscreva a sua equipe para ajudar a reconciliar os usuários de desenvolvimento e teste com seu ambiente de desenvolvimento e teste.

> [!NOTE]
> O software das assinaturas do Visual Studio não está licenciado para ambientes de produção, incluindo qualquer ambiente acessado por usuários finais para finalidades diferentes de testes de aceitação ou comentários, um ambiente em conexão com um banco de dados de produção, para dar suporte à recuperação de desastres ou backup de produção ou ser usado para a produção durante períodos de pico de atividade. As exceções incluem benefícios específicos para determinados níveis de assinatura, descritos no [White Paper de licenciamento do Visual Studio](https://aka.ms/vslicensing).  

## <a name="resources"></a>Recursos
- [White paper de licenciamento do Visual Studio](https://visualstudio.microsoft.com/wp-content/uploads/2019/06/Visual-Studio-Licensing-Whitepaper-May-2019.pdf)
- [Suporte a assinaturas do Visual Studio](https://aka.ms/vsadminhelp)
- [Termos de licenciamento por volume](https://www.microsoft.com/licensing/product-licensing/products.aspx)

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre as responsabilidades para administradores:
- [Responsabilidades do administrador](admin-responsibilities.md)
- [Gerenciar equipes grandes e prestadores de serviço externos](manage-teams.md)
- [Rastrear atribuições de usuário e processar pedidos](assignments-orders.md)
- Utilizar o [Uso Máximo](maximum-usage.md) para rastrear os compromissos de compra
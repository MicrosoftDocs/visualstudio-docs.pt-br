---
title: Área de trabalho virtual do Microsoft Windows em assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 872c5746-5357-4764-949b-aa525a0adf1a
ms.date: 03/17/2021
ms.topic: conceptual
description: Saiba como você pode tirar proveito da área de trabalho virtual do Microsoft Windows por meio de sua assinatura do Visual Studio
ms.openlocfilehash: 2e7aad5d3f8214d39e5671e4bf5c4d5d357cd930
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671733"
---
# <a name="access-windows-virtual-desktop-in-subscriptions"></a>Acessar a área de trabalho virtual do Windows em assinaturas 
Os assinantes do Visual Studio agora podem usar seus créditos individuais de desenvolvimento/teste do Azure para os serviços de área de trabalho virtual do Microsoft Windows.  
A área de trabalho virtual do Windows é um serviço abrangente de virtualização de desktops e aplicativos em execução na nuvem. É a única VDI (Virtual Desktop Infrastructure) que fornece gerenciamento simplificado, várias sessões do Windows 10, otimizações para aplicativos Microsoft 365 para empresas e suporte para ambientes de Serviços de Área de Trabalho Remota (RDS). Implante e dimensione suas áreas de trabalho e aplicativos do Windows no Azure em minutos e obtenha recursos internos de segurança e conformidade.
Veja o que você pode fazer ao executar a Área de Trabalho Virtual do Windows no Azure:
- Configurar uma implantação do Windows 10 de várias sessões que fornece uma escalabilidade completa do Windows 10
- Virtualizar os Aplicativos do Microsoft 365 para Empresas e otimizá-los para execução em cenários virtuais de vários usuários
- Fornecer áreas de trabalho virtuais do Windows 7 com Atualizações de Segurança Estendida gratuitas
- Trazer seu RDS (Serviços de Área de Trabalho Remota) existente, além de aplicativos e áreas de trabalho do Windows Server para qualquer computador
- Virtualizar aplicativos e áreas de trabalho
- Gerencie aplicativos e desktops Windows 10, Windows Server e Windows 7 com uma experiência de gerenciamento unificada para obter mais informações sobre o que você pode fazer com a área de trabalho virtual do Windows, Assista ao [vídeo introdutório](/azure/virtual-desktop/overview).

## <a name="use-windows-virtual-desktop-with-azure"></a>Usar a área de trabalho virtual do Windows com o Azure 
Os assinantes do Visual Studio agora têm várias maneiras de usar as assinaturas do Azure para pagar pelos serviços de área de trabalho virtual do Windows:
- [Créditos individuais do Azure DevTest](vs-azure.md).  Os assinantes que recebem créditos individuais do Azure DevTest como parte de suas assinaturas podem usar esses créditos para pagar pelos serviços de área de trabalho virtual do Windows.  A quantidade de crédito mensal depende do nível de assinatura.
- [Assinaturas pagas conforme o uso do Azure DevTest](vs-azure-payg.md).  Você pode criar assinaturas do Azure e anexar um instrumento de pagamento para ter uma maneira simples de pagar pelo uso da área de trabalho virtual do Windows. 
- [Oferta do Azure contrato Enterprise DevTest](azure-ea-devtest.md).  Com essa oferta, os assinantes com Enterprise Agreements podem pagar pela área de trabalho virtual do Windows com o preço com desconto no Azure. 

## <a name="requirements"></a>Requisitos
A área de trabalho virtual do Windows requer um Azure Active Directory (Azure AD) para o qual as VMs serão Unidas.  Os usuários devem ser membros deste Azure AD.  Há duas opções para implementar o Azure AD:
- Serviços de diretório do Azure AD.  Para a maioria dos usuários, essa é a opção mais fácil de implementar.
- Uma máquina virtual que executa uma promoção de controlador de domínio.  Essa opção requer mais trabalho para configurar, mas oferece aos usuários um custo operacional mais baixo.
Para ver uma lista completa de pré-requisitos para usar a área de trabalho virtual do Windows, visite a [página Visão geral](/azure/virtual-desktop/overview#requirements)da área de trabalho virtual do Windows. 

## <a name="get-started"></a>Introdução 
Quando todos os seus pré-requisitos estiverem em vigor, você desejará concluir várias ações para colocar sua implementação em vigor.  Confira estes tutoriais para começar:
- [Criar um locatário da Área de Trabalho Virtual do Windows](/azure/virtual-desktop/virtual-desktop-fall-2019/tenant-setup-azure-active-directory)
- [Criar um pool de hosts](/azure/virtual-desktop/create-host-pools-azure-marketplace) usando o portal do Azure
- [Gerenciar grupos de aplicativos](/azure/virtual-desktop/manage-app-groups) para área de trabalho virtual do Windows

## <a name="eligibility"></a>Qualificação
| Nível de Assinatura                                                 |     Canais                                            | Benefício                                                          | Renovável?    |
|--------------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------------|---------------|
| Visual Studio Enterprise (Standard)   | VL, Azure, Retail, | Disponível|  Sim          |
| Assinatura Visual Studio Enterprise com o GitHub Enterprise  | VL | Disponível|  Sim          |
| Visual Studio Professional (Standard) | VL, Azure, Retail                                       | Disponível                                                             |  Sim             |
| Assinatura Visual Studio Professional com o GitHub Enterprise | VL                                       | Disponível                                        |  Sim           |
| Visual Studio Test Professional (Padrão)                         | VL, Retail                                              | Disponível|  Sim          |
| Plataformas MSDN (Padrão)                                          | VL, Retail                                              | Disponível                                         |  Sim          |
| Visual Studio Enterprise (Standard)  | NFR<sup>1</sup> |Não disponível  | N/D |
| Visual Studio Enterprise, Visual Studio Professional (nuvem mensal) | Azure | Não disponível | N/D |

<sup>1</sup>  *inclui: não para revenda (NFR), FTE, profissional mais valioso (MVP), diretor regional (RD), Microsoft Partner Network (MPN), parceiro do setor do Visual Studio (VSIP), Microsoft Certified Trainer, BizSpark, imagine, NFR básico*

> [!NOTE]
> A Microsoft não oferece mais assinaturas anuais do Visual Studio Professional e do Visual Studio Enterprise nas Assinaturas na Nuvem. Não haverá nenhuma alteração na experiência dos clientes existentes nem na capacidade de renovar, aumentar, diminuir ou cancelar suas assinaturas. Novos clientes são incentivados a ir para [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) a fim de explorar diferentes opções para comprar o Visual Studio.

Não tem certeza de qual assinatura você está usando?  Conecte-se ao [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs) para ver todas as assinaturas atribuídas ao seu endereço de email. Se não vir todas as suas assinaturas, talvez você tenha uma ou mais atribuídas a outro endereço de email.  Você precisará entrar com esse endereço de email para ver as assinaturas.

## <a name="see-also"></a>Veja também
- [Documentação do Azure](/azure/)
- [Documentação da Área de Trabalho Virtual do Windows](/azure/virtual-desktop/)
- [Suporte a assinaturas do Visual Studio](https://my.visualstudio.com/gethelp)

## <a name="next-steps"></a>Próximas etapas
-   Se você precisar comprar assinaturas do Visual Studio, confira:
     - [Preços para compras de varejo](https://visualstudio.microsoft.com/vs/pricing/) por meio do Microsoft Store
     - [Programas de licenciamento por volume](https://www.microsoft.com/licensing/default)
-   Saiba mais sobre a [área de trabalho virtual do Windows](/azure/virtual-desktop/overview)
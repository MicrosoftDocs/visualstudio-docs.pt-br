---
title: Anonimização de dados de assinante do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: ce5fc8a4-484c-4df6-97c3-cb60174fb66b
ms.date: 03/11/2021
ms.topic: conceptual
description: Saiba como os dados de assinante são anonimizados quando o acesso às assinaturas é perdido.
ms.openlocfilehash: 2a3d55824db1c90ff0868dda6d398e8c0e9a53d7
ms.sourcegitcommit: d8d230791890cda532c263d04288dc13d2261c7f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104757601"
---
# <a name="anonymization-of-visual-studio-subscriber-information"></a>Anonimização de informações de assinante do Visual Studio
Quando ocorre um evento que bloqueia o uso de uma assinatura pelo assinante, como o término de uma assinatura ou a exclusão da conta de logon de um assinante, as informações pessoais do usuário, como nome e a conta de logon, são essencialmente embaralhadas para torná-las inutilizáveis.  Isso é feito para proteger as informações pessoais do assinante.

[!INCLUDE [GDPR-related guidance](includes/gdpr-intro-sentence.md)]

## <a name="when-does-anonymization-occur"></a>Quando a anonimização ocorre?
Eventos que inutilizam uma assinatura para um assinante dispararão a anonimização.  A rapidez com que a anonimização ocorre depende do tipo de assinatura e do evento de disparo. Consulte a tabela abaixo para obter mais informações.

| Tipo de Assinatura                                                                                                                       | Anonimização do gatilho de evento                                                                                                     | Quando a anonimização ocorre |
|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|---------------------------|
| Visual Studio Dev Essentials                                                                                                            | O assinante recusa o programa ou não aceita os termos de uso                                    | 30 dias               |
| Assinaturas do Visual Studio compradas por meio da Microsoft Store (varejo)                                                                      | A assinatura expira ou não é ativada                                                                   | 360 dias                  |
| Assinaturas do Visual Studio adquiridas por meio da Licença de Volume, Visual Studio Marketplace (assinaturas da nuvem) ou programas como MPN | A assinatura expira ou não é atribuída a um usuário                                                          | 180 dias                  |
| Todas as assinaturas                                                                                                                       | Uma conta do Azure Active Directory ou MSA (Conta da Microsoft) usada para entrar na assinatura está fechada | Imediatamente               |
| Todas as assinaturas                                                                                                                       | Um assinante é removido do locatário associado à conta do Azure Active Directory                                | Imediatamente               |

## <a name="faq"></a>Perguntas frequentes
### <a name="q--does-the-anonymization-of-the-subscribers-personal-information-cause-them-to-lose-access-to-the-subscription"></a>P: A anonimização das informações pessoais do assinante fará com que ele perca o acesso à assinatura?
R: Não.  A anonimização é em resposta a um evento que ocasiona a perda de acesso à assinatura, mas não ocasiona a falta de acesso.

### <a name="q--im-an-admin-for-my-organizations-subscriptions--if-one-of-my-subscribers-information-is-anonymized-can-that-subscription-be-reassigned-to-another-user"></a>P: sou administrador das assinaturas da minha organização.  Se uma das informações do meu assinante for anonimizada, essa assinatura poderá ser atribuída novamente a outro usuário?
R: Sim.  Uma assinatura poderá ser reatribuída se esses critérios forem atendidos:
- A assinatura não expirou
- Um mínimo de 90 dias passou desde que a assinatura foi atribuída pela última vez a um assinante.  Por exemplo, se uma assinatura foi atribuída a um assinante em 1º de junho, ela não pode ser reatribuída até pelo menos 30 de agosto.

### <a name="q-how-can-i-prevent-anonymization-caused-by-deleting-a-sign-in-email-address"></a>P: como evitar a anonimato causada pela exclusão de um endereço de email de entrada?
R: há duas maneiras de evitar o problema:
- Implante um sistema de gerenciamento de identidades único, MSA ou AAD, mas não ambos.  
- Associe as identidades do AAD e MSA por meio do locatário. 

## <a name="support-resources"></a>Recursos de suporte
- Para obter assistência com vendas, assinaturas, contas e cobrança para assinaturas do Visual Studio, consulte [suporte a assinaturas](https://aka.ms/vssubscriberhelp)do Visual Studio.

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba como impedir a anonimato ao [associar as identidades do MSA e do AAD](/azure/active-directory/b2b/add-users-administrator).
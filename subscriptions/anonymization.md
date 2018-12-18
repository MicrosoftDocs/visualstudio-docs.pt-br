---
title: Anonimização de dados de assinante do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 10/31/2018
ms.topic: conceptual
description: Saiba como os dados de assinante são anonimizados quando o acesso às assinaturas é perdido.
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: 4570ff43f946c25c50d298e22de3b0c8a261f870
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51811246"
---
# <a name="anonymization-of-visual-studio-subscriber-information"></a>Anonimização de informações de assinante do Visual Studio

Quando ocorre um evento que bloqueia o uso de uma assinatura pelo assinante, como o término de uma assinatura ou a exclusão da conta de logon de um assinante, as informações pessoais do usuário, como nome e a conta de logon, são essencialmente embaralhadas para torná-las inutilizáveis.  Isso é feito para proteger as informações pessoais do assinante.

[!INCLUDE [GDPR-related guidance](includes/gdpr-intro-sentence.md)]

## <a name="when-does-anonymization-occur"></a>Quando a anonimização ocorre?

Eventos que inutilizam uma assinatura para um assinante dispararão a anonimização.  A rapidez com que a anonimização ocorre depende do tipo de assinatura e do evento de disparo. Confira a tabela abaixo para obter mais informações.

| Tipo de assinatura                                                                                                                       | Anonimização do gatilho de evento                                                                                                     | Quando a anonimização ocorre |
|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|---------------------------|
| Visual Studio Dev Essentials                                                                                                            | O assinante recusa o programa ou não aceita os termos de uso                                    | 30 dias               |
| Assinaturas do Visual Studio compradas por meio da Microsoft Store (varejo)                                                                      | A assinatura expira ou não é ativada                                                                   | 360 dias                  |
| Assinaturas do Visual Studio adquiridas por meio da Licença de Volume, Visual Studio Marketplace (assinaturas da nuvem) ou programas como MPN | A assinatura expira ou não é atribuída a um usuário                                                          | 180 dias                  |
| Todas as assinaturas                                                                                                                       | Uma conta do Azure Active Directory ou MSA (Conta da Microsoft) usada para entrar na assinatura está fechada | Imediatamente               |
| Todas as assinaturas                                                                                                                       | Um assinante é removido do locatário associado à conta do Azure Active Directory                                | Imediatamente               |

## <a name="faq"></a>Perguntas Frequentes

### <a name="q--does-the-anonymization-of-the-subscribers-personal-information-cause-them-to-lose-access-to-the-subscription"></a>P: A anonimização das informações pessoais do assinante fará com que ele perca o acesso à assinatura?
R: Não.  A anonimização é em resposta a um evento que ocasiona a perda de acesso à assinatura, mas não ocasiona a falta de acesso.

### <a name="q--im-an-administrator-for-my-organizations-subscriptions--if-one-of-my-subscribers-information-is-anonymized-can-that-subscription-be-reassigned-to-another-user"></a>P: Sou um administrador das assinaturas da minha organização.  Se uma das informações do meu assinante for anonimizada, essa assinatura poderá ser atribuída novamente a outro usuário?
R: Sim. Desde que a assinatura não tenha expirado, ela poderá ser reatribuída a outro assinante.

## <a name="next-steps"></a>Próximas etapas

Saiba como evitar a anonimização [vinculando identidades do AAD e da MSA](/azure/active-directory/b2b/add-users-administrator).

---
title: Assinaturas do Visual Studio no MPSA | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: b331c837-3524-42b7-820e-b4fdd5e12793
ms.date: 03/05/2021
ms.topic: conceptual
description: Saiba mais sobre como gerenciar assinaturas do Visual Studio em um contrato de produtos e serviços da Microsoft (MPSA)
ms.openlocfilehash: 49f18b540d27678b46a5fa111c76a069b705309d
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249457"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft)
Se você comprou assinaturas do Visual Studio por meio do programa MPSA, há algumas coisas que você deve conhecer antes de se tornar um administrador de assinaturas do Visual Studio e atribuir assinaturas a seus usuários. Se você já tiver configurado como administrador, poderá ir diretamente para o [portal de administração](https://manage.visualstudio.com/)de assinaturas do Visual Studio.

Os clientes do MPSA gerenciam os ativos adquiridos por meio do MPSA em um portal chamado de [Business Center](https://businessaccount.microsoft.com/Customer), que dá suporte a funcionalidades semelhantes ao VLSC (centro de serviços de licenciamento por volume). Isso inclui a exibição de seu resumo de licenças, pedidos, downloads, chaves, usuários, etc. No entanto, as assinaturas do Visual Studio no MPSA se comportam de maneira muito semelhante aos serviços de nuvem. O Centro de Empresas também usa contas corporativas para entrar, em vez de contas da Microsoft (MSA). Se sua organização usar serviços de nuvem, como o Office 365 ou Azure Active Directory e seu email fizer parte de um desses dois serviços, ela já será uma conta corporativa. Isso permitirá que você se registre no Centro de Empresas com sua senha existente. Se sua organização não estiver usando serviços de nuvem e seu email não for de uma conta corporativa, você poderá usá-lo para se registrar no Centro de Empresas.

Além disso, o [portal de administração](https://manage.visualstudio.com/) das assinaturas do Visual Studio é onde você atribuirá assinaturas depois de se tornar um administrador de assinaturas do Visual Studio. No MPSA, as assinaturas do Visual Studio devem ser provisionadas em seu respectivo portal de gerenciamento, que é o portal de administração de assinaturas do Visual Studio. Para fazer isso, você precisa associar sua conta de compra a um locatário (por exemplo, contoso.onmicrosoft.com).

Observe que há dois tipos de locatários gerenciados por locatários e locatários não gerenciados. Um locatário gerenciado refere-se a um locatário que já está sendo gerenciado por administradores dentro da organização.

Um locatário não gerenciado é um locatário sem nenhum administrador atribuído e não pode ser usado para serviços online, como o Office 365. Os locatários não gerenciados também são criados durante o registro no Centro de Empresas com um email que não é de uma conta corporativa. Se você recebeu uma solicitação para criar uma senha ao se registrar no Centro de Empresas, isso significa que seu email não era de uma conta corporativa e que foi criado um locatário não gerenciado.

Aqui estão alguns requisitos/etapas para se tornar um administrador de assinaturas do Visual Studio antes de concluir a associação de locatário.

## <a name="pre-tenant-association-managed-tenant"></a>Pré-associação do locatário (locatário gerenciado)
- Você precisa ser um usuário registrado no Centro de Empresas.
- É necessário ser um administrador de usuários (no mínimo) ou um administrador global no locatário do qual faz parte. (Isso se aplica se sua empresa já usa serviços de nuvem). Uma das funções é necessária para ser um administrador de assinaturas do Visual Studio.
- É necessário ser um administrador global no locatário do qual faz parte para poder associar sua conta de compra ao locatário.
- Você precisa ser um administrador de conta ou um gerente de conta no Centro de Empresas.
- O campo "País ou Região" em seu perfil de usuário (e de qualquer outro usuário) no [Azure](https://portal.azure.com/) precisa ser preenchido corretamente, dependendo da região (ou seja, EUA, Canadá, etc.). 

> [!NOTE]
> Todos os usuários que você deseja tornar administradores de assinaturas do Visual Studio não precisam ser usuários no Business Center, pois eles só precisam atender aos critérios 2 e 5.

Depois de atender aos critérios acima, você pode continuar a associar sua conta de compra ao seu locatário seguindo as etapas abaixo.
1. Faça logon no [Centro de Empresas](https://businessaccount.microsoft.com/Customer).
2. Clique na guia **Conta** e escolha **Associar Domínios**.
3. Selecione a **Conta de Compra** (se você tiver mais de uma).
4. Selecione seu **locatário** (exemplo: contoso.onmicrosoft.com).
5. Clique em **Associar Domínio**.

Mediante associação, todos os usuários que atenderem aos critérios normalmente serão provisionados como administradores de assinaturas do Visual Studio em minutos. No entanto, às vezes isso pode levar até 24 horas. Depois que o locatário for provisionado, você poderá acessar o portal de administração de assinaturas do Visual Studio. Se isso demorar mais de 24 horas, entre em contato com o [suporte do Business Center](https://businessaccount.microsoft.com/Customer/ContactUs).

> [!NOTE]
> Se novos usuários atenderem aos critérios das etapas 2 e 5 (após a associação), você precisará contatar o suporte do MPSA. O suporte do MPSA fornecerá assistência para provisionar os novos administradores de assinaturas do Visual Studio.

## <a name="tenant-association-unmanaged"></a>Associação do locatário (não gerenciado)
Se você se registrou no Centro de Empresas com um email que não era de uma conta corporativa [não registrado no Azure AD (Azure Active Directory)], como explicado acima, a associação do locatário será um pouco diferente. Você precisará executar o que chamamos de "tomada de controle de domínio". Durante esse processo, você se tornará o administrador global que vai alterar o locatário de não gerenciado para gerenciado.

Para obter uma explicação mais detalhada desse processo, use os [guias de Início Rápido](https://www.microsoft.com/Licensing/existing-customer/business-center-training-and-resources.aspx). Baixe o guia chamado *"configurar e usar seus serviços online"* , que o orientará durante o uso de um domínio. Depois que isso for concluído, sua conta de compra também será associada ao seu locatário.

> [!NOTE]
> Ao concluir o processo de processamento de domínio, você deve aderir aos critérios das cinco etapas na seção para a associação pré-locatário (gerenciada). Depois que os critérios forem atendidos, só será necessário entrar em contato com o suporte do MPSA para provisionar administradores adicionais de assinaturas do Visual Studio.

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como gerenciar assinaturas do Visual Studio.
- [Atribuir assinaturas individuais](assign-license.md)
- [Atribuir várias assinaturas](assign-license-bulk.md)
- [Editar assinaturas](edit-license.md)
- [Excluir assinaturas](delete-license.md)
- [Determinar o uso máximo](maximum-usage.md)
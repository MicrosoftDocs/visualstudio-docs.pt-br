---
title: Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft) | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/14/2018
ms.topic: Get-Started-Article
description: Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft)
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: a18565a97c0cd85ce42109961592a57c490d92a1
ms.sourcegitcommit: 3724338a5da5a6d75ba00452b0a607388b93ed0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30864266"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft)

Quando você compra as assinaturas do Visual Studio por meio do programa MPSA, há algumas coisas a serem consideradas antes que você possa se tornar um administrador de assinaturas do Visual Studio e atribuir assinaturas a seus usuários. Se você já tiver sido configurado como administrador, acesse diretamente o [Portal de Administração](https://manage.visualstudio.com/) de assinaturas do Visual Studio. 

Como cliente do MPSA, você terá acesso a um portal onde poderá gerenciar seus ativos comprados por meio do MPSA. Esse novo portal é chamado de [Centro de Empresas](https://businessaccount.microsoft.com/) e permite algumas funcionalidades novas e antigas, como o Centro de Empresas da Microsoft. Isso inclui exibir o resumo das licenças, os pedidos, os downloads, as chaves, os usuários, etc. No entanto, as assinaturas do Visual Studio no MPSA têm um comportamento semelhante aos dos serviços de nuvem. O Centro de Empresas também usa contas corporativas para entrar, em vez de contas da Microsoft. Se sua organização usa serviços de nuvem, como o Office 365 ou Azure Active Directory, e seu email faz parte de um desses dois serviços, então a conta já é corporativa. Isso permite que você se registre no Centro de Empresas com a senha existente indicada por sua organização. Se sua organização não estiver usando serviços de nuvem e seu email não for de uma conta corporativa, não se preocupe, pois você poderá usá-lo para se registrar no Centro de Empresas.

Além disso, o [Portal de Administração](https://manage.visualstudio.com/) de assinaturas do Visual Studio é onde as assinaturas são atribuídas aos assinantes depois que você se torna um administrador do Visual Studio. No MPSA, as assinaturas do Visual Studio precisam ser provisionadas no respectivo portal de gerenciamento, que é o Portal de Administração de Assinatura do Visual Studio. Para fazer isso, você precisa associar sua conta de compra a um locatário (por exemplo, contoso.onmicrosoft.com). 

Observe que há dois tipos de locatários (um locatário gerenciado e um locatário não gerenciado). Locatário gerenciado é um locatário que já está sendo gerenciado pela organização com administradores internos. 

Locatário não gerenciado é um locatário sem nenhum administrador interno, que não pode ser usado para serviços online, como o Office 365. Os locatários não gerenciados também são criados durante o registro no Centro de Empresas com um email que não é de uma conta corporativa. Se você recebe uma solicitação para criar uma senha ao se registrar no Centro de Empresas, isso significa que seu email não era de uma conta corporativa e que foi criado um locatário não gerenciado.

Antes de concluir a associação do locatário, aqui estão alguns requisitos ou etapas necessárias para tornar-se um administrador de assinaturas do Visual Studio.

## <a name="pre-tenant-association-managed-tenant"></a>Pré-associação do locatário (locatário gerenciado)
-   Você precisa ser um usuário registrado no Centro de Empresas.
-   É necessário ser um administrador de usuários (no mínimo) ou um administrador global no locatário do qual faz parte. (Isso se aplica se sua empresa já usa serviços de nuvem). Uma dessas funções é necessária para ser um administrador de assinaturas do Visual Studio.
-   É necessário ser um administrador global no locatário do qual faz parte para poder associar sua conta de compra ao locatário.
-   Você precisa ser um administrador de conta ou um gerente de conta no Centro de Empresas.
-   O campo "País ou Região" em seu perfil de usuário (e de qualquer outro usuário) no [Azure](https://portal.azure.com/) precisa ser preenchido corretamente, dependendo da região (ou seja, EUA, Canadá, etc.). 

> [!NOTE]
> Os usuários que você deseja tornar administradores de assinaturas do Visual Studio não precisam ser usuários do Centro de Empresas, pois eles só precisam atender aos critérios das Etapas 2 e 5.

Depois de atender aos critérios nas 5 etapas acima, você poderá associar sua conta de compra ao locatário seguindo as etapas abaixo.
1.  Faça logon no [Centro de Empresas](https://businessaccount.microsoft.com/).
2.  Clique na guia **Conta** e escolha **Associar Domínios**.
3.  Selecione a **Conta de Compra** (se você tiver mais de uma).
4.  Selecione o **locatário** (por exemplo, contoso.onmicrosoft.com).
5.  Clique em **Associar Domínio**.

Após a associação, todos os usuários que atenderem aos critérios necessários serão provisionados como administradores de assinaturas do Visual Studio provavelmente em minutos. No entanto, às vezes isso pode levar até 24 horas. Após o provisionamento, você poderá acessar o Portal de Administração de Assinaturas do Visual Studio. Se esse processo levar mais de 24 horas, contate o suporte do MPSA.

> [!NOTE]
> Se novos usuários atenderem aos critérios das Etapas 2 e 5 (após a associação), você precisará contatar o suporte do MPSA. O suporte do MPSA fornecerá assistência para provisionar novos administradores de assinaturas do Visual Studio.

## <a name="tenant-association-unmanaged"></a>Associação do locatário (não gerenciado)

Se você se registrou no Centro de Empresas com um email que não era de uma conta corporativa [não registrado no Azure AD (Azure Active Directory)], como explicado no parágrafo cinco acima, a associação do locatário será um pouco diferente. Você precisará executar o que chamamos de "tomada de controle de domínio". Durante esse processo, você se tornará o administrador global que vai alterar o locatário de não gerenciado para gerenciado.

Para obter uma explicação mais detalhada desse processo, use os [guias de Início Rápido](https://www.microsoft.com/en-us/Licensing/existing-customer/business-center-training-and-resources.aspx). Baixe o guia chamado *"Instalação e uso de serviços online"* que o mostrará como realizar uma tomada de controle de domínio. Quando esse processo for concluído, sua conta de compra também estará associada ao locatário.

> [!NOTE]
> Depois de concluir o processo de tomada de controle de domínio, você precisará atender aos critérios das cinco etapas na seção Pré-associação do locatário (gerenciado). Quando os critérios forem atendidos, bastará contatar o suporte do MPSA para provisionar outros administradores de assinaturas do Visual Studio.

É possível contatar o suporte por telefone ou email em caso de dúvidas ou necessidade de assistência.

Suporte do MPSA: **1-866-200-9611**, disponível de segunda a sexta-feira das 5h30 às 17h30, Hora do Pacífico

Email: ngvlsup@microsoft.com

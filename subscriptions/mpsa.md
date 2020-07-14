---
title: Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft) | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: b331c837-3524-42b7-820e-b4fdd5e12793
ms.date: 03/03/2020
ms.topic: conceptual
description: Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft)
ms.openlocfilehash: d38da1784eb543519f1a36ba7342f0b13ab2b1ac
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289346"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>Assinaturas do Visual Studio em um MPSA (Contrato de Produtos e Serviços da Microsoft)
Quando você compra as assinaturas do Visual Studio por meio do programa MPSA, há algumas coisas a serem consideradas antes que você possa se tornar um administrador de assinaturas do Visual Studio e atribuir assinaturas a seus usuários. Se você já tiver sido configurado como administrador, acesse diretamente o [portal de administração](https://manage.visualstudio.com/) de assinaturas do Visual Studio.

Os clientes do MPSA agora gerenciam ativos adquiridos por meio do MPSA em um novo portal chamado de [Centro de Empresas](https://businessaccount.microsoft.com/Customer), que dá suporte a funcionalidades semelhantes às do VLSC (Centro de Serviços de Licenciamento por Volume). Isso inclui a exibição de seu resumo de licenças, pedidos, downloads, chaves, usuários, etc. No entanto, as assinaturas do Visual Studio no MPSA se comportam de maneira muito semelhante aos serviços de nuvem. O Centro de Empresas também usa contas corporativas para entrar, em vez de contas da Microsoft (MSA). Se sua organização usar serviços de nuvem, como o Office 365 ou Azure Active Directory e seu email fizer parte de um desses dois serviços, ela já será uma conta corporativa. Isso permitirá que você se registre no Centro de Empresas com sua senha existente. Se sua organização não estiver usando serviços de nuvem e seu email não for de uma conta corporativa, você poderá usá-lo para se registrar no Centro de Empresas.

Além disso, o [portal de administração](https://manage.visualstudio.com/) de assinaturas do Visual Studio é onde as assinaturas são atribuídas aos assinantes depois que você se torna um administrador de assinaturas do Visual Studio. No MPSA, as assinaturas do Visual Studio precisam ser provisionadas no respectivo portal de gerenciamento, que é o portal de administração de assinaturas do Visual Studio. Para fazer isso, você precisa associar sua conta de compra a um locatário (por exemplo, contoso.onmicrosoft.com).

Observe que há dois tipos de locatários (gerenciados e não gerenciados). Locatário gerenciado é um locatário que já está sendo gerenciado por administradores internos à organização.

Locatário não gerenciado é um locatário sem nenhum administrador atribuído e que não pode ser usado para serviços online, tais como o Office 365. Os locatários não gerenciados também são criados durante o registro no Centro de Empresas com um email que não é de uma conta corporativa. Se você recebeu uma solicitação para criar uma senha ao se registrar no Centro de Empresas, isso significa que seu email não era de uma conta corporativa e que foi criado um locatário não gerenciado.

Aqui estão alguns requisitos ou etapas necessárias para tornar-se um administrador de assinaturas do Visual Studio antes de concluir a associação do locatário.

## <a name="pre-tenant-association-managed-tenant"></a>Pré-associação do locatário (locatário gerenciado)
- Você precisa ser um usuário registrado no Centro de Empresas.
- É necessário ser um administrador de usuários (no mínimo) ou um administrador global no locatário do qual faz parte. (Isso se aplica se sua empresa já usa serviços de nuvem). Uma dessas funções é necessária para ser um administrador de assinaturas do Visual Studio.
- É necessário ser um administrador global no locatário do qual faz parte para poder associar sua conta de compra ao locatário.
- Você precisa ser um administrador de conta ou um gerente de conta no Centro de Empresas.
- O campo "País ou Região" em seu perfil de usuário (e de qualquer outro usuário) no [Azure](https://portal.azure.com/) precisa ser preenchido corretamente, dependendo da região (ou seja, EUA, Canadá, etc.). 

> [!NOTE]
> Os usuários que você deseja tornar administradores de assinaturas do Visual Studio não precisam ser usuários do Centro de Empresas, pois eles só precisam atender aos critérios 2 e 5.

Depois de atender aos critérios acima, você poderá associar sua conta de compra ao locatário seguindo as etapas abaixo.
1. Faça logon no [Centro de Empresas](https://businessaccount.microsoft.com/Customer).
2. Clique na guia **Conta** e escolha **Associar Domínios**.
3. Selecione a **Conta de Compra** (se você tiver mais de uma).
4. Selecione o **locatário** (por exemplo, contoso.onmicrosoft.com).
5. Clique em **Associar Domínio**.

Após a associação, todos os usuários que atenderem aos critérios serão provisionados como administradores de assinaturas do Visual Studio em questão de minutos. No entanto, às vezes isso pode levar até 24 horas. Após o provisionamento do locatário, você poderá acessar o portal de administração de assinaturas do Visual Studio. Se isso demorar mais de 24 horas, entre em contato com o suporte do MPSA usando estas etapas:
1. Conectar-se a<https://www.microsoft.com/licensing/mpsa/default>
2. Clique no menu **mais** na parte superior da página. 
3. Escolha o **suporte**
4. Escolher **suporte de licenciamento**
5. Selecione a opção de suporte que melhor atenda às suas necessidades. 

> [!NOTE]
> Se novos usuários atenderem aos critérios das etapas 2 e 5 (após a associação), você precisará contatar o suporte do MPSA. O suporte do MPSA fornecerá assistência para provisionar novos administradores de assinaturas do Visual Studio.

## <a name="tenant-association-unmanaged"></a>Associação do locatário (não gerenciado)
Se você se registrou no Centro de Empresas com um email que não era de uma conta corporativa [não registrado no Azure AD (Azure Active Directory)], como explicado acima, a associação do locatário será um pouco diferente. Você precisará executar o que chamamos de "tomada de controle de domínio". Durante esse processo, você se tornará o administrador global que vai alterar o locatário de não gerenciado para gerenciado.

Para obter uma explicação mais detalhada desse processo, use os [guias de Início Rápido](https://www.microsoft.com/Licensing/existing-customer/business-center-training-and-resources.aspx). Baixe o guia chamado *"Instalação e uso de serviços online"* que o mostrará como realizar uma tomada de controle de domínio. Quando esse processo for concluído, sua conta de compra também estará associada ao locatário.

> [!NOTE]
> Depois de concluir o processo de tomada de controle de domínio, você precisará atender aos critérios das cinco etapas na seção Pré-associação do locatário (gerenciado). Quando os critérios forem atendidos, bastará contatar o suporte do MPSA para provisionar outros administradores de assinaturas do Visual Studio.

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](https://docs.microsoft.com/visualstudio/)
- [Documentação do Azure DevOps](https://docs.microsoft.com/azure/devops/)
- [Documentação do Azure](https://docs.microsoft.com/azure/)
- [Documentação do Microsoft 365](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como gerenciar assinaturas do Visual Studio.
- [Atribuir assinaturas individuais](assign-license.md)
- [Atribuir várias assinaturas](assign-license-bulk.md)
- [Editar assinaturas](edit-license.md)
- [Excluir assinaturas](delete-license.md)
- [Determinar o uso máximo](maximum-usage.md)

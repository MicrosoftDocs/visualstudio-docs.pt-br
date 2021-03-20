---
title: A entrada nas assinaturas do Visual Studio pode falhar ao usar aliases | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 97bf7474-c6c2-49b3-b2c9-f1b2808eed1a
ms.date: 03/19/2021
ms.topic: conceptual
description: A entrada poderá falhar se forem usados aliases ou nomes amigáveis
ms.openlocfilehash: d3a3cd962bafcf6a3e0c5aa20c98128233ace988
ms.sourcegitcommit: d8d230791890cda532c263d04288dc13d2261c7f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104757692"
---
# <a name="signing-into-visual-studio-subscriptions-may-fail-when-using-aliases"></a>Entrar em assinaturas do Visual Studio pode falhar ao usar aliases
Dependendo do tipo de conta usado para entrar, as assinaturas disponíveis podem não ser exibidas corretamente ao entrar no [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) . Uma possível causa é o uso de "alias" ou "nomes amigáveis" em vez da identidade à qual a assinatura foi atribuída. Isso é chamado de "alias".

## <a name="what-is-aliasing"></a>O que é um alias?
O termo "alias" refere-se a usuários com identidades diferentes para entrar no Windows (ou no Active Directory) e para acessar o email.

Os aliases podem ser encontrados quando uma empresa tem um Serviço Online da Microsoft para a entrada no diretório, como ‘JohnD@contoso.com’, mas os usuários acessam as contas de email usando aliases ou nomes amigáveis, como ‘John.Doe@contoso.com’. Verifique se os usuários estão usando o "endereço de email de entrada", conforme listado no portal de administração, em https://manage.visualstudio.com para acessar suas assinaturas. 

## <a name="what-are-the-potential-issues"></a>Quais são os problemas potenciais?

Dependendo do tipo de conta do Assinante, eles podem encontrar um dos dois problemas. 

### <a name="work-or-school-account-upn-mismatch-issue"></a>Problema de incompatibilidade de UPN da conta corporativa ou de estudante 
Uma incompatibilidade de UPN pode ser encontrada quando uma empresa tem uma Active Directory configurada onde o UserPrincipalName (UPN) não é o mesmo que o endereço SMTP primário. 

#### <a name="how-to-detect-if-your-sign-in-address-is-impacted-by-a-upn-mismatch"></a>Como detectar se o endereço de entrada é afetado por uma incompatibilidade de UPN 

1. Entre https://my.visualstudio.com/subscriptions usando o endereço de entrada mencionado em seu email de atribuição de assinatura.

2. Clique em seu nome no canto superior direito da página.  Isso abrirá seu perfil.  Verifique se o endereço de email de entrada listado em seu perfil corresponde ao endereço usado para entrar.  Se não tiver, seu UPN não corresponde e você não poderá exibir sua assinatura. 

> [!div class="mx-imgBorder"]
> ![Endereço de email de entrada](_img//aliasing/sign-in-email.png "Verifique se o endereço de email exibido no seu perfil corresponde ao que você usa para entrar.")

#### <a name="how-to-fix-a-upn-mismatch"></a>Como corrigir uma incompatibilidade de UPN

1. Acessar o portal de gerenciamento da administração do Visual Studio [https://manage.visualstudio.com](https://manage.visualstudio.com) 

2. Localize o Assinante que tem o problema de incompatibilidade de UPN. (O recurso de [filtro](search-license.md) pode facilitar a localização de um assinante.)

3. Alterar o endereço de email de entrada para o UPN do assinante 

0. Salve as alterações 

0. Informe o Assinante para sair do portal do assinante e acessar novamente usando o UPN 

### <a name="personal-account-aliasing-issue"></a>Problema de alias de conta pessoal

As contas de assinatura pessoal também poderão enfrentar problemas se o endereço de email usado para entrar no portal de assinaturas do Visual Studio não corresponder ao endereço de email associado à assinatura. 

#### <a name="how-to-detect-if-your-personal-subscription-account-is-impacted-by-an-aliasing-issue"></a>Como detectar se sua conta de assinatura pessoal é afetada por um problema de alias

1. Entrar no [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions)

0. Verifique se o endereço de email de entrada listado no canto superior direito da página corresponde ao endereço usado para entrar.  Se o endereço de email conectado não for o mesmo que o endereço de email usado para acessar o site, haverá um conflito entre sua conta e o alias.

#### <a name="how-to-fix-an-alias-issue"></a>Como corrigir um problema de alias

A plataforma do Visual Studio prioriza o alias principal para mostrar os detalhes da assinatura. 

1. Vá para **gerenciar como entrar na Microsoft**. Entre em seu conta Microsoft, se solicitado. 

2. Em aliases de conta, selecione **tornar primário** ao lado do endereço de email usado para atribuir a assinatura. 

> [!div class="mx-imgBorder"]
> ![Definir o endereço de email principal](_img//aliasing/account-aliases.png "Use o link tornar primário para escolher o alias principal para suas assinaturas.")

3. Saia do portal de assinaturas do Visual Studio (https://my.visualstudio.com) 

4. Entre novamente usando a conta usada para atribuir a assinatura que agora deve ser configurada como alias principal. 

## <a name="preventing-aliasing-issues"></a>Impedindo problemas de alias

Como administrador, há duas opções para garantir que seus assinantes tenham uma experiência de entrada bem-sucedida no [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) .
- A primeira opção (recomendada) é aproveitar a conta de diretório como a entrada para o portal de assinaturas do Visual Studio em https://my.visualstudio.com .  
- A segunda opção (menos segura) é permitir que seus assinantes entrem usando um endereço de email diferente do seu endereço de email do diretório.

Ambas as opções são configuradas no portal de administração ao concluir as seguintes etapas:  
1. Entrar [https://manage.visualstudio.com](https://manage.visualstudio.com) 

0. Se você estiver alterando um único usuário, selecione esse usuário na tabela e clique com o botão direito do mouse para editar. Isso abrirá um painel em que você pode modificar o endereço de email de entrada. Faça as atualizações necessárias no campo endereço de email de entrada. Clique em salvar e as alterações entrarão em vigor.  

0. Se você precisar fazer essas alterações em uma grande quantidade de usuários, poderá utilizar o recurso de edição em massa. Leia o artigo [Editar vários assinantes usando a edição em massa](./edit-license.md#edit-multiple-subscribers-using-bulk-edit) para obter mais informações.

> [!NOTE]
> Para alterações individuais e em massa, os Assinantes receberão um email com instruções de que seu endereço de email de entrada foi alterado e precisarão entrar usando o endereço de email atualizado. Também é importante observar que, se o assinante ativou anteriormente os benefícios do outro endereço de entrada, eles precisarão continuar usando o outro endereço de entrada para acessá-los.  

## <a name="support-resources"></a>Recursos de suporte
- Para obter assistência com a administração de assinaturas do Visual Studio, entre em contato com o [suporte de assinaturas do Visual Studio](https://aka.ms/vsadminhelp).

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como gerenciar assinaturas do Visual Studio.
- [Atribuir assinaturas individuais](assign-license.md)
- [Atribuir várias assinaturas](assign-license-bulk.md)
- [Editar assinaturas](edit-license.md)
- [Determinar o uso máximo](maximum-usage.md)
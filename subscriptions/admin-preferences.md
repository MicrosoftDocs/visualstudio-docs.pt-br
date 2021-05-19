---
title: Definir preferências no portal de administração Visual Studio assinaturas
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 0fe9eaa4-f589-429e-a443-13bf86637d5a
ms.date: 05/18/2021
ms.topic: conceptual
description: Saiba como definir preferências de idioma, contatos, nível de assinatura e outros no Portal de Administração
ms.openlocfilehash: 348febd6b964feec54053cff4a3d50cc02eba3d0
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "110018491"
---
# <a name="set-preferences-for-your-agreements-in-the-admin-portal"></a>Definir preferências para seus contratos no portal de administração
Os superd admins podem definir determinadas preferências no Portal de Administração (portal de administração) que serão aplicadas globalmente para cada contrato.  Essas preferências preencherão automaticamente os detalhes da assinatura para seus administradores quando eles adicionarem assinantes e só poderão ser modificadas globalmente por superd admins.  

## <a name="access-preferences"></a>Preferências de acesso
Você precisa estar conectado ao [portal de administração](https://manage.visualstudio.com) usando uma ID de entrada que tenha direitos de superadministrador no contrato para exibir ou modificar as preferências.  

Para definir suas preferências:
1. Entre no portal de administração com uma ID que tenha privilégios de superadministrador.
2. Clique no ícone de configuração no painel esquerdo.
   > [!div class="mx-imgBorder"]
   > ![Botão Preferências de Administrador](_img/admin-preferences/admin-preferences-button.png "Clique em gerenciar administradores e, em seguida, as preferências de contrato para exibir as preferências")

3. Clique em **Preferências de Contrato**.
Um painel será aberto à esquerda e suas preferências disponíveis serão exibidas. 

   > [!div class="mx-imgBorder"]
   > ![Caixa de diálogo de submenu Preferências de Administrador](_img/admin-preferences/admin-preferences-flyout-2.png "Defina suas preferências e clique em salvar")

## <a name="set-your-preferences"></a>Definir suas preferências
Vamos explorar cada uma das preferências disponíveis e seus efeitos. 

### <a name="agreement"></a>Contrato
Se você tiver vários contratos para os quais é um superd admin, poderá escolher o contrato desejado na lista de menus à direita do painel de configurações expandido.  As preferências definidas serão aplicadas somente a esse contrato.  Os administradores individuais podem substituir algumas dessas preferências, conforme o caso, ao atribuir assinaturas. 

Se houver apenas um contrato associado ao endereço de email usado para entrar, ele será exibido à direita do painel de configurações expandidos e a lista de menus será desabilitada. 

### <a name="contact-email-address"></a>Endereço de email de contato
Essa preferência fornece uma maneira para os assinantes contatarem  os administradores por meio do uso do botão Entrar em contato com meu administrador na página de [assinaturas](https://my.visualstudio.com/subscriptions) do portal do assinante.  Se essa preferência for deixada em branco, as mensagens de assinante serão encaminhadas para todos os administradores e superd administradores no contrato.  Recomendamos o uso de um alias de email de grupo ou um grupo de segurança para adaptar o público-alvo a esse email de contato. Você também poderá optar por inserir o endereço de email de um indivíduo, se preferir.

> [!NOTE]
> O endereço de email listado aqui NÃO será fornecido aos assinantes.  Quando um assinante enviar uma solicitação Contatar meu Administrador no portal do assinante, **a** mensagem será encaminhada para o alias sem expô-la ao assinante. 

### <a name="default-subscription-level"></a>Nível de assinatura padrão
Use essa configuração para determinar qual dos níveis de assinatura incluídos no contrato é selecionado por padrão quando uma assinatura é atribuída a um usuário.  Os administradores podem alterar a configuração para qualquer nível de assinatura em seu contrato– isso apenas impede que você tenha que fazer repetidamente sua escolha mais comum. 

### <a name="default-communication-preferences"></a>Opções de comunicação padrão
A definição de uma localidade e um idioma de comunicação padrão pode simplificar o processo de atribuição de assinaturas.  Por exemplo, caso sua equipe de desenvolvimento esteja localizada em um país diferente daquele da equipe de administração, você poderá definir as preferências mais adequadas à localização dos assinantes. Essas configurações ainda podem ser alteradas por todos os administradores para assinantes individuais. 

### <a name="default-external-subscribers-setting"></a>Configuração padrão de assinantes externos
Essa preferência permite que você decida se os administradores podem adicionar assinantes de fora do locatário/diretório da sua organização.  Se você desligar essa opção, nenhum assinante externo será permitido.  Se você habilitá-la e um administrador tentar adicionar um assinante externo, ele deverá confirmar sua escolha e terá permissão para atribuir a assinatura. Os administradores não podem substituir essa configuração. 

### <a name="default-downloads-setting"></a>Configuração padrão de downloads
A habilitação dessa configuração, que está ativada por padrão, permitirá que os assinantes acessem os downloads quando os administradores criarem assinaturas.  Os administradores ainda podem desabilitar os downloads para cada assinatura individual.  Desabilitar o acesso a downloads também desabilita o acesso às chaves do produto .  

### <a name="overallocation-notification"></a>Notificação de superalocação 
Opte por receber um email quando as atribuições em seu contrato se tornarem superalocadas. Essa notificação por email [](admin-preferences.md#contact-email-address)será enviada para o endereço de email Contato ou para todos os administradores em seu contrato se não houver nenhum endereço de email de Contato. Use o menu suspenso para configurar o limite no qual você deseja ser notificado. 

 
## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="q--can-i-disable-the-contact-email-address-so-subscribers-cannot-contact-admins"></a>P: posso desabilitar o **endereço de email de contato** para que os assinantes não possam contatar administradores?
R: não, embora você possa determinar quais administradores são contatados usando um grupo de segurança, o alias de email do grupo ou um endereço de email individual, o recurso não pode ser desabilitado.

### <a name="q-if-i-answer-a-subscribers-email-will-they-have-my-email-address"></a>P: se eu responder ao email de um assinante, ele terá meu endereço de email?
R: como sua resposta será proveniente de qualquer cliente de email que você esteja usando, a resposta recebida pelo assinante mostrará o endereço de email que você está usando.  Portanto, se você estiver respondendo com um alias de grupo, ele verá o alias de grupo.  Se você responder com seu próprio endereço de email, ele verá isso.  

### <a name="q-where-can-i-find-out-more-about-the-contact-my-admin-feature-in-the-subscriber-portal"></a>P: onde posso saber mais sobre o recurso **contatar meu administrador** no portal do assinante?
R: Confira nosso artigo sobre [o meu administrador de contatos](contact-my-admin.md) . 

### <a name="q-if-we-dont-complete-the-contact-email-address-and-a-subscriber-uses-the-contact-my-admin-feature-who-receives-their-request"></a>P: se não concluirmos o **endereço de email de contato** e um assinante usar o recurso **contatar meu administrador** , quem receberá sua solicitação?
R: se nenhum endereço de email específico for definido na preferência de **endereço de email de contato** , todos os administradores no contrato receberão a solicitação. 

## <a name="resources"></a>Recursos
- [Suporte para administração e assinaturas do Visual Studio](https://aka.ms/vsadminhelp)

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
- [Determinar o uso máximo](maximum-usage.md)
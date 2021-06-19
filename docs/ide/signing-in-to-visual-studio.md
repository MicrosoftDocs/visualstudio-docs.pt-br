---
title: Entrar no Windows
description: Saiba como entrar no Visual Studio.
titleSuffix: ''
ms.custom: seodec18, contperf-fy21q1
ms.date: 09/11/2020
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1b0ed679188cc0a4df9329fdd0adff4ad69667e6
ms.sourcegitcommit: c3713f284c4fe10b10996d5eb67077ddd8641424
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112375754"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>Entre no Visual Studio no Windows

Embora você não tenha que entrar, há muitas vantagens em fazer isso. Ao entrar, você pode personalizar, otimizar e enriquecer sua Visual Studio experiência. 

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in).

::: moniker range="vs-2017"

> [!WARNING]
> Para trabalhar com recursos configurados para acesso condicional, atualize para o Visual Studio 2019 Atualização 16.6 ou posterior. Para obter mais informações, [consulte Como usar o Visual Studio com contas que exigem autenticação multifafação](work-with-multi-factor-authentication.md).
> Usar o Visual Studio 2017 para acessar recursos configurados para acesso condicional pode disparar uma experiência de autenticação degradada, solicitando a autenticação várias vezes na mesma sessão Visual Studio. 
> 
::: moniker-end

## <a name="benefits"></a>Benefícios

Veja uma lista completa do que é possível esperar e fazer após entrar:


#### <a name="extend-the-visual-studio-trial-period"></a>Estender o período Visual Studio de avaliação

Você pode usar Visual Studio Professional ou Visual Studio Enterprise por mais 90 dias, em vez de ser limitado ao período de avaliação de 30 dias. Para obter mais informações, consulte [Estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md).

#### <a name="synchronize-your-visual-studio-settings"></a>Sincronizar as configurações Visual Studio configurações

As configurações que você personaliza, como associação de teclas, layout de janela e tema de cores, se aplicam imediatamente quando você entrar Visual Studio em qualquer dispositivo. Consulte [Sincronizar configurações no Visual Studio](../ide/synchronized-settings-in-visual-studio.md).

#### <a name="use-visual-studio-community-edition"></a>Usar Visual Studio Community edição

Se a instalação do Community Edition solicitar uma licença, entre no IDE para continuar usando Visual Studio Community **gratuitamente.** 

#### <a name="unlock-visual-studio-visual-studio-subscription-or-an-azure-devops-organization"></a>Desbloquear Visual Studio (Visual Studio ou uma Azure DevOps organização)

Desbloqueie Visual Studio se você usar uma conta associada a uma assinatura do Visual Studio ou a uma organização Azure DevOps usando as etapas em Estender uma versão de avaliação ou atualizar uma [licença](../ide/how-to-unlock-visual-studio.md).

#### <a name="the-visual-studio-dev-essentials-program"></a>O Visual Studio Dev Essentials de programação

Este programa inclui ofertas gratuitas de software, treinamento, suporte e muito mais. Para obter mais informações, consulte [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).

#### <a name="automatically-connect-to-services"></a>Conectar-se automaticamente aos serviços

Conecte-se a serviços, como o Azure e Azure DevOps Services, no IDE sem solicitar novamente credenciais para a mesma conta.

## <a name="how-to-sign-in"></a>Como entrar 

Ao abrir Visual Studio pela primeira vez, você será solicitado a entrar e fornecer algumas informações básicas de registro.

![Prompt de entrada](../ide/media/vs2019_signinpopup.png)

1. Escolha uma conta Microsoft ou uma conta de trabalho ou de estudante que melhor represente você. Se você não tiver nenhuma dessas contas, poderá criar um conta Microsoft gratuitamente clicando no link sob o botão de entrada. Se você estiver tendo problemas, consulte [Como fazer inscrever-se para um conta Microsoft?](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)

2. Escolha as configurações de interface do usuário e o tema de cor que você deseja usar Visual Studio. O Visual Studio se lembra essas configurações e sincroniza-as em todos os ambientes do Visual Studio nos quais você entrou. Para ver uma lista das configurações sincronizadas, consulte [Configurações sincronizadas.](../ide/synchronized-settings-in-visual-studio.md) Você poderá alterar as configurações posteriormente se abrir o menu **Opções**  >  **de** Ferramentas no Visual Studio.
   Depois de fornecer as configurações, o Visual Studio é iniciado, e você está conectado e pronto para começar. 
   
1. Para verificar se você entrou, procure seu nome de perfil no canto superior direito do ambiente do Visual Studio.

![Usuário conectado atualmente no VS2019](../ide/media/vs2019_username.png)

Se você optar por não entrar quando abrir o Visual Studio, será fácil fazer isso mais tarde. Procure o link **Entrar** no canto superior direito do Visual Studio ambiente.

![Usuário não assinado](../ide/media/vs2019_usernotsignedin.png)

A menos que você se desconecte, você será conectado automaticamente ao Visual Studio sempre que o iniciar, e todas as alterações nas configurações sincronizadas são aplicadas automaticamente. Para sair, clique no ícone com o nome do perfil no canto superior direito do ambiente Visual Studio, escolha o comando **Configurações da** conta e, em seguida, escolha o **link** Sair. Para entrar novamente, escolha o comando **Entrar** no canto superior direito do ambiente do Visual Studio.

## <a name="update-your-profile"></a>Atualizar seu perfil

1. Acesse **Configurações**  >  **da Conta de Arquivo** e escolha o link Gerenciar Visual Studio **perfil.**

1. Na janela do navegador, escolha **Editar perfil** e altere as configurações desejadas.

1. Quando terminar, escolha **Salvar alterações**.

## <a name="troubleshooting"></a>Solução de problemas

Consulte a [página Suporte à](https://visualstudio.microsoft.com/subscriptions/support/) assinatura para obter ajuda.

## <a name="see-also"></a>Confira também

* [Estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md)
* [Trabalhar com contas do GitHub no Visual Studio](../ide/work-with-github-accounts.md)
* [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md)

---
title: Entrar
description: entre no Visual Studio para estender o período de avaliação Visual Studio, desbloquear Visual Studio e muito mais
ms.custom: contperf-fy21q1
ms.date: 09/11/2020
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4b4c91a2ff4693b62ce8ac4d40d493995c52b81b
ms.sourcegitcommit: 4e09130bcd55bb9cb8ad157507c23b67aa209fad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113549466"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>entrar no Visual Studio em Windows 

Embora você não precise entrar, há muitas vantagens para fazer isso. neste artigo, você aprenderá [como entrar](#how-to-sign-in), como [atualizar seu perfil](#update-your-profile)e os benefícios para sua experiência de Visual Studio. 

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in).

::: moniker range="vs-2017"

> [!WARNING]
> para trabalhar com recursos configurados para acesso condicional, atualize para Visual Studio 2019 atualização 16,6 ou posterior. para obter mais informações, consulte [como usar Visual Studio com contas que exigem autenticação multifator](work-with-multi-factor-authentication.md).
> usar Visual Studio 2017 para acessar os recursos configurados para acesso condicional pode disparar uma experiência de autenticação degradada, solicitando a reautenticação várias vezes na mesma sessão de Visual Studio. 
> 
::: moniker-end

Veja uma lista completa do que é possível esperar e fazer após entrar:

|Benefício|Descrição|
|---|---|
|estender o período de avaliação do Visual Studio|Use Visual Studio Professional ou Visual Studio Enterprise **por mais 90 dias**, em vez de ser limitado ao período de avaliação de 30 dias. <br/>Consulte [estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md).|
|desbloquear Visual Studio (Visual Studio assinatura ou uma organização Azure DevOps)|Desbloquear o Visual Studio se você usar uma conta associada a uma Assinatura do Visual Studio ou a uma organização do Azure DevOps.<br/>Consulte [estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md).|
|sincronizar suas configurações de Visual Studio|Configurações que você personaliza, como associações de teclas, layout de janela e tema de cores, aplica-se imediatamente quando você entra no Visual Studio em qualquer dispositivo. <br/>Consulte [sincronizar configurações no Visual Studio](../ide/synchronized-settings-in-visual-studio.md).|
|Conectar-se automaticamente aos serviços|Conexão a serviços, como o Azure e Azure DevOps Services, no IDE sem solicitar novamente as credenciais para a mesma conta.|
|continuar usando a edição Visual Studio Community|se sua instalação do Community edition solicitar uma licença, entre no IDE para continuar usando o Visual Studio Community **gratuitamente**. |
|Obter ' Visual Studio Dev Essentials '|Este programa inclui ofertas de software gratuitas, treinamento, suporte e muito mais. <br/>consulte [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).|


## <a name="how-to-sign-in"></a>Como entrar 

ao abrir Visual Studio pela primeira vez, você será solicitado a entrar e fornecer algumas informações básicas de registro.

![Prompt de entrada](../ide/media/vs2019_signinpopup.png)

1. Escolha um conta Microsoft ou uma conta corporativa ou de estudante que melhor represente você. Se você não tiver nenhuma dessas contas, poderá criar um conta Microsoft gratuitamente clicando no link sob o botão entrar. Se você tiver problemas, consulte [como fazer inscrever-se em um conta Microsoft?](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)

2. Escolha as configurações de interface do usuário e o tema de cor que você deseja usar em Visual Studio. O Visual Studio se lembra essas configurações e sincroniza-as em todos os ambientes do Visual Studio nos quais você entrou. Para obter uma lista das configurações que são sincronizadas, consulte [configurações sincronizadas](../ide/synchronized-settings-in-visual-studio.md). você poderá alterar as configurações mais tarde se abrir o   >  menu **opções** de ferramentas no Visual Studio.
   Depois de fornecer as configurações, o Visual Studio é iniciado, e você está conectado e pronto para começar. 
   
1. Para verificar se você entrou, procure seu nome de perfil no canto superior direito do ambiente do Visual Studio.

![Usuário conectado no momento no VS2019](../ide/media/vs2019_username.png)

se você optar por não entrar ao abrir o Visual Studio pela primeira vez, será fácil fazer isso mais tarde. procure o link **entrar** no canto superior direito do ambiente de Visual Studio.

![Usuário não conectado](../ide/media/vs2019_usernotsignedin.png)

A menos que você se desconecte, você será conectado automaticamente ao Visual Studio sempre que o iniciar, e todas as alterações nas configurações sincronizadas são aplicadas automaticamente. para sair, clique no ícone com o nome do seu perfil no canto superior direito do ambiente de Visual Studio, escolha o comando **configurações de conta** e, em seguida, escolha **o link sair** . Para entrar novamente, escolha o comando **Entrar** no canto superior direito do ambiente do Visual Studio.

## <a name="update-your-profile"></a>Atualizar seu perfil

1. vá para a conta de **arquivo**  >  **Configurações** e escolha o link **gerenciar perfil de Visual Studio** .

1. Na janela do navegador, escolha **Editar perfil** e altere as configurações desejadas.

1. Quando terminar, escolha **Salvar alterações**.

## <a name="troubleshooting"></a>Solução de problemas

Consulte a página de [suporte à assinatura](https://visualstudio.microsoft.com/subscriptions/support/) para obter ajuda.

---
title: Entrar no Visual Studio
titleSuffix: ''
ms.custom: seodec18
ms.date: 03/10/2020
ms.topic: conceptual
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85d4be9ffd8d1f5ccc6c6d1a1ba5f83e7f0fccf6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285290"
---
# <a name="sign-in-to-visual-studio"></a>Entrar no Visual Studio

Você pode personalizar e otimizar sua experiência de desenvolvimento no Visual Studio entrando em sua conta de personalização.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in).

::: moniker range="vs-2017"

> [! AVISO] usar o Visual Studio 2017 para acessar os recursos configurados para acesso condicional pode disparar uma experiência de autenticação degradada, solicitando a reautenticação várias vezes na mesma sessão do Visual Studio. 
> Para trabalhar com recursos configurados para acesso condicional, atualize para o Visual Studio 2019 atualização 16,6 ou posterior. Para obter mais informações, consulte [como usar o Visual Studio com contas que exigem autenticação multifator](work-with-multi-factor-authentication.md).

::: moniker-end

## <a name="why-should-i-sign-in-to-visual-studio"></a>Por que devo me registrar no Visual Studio?

Quando você entrar, enriquecerá sua experiência no Visual Studio. Por exemplo, depois de entrar, você poderá [sincronizar as configurações](synchronized-settings-in-visual-studio.md) entre dispositivos, estender uma avaliação e se conectar automaticamente a um serviço do Azure, para citar apenas alguns.

Veja uma lista completa do que é possível esperar e fazer após entrar:
- **Estender o período de avaliação gratuita do Visual Studio** – É possível usar o Visual Studio Professional ou o Visual Studio Enterprise por um período adicional de 90 dias, em vez ficar limitado ao período de avaliação gratuita de 30 dias. Para obter mais informações, consulte [estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md).

- **Desbloquear o Visual Studio Community Edition** – Se a instalação do Community Edition solicitar uma licença, entre no IDE para desbloqueá-la.

- **Desbloquear o Visual Studio se você usar uma conta associada a uma Assinatura do Visual Studio ou a uma organização do Azure DevOps**. Para obter instruções detalhadas, consulte [estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md).

- **Acesso ao programa de Visual Studio dev Essentials** – este programa inclui ofertas de software gratuitas, treinamento, suporte e muito mais. Para obter mais informações, consulte [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).

- **Sincronizar as configurações do Visual Studio** – As configurações que você personaliza, como associações de teclas, layout da janela e tema de cores, são aplicadas imediatamente quando você entra no Visual Studio em qualquer dispositivo. Consulte [sincronizar configurações no Visual Studio](../ide/synchronized-settings-in-visual-studio.md).

- **Conectar-se automaticamente a serviços como o Azure e o Azure DevOps Services** no IDE sem solicitar credenciais da mesma conta novamente.

## <a name="how-to-sign-in-to-visual-studio"></a>Como entrar no Visual Studio

Ao abrir o Visual Studio pela primeira vez, você será solicitado a entrar e fornecer algumas informações básicas de registro. 

![Prompt de entrada](../ide/media/vs2019_signinpopup.png)

Você deve escolher uma conta da Microsoft ou uma conta corporativa ou de estudante que melhor lhe representa. Se você não tiver nenhuma dessas contas, poderá criar um conta Microsoft gratuitamente clicando no link sob o botão entrar. Se você tiver problemas, consulte [como fazer inscrever-se em um conta Microsoft?](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)

Em seguida, escolha as configurações da interface de usuário e o tema de cor que você deseja usar no Visual Studio. O Visual Studio se lembra essas configurações e sincroniza-as em todos os ambientes do Visual Studio nos quais você entrou. Para obter uma lista das configurações que são sincronizadas, consulte [configurações sincronizadas](../ide/synchronized-settings-in-visual-studio.md). Você poderá alterar as configurações mais tarde se abrir o **Tools**  >  menu**Opções** de ferramentas no Visual Studio.

Depois de fornecer as configurações, o Visual Studio é iniciado, e você está conectado e pronto para começar. Para verificar se você entrou, procure seu nome de perfil no canto superior direito do ambiente do Visual Studio.

![Usuário conectado no momento no VS2019](../ide/media/vs2019_username.png)

Se você optar por não entrar ao abrir o Visual Studio pela primeira vez, será fácil fazer isso mais tarde. Procure o link **entrar** no canto superior direito do ambiente do Visual Studio. 

![Usuário não conectado](../ide/media/vs2019_usernotsignedin.png)

A menos que você se desconecte, você será conectado automaticamente ao Visual Studio sempre que o iniciar, e todas as alterações nas configurações sincronizadas são aplicadas automaticamente. Para sair, clique no ícone com o nome do seu perfil no canto superior direito do ambiente do Visual Studio, escolha o comando **configurações de conta** e, em seguida, escolha **o link sair** . Para entrar novamente, escolha o comando **Entrar** no canto superior direito do ambiente do Visual Studio.

## <a name="to-change-your-profile-information"></a>Para alterar as informações do perfil

1. Vá para **arquivo**  >  **configurações de conta** e escolha o link **Gerenciar perfil do Visual Studio** .

1. Na janela do navegador, escolha **Editar perfil** e altere as configurações desejadas.

1. Quando terminar, escolha **Salvar alterações**.

## <a name="troubleshooting"></a>Solução de problemas

Se você encontrar problemas ao entrar, consulte a página de [suporte à assinatura](https://visualstudio.microsoft.com/subscriptions/support/) para obter ajuda.

## <a name="see-also"></a>Veja também

* [Estender uma versão de avaliação ou atualizar uma licença](../ide/how-to-unlock-visual-studio.md)
* [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md)
* [Entrar (Visual Studio para Mac)](/visualstudio/mac/signing-in)
* [Ativação (Visual Studio para Mac)](/visualstudio/mac/activation)

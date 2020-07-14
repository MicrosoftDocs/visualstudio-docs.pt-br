---
title: Configurar um agente de teste
ms.date: 09/18/2018
ms.topic: how-to
helpviewer_keywords:
- agents, configuring for interaction with desktop
ms.assetid: 3a94dd07-6d17-402c-ae8f-7947143755c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 994d5da8af7b00ab8af55681d4a67e9681ebbde6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287526"
---
# <a name="how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop"></a>Como configurar o agente de teste para executar testes que interagem com a área de trabalho

::: moniker range="vs-2017"
Se desejar executar testes automatizados que interajam com a área de trabalho, configure o agente para ser executado como um processo em vez de um serviço. Por exemplo, se você desejar executar um teste de IU codificado remotamente usando um controlador de teste e um agente de teste ou se desejar executar um teste e capturar uma gravação de vídeo ao executá-lo, será preciso configurar o agente para ser executado como um processo. Quando você atribui agentes a funções nas configurações de teste usando o Visual Studio ou atribui agentes a funções no seu ambiente usando o Microsoft Test Manager, é preciso alterar a configuração para todos os agentes atribuídos às funções que têm que interagir com a área de trabalho.
::: moniker-end
::: moniker range=">=vs-2019"
Se desejar executar testes automatizados que interajam com a área de trabalho, configure o agente para ser executado como um processo em vez de um serviço. Por exemplo, se você desejar executar um teste de IU codificado remotamente usando um controlador de teste e um agente de teste ou se desejar executar um teste e capturar uma gravação de vídeo ao executá-lo, será preciso configurar o agente para ser executado como um processo. Ao atribuir agentes a funções em suas configurações de teste usando o Visual Studio, você deve alterar a configuração de todos os agentes atribuídos a funções que precisam interagir com a área de trabalho.
::: moniker-end

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

::: moniker range="vs-2017"
> [!WARNING]
> Se você usar o Microsoft Test Manager para configurar um ambiente de laboratório, ele instalará o agente de teste. No **Assistente para Criação de Ambiente**, especifique que você deseja configurar uma das funções para executar testes de IU codificados.
:::moniker-end

> [!IMPORTANT]
> O computador que está executando um agente no qual você deseja executar testes de IU codificados não pode ser bloqueado nem ter um protetor de tela ativo.

Se você estiver executando testes de IU codificados que iniciem um navegador, a conta de serviço do agente de teste será usada para iniciar o navegador. Essa conta de serviço deve ser a mesma que a conta de usuário que é o usuário ativo nesse computador. Se não for a mesma conta de usuário, o navegador não será iniciado.

> [!IMPORTANT]
> Se você estiver executando um teste de IU codificado que inicie um navegador como parte de uma definição de compilação, a conta de serviço do serviço de compilação será usada para iniciar o navegador. Essa conta de serviço deve ser a mesma que a conta de usuário que é o usuário ativo nesse computador. Se não for a mesma conta de usuário, o navegador não será iniciado.

Use o procedimento a seguir para configurar todos os agentes que são atribuídos a uma função que executa uma tarefa que precisa interagir com a área de trabalho.

## <a name="to-set-up-an-agent-to-run-as-a-process"></a>Para configurar um agente para ser executado como um processo

1. Para configurar o agente de teste que você instalou para executar como um processo, vá para **Iniciar**  >  **ferramenta de configuração do agente de teste**.

   A caixa de diálogo **Configurar Agente de Teste** é exibida.

   ![Configurar Agente de teste para o Visual Studio](media/configure-test-agent.png)

2. Selecione **Processo Interativo**. O agente de teste será iniciado como um processo, e não como um serviço. Escolha **Próxima**.

3. Insira o nome de usuário e a senha do usuário que executará o processo do agente de teste.

   > [!NOTE]
   > - O usuário que você adiciona para iniciar o processo também deve ser adicionado como um membro do grupo TeamTestAgentService no computador do controlador de teste para esse agente. Se esse for o usuário atual, quando você adicioná-lo ao computador do controlador de teste, será preciso fazer logoff ou reiniciar o computador.
   > - As senhas nulas não são compatíveis com contas de usuário.
   > - Se você quiser usar o IntelliTrace ou os dados da emulação de rede e o adaptador de diagnóstico, a conta de usuário deverá ser um membro do grupo Administradores. Se o computador que está executando o agente de teste estiver usando um sistema operacional que tenha uma conta de usuário com privilégios mínimos, você também precisará executá-lo como um administrador (elevado). Se o nome de usuário do agente não estiver no serviço de agente, ele tentará adicioná-lo, o que requer permissões no controlador de teste.
   > - O usuário que tentar usar o controlador de teste deverá estar na conta Usuários do controlador de teste ou não poderá executar os testes relacionados ao controlador.

4. Para ter certeza de que um computador que tem um agente de teste pode executar testes após ser reinicializado, você pode configurar o computador para fazer logon automaticamente como usuário do agente de teste. Selecione **Fazer logon automaticamente**. Isso armazenará o nome de usuário e a senha em um formato criptografado no Registro.

   > [!NOTE]
   > Quando você está conectado ao ambiente de laboratório usando uma área de trabalho remota ou uma conexão baseada em convidado, talvez se depare com desconexões frequentes e inesperadas. Uma possível causa da perda de conexão é que o computador esteja configurado para acessar automaticamente a rede.

5. Para garantir que a proteção de tela esteja desabilitada, uma vez que isso pode interferir em todos os testes automatizados que devem interagir com a área de trabalho, selecione **Certifique-se de que a proteção de tela está desabilitada**.

   > [!WARNING]
   > Haverá riscos à segurança se você fizer logon automaticamente ou desabilitar a proteção de tela. Ao ativar o logon automático, você permite que outros usuários iniciem esse computador e permite que eles usem a conta que faz logon automaticamente. Se você desabilitar a proteção de tela, o computador talvez não solicite o logon de um usuário para desbloquear o computador. Isso permite que qualquer pessoa acesse o computador se ela tiver acesso físico a ele. Se habilitar esses recursos em um computador, você deverá verificar se esses computadores estão fisicamente seguros. Por exemplo, esses computadores estão localizados em um laboratório fisicamente seguro. Se você desmarcar **garantir que a proteção de tela está desabilitada**, isso não habilitará a proteção de tela.

   Para que o agente volte a ser executado como um serviço, você pode usar essa ferramenta e selecionar **Serviço**.

6. Para aplicar suas alterações, escolha **Aplicar Configurações**.

   É exibida uma caixa de diálogo **Resumo da configuração** que mostra o status de cada uma das etapas para configurar o agente de teste.

7. Para fechar a caixa de diálogo **Resumo da configuração**, escolha **Fechar**. Em seguida, escolha **Fechar** novamente para fechar a **Ferramenta de Configuração do Test Agent**.

   > [!NOTE]
   > Há um ícone da área de notificação que é executado no computador para um agente de teste que está sendo executado como um processo. Ele mostra o status do agente de teste. Você poderá iniciar, parar ou reiniciar o agente se ele estiver sendo executado como um processo usando essa ferramenta. Para iniciar o agente de teste como um processo, se ele não estiver em execução, escolha **Iniciar**o  >  **Visual Studio**  >  **Microsoft Visual Studio agente de teste**.

   ::: moniker range="vs-2017"
   Se o controlador de teste para o agente de teste estiver registrado no Team Foundation Server, o status de um agente de teste que estiver sendo executado como um processo interativo será exibido no modo de exibição **Controladores** na **Central do Laboratório** do Microsoft Test Manager. Ele é listado com um símbolo de asterisco precedente para denotar que está sendo executado como um processo interativo. Para reiniciar o agente de teste, você deve usar a ferramenta que é executada no computador para o agente de teste e não o modo de exibição **Controladores**.
   ::: moniker-end

## <a name="see-also"></a>Veja também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)

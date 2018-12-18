---
title: Gerenciar controladores e agentes de teste no Visual Studio
ms.date: 09/18/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 48c377a8a5c48db7e0726ab5d5cc238e6b83c71c
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895282"
---
# <a name="manage-test-controllers-and-test-agents"></a>Gerenciar controladores e agentes de teste

Se quiser usar o Visual Studio para executar testes remotamente, distribuir testes entre várias máquinas ou executar testes de carga, você deverá configurar um controlador de teste, agentes de teste e um arquivo de configurações de teste. Este tópico descreve como gerenciar controladores e agentes de teste depois de instalá-los e configurá-los pela primeira vez.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Se você usa o Microsoft Test Manager para executar testes em ambientes de laboratório, você gerencia controladores de teste e seus agentes usando o **Gerenciador do Controlador de Teste** na **Central do Laboratório** para o Microsoft Test Manager. Este tópico só será aplicável se você usar o Visual Studio para executar testes.

Para obter informações sobre como instalar e configurar agentes de teste e controladores de teste para executar testes no Visual Studio, consulte [Configurar agentes e controladores de teste](../test/configure-test-agents-and-controllers-for-load-tests.md).

Para configurar e monitorar o controlador de teste e quaisquer agentes registrados, você tem que ter um arquivo de configurações de teste no seu projeto de teste, que contenha os testes que deseja executar. Abra o arquivo de configurações de teste, selecione **Função**, em seguida, **Gerenciar Controladores de Teste** no menu suspenso do campo **Controlador**.

Para um projeto de teste de carga, você também pode selecionar **Gerenciar Controladores de Teste** no menu **Teste de Carga**.

## <a name="add-a-test-agent-to-a-test-controller"></a>Adicionar um agente de teste a um controlador de teste

Você talvez queira adicionar um agente de teste a um controlador de teste diferente ou tenha que adicionar um agente de teste a um controlador de teste que acabou de instalar.

### <a name="to-add-a-test-agent-to-a-test-controller"></a>Para adicionar um agente de teste a um controlador de teste

1. Escolha **Iniciar** > **Ferramenta de Configuração do Test Agent**.

     A caixa de diálogo **Configurar Agente de Teste** é exibida.

    > [!NOTE]
    > Você deve ter um agente de teste já instalado para adicioná-lo a um controlador de teste. Para obter mais informações de como instalar um agente de teste, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

2. São apresentadas duas opções para executar o agente de teste:

   - **Serviço**: se você não precisar executar testes automatizados que interajam com a área de trabalho, como testes de IU codificados ou a criação de uma gravação de vídeo quando o teste for executado, em **Executar o agente de teste como**, selecione **Serviço**. O agente de teste será iniciado como um serviço. Escolha **Avançar**.

      Agora você pode inserir os detalhes sobre o usuário quando inicia o agente de teste como um serviço.

      1. Insira o nome em **Nome de usuário**.

      2. Insira a senha em **Senha**.

        |**Informações importantes sobre a conta de usuário**|
        |-|
        |– Senhas nulas não têm suporte com contas de usuário.|
        |– Se você quiser usar o coletor IntelliTrace ou a emulação de rede, a conta de usuário deverá ser um membro do grupo Administradores.|
        |– Se o nome de usuário do agente não estiver no serviço de agente, ele tentará adicioná-lo, o que requer permissões no controlador de teste.|
        |– O usuário que está tentando usar o controlador de teste deve estar na conta Usuários do controlador de teste ou não poderá executar os testes no controlador.|

   - **Processo interativo**: se você desejar executar testes automatizados que precisem interagir com a área de trabalho, como testes de IU codificados ou a criação de uma gravação de vídeo durante as execuções de teste, selecione **Processo Interativo**. O agente de teste será iniciado como um processo interativo, em vez de um serviço.

      Na página seguinte, insira os detalhes sobre o usuário quando o agente de teste iniciar como um processo e outras opções.

      1. Insira o nome em **Nome de usuário**.

      2. Insira a senha em **Senha**.

        > [!NOTE]
        > Se configurar o agente de teste para ser executado como um processo interativo com um usuário diferente do usuário atualmente ativo, você deverá reiniciar o computador e fazer logon como esse usuário diferente para poder iniciar o agente. Além disso, as senhas nulas não são compatíveis com contas de usuário. Se você quiser usar o coletor IntelliTrace ou a emulação de rede, a conta de usuário deverá ser um membro do grupo Administradores.

      3. Para garantir que um computador com um agente de teste possa executar testes após ser reinicializado, você pode configurar o computador para fazer logon automaticamente como o usuário do agente de teste. Selecione **Fazer logon automaticamente**. Isso armazenará o nome de usuário e a senha em um formato criptografado no Registro.

      4. Para garantir que a proteção de tela esteja desabilitada, uma vez que isso pode interferir em todos os testes automatizados que devem interagir com a área de trabalho, selecione **Certifique-se de que a proteção de tela está desabilitada**.

        > [!WARNING]
        > Haverá riscos à segurança se você fizer logon automaticamente ou desabilitar a proteção de tela. Ao ativar o logon automático, você permite que outros usuários iniciem esse computador e permite que eles usem a conta que faz logon automaticamente. Se você desabilitar a proteção de tela, o computador talvez não solicite o logon de um usuário para desbloquear o computador. Isso permite que qualquer pessoa acesse o computador se ela tiver acesso físico a ele. Se habilitar esses recursos em um computador, você deverá verificar se esses computadores estão fisicamente seguros. Por exemplo, esses computadores estão localizados em um laboratório fisicamente seguro. (Se você desmarcar **Certifique-se de que a proteção de tela está desabilitada**, isso não habilitará a proteção de tela.)

3. Para registrar esse agente com um controlador de teste diferente, marque **Registrar com controlador de teste.** Digite o nome do seu controlador de teste seguido de **:** e o número da porta que você está usando em **Registrar este agente de teste com o controlador de teste a seguir**. Por exemplo, digite **agent1:6901**.

    > [!NOTE]
    > O número de porta padrão é 6901.

4. Para salvar suas alterações, escolha **Aplicar Configurações**. Feche a caixa de diálogo **Resumo da configuração** e, em seguida, feche a **Ferramenta de Configuração do Test Agent**.

> [!WARNING]
> Se o agente estiver configurado atualmente para ser executado em outro controlador de teste, você deverá remover o agente de teste desse controlador.

## <a name="remove-a-test-agent-from-a-test-controller"></a>Remover um agente de teste de um controlador de teste

Um agente de teste deve ser definido para o estado offline antes de ser removido.

> [!NOTE]
> Você não pode usar este procedimento para remover agentes registrados em um controlador como parte de um ambiente de laboratório. Para remover esses agentes de um controlador, você precisa remover o ambiente usando o Microsoft Test Manager.

### <a name="to-remove-a-test-agent-from-a-test-controller"></a>Para excluir um agente de teste de um controlador de teste

1. Se o controlador de teste não estiver registrado em um projeto, siga estas etapas.

    1. No Visual Studio, abra o arquivo de configurações de teste do seu projeto de teste, selecione **Função**, em seguida, **Gerenciar Controladores de Teste** no menu suspenso do campo **Controlador**.

         A caixa de diálogo **Administrar Controlador de Teste** é exibida.

    2. Na lista suspensa **Controlador**, digite o nome do computador no qual você instalou o controlador de teste. Se tiver administrado um controlador de teste específico anteriormente, você poderá selecionar o nome na lista.

    3. No painel **Agentes**, selecione o nome do agente de teste. Se o agente ainda estiver online, escolha **Offline**. Para removê-lo, clique em **Remover**.

        > [!NOTE]
        > Remover um agente de teste apenas o desassocia do controlador de teste. Para desinstalar completamente o agente de teste, use **Programas e Recursos** do Painel de Controle no computador do agente de teste.

2. Se o controlador de teste estiver registrado com um projeto, remova o agente usando o Microsoft Test Manager.

## <a name="change-the-settings-for-a-test-agent"></a>Alterar as configurações de um agente de teste

O status do agente de teste pode ser qualquer um dos seguintes valores:

|Status|Descrição|
|-|-----------------|
|Executando teste|Executando testes|
|Pronto|Disponível para executar testes ou coletar dados e diagnóstico|
|Offline|Indisponível para executar testes ou coletar dados e diagnósticos|
|Desconectado|O agente de teste não foi iniciado|

Você pode alterar o status e outras configurações para um agente de teste que usa os seguintes procedimentos.

### <a name="to-change-the-settings-of-a-test-agent"></a>Para alterar as configurações de um agente de teste

> [!NOTE]
> Se o agente de teste estiver registrado em um controlador de teste registrado em um projeto, altere as configurações no Microsoft Test Manager.

1. Para configurar e monitorar o controlador de teste e quaisquer agentes registrados de um teste de carga, selecione o menu **Teste de Carga** no Visual Studio e escolha **Gerenciar Controladores de Teste**. Para quaisquer outros testes, abra o arquivo de configurações de teste do seu projeto de teste no Visual Studio, selecione **Função**, em seguida, **Gerenciar Controladores de Teste** no menu suspenso do campo **Controlador**.

   A caixa de diálogo **Gerenciar Controlador de Teste** é exibida.

1. Selecione o nome do controlador de teste cujos agentes de teste você deseja alterar na lista de controladores de teste. Se o controlador de teste não aparecer na lista, verifique se o controlador de teste está registrado corretamente. Para obter mais informações, consulte o procedimento a seguir sobre como configurar um controlador de teste.

1. (Opcional) No painel **Agentes de Teste**, selecione o computador do agente de teste cujas propriedades você deseja alterar.

1. Escolha **Propriedades**.

1. Altere as seguintes propriedades do agente de teste conforme necessário:

|Propriedade do agente de teste|Descrição|
|-|-----------------|
|**Importância**|Usado para distribuir a carga quando você usa agentes de teste com níveis de desempenho diferentes. Por exemplo, um agente de teste com uma importância de 100 recebe duas vezes a carga como um agente de teste com uma importância de 50.|
|**Troca de IPs**|Usado para configurar a troca de IP. A troca de IP permite que um agente de teste envie solicitações para um servidor usando um intervalo de endereços IP. Isso simula chamadas que venham de computadores cliente diferentes.<br /><br /> A troca de IP será importante se seu teste de carga estiver acessando um Web farm. A maioria de balanceadores de carga estabelece afinidade entre um cliente e um servidor Web específico usando o endereço IP do cliente. Se todas as solicitações estiverem vindo aparentemente de um único cliente, o balanceador de carga não balanceará a carga. Para obter um bom balanceamento de carga no Web farm, verifique se as solicitações vêm de um intervalo de endereços IP. **Observação:** você pode especificar um adaptador de rede ou usar **(Todos sem não atribuídos)** para selecionar automaticamente um que não esteja sendo usado atualmente. <br /><br /> Para usar o recurso de troca de IP, o serviço Visual Studio Test Agent deve ser executado como um usuário do grupo Administradores do computador do agente. Esse usuário é selecionado durante a configuração do agente, mas pode ser alterado modificando-se as propriedades do serviço e reiniciando-o.<br /><br /> Para verificar se a troca de IP está funcionando corretamente, habilite o registro em log IIS no servidor Web, use a funcionalidade de registro em log IIS para verificar se as solicitações vêm dos endereços IP que configurados por você.|
|**Atributos**|Conjunto de pares de nome/valor que podem ser usados na seleção do agente de teste. Por exemplo, um teste pode exigir um sistema operacional específico. Você pode adicionar atributos na guia **Funções** do seu arquivo de configurações de teste e eles podem ser usados para selecionar um agente de teste que tenha atributos compatíveis. Se quiser executar um teste em vários computadores, crie um atributo na função de configurações de teste definida para executar seus testes e configure um atributo correspondente em cada agente de teste que você queira usar nessa função. **Observação:** essa configuração está disponível apenas para agentes de teste registrados em um controlador de teste que não está registrado em um projeto, pois esses atributos são usados somente nas configurações de teste do Visual Studio.|

As alterações de atributo e importância do agente de teste entram em vigor imediatamente, mas não afetam os testes que estão em execução. O Intervalo de Endereços IP entra em vigor depois que o controlador de teste é reiniciado.

(Opcional) Para alterar o status de um agente de teste, selecione o agente na lista e, em seguida, selecione a ação nas opções disponíveis com base no status atual do agente.

> [!NOTE]
> Se o agente de teste estiver sendo executado como um processo, você gerencia o status do agente de teste no ícone da área de notificação executado no computador em que seu agente de teste está instalado. Ele mostra o status do agente de teste. Você poderá iniciar, parar ou reiniciar o agente se ele estiver sendo executado como um processo usando essa ferramenta.

## <a name="configure-a-test-controller"></a>Configura um controlador de teste

Para configurar um controlador de teste, você deve usar a **Ferramenta de Configuração do Team Test Controller**. Ao configurar seu controlador de teste, você pode registrá-lo em uma coleção de projetos diferente ou cancelar o registro de seu controlador de teste de uma coleção de projetos.

Se quiser registrar seu controlador de teste em sua coleção de projetos do Team Foundation Server, a conta que você usa para o serviço do controlador de teste deverá ser membro do grupo Contas de Serviço de Teste de Coleção de Projeto da Coleção de Projeto ou a conta usada para executar a ferramenta de configuração do controlador de teste deverá ser um Administrador de Coleção de Projetos.

> [!NOTE]
> Se você cancelar o registro de um controlador de teste de uma coleção de projetos com ambientes existentes em uma coleção de projetos, os ambientes ainda serão mantidos se você tiver movido essa coleção de projetos e registrado novamente o controlador de teste na coleção de projetos movida.

### <a name="to-configure-a-test-controller"></a>Para configurar um controlador de teste

1. Para executar a ferramenta para reconfigurar o controlador de teste a qualquer momento, escolha **Iniciar** > **Ferramenta de Configuração do Controlador de Teste**.

     A caixa de diálogo **Configurar controlador de teste** é exibida.

2. Selecione o usuário a ser usado como a conta de logon para o serviço do controlador de teste.

    > [!NOTE]
    > As senhas nulas não são compatíveis com contas de usuário.

4. (Opcional) Se você não quiser usar o controlador de teste com um ambiente de laboratório, mas somente para executar testes do Visual Studio, desmarque **Registrar controlador de teste com Coleção de Projetos de Equipe**.

5. (Opcional) Para configurar seu controlador de teste para o teste de carga, selecione **Configurar controlador de teste para teste de carga**. Digite sua instância do SQL Server em **Criar banco de dados de resultados de teste de carga na seguinte instância de SQL Server**.

> [!NOTE]
> Para obter mais informações sobre solução de problemas de controladores de teste, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

## <a name="manage-your-agents-when-you-run-your-tests-with-a-test-controller"></a>Gerenciar os agentes ao executar testes com um controlador de teste

Ao adicionar funções para seu aplicativo às configurações de teste para Visual Studio, você pode adicionar propriedades de agente para cada uma de suas funções. Isso determina que agentes de teste estão disponíveis para essa função. Quando você executa seus testes usando essas configurações de teste, o controlador de teste que é selecionado para as configurações determina a disponibilidade de agentes necessários. Estas são as seguintes situações que podem ocorrer quando a disponibilidade do agente é determinada:

-   Não há nenhum agente disponível para a função que deve executar os testes. Seus testes não podem ser executados. Você pode executar uma das seguintes ações e executar novamente seus testes:

    -   Você pode esperar um agente para ficar disponível para essa função para executar os testes.

    -   Se houver qualquer agente que esteja offline que possa ser usado para esta função, você poderá reiniciar o agente para que ele fique disponível.

    -   Você pode adicionar outro agente com as propriedades corretas de agente para essa função ao controlador de teste.

    -   Você pode alterar as propriedades do agente para esta função nas configurações de teste para ativar outros agentes que deseja usar.

-   Não há nenhum agente disponível para uma ou mais funções que executam adaptadores de dados de diagnóstico. Os testes podem ser executados, mas o adaptador de dados de diagnóstico não pode ser executado. Você pode executar seus testes sem o adaptador de dados de diagnóstico, ou pode executar uma das seguintes ações e executar novamente seus testes:

    -   Você pode esperar um agente ficar disponível para essas funções.

    -   Se houver qualquer agente que esteja offline e que possa ser usado para esta função, você deverá alterar o estado do agente para online de **Administrar Controlador de Teste** no menu **Testar**. Além disso, você poderá ter que reiniciar o agente se ele tiver sido desconectado do controlador.

    -   Certifique-se de que nenhum agente que você possa precisar para esta execução de teste esteja ocupado executando testes. Você pode verificar o status de todos os agentes de **Administrar Controlador de Teste** no menu **Testar**.

    -   Você pode adicionar outro agente com as propriedades corretas de agente para a função ao controlador de teste.

    -   Você pode alterar as propriedades do agente para a função nas configurações de teste para ativar outros agentes que deseja usar.

## <a name="load-tests-from-delay-signed-assemblies"></a>Carregar testes de assemblies assinados com atraso

O controlador de teste e os agentes de teste podem apenas carregar assemblies de teste que tenham assinatura forte, ou assemblies sem assinatura. Alguns assemblies de teste são assinados com atraso porque precisam ter acesso aos assemblies de produção do aplicativo. No entanto, esses assemblies não são fortemente assinados porque são apenas assemblies de teste e não são distribuídos. Esses assemblies não podem ser carregados porque foram assinados com atraso, portanto você deve desabilitar a verificação de nome forte para esses assemblies em todos os computadores em que eles serão carregados, incluindo o computador do controlador de teste. Para desabilitar a verificação assinada com atraso, use *sn.exe*. O token de chave pública do assembly assinado com atraso para o qual a verificação de nome forte é solicitada para ser ignorada também pode precisar ser incluído.

Use *Sn.exe* (ferramenta Nome Forte) para desabilitar a verificação assinada com atraso.

Isso desabilita a verificação de nome forte, para o conjunto especificado apenas, no computador em que você executa o comando. Você só poderá fazer isso se tiver permissões suficientes.

Após a execução de teste, habilite novamente a verificação de assinatura atrasada usando o comando do *SN.exe*.

Uma maneira recomendada de desabilitar e habilitar novamente a verificação de assinatura é usar os comandos do *SN.exe* nos scripts. Você pode desabilitar a verificação em um script de configuração e reativar a verificação em um script de limpeza.

## <a name="see-also"></a>Consulte também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
---
title: Criar uma configuração de teste para um teste de carga distribuída
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, for distributed load tests
ms.assetid: b63d4b71-3b74-4872-b2d1-f0bd1a9a8544
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9f8cb4c3c2cba9f7734aa50c95f28bb6cef6bcba
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55928875"
---
# <a name="how-to-create-a-test-setting-for-a-distributed-load-test"></a>Como: Criar uma configuração de teste para um teste de carga distribuída

Defina *configurações de teste* para seus testes de carga para que você possa distribuir esses testes entre vários computadores usando agentes e controladores de teste. Também é possível definir configurações de teste para usar *adaptadores de dados de diagnóstico*, que especificam os tipos de dados que você deseja coletar ou como afetar os computadores de teste quando você executa testes de carga com o Visual Studio.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Por exemplo, você pode usar o adaptador de dados de diagnóstico do Criador de Perfis do ASP.NET para coletar a divisão de desempenho de código. Além disso, os adaptadores de dados de diagnóstico podem ser usados para simular possíveis gargalos no computador de teste ou para reduzir a memória disponível do sistema.

As configurações de teste do Visual Studio são armazenadas em um arquivo. As configurações de teste definem as seguintes informações sobre cada função:

-   O conjunto de funções que são necessárias para seu aplicativo em teste

-   A função a ser usada para executar seus testes

-   Os adaptadores de dados de diagnóstico a serem usados para cada função

Ao executar seus testes, você seleciona as configurações de teste para usar como as configurações ativas de teste, dependendo do que você precisa para essa execução específica de teste. O arquivo de configurações de teste é armazenado como parte de sua solução. O nome do arquivo tem a extensão *.testsettings*.

Ao adicionar um projeto de teste de carga e desempenho na Web a uma solução, um arquivo *Default.testsettings* é criado. O arquivo é automaticamente adicionado à solução na pasta **Itens de Solução**. Este arquivo executa seus testes localmente sem adaptadores de dados de diagnóstico. É possível adicionar ou editar um arquivo *.testsettings* para especificar adaptadores de dados de diagnóstico e controladores de teste.**

O controlador de teste terá agentes que podem ser usados para cada função nas configurações de teste. Para obter mais informações sobre controladores e agentes de teste, confira [Gerenciar controladores e agentes de teste com o Visual Studio](../test/manage-test-controllers-and-test-agents.md).

Siga estas etapas para criar e remover configurações de teste em sua solução para testes de carga que você pretende executar do Visual Studio.

## <a name="create-a-test-setting-for-a-distributed-load-test"></a>Criar uma configuração de teste para um teste de carga distribuída

### <a name="to-add-a-test-settings-for-a-distributed-load-test"></a>Para adicionar configurações de teste para um teste de carga distribuído

1.  Na **Gerenciador de Soluções**, clique com o botão direito do mouse em **Itens da Solução**, aponte para **Adicionar** e, em seguida, escolha **Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** é exibida.

2.  No painel **Modelos Instalados**, escolha **Configurações de Teste**.

3.  (Opcional) Na caixa de **Nome**, altere o nome do arquivo de configurações de teste.

4.  Escolha **Adicionar**.

     O novo arquivo de configurações de teste é exibido no **Gerenciador de Soluções**, na pasta **Itens da Solução**.

    > [!NOTE]
    > A lista de configurações de teste que o Visual Studio Enterprise exibe é derivada da lista de arquivos de configurações de teste na pasta **Itens de Solução**. Por exemplo, os arquivos de configurações de teste da pasta **Itens da Solução** são exibidos quando você usa a opção **Selecionar Configurações de Teste Ativo** no menu **Testar**. Isso significa que se você mover um arquivo de configurações de teste para outro local na sua hierarquia de solução, ele não poderá mais ser usado como uma configuração de teste no ambiente de desenvolvimento integrado do Visual Studio.

5.  A caixa de diálogo **Configurações de Teste** é exibida. A página **Geral** está selecionada.

     Agora você pode editar e salvar valores das configurações de teste.

    > [!NOTE]
    > Cada configuração de teste que você cria é listada como uma escolha para as opções **Selecionar Configurações de Teste Ativo** e **Editar Configurações de Teste** no menu **Teste**.

6.  Em **Nome**, digite o nome das configurações de teste.

7.  (Opcional) Em **Descrição**, digite uma descrição para a configuração do teste para que outros membros da equipe saibam de sua finalidade.

8.  (Opcional) Para selecionar o esquema de nomenclatura padrão para seus ensaios, selecione **Esquema de nomenclatura padrão**. Para definir seus próprios esquema de nomeação, selecione **Esquema definido pelo usuário** e digite o texto que você deseja em **Texto de prefixo**. Para anexar o carimbo de data/hora ao nome da execução de teste, selecione **Acrescentar carimbo de data/hora**.

9. Escolha **Funções**.

     A página **Funções** é exibida.

     ![Função de configuração de teste](../test/media/load_testtestrole.png)

10. Para executar testes remotamente ou executar testes e coletar dados remotamente, use a lista suspensa **Método de execução de teste** e selecione **Execução remota**.

11. Use a lista suspensa **Controlador** para selecionar um controlador de teste para os agentes de teste do **Controlador** que será usado para executar seus testes ou coletar dados.

    > [!NOTE]
    > Se essa for a primeira vez que você está adicionando um controlador, nenhum controlador estará listado na lista suspensa. A lista é populada por controladores anteriores que você especificou em outras configurações de teste. Você deve digitar o nome do controlador na caixa (por exemplo, **TestControllerMachine1**).

12. Para adicionar as funções que você deseja usar para executar testes e coletar dados, em **Funções**, selecione **Adicionar**.

13. Digite um nome para a função na coluna **Nome**. Por exemplo, a função poderia ser "servidor Web".

14. Repita as etapas 12 e 13 para adicionar todas as funções necessárias.

     Cada função usa um agente de teste gerenciado pelo controlador de testes.

15. Selecione a função que você deseja para executar os testes e escolha **Definir como função para executar testes**.

    > [!IMPORTANT]
    > As outras funções que você cria e define não executarão testes, mas serão usadas somente para coletar dados de acordo com os dados e adaptadores de diagnóstico especificados para as funções na página **Dados e Diagnóstico**.

16. Para limitar os agentes que podem ser usados para uma função, selecione a função e, em seguida, escolha **Adicionar** na barra de ferramentas abaixo de **Atributos de agente para função selecionada**.

     A caixa de diálogo **Regra de Seleção de Agente** é exibida.

     Digite o nome em **Nome do Atributo** e o valor em **Valor do Atributo** e, em seguida, escolha **OK**. Adicione quantos atributos forem necessários.

     Por exemplo, você poderá adicionar um atributo denominado "RAM > 16GB" com um valor "True" ou "False" para filtrar os computadores do agente de teste que possuem mais de 16 GB de memória. Para aplicar o mesmo atributo a um ou mais agentes de teste, use a caixa de diálogo **Gerenciar Controlador de Teste**. Para obter mais informações, confira [Gerenciar controladores e agentes de teste com o Visual Studio](../test/manage-test-controllers-and-test-agents.md).

17. Escolha **Dados e Diagnósticos**.

     A página **Dados e Diagnósticos** é exibida.

     ![Dados e diagnósticos da configuração de teste](../test/media/load_testtest.png)

18. Na página **Dados e Diagnóstico**, você define o que a função realiza ao selecionar os *adaptadores de dados de diagnóstico* que a função usará para coletar dados. Portanto, se um ou mais adaptadores de dados e de diagnóstico forem habilitados para a função, o controlador de teste escolherá um computador agente de teste disponível para coletar dados para os dados especificados e adaptadores de diagnóstico baseados nos atributos que você definiu para a função. Para selecionar os dados e os adaptadores de dados de diagnóstico que você deseja coletar para cada função, selecione a função. Para cada função, selecione os adaptadores de dados de diagnóstico de acordo com as necessidades de teste. Para configurar cada adaptador de dados de diagnóstico que você selecionou para cada função, escolha **Configurar**.

     **Exemplo de funções e adaptadores de dados de diagnóstico:**

     Por exemplo, você poderá criar uma função de cliente denominada "Cliente de Área de Trabalho" que possui um atributo "Uses SQL" definido como "True" em uma função de servidor denominada "SQL Server" que possui um conjunto de atributo definido como "RAM > 16GB". Se você especificar que o "cliente de área de trabalho" executará testes escolhendo **Definir como função para executar testes** na página **Funções**, o controlador de teste selecionará máquinas que têm agentes de teste que incluam o atributo "Usa SQL" definido como "Verdadeiro" para executar os testes. O controlador de teste também selecionará computadores de SQL Server que possuem agentes de teste que incluem o atributo “RAM > 16GB” para coletar somente os dados que são definidos pelos dados e os adaptadores de diagnóstico incluídos na função. O agente de testes "Cliente da Área De Trabalho" também pode coletar dados para os computadores em que é executado se você selecionar dados e adaptadores de diagnóstico para essa função também.

     Para obter detalhes sobre cada adaptador de dados de diagnóstico e como configurá-lo, você pode exibir o tópico associado na tabela a seguir.

     Para obter mais informações sobre adaptadores de dados de diagnóstico, confira [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

     **Adaptadores de dados de diagnóstico para testes de carga**

    |Adaptador de dados de diagnóstico|Usado em testes de carga|Tópico associado|
    |-|-------------------------|-|
    |**Proxy de Cliente do ASP.NET para IntelliTrace e Impacto de Teste:** Esse proxy permite que você colete informações sobre as chamadas HTTP de um cliente para um servidor Web para os adaptadores de dados de diagnóstico do IntelliTrace e de Impacto de Teste.|![Ícone de informações](../test/media/vc364f4.gif)<br /><br /> A menos que você tenha uma necessidade específica de coletar informações do sistema para os computadores do agente de teste, não inclua este adaptador. **Cuidado:**  Não recomendamos o uso do adaptador IntelliTrace em testes de carga devido a problemas que ocorrem devido à grande quantidade de dados que são coletados. <br /><br /> Os dados do impacto de teste não são coletados usando testes de carga.||
    |**IntelliTrace:** Configure informações de rastreamento de diagnóstico específicas armazenadas em um arquivo de log. Um arquivo de log tem uma extensão *.tdlog*. Ao executar o teste e uma etapa falhar, você pode criar um bug. O arquivo de log que contém o rastreamento de diagnóstico que é anexado automaticamente a este bug. Os dados coletados no arquivo do log aumentam a produtividade de depuração reduzindo o tempo necessário para reproduzir e diagnosticar um erro no código. Deste arquivo de log, a sessão local pode ser recriada em outro computador. Isso reduz o risco de um bug não poder ser reproduzido.<br /><br /> Para obter mais informações, consulte [Coletar dados do IntelliTrace](../test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md).|![Ícone de importante](../test/media/vc364f3.gif)<br /><br /> Não recomendamos o uso do adaptador IntelliTrace em testes de carga devido a problemas que ocorrem devido à grande quantidade de dados que são coletados e registrados em log. Você deve tentar usar o adaptador de IntelliTrace somente em testes de carga que não são executados por muito tempo e não usam vários agentes de teste.|[Como: Coletar dados do IntelliTrace para ajudar a depurar problemas difíceis](../test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md)|
    |**Criador de Perfil do ASP.NET:** Crie uma configuração de teste que inclui a criação de perfis do ASP.NET, que coleta dados de desempenho em aplicativos Web ASP.NET.|O adaptador de dados de diagnóstico do criador de perfis do ASP.NET cria perfis do processo do IIS (Serviços de Informações da Internet), portanto ele não funcionará em um servidor Web de desenvolvimento. Para analisar o site no teste de carga, você precisa instalar um agente de teste no computador em que o IIS está sendo executado. O agente de teste não estará gerando carga, mas será um agente de coleção somente. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).|[Como: Configurar o criador de perfil do ASP.NET para carregar testes usando configurações de teste](../test/how-to-configure-aspnet-profiler-for-load-tests-using-test-settings.md)|
    |**Log de eventos:** Defina uma configuração de teste para incluir a coleta de logs de eventos, que será incluída nos resultados do teste.||[Como: Configurar a coleta de logs de evento usando configurações de teste](https://msdn.microsoft.com/48d67891-6018-4549-83e3-213d5d824a02)|
    |**Emulação de rede:** Especifique que você deseja colocar uma carga de rede artificial no teste usando uma configuração de teste. A emulação de rede afeta a comunicação para e do computador emulando uma velocidade de conexão de rede específica, como a conexão discada. **Observação:**  A emulação de rede não pode ser usada para aumentar a velocidade de conexão de rede.|O adaptador Emulação de Rede é ignorado por teste de carga. Em vez disso, os testes de carga usam as configurações especificadas na mistura de rede do cenário de teste de carga.<br /><br /> Para obter mais informações, confira [Especificar tipos de rede virtual](../test/specify-virtual-network-types-in-a-load-test-scenario.md).||
    |**Informações do sistema:** Uma configuração de teste pode ser definida para incluir as informações do sistema sobre os computadores nos quais o coletor de dados e diagnóstico de Informações do Sistema é executado. As informações do sistema são especificadas nos resultados do teste usando uma configuração de teste.|![Ícone de informações](../test/media/vc364f4.gif)<br /><br /> Você pode reunir informações do sistema de agentes de carregamento e do sistema em teste.|Nenhuma configuração é necessária para coletar essa informação.|
    |**Impacto de teste:** Colete informações sobre quais métodos do código de aplicativos foram usados quando um caso de teste estava sendo executado. Podem ser usadas em conjunto com as alterações feitas no código do aplicativo por desenvolvedores para determinar quais testes foram afetados pelas alterações de desenvolvimento.|Os dados do impacto de teste não são coletados com testes de carga.||
    |**Gravador de vídeo:** Crie uma gravação de vídeo da sessão de área de trabalho ao executar um teste automatizado. Isso pode ser útil para a exibição das ações do usuário para um teste codificado de interface do usuário. O vídeo pode ajudar outros membros de equipe a isolar problemas de aplicativo que sejam difíceis de reproduzir. **Observação:**  Ao executar testes remotamente, o gravador de exibição não funcionará a menos que o agente esteja executando no modo interativo do processo.|![Ícone Importante](../test/media/vc364f3.gif) **Aviso:**  Não recomendamos o uso do adaptador de gravação de vídeo para testes de carga.|[Como: Incluir gravações da tela e de voz durante testes usando as configurações de teste](../test/how-to-include-recordings-of-the-screen-and-voice-during-tests.md)|

19. Escolha **Implantação**.

     A página **Implantação** é exibida.

20. Para criar um diretório separado para implantação sempre que você executar seus testes, selecione **Habilitar implantação**.

    > [!NOTE]
    > Se você fazer isso, será possível continuar compilando o aplicativo ao executar os testes.

21. Para adicionar um arquivo ao diretório que você está usando para executar os testes, escolha **Adicionar arquivo** e selecione o arquivo que você deseja adicionar.

    > [!NOTE]
    > Quando executar testes de carga, assemblies de plug-in, arquivos de dados e arquivos carregados são implantados automaticamente.

22. Para adicionar um diretório ao diretório que você está usando para executar os testes, escolha **Adicionar diretório** e selecione o diretório que você deseja adicionar.

23. Para executar scripts antes e depois dos testes, escolha **Scripts de Instalação e Limpeza**.

     A página **Scripts de Instalação e Limpeza** é exibida.

    1.  Digite o local do arquivo de script em **Script de instalação** ou escolha as reticências (**…**) para localizar o script de instalação.

    2.  Digite o local do arquivo de script em **Script de limpeza** ou escolha as reticências (**…**) para localizar o script de limpeza.

24. Para executar testes usando um host diferente, escolha **Hosts**.

    1.  Em **Tipo de Host**, verifique se **Padrão** está selecionado.

        > [!NOTE]
        > **ASP.NET** em **Tipo de host** não tem suporte em testes de carga.

    2.  Use o menu suspenso **Executar teste em processo de 32 ou 64 bits** para selecionar se deseja que os testes de desempenho Web e os testes de unidade no teste de carga sejam executados como processos de 32 ou 64 bits.

        > [!NOTE]
        > Para a máxima flexibilidade, você deve compilar seus projetos de teste de carga e de desempenho na Web usando a configuração **Qualquer CPU**. Em seguida, você poderá executar os agentes de 32 bits e de 64 bits. A compilação de projetos de teste de carga e de desempenho na Web com a configuração de **64 bits** não oferece nenhuma vantagem.

25. (Opcional) Para delimitar o tempo para cada execução de teste e testes individuais, selecione **Tempos limite de testes.**

    1.  Para anular uma execução de teste quando um limite de tempo for excedido, selecione **Anular uma execução de teste se o tempo total exceder** e digite um valor para esse limite.

    2.  Para não passar em um teste individual quando um limite de tempo for excedido, selecione **Marcar um teste individual como reprovado se seu tempo de execução exceder** e digite um valor para este limite.

26. Ignorar **Teste de unidade**. Os testes de carga não usam essas configurações.

27. Ignorar **Teste na Web**. Os testes de carga não usam essas configurações.

28. Para salvar as configurações de teste, escolha **Salvar como**. Digite o nome do arquivo que você deseja em **Nome do objeto**.

    > [!NOTE]
    > Se você deve alterar suas configurações de teste, escolha **Testar** e então escolha **Editar Configurações de Teste** e aponte para as configurações de teste criadas.

### <a name="to-remove-a-test-settings-from-your-solution"></a>Para excluir configurações de teste de sua solução

Na pasta **Itens da Solução** no **Gerenciador de Soluções**, clique com o botão direito do mouse nas configurações de teste que deseja remover e, em seguida, escolha **Remover**.

O arquivo de configurações de teste é removido de sua solução. Essa alteração é refletida na lista de opções de **Selecionar Configurações de Teste Ativo** e **Editar Configurações de Teste** no menu **Teste**.

## <a name="see-also"></a>Consulte também

- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
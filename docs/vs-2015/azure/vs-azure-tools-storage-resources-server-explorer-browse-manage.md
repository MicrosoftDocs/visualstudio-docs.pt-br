---
title: Procurar e gerenciar recursos de armazenamento usando o Gerenciador de servidores | Microsoft Docs
description: Navegando e gerenciando recursos de armazenamento usando o Gerenciador de servidores
author: ghogen
manager: douge
assetId: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/24/2017
ms.author: ghogen
ms.openlocfilehash: 00229cd88ddcab4d2d59ae40202620c374415e4b
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001334"
---
# <a name="browse-and-manage-storage-resources-by-using-server-explorer"></a>Procurar e gerenciar recursos de armazenamento usando o Gerenciador de Servidores

[!INCLUDE [storage-try-azure-tools](./includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Visão geral

Se você tiver instalado as ferramentas do Azure para Microsoft Visual Studio, você pode exibir blob, fila e dados da tabela de suas contas de armazenamento do Azure. O Azure **armazenamento** nó no Gerenciador de servidores mostra os dados que estão em sua conta do emulador de armazenamento local e outras contas de armazenamento do Azure.

Para exibir o Gerenciador de servidores no Visual Studio, na barra de menus, selecione **modo de exibição** > **Gerenciador de servidores**. O **armazenamento** nó mostra todas as contas de armazenamento que existem em cada assinatura do Azure ou o certificado que você está conectado. Se sua conta de armazenamento não aparecer, você pode adicioná-lo seguindo as instruções [mais adiante neste artigo](#add-storage-accounts-by-using-server-explorer).

A partir do Azure SDK 2.7, você também pode usar Cloud Explorer para exibir e gerenciar seus recursos do Azure. Para obter mais informações, consulte [recursos de gerenciamento do Azure com o Gerenciador de nuvem](vs-azure-tools-resources-managing-with-cloud-explorer.md).

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Exibir e gerenciar recursos de armazenamento no Visual Studio

Gerenciador de servidores automaticamente mostra uma lista de blobs, filas e tabelas em sua conta do emulador de armazenamento. A conta do emulador de armazenamento está listada no Gerenciador de servidores sob o **armazenamento** nó como o **desenvolvimento** nó.

Para ver os recursos da conta do emulador de armazenamento, expanda o **desenvolvimento** nó. Se o emulador de armazenamento não foi iniciado quando você expande o **desenvolvimento** nó, ele será iniciado automaticamente. Esse processo pode levar vários segundos. Você pode continuar a trabalhar em outras áreas do Visual Studio enquanto o emulador de armazenamento é iniciado.

Para exibir recursos em uma conta de armazenamento, expanda o nó da conta de armazenamento no Gerenciador de servidores onde você vê **Blobs**, **filas**, e **tabelas** nós.

## <a name="work-with-blob-resources"></a>Trabalhar com recursos de blob

O **Blobs** nó exibe uma lista de contêineres para a conta de armazenamento selecionada. Contêineres de blob contêm arquivos de blob, e você pode organizar esses blobs em pastas e subpastas. Para obter mais informações, consulte [como usar o armazenamento de BLOBs do .NET](/azure/storage/blobs/storage-dotnet-how-to-use-blobs).

### <a name="to-create-a-blob-container"></a>Para criar um contêiner de blob

1. Abra o menu de atalho para o **Blobs** nó e, em seguida, selecione **criar contêiner de Blob**.
1. No **criar contêiner de Blob** caixa de diálogo, digite o nome do novo contêiner.  
1. Pressione Enter no teclado, ou você poderá clicar ou tocar fora do campo de nome para salvar o contêiner de blob.

   > [!NOTE]
   > O nome do contêiner de blob deve começar com uma letra minúscula (a-z) ou um número (0-9).

### <a name="to-delete-a-blob-container"></a>Para excluir um contêiner de blob

Abra o menu de atalho para o contêiner de blob que você deseja remover e, em seguida, selecione **excluir**.

### <a name="to-display-a-list-of-the-items-in-a-blob-container"></a>Para exibir uma lista dos itens em um contêiner de blob

Abra o menu de atalho para um nome de contêiner de blob na lista e, em seguida, selecione **aberto**.

Quando você exibe o conteúdo de um contêiner de blob, ele aparece em uma guia conhecida como exibição do contêiner de blob.

![Exibição do contêiner de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)

Você pode executar as seguintes operações em blobs usando os botões no canto superior direito da exibição do contêiner de blob:

* Insira um valor de filtro e aplicá-lo.
* Atualize a lista de blobs no contêiner.
* Carrega um arquivo.
* Exclua um blob. (A exclusão de um arquivo de um contêiner de blob não exclui o arquivo subjacente. Ele apenas o remove do contêiner de blob.)
* Abra um blob.
* Salve um blob no computador local.

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a>Para criar uma pasta ou subpasta em um contêiner de blob

1. Escolha o contêiner de blob no Cloud Explorer. Na janela do contêiner, selecione a **carregar Blob** botão.

1. No **carregar novo arquivo** caixa de diálogo, selecione o **procurar** botão para especificar o arquivo que você deseja carregar e, em seguida, insira um nome de pasta no **pasta (opcional)** caixa.

   ![Carregar um arquivo em uma pasta de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)

   Você pode adicionar as subpastas nas pastas de contêiner, seguindo as mesmas etapas. Se você não especificar um nome de pasta, o arquivo é carregado para o nível superior do contêiner de BLOBs. O arquivo aparece na pasta especificada no contêiner.

   ![Pasta adicionada a um contêiner de blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)

1. Clique duas vezes na pasta ou pressione Enter para ver o conteúdo da pasta. Quando você estiver na pasta do contêiner, você pode voltar para a raiz do contêiner selecionando o **abrir diretório pai** botão (seta).

### <a name="to-delete-a-container-folder"></a>Para excluir um contêiner

Exclua todos os arquivos na pasta.

Como as pastas em contêineres de blob são pastas virtuais, você não pode criar uma pasta vazia. Você também não é possível excluir uma pasta para excluir o conteúdo do arquivo, mas em vez disso, deverá excluir todo o conteúdo de uma pasta para excluir a própria pasta.

### <a name="to-filter-blobs-in-a-container"></a>Para filtrar os blobs em um contêiner

Você pode filtrar os blobs que são exibidos especificando um prefixo comum.

Por exemplo, se você inserir o prefixo **hello** na caixa de texto de filtro e em seguida, selecione o **Execute** (**!**) botão, somente os blobs que começam com "hello" aparecem.

![Caixa de texto de filtro](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

A caixa de texto de filtro diferencia maiusculas de minúsculas e não dá suporte a filtragem com caracteres curinga. BLOBs podem ser filtrados apenas pelo prefixo. O prefixo pode incluir um delimitador se você estiver usando um delimitador para organizar blobs em uma hierarquia virtual. Por exemplo, filtrar pelo prefixo "HelloFabric /" retorna todos os blobs que começam com essa cadeia de caracteres.

### <a name="to-download-blob-data"></a>Para baixar os dados de blob

No Cloud Explorer, use qualquer um dos seguintes métodos:

* Abra o menu de atalho para um ou mais blobs e, em seguida, selecione **aberto**.
* Escolha o nome do blob e, em seguida, selecione a **abrir** botão.
* Clique duas vezes no nome do blob.

O andamento de um download de blob é exibido na **Log de atividades do Azure** janela.

O blob é aberto no editor padrão para esse tipo de arquivo. Se o sistema operacional reconhecer o tipo de arquivo, o arquivo é aberto em um aplicativo instalado localmente. Caso contrário, você será solicitado a escolher um aplicativo que é apropriado para o tipo de arquivo do blob. O arquivo local que é criado quando você baixa um blob está marcado como somente leitura.

Dados de blob é armazenado em cache localmente e verificados em relação a hora da última modificação do blob no armazenamento de BLOBs do Azure. Se o blob tiver sido atualizado desde que foi baixado, ele será baixado novamente. Caso contrário, o blob é carregado do disco local.

Por padrão, um blob é baixado para um diretório temporário. Para baixar blobs para um diretório específico, abra o menu de atalho para os nomes dos blobs selecionados e selecione **Salvar como**. Quando você salva um blob dessa maneira, não é possível abrir o arquivo de blob e o arquivo local é criado com atributos de leitura/gravação.

### <a name="to-upload-blobs"></a>Para carregar blobs

Para carregar blobs, selecione a **carregar Blob** botão quando o contêiner for aberto para visualização na exibição do contêiner de blob.

Você pode escolher um ou mais arquivos para carregar, e você pode carregar arquivos de qualquer tipo. O **Log de atividades do Azure** janela mostra o progresso do carregamento. Para obter mais informações sobre como trabalhar com dados de blob, consulte [como usar o armazenamento de BLOBs do Azure no .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="to-view-logs-transferred-to-blobs"></a>Para exibir os logs transferidos para os blobs

Se você estiver usando o diagnóstico do Azure para registrar dados de seu aplicativo do Azure e tiver transferido logs para sua conta de armazenamento, você verá os contêineres que o Azure criou para esses logs. Exibir esses logs no Gerenciador de servidores é uma maneira fácil de identificar problemas com seu aplicativo, especialmente se ele foi implantado no Azure.

Para obter mais informações sobre o diagnóstico do Azure, consulte [coletar dados de log usando o diagnóstico do Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="to-get-the-url-for-a-blob"></a>Para obter a URL para um blob

Abra o menu de atalho do blob e, em seguida, selecione **Copiar URL**.

### <a name="to-edit-a-blob"></a>Para editar um blob

Selecione o blob e, em seguida, selecione a **abrir Blob** botão.

O arquivo é baixado para um local temporário e aberto no computador local. Carregar o blob novamente depois de fazer alterações.

## <a name="work-with-queue-resources"></a>Trabalhar com recursos de fila

Filas de serviços de armazenamento são hospedadas em uma conta de armazenamento do Azure. Você pode usá-los para permitir que sua nuvem de funções de serviço para se comunicar entre si e com outros serviços por um mecanismo de transmissão de mensagens. Você pode acessar a fila programaticamente por meio de um serviço de nuvem e em um serviço web para clientes externos. Você também pode acessar a fila diretamente, usando o Gerenciador de servidores no Visual Studio.

Ao desenvolver um serviço de nuvem que usa filas, você talvez queira usar o Visual Studio para criar filas e trabalhar interativamente com elas enquanto desenvolver e testar seu código.

No Gerenciador de servidores, você pode exibir as filas em uma conta de armazenamento, criar e excluir filas, abrir uma fila para exibir suas mensagens e adicionar mensagens a uma fila. Quando você abrir uma fila para exibição, você pode exibir as mensagens individuais, e você pode executar as seguintes ações na fila usando os botões no canto superior esquerdo:

* Atualize a exibição da fila.
* Adicione uma mensagem à fila.
* Remover a mensagem de nível mais alta.
* Limpe a fila inteira.

A imagem a seguir mostra uma fila que contém duas mensagens:

![Exibindo uma fila](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Para obter mais informações sobre o armazenamento de filas de serviço, consulte [Introdução ao armazenamento de filas do Azure usando o .NET](http://go.microsoft.com/fwlink/?LinkID=264702). Para obter informações sobre o serviço web para filas de serviço de armazenamento, consulte [conceitos do serviço fila](http://go.microsoft.com/fwlink/?LinkId=264788). Para obter informações sobre como enviar mensagens para uma fila de serviços de armazenamento usando o Visual Studio, consulte [enviando mensagens para uma fila de serviços de armazenamento](https://docs.microsoft.com/azure/visual-studio/vs-storage-cloud-services-getting-started-queues).

> [!NOTE]
> Filas de serviços de armazenamento são diferentes das filas do barramento de serviço do Azure. Para obter mais informações sobre as filas do barramento de serviço, consulte [filas do barramento de serviço, tópicos e assinaturas](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-queues-topics-subscriptions).

## <a name="work-with-table-resources"></a>Trabalhar com recursos de tabela

Armazenamento de tabela do Azure armazena grandes quantidades de dados estruturados. O serviço é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora da nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.

### <a name="to-create-a-table"></a>Para criar uma tabela

1. No Cloud Explorer, selecione o **tabelas** nó da conta de armazenamento e em seguida, selecione **Create Table**.
1. No **Create Table** caixa de diálogo, digite um nome para a tabela.

### <a name="to-view-table-data"></a>Para exibir dados da tabela

1. No Cloud Explorer, abra o **Azure** nó e, em seguida, abra o **armazenamento** nó.
1. Abra o nó da conta de armazenamento que você está interessado e, em seguida, abra o **tabelas** nó para ver uma lista de tabelas para a conta de armazenamento.
1. Abra o menu de atalho para uma tabela e, em seguida, selecione **Exibir tabela**.

    ![Uma tabela do Azure no Gerenciador de soluções](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

A tabela é organizada por entidades (mostradas nas linhas) e propriedades (mostradas nas colunas). Por exemplo, a ilustração a seguir mostra entidades listadas no Designer de tabela.

### <a name="to-edit-table-data"></a>Para editar dados da tabela

No Designer de tabela, abra o menu de atalho para uma entidade (uma única linha) ou uma propriedade (uma única célula) e, em seguida, selecione **editar**.

    ![Add or edit a table entity](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)

Entidades em uma única tabela não é necessárias ter o mesmo conjunto de propriedades (colunas). Tenha em mente as seguintes restrições sobre como exibir e editar dados da tabela:

* Você não pode exibir ou editar dados binários (`type byte[]`), mas você pode armazená-lo em uma tabela.
* Não é possível editar a **PartitionKey** ou **RowKey** valores, porque o armazenamento de tabela no Azure não dá suporte a essa operação.
* Você não pode criar uma propriedade chamada **carimbo de hora**. Serviços de armazenamento do Azure usam uma propriedade com esse nome.
* Se você inserir uma **DateTime** valor, você deve seguir o formato apropriado para as configurações de região e idioma do seu computador (por exemplo, MM/DD/AAAA HH: mm ss [AM | PM] para inglês dos EUA).

### <a name="to-add-entities"></a>Para adicionar entidades

1. No Designer de tabela, selecione a **Adicionar entidade** botão.

    ![Botão Adicionar entidade](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)

1. No **Adicionar entidade** caixa de diálogo, digite os valores da **PartitionKey** e **RowKey** propriedades.

    ![Adicionar caixa de diálogo de entidade](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)

    Insira os valores com cuidado. Você não pode alterá-los depois de fechar a caixa de diálogo, a menos que você exclua a entidade e adicioná-lo novamente.

### <a name="to-filter-entities"></a>Para filtrar entidades

Você pode personalizar o conjunto de entidades que aparecem em uma tabela, se você usar o construtor de consultas.

1. Para abrir o construtor de consultas, abra uma tabela para exibir.
1. Selecione o **construtor de consultas** botão na barra de ferramentas de exibição de tabela.

    O **construtor de consultas** caixa de diálogo é exibida. A ilustração a seguir mostra uma consulta que está sendo criada no construtor de consultas.

    ![Construtor de consultas](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
1. Quando você terminar de compilar a consulta, feche a caixa de diálogo. O formulário de texto resultante da consulta aparece em uma caixa de texto como um filtro do WCF Data Services.
1. Para executar a consulta, selecione o ícone de triângulo verde.

Você também pode filtrar os dados de entidade que aparecem no Designer de tabela se inserir uma cadeia de caracteres de filtro do WCF Data Services diretamente na caixa de texto de filtro. Esse tipo de cadeia de caracteres é semelhante a uma cláusula SQL WHERE, mas é enviado ao servidor como uma solicitação HTTP. Para obter informações sobre como construir cadeias de caracteres de filtro, consulte [construindo cadeias de caracteres de filtro para o designer de tabela](https://docs.microsoft.com/azure/vs-azure-tools-table-designer-construct-filter-strings).

A ilustração a seguir mostra um exemplo de uma cadeia de caracteres de filtro válidas:

![Cadeia de caracteres de filtro](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

## <a name="refresh-storage-data"></a>Atualizar os dados de armazenamento

Quando o Gerenciador de servidores é conectado ou obtém dados de uma conta de armazenamento, a operação pode levar até um minuto para concluir. Se o Gerenciador de servidores não pode se conectar, a operação pode atingir o tempo limite. Enquanto os dados são recuperados, você pode continuar a trabalhar em outras partes do Visual Studio. Para cancelar a operação se ele estiver demorando muito, selecione a **Parar atualização** na barra de ferramentas do Gerenciador de servidores.

### <a name="to-refresh-blob-container-data"></a>Para atualizar os dados de contêiner de blob

* Selecione o **Blobs** nó sob **armazenamento**e, em seguida, selecione o **atualizar** na barra de ferramentas do Gerenciador de servidores.
* Para atualizar a lista de blobs que é exibida, selecione a **Execute** botão.

### <a name="to-refresh-table-data"></a>Para atualizar os dados de tabela

* Selecione o **tabelas** nó sob **armazenamento**e, em seguida, selecione o **atualizar** na barra de ferramentas do Gerenciador de servidores.
* Para atualizar a lista de entidades que é exibida no Designer de tabela, selecione a **Execute** botão no Designer de tabela.

### <a name="to-refresh-queue-data"></a>Para atualizar os dados da fila

Selecione o **filas** nó sob **armazenamento**e, em seguida, selecione o **atualizar** na barra de ferramentas do Gerenciador de servidores.

### <a name="to-refresh-all-items-in-a-storage-account"></a>Para atualizar todos os itens em uma conta de armazenamento

Escolha o nome da conta e, em seguida, selecione a **Refresh** na barra de ferramentas do Gerenciador de servidores.

## <a name="add-storage-accounts-by-using-server-explorer"></a>Adicionar contas de armazenamento usando o Gerenciador de servidores

Há duas maneiras de adicionar contas de armazenamento usando o Gerenciador de servidores. Você pode criar uma conta de armazenamento na sua assinatura do Azure, ou você pode anexar uma conta de armazenamento existente.

### <a name="to-create-a-storage-account-by-using-server-explorer"></a>Para criar uma conta de armazenamento usando o Gerenciador de servidores

1. No Gerenciador de servidores, abra o menu de atalho para o **armazenamento** nó e, em seguida, selecione **criar conta de armazenamento**.

1. No **criar conta de armazenamento** caixa de diálogo caixa, selecione ou insira as seguintes informações:

   * A assinatura do Azure para o qual você deseja adicionar a conta de armazenamento.
   * O nome que você deseja usar para a nova conta de armazenamento.
   * A região ou grupo de afinidade (como Oeste dos EUA ou Leste Asiático).
   * O tipo de replicação que você deseja usar para a conta de armazenamento, tal como localmente redundante.

   ![Criar uma conta de armazenamento do Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)

1. Selecione **Criar**.

A nova conta de armazenamento aparece na **armazenamento** lista no Gerenciador de soluções.

### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a>Para anexar uma conta de armazenamento existente usando o Gerenciador de servidores

1. No Gerenciador de servidores, abra o menu de atalho para o Azure **armazenamento** nó e, em seguida, selecione **anexar armazenamento externo**.

    ![Adicionar uma conta de armazenamento existente](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
1. No **criar conta de armazenamento** caixa de diálogo caixa, selecione ou insira as seguintes informações:

   * O nome da conta de armazenamento existente que você deseja anexar.
   * A chave para a conta de armazenamento selecionada. Esse valor normalmente é fornecido para você quando você seleciona uma conta de armazenamento. Se quiser que o Visual Studio se lembre da chave de conta de armazenamento, selecione o **lembrar chave da conta** caixa de seleção.
   * O protocolo a ser usado para se conectar à conta de armazenamento, como HTTP, HTTPS ou um ponto de extremidade personalizado. Para obter mais informações sobre pontos de extremidade personalizados, consulte [como configurar cadeias de Conexão](https://msdn.microsoft.com/library/azure/ee758697.aspx).

### <a name="to-view-the-secondary-endpoints"></a>Para exibir os pontos de extremidade secundários

Se você criou uma conta de armazenamento usando o **redundância geográfica com acesso de leitura** opção de replicação, você pode exibir seus pontos de extremidade secundários, abrindo o menu de atalho para o nome da conta e, em seguida, selecione **propriedades**.

![Pontos de extremidade de armazenamento secundários](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a>Para remover uma conta de armazenamento do Gerenciador de servidores

No Gerenciador de servidores, abra o menu de atalho para o nome da conta e, em seguida, selecione **excluir**. 

Se você excluir uma conta de armazenamento, qualquer informação de chave salva para essa conta também é removida.

Se você excluir uma conta de armazenamento do Gerenciador de servidores, ela não afeta sua conta de armazenamento ou quaisquer dados que ele contém. Ele simplesmente remove a referência do Gerenciador de servidores. Para excluir permanentemente uma conta de armazenamento, use o [portal do Azure](https://portal.azure.com/).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como usar os serviços de armazenamento do Azure, consulte [acessando os serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/ee405490.aspx).

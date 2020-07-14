---
title: Adicionar novas conexões
ms.date: 11/04/2016
ms.topic: how-to
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5f6f34c28a6bbba236a4d90e2f936fad0b2a3f60
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283054"
---
# <a name="add-new-connections"></a>Adicionar novas conexões

Você pode testar a conexão com um banco de dados ou serviço e explorar o conteúdo e os esquemas do banco de dados, usando **Gerenciador de servidores**, **Cloud Explorer**ou **pesquisador de objetos do SQL Server**. A funcionalidade dessas janelas se sobrepõe a alguma extensão. As diferenças básicas são:

- Gerenciador de Servidores

   Instalado por padrão no Visual Studio. Pode ser usado para testar conexões e exibir SQL Server bancos de dados, qualquer outro banco de dados que tenha um provedor ADO.NET instalado e alguns serviços do Azure. Também mostra objetos de baixo nível, como contadores de desempenho do sistema, logs de eventos e filas de mensagens. Se uma fonte de dados não tiver um provedor ADO.NET, ela não aparecerá aqui, mas você ainda poderá usá-la no Visual Studio conectando-se programaticamente.

- Gerenciador de Nuvem

   Instale essa janela manualmente como uma extensão do Visual Studio de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS). Fornece uma funcionalidade especializada para explorar e se conectar aos serviços do Azure.

- Pesquisador de Objetos do SQL Server

   Instalado com SQL Server Data Tools e visível no menu **Exibir** . Se você não o vir lá, vá para **programas e recursos** no painel de controle, encontre o Visual Studio e, em seguida, selecione **alterar** para executar novamente o instalador depois de marcar a caixa de seleção para SQL Server Data Tools. Use **pesquisador de objetos do SQL Server** para exibir bancos de dados SQL (se eles tiverem um provedor de ADO.net), criar novos bancos de dados, modificar esquemas, criar procedimentos armazenados, recuperar cadeias de conexão, exibir e muito mais. Os bancos de dados SQL que não têm nenhum provedor ADO.NET instalado não aparecerão aqui, mas você ainda poderá se conectar a eles de forma programática.

## <a name="add-a-connection-in-server-explorer"></a>Adicionar uma conexão no Gerenciador de Servidores

Para criar uma conexão com o banco de dados, clique no ícone **Adicionar conexão** no **Gerenciador de servidores**ou clique com o botão direito do mouse em **Gerenciador de servidores** no nó **conexões de dados** e selecione **Adicionar conexão**. A partir daqui, você também pode se conectar a um banco de dados em outro servidor, um serviço do SharePoint ou um serviço do Azure.

![Ícone de nova conexão Gerenciador de Servidores](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

Isso abre a caixa de diálogo **Adicionar conexão** . Aqui, inserimos o nome da instância do SQL Server LocalDB.

![Adicionar Nova Conexão](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>Alterar o provedor

Se a fonte de dados não for o que você deseja, clique no botão **alterar** para escolher uma nova fonte de dados e/ou um novo provedor de dados ADO.net. O novo provedor pode solicitar suas credenciais, dependendo de como você a configurou.

![Alterar AD0.NET Provedor de Dados](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>Testar a conexão

Depois de escolher a fonte de dados, clique em **testar conexão**. Se não tiver sucesso, será necessário solucionar problemas com base na documentação do fornecedor.

![Teste a conexão](../data-tools/media/raddata-test-connection.png)

Se o teste for bem sucedido, você estará pronto para criar uma *fonte de dados*, que é um termo do Visual Studio que significa realmente um *modelo de dados* com base no serviço ou banco subjacente.

## <a name="see-also"></a>Veja também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)

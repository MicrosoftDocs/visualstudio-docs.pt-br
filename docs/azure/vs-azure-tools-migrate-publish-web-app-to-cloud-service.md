---
title: Migrar e publicar o aplicativo Web no serviço de nuvem do Azure
description: Saiba como migrar e publicar seu aplicativo Web em um serviço de nuvem do Azure por meio do Visual Studio
author: ghogen
manager: jillfra
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: c95c96815872c259cab761d8b4af36141f866dbd
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280551"
---
# <a name="how-to-migrate-and-publish-a-web-application-to-an-azure-cloud-service-from-visual-studio"></a>Como migrar e publicar um aplicativo Web em um serviço de nuvem do Azure por meio do Visual Studio

Para tirar proveito dos serviços de hospedagem e a escalabilidade do Azure, você pode migrar e implantar seu aplicativo Web em um serviço de nuvem do Azure. Somente alteração mínimas são necessárias. Este artigo aborda somente a implantação em serviços de nuvem; para o Serviço de Aplicativo, consulte [Implantar um aplicativo Web no Serviço de Aplicativo do Azure](/azure/app-service/app-service-deploy-local-git).

> [!Important]
> Essa migração só tem suporte para os projetos específicos de fluxo de trabalho ASP.NET, WCF e WCF. Não há suporte para projetos do ASP.NET Core. Consulte [Modelos de projeto com suporte](#supported-project-templates).

## <a name="migrate-a-project-to-cloud-services"></a>Migrar um projeto para serviços de nuvem

1. Clique com o botão direito do mouse no nó da solução e selecione **adicionar > novo projeto...** e adicione um novo projeto do **serviço de nuvem do Azure (clássico)** à solução existente.
1. Na caixa de diálogo **novo serviço de nuvem Microsoft Azure (clássico)** , clique em OK sem adicionar nenhuma função ao projeto.
1. Clique com o botão direito do mouse no nó funções no projeto serviços de nuvem recém-adicionado e selecione **Adicionar projeto de função Web na solução...**.
1. Na caixa de diálogo **associar ao projeto de função** , selecione o projeto que você deseja associar como uma função Web.

   > [!Important]
   > Se tiver outros assemblies ou arquivos necessários para o aplicativo Web, você precisa definir manualmente as propriedades para esses arquivos. Para obter informações sobre como definir essas propriedades, consulte [Incluir arquivos no pacote de serviço](vs-azure-tools-publishing-a-cloud-service.md#include-files-in-the-service-package).

### <a name="errors-and-warnings"></a>Erros e avisos

Quaisquer avisos ou erros indicam problemas a serem corrigidos antes de implantar o Azure, como assemblies ausentes.

Se você compilar seu aplicativo, executá-lo localmente usando o emulador de computação ou publicá-lo no Azure, poderá ver o seguinte erro: “O caminho especificado, o nome do arquivo ou ambos são muito longos”. Esse erro indica que o comprimento do nome totalmente qualificado do projeto do Azure excede 146 caracteres. Para corrigir o problema, mova sua solução para uma pasta diferente com um caminho mais curto.

Para obter mais informações sobre como tratar avisos como erros, consulte [Configurar um projeto de serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configuring-an-azure-project.md).

### <a name="test-the-migration-locally"></a>Testar a migração localmente

1. No **Gerenciador de Soluções** do Visual Studio, clique com o botão direito do mouse no projeto do serviço de nuvem adicionado e selecione **Configurar como Projeto de Inicialização**.
1. Selecione **Depurar > Iniciar depuração** (F5) para inicializar o ambiente de depuração do Azure. Esse ambiente fornece especificamente emulação de vários serviços do Azure.

### <a name="use-an-azure-sql-database-for-your-application"></a>Usar um Banco de Dados SQL do Azure para seu aplicativo

Se tiver uma cadeia de conexão para seu aplicativo Web que usa um banco de dados SQL Server local, você deve migrar seu banco de dados para o Banco de Dados SQL do Azure e atualizar a cadeia de conexão. Para obter orientações com esse processo, consulte os tópicos a seguir:

- [Migração de banco de dados do SQL Server para o Banco de Dados SQL na nuvem](/azure/sql-database/sql-database-cloud-migrate)
- [Usar o .NET (C#) com o Visual Studio para conectar e consultar um banco de dados SQL do Azure](/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).

## <a name="publish-the-application-to-azure-cloud-service"></a>Publicar o aplicativo em um Serviço de Nuvem do Azure

1. Crie o serviço de nuvem e as contas de armazenamento necessários em sua assinatura do Azure, conforme descrito em [Preparar para publicar ou implantar um aplicativo do Azure a partir do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
1. No Visual Studio, clique com botão direito no projeto do aplicativo e selecione **Publicar no Microsoft Azure...** (que é diferente do comando “Publicar...”).
1. No **Publicar aplicativo do Azure** que aparece, entre usando a conta com sua assinatura do Azure e selecione **Avançar >**.
1. Na guia **Configurações > Configurações Comuns**, selecione o serviço de nuvem de destino na lista suspensa **Serviço de Nuvem**, juntamente com o ambiente e as configurações escolhidas.
1. Em **Configurações > Configurações Avançadas**, selecione a conta de armazenamento a ser usada e depois selecione **Avançar >**.
1. Em **Diagnósticos**, escolha se deseja enviar informações ao Application Insights.
1. Selecione **Avançar >** para exibir um resumo, depois selecione **Publicar** para iniciar a implantação.
1. O Visual Studio abre uma janela de log de atividade na qual você pode acompanhar o progresso:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)

1. (Opcional) Para cancelar o processo de implantação, clique com o botão direito do mouse no item de linha no log de atividades e escolha **Cancelar e remover**. Esse comando interrompe o processo de implantação e exclui o ambiente de implantação do Azure. Observação: para remover este ambiente de implantação depois de ele ter sido implantado, você deve usar o [Portal do Azure](https://portal.azure.com).
1. (Opcional) Depois de ter iniciado as instâncias de função, o Visual Studio mostra automaticamente o ambiente de implantação no nó **Gerenciador de Servidores > Serviços de Nuvem**. Aqui você pode exibir o status das instâncias de função individuais.
1. Para acessar seu aplicativo após a implantação, escolha a seta ao lado de sua implantação quando um status de **Concluído** aparecer no **Log de atividades do Azure** junto com a URL. Consulte a tabela a seguir para obter detalhes sobre como iniciar um tipo específico de aplicativo Web do Azure.

## <a name="using-the-compute-emulator-and-starting-application-in-azure"></a>Usar o emulador de computação e iniciar o aplicativo no Azure

Todos os tipos de aplicativo podem ser iniciados em um navegador conectado ao depurador do Visual Studio selecionando **Depurar > Iniciar Depuração** (F5). Com um projeto de Aplicativo Web Vazio do ASP.NET, primeiro você deve adicionar uma página `.aspx` em seu aplicativo e defini-la como a página inicial do seu projeto Web.

A tabela a seguir fornece detalhes sobre como iniciar o aplicativo no Azure:

| Tipo de aplicativo Web | em execução no Azure |
| --- | --- |
| Aplicativo Web do ASP.NET<br/>(incluindo MVC 2, MVC 3, MVC 4) | Selecione a URL na guia **Implantação** para o **Log de Atividades do Azure**. |
| Aplicativo Web ASP.NET vazio | Caso tenha uma página `.aspx` padrão em seu aplicativo, selecione a URL na guia **Implantação** para o **Log de Atividades do Azure**. Para navegar para uma página diferente, insira uma URL do formulário a seguir em um navegador: `<deployment_url>/<page_name>.aspx` |
| Aplicativo de serviço WCF<br/>Aplicativo de serviço de fluxo de trabalho WCF | Defina o arquivo `.svc` como a página inicial do seu projeto de Serviço WCF. Depois navegue até `<deployment_url>/<service_file>.svc` |
| Entidades dinâmicas do ASP.NET<br/>Dados dinâmicos ASP.NET Linq to SQL | Atualize a cadeia de conexão conforme descrito na próxima seção. Depois navegue até `<deployment_url>/<page_name>.aspx`. Para Linq em SQL, você deve usar um banco de dados SQL do Azure. |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Atualizar uma cadeia de conexão para Entidades dinâmicas do ASP.NET

1. Crie um banco de dados SQL do Azure para um aplicativo Web de entidades dinâmicas do ASP.NET, conforme descrito anteriormente em (#use-an-azuresql-database-for-your-application).
1. Adicione as tabelas e os campos necessários para esse banco de dados por meio do Portal do Azure.
1. Especifique uma cadeia de conexão no arquivo `web.config` com o seguinte formato e salve o arquivo:

    ```xml
    <add name="tempdbEntities"
     connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"
     providerName="System.Data.EntityClient"/>
    ```

    Atualize o valor de *connectionString* com a cadeia de conexão ADO.NET para seu banco de dados do SQL Azure da seguinte maneira:

    ```xml
    <add name="tempdbEntities"
     connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"
     providerName="System.Data.EntityClient"/>
    ```

## <a name="supported-project-templates"></a>Modelos de projeto com suporte

Aplicativos que podem ser migrados e publicados nos serviços de nuvem devem usar um dos modelos da tabela a seguir. Não há suporte para o ASP.NET Core.

| Grupo de modelos | Modelo do projeto |
| --- | --- |
| Web | Aplicativo Web do ASP.NET (.NET Framework) |
| Web | Aplicativo Web ASP.NET MVC 2 |
| Web | Aplicativo Web ASP.NET MVC 3 |
| Web | Aplicativo Web ASP.NET MVC 4 |
| Web | Aplicativo (ou Site) Web do ASP.NET vazio |
| Web | Aplicativo Web ASP.NET MVC 2 vazio |
| Web | Aplicativo Web de entidades de dados dinâmicos ASP.NET |
| Web | Aplicativo Web de dados dinâmicos ASP.NET Linq do SQL |
| WCF | Aplicativo de serviço WCF |
| WCF | Aplicativo de serviço de fluxo de trabalho WCF |
| Fluxo de trabalho | Aplicativo de serviço de fluxo de trabalho WCF |

## <a name="next-steps"></a>Próximas etapas

- [Preparar para publicar ou implantar um aplicativo do Azure do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)
- [Configurando credenciais de autenticação nomeadas](vs-azure-tools-setting-up-named-authentication-credentials.md).

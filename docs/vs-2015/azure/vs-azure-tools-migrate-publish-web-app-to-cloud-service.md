---
title: Como migrar e publicar um aplicativo Web para um serviço de nuvem do Visual Studio | Microsoft Docs
description: Saiba como migrar e publicar seu aplicativo web para um serviço de nuvem do Azure usando o Visual Studio
author: ghogen
manager: douge
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: c122b54a4e22285678d13213cc73d6492baba629
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001333"
---
# <a name="how-to-migrate-and-publish-a-web-application-to-an-azure-cloud-service-from-visual-studio"></a>Como: migrar e publicar um aplicativo Web a um serviço de nuvem do Azure do Visual Studio

Para tirar proveito dos serviços de hospedagem e a capacidade de dimensionamento do Azure, talvez você queira migrar e implantar seu aplicativo web para um serviço de nuvem do Azure. Somente alterações mínimas são necessárias. Este artigo aborda a implantação de serviços de nuvem apenas; para o serviço de aplicativo, consulte [implantar um aplicativo web no serviço de aplicativo do Azure](/azure/app-service/app-service-deploy-local-git).

> [!Important]
> Essa migração tem suporte somente para projetos ASP.NET, Silverlight, WCF e fluxo de trabalho WCF específicos. Não há suporte para projetos do ASP.NET Core. Ver [suporte para modelos de projeto](#supported-project-templates).

## <a name="migrate-a-project-to-cloud-services"></a>Migrar um projeto para serviços de nuvem

1. O projeto de aplicativo web com o botão direito e selecione **converter > Converter em projeto de serviço de nuvem do Microsoft Azure**. (Observe que esse comando não será exibida se você já tiver um projeto de função web na solução).
1. Visual Studio cria um projeto de serviço de nuvem na solução que contém a função web necessária. O nome deste projeto é o mesmo que seu projeto de aplicativo com mais o sufixo `.Azure`.
1. O Visual Studio também define o **Copy Local** propriedade como true para todos os assemblies que são necessários para MVC 2, MVC 3, MVC 4 e aplicativos de negócios do Silverlight. Essa propriedade adiciona esses assemblies ao pacote de serviço que é usado para implantação.

   > [!Important]
   > Se você tiver outros assemblies ou arquivos que são necessários para este aplicativo web, você deve definir manualmente as propriedades para esses arquivos. Para obter informações sobre como definir essas propriedades, consulte [incluir arquivos no pacote de serviço](#include-files-in-the-service-package).

### <a name="errors-and-warnings"></a>Erros e avisos

Os avisos ou erros que ocorrem indicam problemas a serem corrigidos antes de implantar no Azure, como assemblies ausentes.

Se você cria seu aplicativo, executá-lo localmente usando o emulador de computação ou publicá-lo no Azure, você poderá ver o erro: "o caminho especificado, o nome do arquivo ou ambos são muito longos." Esse erro indica que o comprimento do nome totalmente qualificado do projeto do Azure excede 146 caracteres. Para corrigir o problema, mova sua solução para uma pasta diferente com um caminho mais curto.

Para obter mais informações sobre como tratar avisos como erros, consulte [configurar um projeto de serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configuring-an-azure-project.md).

### <a name="test-the-migration-locally"></a>Testar a migração localmente

1. No Visual Studio **Gerenciador de soluções**, o projeto de serviço de nuvem adicionado com o botão direito e selecione **definir como projeto de inicialização**.
1. Selecione **Depurar > Iniciar depuração** (F5) para iniciar o ambiente de depuração do Azure. Esse ambiente fornece especificamente emulação de vários serviços do Azure.

### <a name="use-an-azure-sql-database-for-your-application"></a>Usar um banco de dados do SQL Azure para seu aplicativo

Se você tiver uma cadeia de caracteres de conexão para seu aplicativo web que usa um banco de dados do SQL Server local, você deve migrar seu banco de dados para o banco de dados SQL em vez disso e atualizar sua cadeia de conexão. Para obter orientações com esse processo, consulte os tópicos a seguir:

- [Migração de banco de dados do SQL Server para o banco de dados SQL na nuvem](/azure/sql-database/sql-database-cloud-migrate)
- [Usar o .NET (C#) com o banco de dados SQL do Azure e o Visual Studio para se conectar e consultar](/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).

## <a name="publish-the-application-to-azure-cloud-service"></a>Publicar o aplicativo no serviço de nuvem do Azure

1. Criar os necessários para a nuvem as contas de serviço e armazenamento em sua assinatura do Azure conforme descrito em [preparar para publicar ou implantar um aplicativo do Azure do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
1. No Visual Studio, clique com botão direito no projeto de aplicativo e selecione **publicar no Microsoft Azure...**  (que é diferente do comando "Publicar...").
1. No **publicar aplicativo do Azure** que aparece, entre usando a conta com sua assinatura do Azure e selecione **próximo >**.
1. No **Configurações > configurações comuns** , selecione o serviço de nuvem de destino a **serviço de nuvem** lista suspensa, juntamente com suas configurações e ambiente escolhido. 
1. Na **Configurações > Configurações avançadas**, selecione a conta de armazenamento para usar e, em seguida, selecione **próximo >**.
1. Na **diagnóstico**, escolha se deseja enviar informações para o Application Insights.
1. Selecione **Avançar >** para exibir um resumo, em seguida, selecione **publicar** para iniciar a implantação.
1. O Visual Studio abre uma janela de log de atividades em que você pode acompanhar o progresso:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)

1. (Opcional) Para cancelar o processo de implantação, o item de linha no log de atividades com o botão direito e escolha **Cancelar e remover**. Esse comando interrompe o processo de implantação e exclui o ambiente de implantação do Azure. Observação: para remover este ambiente de implantação após ele ter sido implantado, você deve usar o [portal do Azure](https://portal.azure.com).
1. (Opcional) Depois de ter iniciado as instâncias de função, o Visual Studio mostra automaticamente o ambiente de implantação na **Gerenciador de servidores > Serviços de nuvem** nó. A partir daqui, você pode exibir o status das instâncias de função individuais.
1. Para acessar seu aplicativo após a implantação, escolha a seta ao lado de sua implantação quando um status de **Completed** aparece na **log de atividades do Azure** juntamente com a URL. Consulte a tabela a seguir para obter detalhes sobre como iniciar um tipo específico de aplicativo web do Azure.

## <a name="using-the-compute-emulator-and-starting-application-in-azure"></a>Usando o emulador de computação e iniciar o aplicativo no Azure

Todos os tipos de aplicativo podem ser iniciados em um navegador conectado ao depurador do Visual Studio, selecionando **Depurar > Iniciar depuração** (F5). Com um projeto de aplicativo Web vazio ASP.NET, você deve primeiro adicionar um `.aspx` página em seu aplicativo e defini-lo como a página inicial do projeto da web.

A tabela a seguir fornece detalhes sobre como iniciar o aplicativo no Azure:

   | Tipo de aplicativo Web | Em execução no Azure |
   | --- | --- | --- |
   | Aplicativo Web ASP.NET<br/>(incluindo MVC 2, MVC 3, MVC 4) | Selecione a URL na **implantação** guia para o **log de atividades do Azure**. |
   | Aplicativo Web ASP.NET vazio | Se você tiver um padrão `.aspx` em seu aplicativo, selecione a URL na **implantação** guia para o **log de atividades do Azure**. Para navegar até uma página diferente, insira uma URL da seguinte forma em um navegador: `<deployment_url>/<page_name>.aspx` |
   | Aplicativo do Silverlight<br/>Aplicativo de negócios Silverlight<br/>Aplicativo de navegação do Silverlight | Navegue até a página específica para seu aplicativo usando o seguinte formato de URL: `<deployment_url>/<page_name>.aspx` |
    Aplicativo de serviço WCF<br/>Aplicativo de Serviço de Fluxo de Trabalho do WCF | Defina o `.svc` arquivo como a página inicial do seu projeto de serviço do WCF. Em seguida, navegue até `<deployment_url>/<service_file>.svc` |
   | Entidades dinâmicas do ASP.NET<br/>Dados dinâmicos ASP.NET Linq to SQL | Atualize a cadeia de caracteres de conexão, conforme descrito na próxima seção. Em seguida, navegue até `<deployment_url>/<page_name>.aspx`. LINQ to SQL, você deve usar um banco de dados SQL do Azure. |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Atualizar uma cadeia de Conexão para entidades dinâmicas do ASP.NET

1. Crie um banco de dados do SQL Azure para um aplicativo web de entidades dinâmicas do ASP.NET, conforme descrito anteriormente (#use-an-azuresql-database-for-your-application).
1. Adicione as tabelas e campos que você precisa para esse banco de dados do portal do Azure.
1. Especifique uma cadeia de caracteres de conexão no `web.config` com o seguinte formato de arquivo e salve o arquivo:

    ```xml
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Atualizar o *connectionString* valor com a cadeia de conexão ADO.NET do banco de dados do SQL Azure da seguinte maneira:

    ```xml
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

## <a name="supported-project-templates"></a>Modelos de projeto com suporte

Aplicativos que podem ser migrados e publicados nos serviços de nuvem devem usar um dos modelos na tabela a seguir. Não há suporte para o ASP.NET Core.

| Grupo de modelos | Modelo de projeto |
| --- | --- |
| Web | Aplicativo Web do ASP.NET (.NET Framework) |
| Web | Aplicativo Web ASP.NET MVC 2 |
| Web | Aplicativo Web ASP.NET MVC 3 |
| Web | Aplicativo da Web ASP.NET MVC4 |
| Web | Aplicativo Web ASP.NET vazio (ou Site) |
| Web | Aplicativo Web vazio ASP.NET MVC 2 |
| Web | Aplicativo Web de entidades de dados dinâmicos do ASP.NET |
| Web | Dados dinâmicos ASP.NET Linq para o aplicativo Web do SQL |
| Silverlight | Aplicativo do Silverlight |
| Silverlight | Aplicativo de negócios Silverlight |
| Silverlight | Aplicativo de navegação do Silverlight |
| WCF | Aplicativo de serviço WCF |
| WCF | Aplicativo de Serviço de Fluxo de Trabalho do WCF |
| Fluxo de Trabalho | Aplicativo de Serviço de Fluxo de Trabalho do WCF |

## <a name="next-steps"></a>Próximas etapas

- [Preparar para publicar ou implantar um aplicativo do Azure do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)
- [Configurando credenciais de autenticação nomeadas](vs-azure-tools-setting-up-named-authentication-credentials.md).

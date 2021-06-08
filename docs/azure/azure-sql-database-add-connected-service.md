---
title: Adicionar uma conexão ao Banco de Dados SQL do Azure | Microsoft Docs
description: Adicionar Banco de Dados SQL do Azure conexão ao seu aplicativo usando o Visual Studio Connected Services
author: AngelosP
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 26a01bfe2a34422f9596710f832a1c4af699fd3b
ms.sourcegitcommit: 3fe04d5b931ae459a802a1b965f84186757cbc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2021
ms.locfileid: "111588482"
---
# <a name="add-a-connection-to-azure-sql-database"></a>Adicionar uma conexão ao Banco de Dados SQL do Azure

Com Visual Studio, você pode conectar qualquer uma das seguintes Banco de Dados SQL do Azure usando o **recurso Serviços Conectados:**

- .NET Framework de console
- ASP.NET MVC (.NET Framework) 
- ASP.NET Core
- .NET Core (incluindo aplicativo de console, WPF, Windows Forms, biblioteca de classes)
- Função de trabalho do .NET Core
- Funções do Azure
- Plataforma Universal do Windows aplicativo
- Xamarin
- Cordova

A funcionalidade do serviço conectado adiciona todas as referências necessárias e o código de conexão ao seu projeto, bem como modifica os arquivos de configuração adequadamente.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Serviços conectados no Visual Studio para Mac](/visualstudio/mac/connected-services).
## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio com a carga de trabalho do Azure instalada.
- Um projeto de um dos tipos com suporte

## <a name="connect-to-azure-sql-database-using-connected-services"></a>Conectar-se Banco de Dados SQL do Azure usando serviços conectados

1. Abra o projeto no Visual Studio.

1. No **Gerenciador de Soluções**, clique com  o botão direito do mouse no nó Serviços Conectados e, no menu de contexto, **selecione Adicionar Serviço Conectado**.

1. Na guia **Serviços Conectados,** selecione o ícone + para **Dependências de Serviço**.

    ![Adicionar dependência de serviço](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. Na página **Adicionar Dependência,** selecione **Banco de Dados SQL do Azure**.

    ![Adicionar Banco de Dados SQL do Azure serviço](./media/azure-sql-database-add-connected-service/azure-sql-database.png)

    Se você ainda não tiver se assinado, entre em sua conta do Azure. Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/account/free).

1. Na tela **Configurar Banco de Dados SQL do Azure,** selecione um Banco de Dados SQL do Azure existente e selecione **Próximo.**

    Se você precisar criar um novo componente, vá para a próxima etapa. Caso contrário, passe à etapa 7.

    ![Conectar-se ao componente Banco de Dados SQL do Azure existente](./media/azure-sql-database-add-connected-service/created-azure-sql-database.png)

1. Para criar um Banco de Dados SQL do Azure:

   1. Selecione **Criar um Banco de Dados SQL** na parte inferior da tela.

   1. Preencha o **Banco de Dados SQL do Azure: Criar nova** tela e selecione **Criar**.

       ![Novos Banco de Dados SQL do Azure](./media/azure-sql-database-add-connected-service/create-new-azure-sql-database.png)

   1. Quando a **tela Banco de Dados SQL do Azure** configuração é exibida, o novo banco de dados aparece na lista. Selecione o novo banco de dados na lista e selecione **Próximo.**

1. Insira um nome de cadeia de conexão ou escolha o padrão e escolha se deseja que a cadeia de conexão seja armazenada em um arquivo de segredos local ou em [Azure Key Vault](/azure/key-vault).

   ![Especificar cadeia de conexão](./media/azure-sql-database-add-connected-service/connection-string.png)

1. A **tela Resumo das alterações** mostra todas as modificações que serão feitas em seu projeto se você concluir o processo. Se as alterações parecer OK, escolha **Concluir**.

   ![Resumo das alterações](./media/azure-sql-database-add-connected-service/summary-of-changes.png)

   Se for solicitado a definir regras de firewall, escolha **Sim.**

   ![Regras de firewall](./media/azure-sql-database-add-connected-service/firewall-rules.png)

1. A conexão aparece na seção **Dependências de** Serviço da **guia Serviços Conectados.**

   ![Dependências de serviço](./media/azure-sql-database-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>Confira também

- [Banco de Dados SQL do Azure do produto](https://azure.microsoft.com/services/sql-database/)
- [Documentação do Banco de Dados SQL do Azure](/azure/azure-sql/database/)
- [Serviço conectados (Visual Studio para Mac)](/visualstudio/mac/connected-services)

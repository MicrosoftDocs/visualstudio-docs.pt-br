---
title: Conectar-se a dados em um banco de dados do Access (Windows Forms)
ms.date: 09/15/2017
ms.topic: conceptual
helpviewer_keywords:
- databases, connecting to
- databases, Access
- data [Visual Studio], connecting
- connecting to data, from Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 33981ac76d8c502d56571a112ee8cd1e0c11dce0
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304569"
---
# <a name="connect-to-data-in-an-access-database-windows-forms"></a>Conectar-se a dados em um banco de dados do Access (Windows Forms)

Você pode se conectar a um banco de dados (qualquer um *. mdf* arquivo ou uma *. accdb* arquivo) usando o Visual Studio. Depois de definir a conexão, os dados são exibidos na Janela Fontes de Dados **. Nela, é possível arrastar tabelas ou exibições para os formulários.

## <a name="prerequisites"></a>Pré-requisitos

Para usar esses procedimentos, você precisa de um Aplicativo Windows Forms e de um banco de dados do Access (arquivo .accdb) ou um banco de dados do Access 2000-2003 (arquivo .mdb). Siga o procedimento correspondente ao tipo de arquivo.

## <a name="creating-the-dataset-for-an-accdb-file"></a>Criando o Conjunto de Dados para um arquivo .accdb

Você pode se conectar aos bancos de dados criados por meio de Access 2013, Office 365, Access 2010 ou Access 2007 usando o procedimento a seguir.

### <a name="to-create-the-dataset"></a>Para criar o conjunto de dados

1.  Abra o Aplicativo Windows Forms ao qual você deseja se conectar dados.

2.  Para abrir o **fontes de dados** janela diante a **exibição** menu, selecione **Other Windows** > **fontes de dados**.

     ![Exibir outras fontes de dados do Windows](../data-tools/media/viewdatasources.png)

3.  Na janela Fontes de Dados **, clique em Adicionar Nova Fonte de Dados**.

     O Assistente de Configuração de Fonte de Dados** é aberto.

4.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, selecione **próxima**.

5.  Selecione **conjunto de dados** sobre o **escolha um modelo de banco de dados** página e, em seguida, selecione **próxima**.

6.  Na página Escolha a Conexão de Dados **, selecione Nova Conexão** para configurar uma nova conexão de dados.

     O **Adicionar Conexão** caixa de diálogo é aberta.

7.  Selecione o **alteração** lado a **fonte de dados** caixa de texto.

     O **fonte de dados de alteração** caixa de diálogo é aberta.

8.  Na lista de fontes de dados, escolha  **\<outras\>**. No **provedor de dados** lista suspensa, selecione **.NET Framework Data Provider para OLE DB**, em seguida, escolha **Okey**.

9. Volta a **Adicionar Conexão** caixa de diálogo, selecione **Microsoft Office 12.0 Access Database Engine OLE DB Provider** do **OLE DB Provider** lista suspensa.

     ![OLE DB Provider do Microsoft Office 12.0 Access](../data-tools/media/dataoledbprovideroffice12access.png)

     > [!NOTE]
     > Se você não vir **Microsoft Office 12.0 Access Database Engine OLE DB Provider** na lista suspensa de provedor do OLE DB, talvez você precise instalar o [driver do sistema Office 2007: componentes de conectividade de dados](https://www.microsoft.com/download/confirmation.aspx?id=23734).

9. No **nome do servidor ou o arquivo** caixa de texto, especifique o caminho e nome de arquivo a *. accdb* arquivo que você deseja se conectar a e, em seguida, selecione **Okey**. (Se o arquivo de banco de dados tem um nome de usuário e senha, especifique-os antes de selecionar **Okey**.)

10. Selecione **próxima** sobre o **escolha sua Conexão de dados** página.

     Você pode receber uma caixa de diálogo informando que o arquivo de dados não está no seu projeto atual. Selecione Sim ou Não

11. Selecione **próxima** sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** página.

12. Expanda o nó Tabelas **na página Escolher Objetos do Banco de Dados**.

13. Selecione quaisquer tabelas ou exibições que você deseja em seu conjunto de dados e, em seguida, selecione **concluir**.

     O Conjunto de Dados é adicionado ao projeto, e as tabelas e as exibições são mostradas na janela Fontes de Dados **.

## <a name="create-the-dataset-for-an-mdb-file"></a>Criar o conjunto de dados para um arquivo. mdb

Você cria o conjunto de dados executando o Assistente de Configuração de Fonte de Dados **.

### <a name="to-create-the-dataset"></a>Para criar o conjunto de dados

1.  Abra o Aplicativo Windows Forms ao qual você deseja se conectar dados.

2.  Sobre o **modo de exibição** menu, selecione **Other Windows** > **fontes de dados**.

     ![Exibir outras fontes de dados do Windows](../data-tools/media/viewdatasources.png)

3.  Na janela Fontes de Dados **, clique em Adicionar Nova Fonte de Dados**.

     O Assistente de Configuração de Fonte de Dados** é aberto.

4.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, selecione **próxima**.

5.  Selecione **conjunto de dados** sobre o **escolha um modelo de banco de dados** página e, em seguida, selecione **próxima**.

6.  Na página Escolha a Conexão de Dados **, selecione Nova Conexão** para configurar uma nova conexão de dados.

7.  Se a fonte de dados não for **arquivo de banco de dados do Microsoft Access (OLE DB)**, selecione **alteração** para abrir o **alterar fonte de dados** caixa de diálogo e selecione **Microsoft Acessar o arquivo de banco de dados**e, em seguida, selecione **Okey**.

8.  No **nome do arquivo de banco de dados**, especifique o caminho e nome da *. mdb* arquivo que você deseja se conectar a e, em seguida, selecione **Okey**.

     ![Adicionar o arquivo de banco de dados de acesso de Conexão](../data-tools/media/dataaddconnectionaccessmdb.png)

9. Selecione **próxima** sobre o **escolha sua Conexão de dados** página.

10. Selecione **próxima** sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** página.

11. Expanda o nó Tabelas **na página Escolher Objetos do Banco de Dados**.

12. Selecione quaisquer tabelas ou exibições que você deseja em seu conjunto de dados e, em seguida, selecione **concluir**.

     O Conjunto de Dados é adicionado ao projeto, e as tabelas e as exibições são mostradas na janela Fontes de Dados **.

## <a name="security"></a>Segurança

O armazenamento das informações confidenciais (como uma senha) pode afetar a segurança do aplicativo. O uso da Autenticação do Windows (também conhecida como segurança integrada) é uma maneira mais segura de controlar o acesso a um banco de dados. Para obter mais informações, consulte [Protegendo informações de conexão](/dotnet/framework/data/adonet/protecting-connection-information).

## <a name="next-steps"></a>Próximas etapas

O conjunto de dados que você acabou de criar agora está disponível na **fontes de dados** janela. Agora é possível realizar qualquer uma das seguintes tarefas:

-   Selecione os itens na **fontes de dados** janela e arrastá-los para seu formulário (consulte [controla a associar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)).

-   Abra a fonte de dados no Designer de Conjunto de Dados** para adicionar ou editar os objetos que constituem o conjunto de dados.

-   Adicionar lógica de validação para o <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> eventos das tabelas de dados no conjunto de dados (consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md)).

## <a name="see-also"></a>Consulte também

- [Adicionar conexões](../data-tools/add-new-connections.md)
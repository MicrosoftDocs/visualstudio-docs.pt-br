---
title: Conectar-se a dados em um banco de dados
ms.date: 07/18/2019
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting
- connecting to data, Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 03c92476e8083106a0d301655be3a1779709c1c1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282729"
---
# <a name="connect-to-data-in-an-access-database"></a>Conectar-se a dados em um banco de dados

Você pode se conectar a um banco de dados do Access (um arquivo *. mdb* ou *. accdb* ) usando o Visual Studio. Depois de definir a conexão, os dados são exibidos na janela **Fontes de Dados**. A partir daí, você pode arrastar tabelas ou exibições para a superfície de design.

## <a name="prerequisites"></a>Pré-requisitos

Para usar esses procedimentos, você precisa de um projeto Windows Forms ou WPF e um banco de dados do Access (arquivo *. accdb* ) ou um banco de dados do Access 2000-2003 (arquivo *. mdb* ). Siga o procedimento correspondente ao tipo de arquivo.

## <a name="create-a-dataset-for-an-accdb-file"></a>Criar um conjunto de um DataSet para um arquivo. accdb

Conecte-se a bancos de dados criados com o Office 365, o Access 2013, o Access 2010 ou o Access 2007 usando o procedimento a seguir.

1. Abra um projeto de aplicativo Windows Forms ou WPF no Visual Studio.

2. Para abrir a janela **fontes de dados** , no menu **Exibir** , selecione **outras**  >  **fontes de dados**do Windows.

   ![Exibir outras fontes de dados do Windows](../data-tools/media/viewdatasources.png)

3. Na janela **Fontes de Dados**, clique em **Adicionar Nova Fonte de Dados**.

   O **Assistente de configuração de fonte de dados** é aberto.

4. Selecione **banco** de dados na página **escolher um tipo de fonte de dado** e, em seguida, selecione **Avançar**.

5. Selecione **DataSet** na página **escolher um modelo de banco de dados** e, em seguida, selecione **Avançar**.

6. Na página **Escolha a Conexão de Dados**, selecione **Nova Conexão** para configurar uma nova conexão de dados.

   A caixa de diálogo **Adicionar conexão** é aberta.

7. Se a **fonte de dados** não estiver definida como arquivo de banco de dado do **Microsoft Access**, selecione o botão **alterar** .

   A caixa de diálogo **Alterar fonte de dados** é aberta. Na lista de fontes de dados, escolha **arquivo de banco de dado do Microsoft Access**. Na lista suspensa **provedor de dados** , selecione **.NET Framework provedor de dados para OLE DB**e, em seguida, escolha **OK**.

8. Escolha **procurar** ao lado de **nome do arquivo de banco de dados**e, em seguida, navegue até o arquivo *. accdb* e escolha **abrir**.

9. Insira um nome de usuário e uma senha (se necessário) e, em seguida, escolha **OK**.

10. Selecione **Avançar** na página **escolher sua conexão de dados** .

    Você pode receber uma caixa de diálogo informando que o arquivo de dados não está em seu projeto atual. Selecione **Sim** ou **não**.

11. Selecione **Avançar** na página **salvar cadeia de conexão no arquivo de configuração do aplicativo** .

12. Expanda o nó **Tabelas** na página **Escolher Objetos do Banco de Dados**.

13. Selecione as tabelas ou exibições que você deseja incluir no conjunto de seus conjuntos de seus e, em seguida, selecione **concluir**.

    O Conjunto de Dados é adicionado ao projeto e as tabelas e as exibições são mostradas na janela **Fontes de Dados**.

## <a name="create-a-dataset-for-an-mdb-file"></a>Criar um conjunto de um DataSet para um arquivo. mdb

Conecte-se a bancos de dados criados com o Access 2000-2003 usando o procedimento a seguir.

1. Abra um projeto de aplicativo Windows Forms ou WPF no Visual Studio.

2. No menu **Exibir** , selecione **outras**  >  **fontes de dados**do Windows.

   ![Exibir outras fontes de dados do Windows](../data-tools/media/viewdatasources.png)

3. Na janela **Fontes de Dados**, clique em **Adicionar Nova Fonte de Dados**.

    O **Assistente de configuração de fonte de dados** é aberto.

4. Selecione **banco** de dados na página **escolher um tipo de fonte de dado** e, em seguida, selecione **Avançar**.

5. Selecione **DataSet** na página **escolher um modelo de banco de dados** e, em seguida, selecione **Avançar**.

6. Na página **Escolha a Conexão de Dados**, selecione **Nova Conexão** para configurar uma nova conexão de dados.

7. Se a fonte de dados não for um **arquivo de banco de dado do Microsoft Access (OLE DB)**, selecione **alterar** para abrir a caixa de diálogo **Alterar fonte de dados** e selecione o arquivo de banco de dado **do Microsoft Access**e, em seguida, selecione **OK**.

8. No **nome do arquivo de banco de dados**, especifique o caminho e o nome do arquivo *. mdb* ao qual você deseja se conectar e, em seguida, selecione **OK**.

   ![Adicionar arquivo de banco de dados de acesso de conexão](../data-tools/media/add-connection-access-db.png)

9. Selecione **Avançar** na página **escolher sua conexão de dados** .

10. Selecione **Avançar** na página **salvar cadeia de conexão no arquivo de configuração do aplicativo** .

11. Expanda o nó **Tabelas** na página **Escolher Objetos do Banco de Dados**.

12. Selecione quaisquer tabelas ou exibições desejadas no conjunto de seus conjuntos de seus e, em seguida, selecione **concluir**.

    O Conjunto de Dados é adicionado ao projeto e as tabelas e as exibições são mostradas na janela **Fontes de Dados**.

## <a name="next-steps"></a>Próximas etapas

O conjunto de dados que você acabou de criar está disponível na janela **Data Sources** . Agora é possível realizar qualquer uma das seguintes tarefas:

- Selecione os itens na janela **fontes de dados** e arraste-os para o formulário ou a superfície de design (consulte [associar controles de Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) ou [visão geral da ligação de dados do WPF](/dotnet/desktop-wpf/data/data-binding-overview)).

- Abra a fonte de dados no **Designer de Conjunto de Dados** para adicionar ou editar os objetos que constituem o conjunto de dados.

- Adicione a lógica de validação para o <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> evento ou das tabelas de dados no DataSet (consulte [Validate data in](../data-tools/validate-data-in-datasets.md)DataSets).

## <a name="see-also"></a>Veja também

- [Adicionar conexões](../data-tools/add-new-connections.md)
- [Visão geral da ligação de dados do WPF](/dotnet/framework/wpf/data/data-binding-overview)
- [Windows Forms Associação de dados](/dotnet/framework/winforms/data-binding-and-windows-forms)

---
title: Como salvar e editar cadeias de conexão
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f8ef3a2c-029c-423b-9d9e-a4f1add4f640
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e3cb3f832f308edb42967d2fe4485b3d6885022a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282014"
---
# <a name="how-to-save-and-edit-connection-strings"></a>Como salvar e editar cadeias de conexão
As cadeias de conexão em aplicativos do Visual Studio são salvas no arquivo de configuração do aplicativo (também conhecido como configurações do aplicativo) ou embutidas em código diretamente em seu aplicativo. Salvar cadeias de conexão no arquivo de configuração do aplicativo simplifica a tarefa de realizar a manutenção de seu aplicativo. Se a cadeia de conexão precisar ser alterada, você poderá atualizá-la no arquivo de configurações do aplicativo (em vez de alterá-la no código-fonte e recompilar o aplicativo).

O armazenamento das informações confidenciais (tal como a senha) dentro da cadeia de conexão pode afetar a segurança do aplicativo. Cadeias de conexão salvas no arquivo de configuração do aplicativo não são criptografadas nem ofuscadas, de modo que talvez seja possível que alguém acesse o arquivo e exiba seu conteúdo. O uso da segurança integrada do Windows é uma maneira mais segura de controlar o acesso a um banco de dados.

Se você optar por não usar a segurança integrada do Windows e seu banco de dados exigir um nome de usuário e uma senha, você poderá omiti-los da cadeia de conexão, mas seu aplicativo precisará fornecer essas informações para se conectar com êxito ao banco de dados. Por exemplo, você pode criar uma caixa de diálogo que solicita ao usuário essas informações e compila dinamicamente a cadeia de conexão no tempo de execução. A segurança ainda pode ser um problema se as informações forem interceptadas no caminho para o banco de dados.
Para obter mais informações, confira [Protegendo informações de conexão](/dotnet/framework/data/adonet/protecting-connection-information).

## <a name="to-save-a-connection-string-from-within-the-data-source-configuration-wizard"></a>Para salvar uma cadeia de conexão de dentro do assistente de configuração da fonte de dados
No **Assistente de configuração da fonte de dados**, selecione a opção para salvar a conexão na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** .

## <a name="to-save-a-connection-string-directly-into-application-settings"></a>Para salvar uma cadeia de conexão diretamente nas configurações do aplicativo
1. No **Gerenciador de Soluções**, clique duas vezes no ícone **Meu Projeto** (Visual Basic) ou no ícone **Propriedades** (C#) para abrir o **Designer de Projeto**.
1. Selecione a guia **configurações** .
1. Insira um **Nome** para a cadeia de conexão. Consulte esse nome ao acessar a cadeia de conexão no código.
1. Configure o **Tipo** como (**Cadeia de conexão**).
1. Mantenha o **Escopo** configurado como **Aplicativo**.
1. Digite a cadeia de conexão no campo **valor** ou clique no botão de **reticências** (...) no campo **valor** para abrir a caixa de diálogo **Propriedades da conexão** para criar a cadeia de conexão.

## <a name="edit-connection-strings-stored-in-application-settings"></a>Editar cadeias de conexão armazenadas nas configurações do aplicativo
Você pode modificar as informações da conexão que são salvas nas configurações do aplicativo usando o **Designer de Projeto**.

### <a name="to-edit-a-connection-string-stored-in-application-settings"></a>Para editar uma cadeia de conexão nas configurações do aplicativo
1. No **Gerenciador de Soluções**, clique duas vezes no ícone **Meu Projeto** (Visual Basic) ou no ícone **Propriedades** (C#) para abrir o **Designer de Projeto**.
1. Selecione a guia **configurações** .
1. Localize a conexão que você deseja editar e selecione o texto no campo **valor** .
1. Edite a cadeia de conexão no campo **valor** ou clique no botão de **reticências** (...) no campo **valor** para editar a conexão com a caixa de diálogo **Propriedades da conexão** .

## <a name="edit-connection-strings-for-datasets"></a>Editar cadeias de conexão para conjuntos de os
Você pode modificar as informações de conexão para cada TableAdapter em um conjunto de dados.

### <a name="to-edit-a-connection-string-for-a-tableadapter-in-a-dataset"></a>Para editar uma cadeia de conexão para um TableAdapter em um DataSet
1. Em **Gerenciador de soluções**, clique duas vezes no conjunto de arquivos (arquivo **. xsd** ) que tem a conexão que você deseja editar.
1. Selecione o **TableAdapter** ou a consulta que tem a conexão que você deseja editar.
1. Na janela **Propriedades** , expanda o **nó conexão**.
1. Para modificar rapidamente a cadeia de conexão, edite a propriedade **ConnectionString** ou clique na seta para baixo na propriedade de **conexão** e escolha **nova conexão**.

## <a name="security"></a>Segurança
O armazenamento das informações confidenciais (tal como uma senha) dentro da cadeia de conexão pode afetar a segurança do aplicativo. O uso da segurança integrada do Windows é uma maneira mais segura de controlar o acesso a um banco de dados.
Para obter mais informações, confira [Protegendo informações de conexão](/dotnet/framework/data/adonet/protecting-connection-information).

## <a name="see-also"></a>Veja também

- [Adicionando conexões](../data-tools/add-new-connections.md)

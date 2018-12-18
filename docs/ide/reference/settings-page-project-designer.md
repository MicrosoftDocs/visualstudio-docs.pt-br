---
title: Página Configurações, Designer de Projeto
ms.date: 06/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- ApplicationSettingsOverview
helpviewer_keywords:
- Settings page in Project Designer
- Project Designer, Settings page
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5c0f7b47b56522f5c4aeef0054e6b7b52434ff87
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "35602057"
---
# <a name="settings-page-project-designer"></a>Página de configurações, Designer de Projeto

Use a página **Configurações** do Designer de Projeto para especificar as configurações de aplicativo do projeto. As configurações de aplicativo permitem armazenar e recuperar as configurações de propriedade e outras informações para seu aplicativo dinamicamente. Elas também permitem que você mantenha aplicativos personalizados e preferências do usuário em um computador cliente. Para obter mais informações, confira [Gerenciar configurações de aplicativo](../managing-application-settings-dotnet.md).

Para acessar a página **Configurações**, selecione um nó do projeto no **Gerenciador de Soluções** e, em seguida, selecione **Projeto** > **Propriedades**. Quando o Designer de Projeto for exibido, selecione a guia **Configurações**.

## <a name="header-bar"></a>Barra de cabeçalho

A barra de cabeçalho na parte superior da página **Configurações** contém vários controles:

**Sincronizar**

**Sincronizar** restaura as configurações no escopo do usuário que o aplicativo usa no tempo de execução ou durante a depuração para seus valores padrão, conforme a definição no tempo de design. Para restaurar os dados, remova os arquivos específicos do aplicativo gerados pelo tempo de execução do disco, não dos dados do projeto.

**Carregar Configurações da Web**

**Carregar Configurações da Web** exibe uma caixa de diálogo **Logon** que permite carregar as configurações de um usuário autenticado ou de usuários anônimos. Este botão fica habilitado apenas quando você habilita os serviços de aplicativo cliente na página **Serviços** e especifica um **Local de serviço das configurações da Web**.

**Exibir Código**

Para projetos C#, o botão **Exibir Código** permite que você exiba o código no arquivo *Settings.cs*. Esse arquivo define a classe `Settings`, que permite que você manipule eventos específicos no objeto `Settings`. Em linguagens diferentes do Visual Basic, você precisa chamar o método `Save` explicitamente dessa classe wrapper para que as configurações do usuário persistam. Geralmente isso é feito no manipulador de eventos **Closing** do formulário principal. A seguir está um exemplo de uma chamada ao método `Save`:

```csharp
Properties.Settings.Default.Save();
```

Para projetos do Visual Basic, o botão **Exibir Código** permite que você exiba o código no arquivo *Settings.vb*. Esse arquivo define a classe `MySettings`, que permite que você manipule eventos específicos no objeto `My.Settings`. Para obter mais informações de como acessar as configurações de aplicativo usando o objeto `My.Settings`, confira [Acessando configurações de aplicativo](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings).

Para obter mais informações de como acessar as configurações do aplicativo, confira [Configurações de aplicativo para Windows Forms](/dotnet/framework/winforms/advanced/application-settings-for-windows-forms).

**Modificador de acesso**

O botão **Modificador de acesso** especifica o nível de acesso das classes auxiliares `Properties.Settings` (em C#) ou `My.Settings` (em Visual Basic) que o Visual Studio gera no *Settings.Designer.cs* ou no *Settings.Designer.vb*.

Para projetos do Visual C#, o modificador de acesso pode ser **Interno** ou **Público**.

Para projetos do Visual Basic, o modificador de acesso pode ser **Amigo** ou **Público**.

Por padrão, a configuração é **Interno** em C# e **Amigo** em Visual Basic. Quando o Visual Studio gera classes auxiliares como **Interno** ou **Amigo**, os aplicativos executáveis (*.exe*) não podem acessar os recursos e as configurações que você adiciona às bibliotecas de classes (arquivos *.dll*). Se você precisar compartilhar recursos e configurações de uma biblioteca de classes, defina o modificador de acesso como **Público**.

Para obter mais informações sobre as classes auxiliares de configurações, confira [Gerenciar configurações de aplicativo](../managing-application-settings-dotnet.md).

## <a name="settings-grid"></a>Grade de configurações

A **Grade de configurações** é usada para definir as configurações do aplicativo. Essa grade inclui as seguintes colunas:

**Nome**

Insira o nome da configuração de aplicativo neste campo.

**Tipo**

Use a lista suspensa para selecionar um tipo para a configuração. Os tipos usados com mais frequência são exibidos na lista suspensa, por exemplo, **Cadeia de caracteres**, **(Cadeia de Conexão)** e **System.Drawing.Font**. Você pode escolher outro tipo, selecionando **Procurar** no final da lista e, em seguida, escolhendo um tipo na caixa de diálogo **Selecionar um Tipo**. Depois de escolher um tipo, ele é adicionado aos tipos mais comuns na lista suspensa (somente para a solução atual).

**Escopo**

Selecione **Aplicativo** ou **Usuário**.

As configurações no escopo do aplicativo, como as cadeias de conexão, são associadas ao aplicativo. Os usuários não podem alterar as configurações no escopo do aplicativo no tempo de execução.

As configurações no escopo do usuário, como fontes do sistema, devem ser usadas para as preferências do usuário. Os usuários podem alterá-las no tempo de execução.

**Value**

Os dados ou o valor associado à configuração de aplicativo. Por exemplo, se a configuração for uma fonte, seu valor poderá ser **Verdana, 9.75pt, style=Bold**.

## <a name="see-also"></a>Consulte também

- [Gerenciar configurações de aplicativo](../managing-application-settings-dotnet.md)
- [Acessar configurações de aplicativo (Visual Basic)](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings)
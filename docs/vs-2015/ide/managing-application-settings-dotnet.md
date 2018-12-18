---
title: Gerenciando configurações de aplicativo (.NET) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- msvse_settingsdesigner.err.nameblank
helpviewer_keywords:
- application settings [Visual Studio]
ms.assetid: 35254321-ad14-47d9-b8c6-39ab3203c5d9
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ac4f670b813970d027925b681a2e3211e1898e1a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49866123"
---
# <a name="managing-application-settings-net"></a>Gerenciando configurações de aplicativo (.NET)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As configurações de aplicativo permitem armazenar informações do aplicativo dinamicamente. As configurações permitem que você armazene informações no computador cliente que não devem ser incluídas no código do aplicativo (por exemplo, uma cadeia de conexão), as preferências do usuário e outras informações necessárias em tempo de execução.  
  
 As configurações de aplicativo substituem as propriedades dinâmicas usadas em versões anteriores do Visual Studio.  
  
 Cada configuração de aplicativo deve ter um nome exclusivo. O nome pode ser qualquer combinação de letras, números ou um sublinhado que não comece com um número e não pode conter espaços. O nome pode ser alterado por meio da propriedade `Name`.  
  
 As configurações do aplicativo podem ser armazenadas como qualquer tipo de dados que pode ser serializado para XML ou tem um `TypeConverter` que implementa `ToString`/`FromString`. Os tipos mais comuns são `String`, `Integer` e `Boolean`, mas você também pode armazenar valores como <xref:System.Drawing.Color>, <xref:System.Object> ou como uma cadeia de conexão.  
  
 As configurações do aplicativo também contêm um valor. O valor é definido com a propriedade **Valor** e deve corresponder ao tipo de dados da configuração.  
  
 Além disso, as configurações de aplicativo podem ser associadas a uma propriedade de um formulário ou controle em tempo de design.  
  
 Há dois tipos de configurações de aplicativo, com base no escopo:  
  
- Configurações de escopo do aplicativo podem ser usadas para informações como uma URL para um serviço Web ou uma cadeia de conexão de banco de dados. Esses valores são associados ao aplicativo. Portanto, os usuários não podem alterá-los em tempo de execução.  
  
- Configurações de escopo do usuário podem ser usadas para informações, como persistir a última posição de um formulário ou uma preferência de fonte. Os usuários podem alterar esses valores em tempo de execução.  
  
  Você pode alterar o tipo de uma configuração usando a propriedade **Escopo**.  
  
  O sistema do projeto armazena configurações de aplicativo em dois arquivos XML: um arquivo app.config, que é criado em tempo de design ao criar a primeira configuração de aplicativo e um arquivo user.config, que é criado em tempo de execução quando o usuário executando o aplicativo altera o valor de qualquer configuração do usuário. Observe que as alterações nas configurações do usuário não são gravadas em disco, a menos que o aplicativo especificamente chame um método para fazer isso.  
  
## <a name="creating-application-settings-at-design-time"></a>Criando configurações de aplicativo em tempo de design  
 Em tempo de design, você pode criar configurações de aplicativo de duas maneiras: usando a página **Configurações** do **Designer de Projeto** ou usando a janela **Propriedades** de um formulário ou controle, que permite que você associe uma configuração a uma propriedade.  
  
 Quando você cria uma configuração de escopo do aplicativo (por exemplo, uma cadeia de conexão de banco de dados ou uma referência a recursos de servidor), [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] a salva no app.config com a marca `<applicationSettings>`. (As cadeias de conexão são salvas sob a marca `<connectionStrings>`.)  
  
 Quando você cria uma configuração de escopo do usuário (por exemplo, fonte padrão, página inicial ou tamanho da janela), [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] a salva no app.config com a marca `<userSettings>`.  
  
> [!IMPORTANT]
>  Quando você armazena cadeias de conexão no app.config, você deve tomar precauções para evitar revelar informações confidenciais como senhas ou caminhos de servidor na cadeia de conexão.  
>   
>  Se você obtiver as informações de cadeia de conexão de uma fonte externa, como um usuário fornecendo uma ID de usuário e senha, deverá ter cuidado para garantir que os valores usados para construir a cadeia de conexão não contêm parâmetros de cadeia de conexão adicionais que alteram o comportamento da conexão.  
>   
>  Considere usar o recurso Configuração Protegida para criptografar informações confidenciais no arquivo de configuração. Consulte [Protegendo informações de conexão](http://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4) para obter mais informações.  
  
> [!NOTE]
>  Como não há nenhum modelo de arquivo de configuração para bibliotecas de classes, as configurações de aplicativo não se aplicam a projetos de biblioteca de classes. A exceção é um projeto de DLL das Ferramentas do Visual Studio para Office, que pode ter um arquivo de configuração.  
  
## <a name="using-customized-settings-files"></a>Usando arquivos de configurações personalizadas  
 Você pode adicionar arquivos de configurações personalizadas ao seu projeto para um gerenciamento conveniente de grupos de configurações. As configurações contidas em um único arquivo são carregadas e salvas como uma unidade. Portanto, ser capaz de armazenar as configurações em arquivos separados para grupos usados com frequência e usados raramente pode poupar tempo ao carregar e salvar as configurações.  
  
 Por exemplo, você pode adicionar um arquivo como SpecialSettings.settings ao projeto. Embora a classe `SpecialSettings` não seja exposta no namespace `My`, **Exibir Código** pode ler o arquivo de configurações personalizadas que contém `Partial Class SpecialSettings`.  
  
 O Designer de Configurações primeiro pesquisa o arquivo Settings.settings que o sistema do projeto cria, esse é o arquivo padrão que o Designer de Projeto exibe na guia **Configurações**. Settings.settings está localizado na pasta Meu Projeto para projetos [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e na pasta Propriedades para projetos [!INCLUDE[csprcs](../includes/csprcs-md.md)]. O Designer de Projeto pesquisa então outros arquivos de configurações na pasta raiz do projeto. Portanto, você deve colocar o arquivo de configurações personalizado lá. Se você adicionar um arquivo .settings em outro lugar no projeto, o Designer de Projeto não conseguirá localizá-lo.  
  
## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-basic"></a>Acessando ou alterando as configurações de aplicativo em tempo de execução no Visual Basic  
 Em projetos [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], você pode acessar as configurações de aplicativo em tempo de execução usando o objeto `My.Settings`. Na página **Configurações**, clique no botão **Exibir código** para exibir o arquivo Settings.vb. Settings.vb define a classe `Settings`, que permite que você manipule esses eventos nas classes de configurações <xref:System.Configuration.ApplicationSettingsBase.SettingChanging>, <xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>, <xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded> e <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>. Observe que a classe `Settings` no Settings.vb é uma classe parcial que mostra apenas o código de propriedade do usuário, não toda a classe gerada. Para obter mais informações sobre como acessar as configurações de aplicativo usando o objeto `My.Settings`, consulte [Acessando configurações de aplicativo](http://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e).  
  
 Os valores de quaisquer configurações de escopo do usuário que o usuário alterar em tempo de execução (por exemplo, a posição de um formulário) são armazenados em um arquivo user.config. Observe que os valores padrão ainda são salvos no app.config.  
  
 Se você tiver alterado quaisquer configurações de escopo do usuário durante o tempo de execução, por exemplo no teste do aplicativo e desejar redefinir essas configurações para seus valores padrão, clique no botão **Sincronizar**.  
  
 É altamente recomendável que você use o objeto `My.Settings` e o arquivo .settings padrão para acessar as configurações. Isso ocorre porque você pode usar o Designer de Configurações para atribuir propriedades às configurações e, adicionalmente, as configurações de usuário são automaticamente salvas antes do desligamento do aplicativo. No entanto, seu aplicativo [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] pode acessar as configurações diretamente. Nesse caso você precisa acessar a classe `MySettings` e usar um arquivo .settings personalizado na raiz do projeto. Você também deve salvar as configurações do usuário antes de encerrar o aplicativo, como você faria para um aplicativo C#. Isso é descrito na próxima seção.  
  
## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-c"></a>Acessando ou alterando as configurações de aplicativo em tempo de execução no Visual C#  
 Em linguagens diferentes do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], como [!INCLUDE[csprcs](../includes/csprcs-md.md)], você deve acessar a classe `Settings` diretamente, conforme mostrado no exemplo [!INCLUDE[csprcs](../includes/csprcs-md.md)] a seguir.  
  
```csharp  
Properties.Settings.Default.FirstUserSetting = "abc";  
```  
  
 Você deve explicitamente chamar o método `Save` dessa classe wrapper para persistir as configurações do usuário. Geralmente isso é feito no manipulador de eventos `Closing` do formulário principal. O exemplo [!INCLUDE[csprcs](../includes/csprcs-md.md)] a seguir mostra uma chamada para o método `Save`.  
  
```csharp  
Properties.Settings.Default.Save();  
```  
  
 Para obter informações gerais sobre como acessar as configurações de aplicativo por meio da classe `Settings`, consulte [Visão geral sobre configurações de aplicativo](http://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc). Para obter informações sobre como fazer a iteração por meio das configurações, consulte esta [postagem no fórum](http://social.msdn.microsoft.com/Forums/vstudio/40fbb470-f1e8-4a02-a4a0-9f62b54d0fc4/is-this-possible-propertiessettingsdefault?forum=csharpgeneral).  
  
## <a name="see-also"></a>Consulte também  
 [Acessando configurações de aplicativo](http://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e)




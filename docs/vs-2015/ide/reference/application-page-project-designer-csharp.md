---
title: Página de Aplicativo, Designer de Projeto (C#) | Microsoft Docs
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
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
ms.assetid: f13701a8-4e2e-4474-9d60-bb43decbe0c1
caps.latest.revision: 61
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4a130a04be7a0645fef44ff6c8ae9dcc31b55dcf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867228"
---
# <a name="application-page-project-designer-c"></a>Página Aplicativo, Designer de Projeto (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use a página **Aplicativo** do **Designer de Projeto** para especificar as propriedades e configurações de aplicativo do projeto.  
  
 Para acessar a página **Aplicativo**, escolha um nó de projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto**, **Propriedades** na barra de menus. Quando o Designer de Projeto for exibido, clique na guia **Aplicativo**.  
  
 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]  
  
## <a name="general-application-settings"></a>Configurações Gerais de Aplicativos  
 As opções a seguir permitem definir as configurações gerais para o aplicativo.  
  
 **Nome do assembly**  
 Especifica o nome do arquivo de saída que guardará o manifesto do assembly. Alterar essa propriedade também alterará a propriedade **Nome de Saída**. Também é possível fazer essa alteração na linha de comando usando [/out (opções do compilador C#)](http://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5). Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.AssemblyName%2A>.  
  
 **Namespace padrão**  
 Especifica o namespace base para arquivos adicionados ao projeto.  
  
 Consulte [namespace](http://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f) para obter mais informações sobre a criação de namespaces em seu código.  
  
 Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.RootNamespace%2A>.  
  
 **Estrutura de destino**  
 Especifica a versão no .NET Framework que o aplicativo direciona. Essa opção pode ter valores diferentes dependendo de quais versões do .NET Framework estão instaladas em seu computador.  
  
 Por padrão, o valor é o mesmo que a estrutura de destino selecionada na caixa de diálogo **Novo Projeto**.  
  
> [!NOTE]
>  Os pacotes de pré-requisitos listados na [Caixa de diálogo Pré-requisitos](../../ide/reference/prerequisites-dialog-box.md) são definidos automaticamente na primeira vez em que a caixa de diálogo é aberta. Se você alterar posteriormente a estrutura de destino do projeto, será necessário selecionar os pré-requisitos manualmente para corresponder à nova estrutura de destino.  
  
 Para obter mais informações, consulte [Como destinar uma versão do .NET Framework](../../ide/how-to-target-a-version-of-the-dotnet-framework.md) e [Visão geral de multiplataforma Visual Studio](../../ide/visual-studio-multi-targeting-overview.md).  
  
 **Tipo de aplicativo**  
 Especifica o tipo de aplicativo a ser compilado. Para aplicativos [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)], é possível especificar **aplicativo da Windows Store**, **Biblioteca de Classes** ou **Arquivo WinMD**. Para a maioria dos outros tipos de aplicativo, é possível especificar **aplicativos do Windows**, **aplicativo de Console**, **Biblioteca de Classes**, **Serviço Windows** ou **Biblioteca de Controles da Web**.  
  
 Para um projeto de aplicativo Web, é necessário especificar **Biblioteca de Classes**.  
  
 Se você especificar a opção **Arquivo WinMD**, os tipos poderão ser projetados em uma linguagem de programação do Windows Runtime. Ao empacotar a saída do projeto como um arquivo WinMD, é possível codificar um aplicativo em várias linguagens e ter interoperação de código como se você tivesse escrito tudo na mesma linguagem. É possível especificar esta opção para soluções que direcionam as bibliotecas do Windows Runtime, incluindo os aplicativos [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)]. Para obter mais informações, consulte [Criando componentes do Windows Runtime em C# e Visual Basic](http://go.microsoft.com/fwlink/?LinkId=231895).  
  
> [!NOTE]
>  O Windows Runtime pode projetar tipos para que eles sejam exibidos como objetos nativos em qualquer que os use. Por exemplo, aplicativos JavaScript que interagem com o Windows Runtime usam-no como um conjunto de objetos JavaScript e aplicativos C# usam a biblioteca como uma coleção de objetos .NET. Ao empacotar a saída do projeto como um arquivo WinMD, é possível usar a mesma tecnologia que o Windows Runtime usa.  
  
 Para obter mais informações sobre a propriedade **Tipo de aplicativo**, consulte [/target (Opções do compilador do C#)](http://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f). Para obter informações sobre como acessar esta propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.OutputType%2A>.  
  
 **Informações do assembly**  
 Clicar neste botão para exibe a [Caixa de diálogo Informações do Assembly](../../ide/reference/assembly-information-dialog-box.md).  
  
 **Objeto de inicialização**  
 Define o ponto de entrada a ser chamado quando o aplicativo é carregado. Geralmente, isso é definido como o principal formulário em seu aplicativo ou como o procedimento `Main` que deve ser executado quando o aplicativo é iniciado. Como as bibliotecas de classe não têm um ponto de entrada, sua única opção para essa propriedade é **(Não definido)**.  
  
 Por padrão, em um projeto do Aplicativo de Navegador do WPF, essa opção é **(Não definido)**. A outra opção é *Projectname*.App. Nesse tipo de projeto, é necessário definir o URI de inicialização para carregar um recurso de interface do usuário quando o aplicativo é iniciado. Para fazer isso, abra o arquivo Application.xaml em seu projeto e defina a propriedade `StartupUri` como um arquivo .xaml em seu projeto, como Window1.xaml. Para obter uma lista dos elementos raiz aceitáveis, consulte <xref:System.Windows.Application.StartupUri%2A>. Também é necessário definir um método `public static void Main()` em uma classe no projeto. Essa classe será exibida na lista **Objeto de inicialização** como *ProjectName.ClassName*. Em seguida, é possível selecionar a classe como o objeto de inicialização.  
  
 Consulte [/main (Opções do compilador do C#)](http://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049) para obter mais informações. Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.StartupObject%2A>.  
  
## <a name="resources"></a>Recursos  
 As opções a seguir permitem definir as configurações gerais para o aplicativo.  
  
 **Ícone e manifesto**  
 Por padrão, este botão de opção é selecionado e as opções **Ícone** e **Manifesto** são habilitadas. Isso permite selecionar seu próprio ícone ou diferentes opções de geração de manifesto. Deixe esse botão de opção selecionado, a menos que você esteja fornecendo um arquivo de recurso para o projeto.  
  
 **Ícone**  
 Define o arquivo .ico que você deseja usar como o ícone do programa. Clique no botão de reticências para procurar um gráfico existente ou digite o nome do arquivo que você deseja. Consulte [-win32icon](http://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138) (Opções do compilador do C#) para obter mais informações. Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>.  
  
 **Manifesto**  
 Seleciona uma opção de geração de manifesto quando o aplicativo é executado no Windows Vista no UAC (Controle de Conta de Usuário). Essa opção pode ter os seguintes valores:  
  
- **Inserir manifesto com configurações padrão**. Dá suporte à maneira típica como o Visual Studio funciona no Windows Vista, que é inserir as informações de segurança no arquivo executável do aplicativo, especificando que `requestedExecutionLevel` seja `AsInvoker`. Esta é a opção padrão.  
  
- **Criar aplicativo sem um manifesto**. Esse método é conhecido como *virtualização*. Use essa opção para compatibilidade com aplicativos anteriores.  
  
- **Properties\app.manifest**. Essa opção é necessária para aplicativos implantados pelo ClickOnce ou COM sem registro. Se você publicar um aplicativo usando a implantação do ClickOnce, **Manifesto** será definido automaticamente como essa opção.  
  
  **Arquivo de recurso**  
  Selecione esse botão de opção quando você estiver fornecendo um arquivo de recurso para o projeto. Selecionar essa opção desabilita as opções **Ícone** e **Manifesto**.  
  
  Insira um nome de caminho ou use o botão Procurar (**...** ) para adicionar um arquivo de recurso Win32 ao projeto.  
  
## <a name="see-also"></a>Consulte também  
[Gerenciando propriedades do aplicativo](../../ide/application-properties.md)  
 [Escrevendo código em soluções do Office](http://msdn.microsoft.com/library/2d4d8fd0-e881-4829-976f-0d1a9221dec0)




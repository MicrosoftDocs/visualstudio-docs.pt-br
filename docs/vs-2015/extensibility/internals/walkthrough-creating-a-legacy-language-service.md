---
title: 'Passo a passo: Criando um serviço de linguagem herdado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
caps.latest.revision: 20
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0d80b40aa1db779c233dea846b49dbbc66084015
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783877"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>Passo a passo: criando um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Usando as classes de linguagem do framework (MPF) de pacote gerenciado para implementar um serviço de linguagem no [!INCLUDE[csprcs](../../includes/csprcs-md.md)] é simples. Você precisa de um VSPackage para hospedar o serviço de linguagem, o serviço de linguagem e um analisador para seu idioma.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../../extensibility/visual-studio-sdk.md).  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Locais para o modelo de projeto de pacote do Visual Studio  
 O modelo de projeto do Visual Studio pacote podem ser encontrado em três locais de modelo diferente na **novo projeto** caixa de diálogo:  
  
1.  Sob a extensibilidade do Visual Basic. O idioma padrão do projeto é o Visual Basic.  
  
2.  Sob c# extensibilidade. O idioma padrão do projeto é c#.  
  
3.  Em outra extensibilidade de tipos de projeto. O idioma padrão do projeto é C++.  
  
### <a name="create-a-vspackage"></a>Crie um VSPackage  
  
1.  Crie um novo VSPackage com o modelo de projeto do Visual Studio Package.  
  
     Se você estiver adicionando um serviço de linguagem a um VSPackage existente, ignore as etapas a seguir e ir diretamente para o procedimento "Criar a classe de serviço de linguagem".  
  
2.  Digite MyLanguagePackage para o nome do projeto e clique em **Okey**.  
  
     Você pode usar qualquer nome que você deseja. Esses procedimentos detalhados aqui pressupõem MyLanguagePackage como o nome.  
  
3.  Selecione [!INCLUDE[csprcs](../../includes/csprcs-md.md)] como a linguagem e a opção de gerar um novo arquivo de chave. Clique em **Avançar**.  
  
4.  Insira as informações da empresa e o pacote apropriadas. Clique em **Avançar**.  
  
5.  Selecione **comando de Menu**. Clique em **Avançar**.  
  
     Se você não pretende dar suporte a trechos de código, basta clicar em Concluir e ignorar a próxima etapa.  
  
6.  Insira **Inserir trecho** como o **comando nome** e `cmdidInsertSnippet` para o **ID do comando**. Clique em **Finalizar**.  
  
     O **nome do comando** e **ID de comando** pode ser que você quiser, esses são apenas exemplos.  
  
### <a name="create-the-language-service-class"></a>Criar a classe de serviço de linguagem  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no projeto MyLanguagePackage, escolha **Add**, **referência**e, em seguida, escolha o **adicionar nova referência** botão.  
  
2.  No **adicionar referência** caixa de diálogo, selecione **Microsoft.VisualStudio.Package.LanguageService** no **.NET** guia e clique em **Okey**.  
  
     Isso precisa ser feito apenas uma vez para o projeto de pacote de idioma.  
  
3.  Na **Gerenciador de soluções**, clique com botão direito no projeto de VSPackage e selecione **Add**, **classe**.  
  
4.  Certifique-se **classe** está selecionado na lista de modelos.  
  
5.  Insira **MyLanguageService.cs** para o nome do arquivo de classe e clique **Add**.  
  
     Você pode usar qualquer nome que você deseja. Esses procedimentos detalhados aqui supõem `MyLanguageService` como o nome.  
  
6.  No arquivo MyLanguageService.cs, adicione o seguinte `using` instruções.  
  
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs#1)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb#1)]  
  
7.  Modificar a `MyLanguageService` classe para derivar o <xref:Microsoft.VisualStudio.Package.LanguageService> classe:  
  
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs#2)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb#2)]  
  
8.  Posicione o cursor em "LanguageService" e a partir de **edite**, **IntelliSense** menu, selecione **implementar classe abstrata**. Isso adiciona os métodos mínimos necessários para implementar uma classe de serviço de linguagem.  
  
9. Implementar os métodos abstratos, conforme descrito em [implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md).  
  
### <a name="register-the-language-service"></a>Registrar o serviço de linguagem  
  
1.  Abra o arquivo MyLanguagePackagePackage.cs e adicione o seguinte `using` instruções:  
  
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguagepackagepackage.cs#3)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguagepackagepackage.vb#3)]  
  
2.  Registrar sua classe de serviço de linguagem, conforme descrito em [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md). Isso inclui os atributos de ProvideXX e as seções "Proffering o serviço de linguagem". Use MyLanguageService onde este tópico usa TestLanguageService.  
  
### <a name="the-parser-and-scanner"></a>O analisador e Scanner  
  
1.  Implementar um analisador e scanner para o seu idioma, conforme descrito em [analisador de serviço de linguagem herdado e o Scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md).  
  
     Como você implementa o analisador e scanner cabe a você e está além do escopo deste tópico.  
  
## <a name="language-service-features"></a>Recursos do serviço de linguagem  
 Para implementar cada recurso no serviço de linguagem, você normalmente deriva uma classe da classe de serviço de linguagem MPF apropriada, implementa todos os métodos abstratos conforme necessário e substituir os métodos apropriados. Quais classes que você cria e/ou deriva está depende dos recursos que você pretende dar suporte. Esses recursos são discutidos em detalhes no [recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md). O procedimento a seguir é a abordagem geral derivando uma classe de classes MPF.  
  
#### <a name="deriving-from-an-mpf-class"></a>Derivando de uma classe MPF  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no projeto de VSPackage e selecione **Add**, **classe**.  
  
2.  Certifique-se **classe** está selecionado na lista de modelos.  
  
     Insira um nome adequado para o arquivo de classe e clique em **adicionar**.  
  
3.  No novo arquivo de classe, adicione o seguinte `using` instruções.  
  
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs#4)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb#4)]  
  
4.  Modifique a classe para derivar da classe MPF desejado.  
  
5.  Adicione um construtor de classe que pelo menos usa os mesmos parâmetros de construtor da classe base e passar os parâmetros do construtor para o construtor de classe base.  
  
     Por exemplo, o construtor para uma classe derivada do <xref:Microsoft.VisualStudio.Package.Source> classe pode parecer com o seguinte:  
  
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs#5)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb#5)]  
  
6.  Dos **edite**, **IntelliSense** menu, selecione **implementar classe abstrata** se a classe base tem quaisquer métodos abstratos que devem ser implementados.  
  
7.  Caso contrário, posicione o cursor dentro da classe e insira o método a ser substituído.  
  
     Por exemplo, digite `public override` para ver uma lista de todos os métodos que podem ser substituídos nessa classe.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)


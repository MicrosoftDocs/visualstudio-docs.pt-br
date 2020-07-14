---
title: 'Walkthrough: Criando um serviço de idioma herdado | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbdad85dd1c0f62b22bb33b5ed6ab2c597e62164
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905983"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>Passo a passo: criando um serviço de linguagem herdado
Usar as classes de linguagem MPF (Managed Package Framework) para implementar um serviço de linguagem no [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] é simples. Você precisa de um VSPackage para hospedar o serviço de idioma, o próprio serviço de linguagem e um analisador para seu idioma.

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../../extensibility/visual-studio-sdk.md).

## <a name="locations-for-the-visual-studio-package-project-template"></a>Locais para o modelo de projeto de pacote do Visual Studio
 O modelo de projeto de pacote do Visual Studio pode ser encontrado em três locais de modelo diferentes na caixa de diálogo **novo projeto** :

1. Em extensibilidade de Visual Basic. O idioma padrão do projeto é Visual Basic.

2. Em extensibilidade do C#. O idioma padrão do projeto é C#.

3. Em outra extensibilidade de tipos de projeto. O idioma padrão do projeto é C++.

### <a name="create-a-vspackage"></a>Criar um VSPackage

1. Crie um novo VSPackage com o modelo de projeto de pacote do Visual Studio.

    Se você estiver adicionando um serviço de idioma a um VSPackage existente, ignore as etapas a seguir e vá diretamente para o procedimento "criar a classe de serviço de linguagem".

2. Digite MyLanguagePackage para o nome do projeto e clique em **OK**.

    Você pode usar qualquer nome que desejar. Esses procedimentos detalhados aqui pressupõem MyLanguagePackage como o nome.

3. Selecione [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] como o idioma e a opção para gerar um novo arquivo de chave. Clique em **Próximo**.

4. Insira as informações apropriadas da empresa e do pacote. Clique em **Próximo**.

5. Selecione o **comando de menu**. Clique em **Próximo**.

    Se você não pretende dar suporte a trechos de código, basta clicar em concluir e ignorar a próxima etapa.

6. Insira o **trecho de inserção** como o nome do **comando** e `cmdidInsertSnippet` para a **ID de comando**. Clique em **Concluir**.

    O **nome do comando** e a **ID do comando** podem ser os seus que você desejar. eles são apenas exemplos.

### <a name="create-the-language-service-class"></a>Criar a classe de serviço de linguagem

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto MyLanguagePackage, escolha **Adicionar**, **referência**e, em seguida, escolha o botão **Adicionar nova referência** .

2. Na caixa de diálogo **Adicionar referência** , selecione **Microsoft. VisualStudio. Package. LanguageService** na guia **.net** e clique em **OK**.

     Isso precisa ser feito apenas uma vez para o projeto de pacote de idioma.

3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto VSPackage e selecione **Adicionar**, **classe**.

4. Verifique se a **classe** está selecionada na lista modelos.

5. Digite **MyLanguageService.cs** para o nome do arquivo de classe e clique em **Adicionar**.

     Você pode usar qualquer nome que desejar. Esses procedimentos detalhados aqui presumem `MyLanguageService` como o nome.

6. No arquivo MyLanguageService.cs, adicione as seguintes `using` diretivas.

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_1.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_1.vb)]

7. Modifique a `MyLanguageService` classe para derivar da <xref:Microsoft.VisualStudio.Package.LanguageService> classe:

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_2.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_2.vb)]

8. Posicione o cursor em "LanguageService" e, no menu **Editar**, **IntelliSense** , selecione **implementar classe abstrata**. Isso adiciona os métodos mínimos necessários para implementar uma classe de serviço de linguagem.

9. Implemente os métodos abstratos conforme descrito em [implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md).

### <a name="register-the-language-service"></a>Registrar o serviço de idioma

1. Abra o arquivo MyLanguagePackagePackage.cs e adicione as seguintes `using` diretivas:

     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_3.vb)]
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_3.cs)]

2. Registre sua classe de serviço de linguagem conforme descrito em [registrando um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md). Isso inclui os atributos ProvideXX e as seções "Proffering The Language Service". Use MyLanguageService em que este tópico usa TestLanguageService.

### <a name="the-parser-and-scanner"></a>O analisador e o scanner

1. Implemente um analisador e um scanner para sua linguagem, conforme descrito em [analisador e verificador de serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md).

     A maneira como você implementa o analisador e o scanner está inteiramente em você e está além do escopo deste tópico.

## <a name="language-service-features"></a>Recursos do serviço de linguagem
 Para implementar cada recurso no serviço de idioma, normalmente você deriva uma classe da classe de serviço de linguagem MPF apropriada, implementa quaisquer métodos abstratos conforme necessário e substitui os métodos apropriados. As classes que você cria e/ou deriva dependem dos recursos aos quais você pretende dar suporte. Esses recursos são discutidos em detalhes em [recursos de serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-features1.md). O procedimento a seguir é a abordagem geral para derivar uma classe a partir das classes do MPF.

#### <a name="deriving-from-an-mpf-class"></a>Derivando de uma classe MPF

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto VSPackage e selecione **Adicionar**, **classe**.

2. Verifique se a **classe** está selecionada na lista modelos.

     Insira um nome adequado para o arquivo de classe e clique em **Adicionar**.

3. No novo arquivo de classe, adicione as seguintes `using` diretivas.

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_4.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_4.vb)]

4. Modifique a classe para derivar da classe MPF desejada.

5. Adicione um construtor de classe que aceite pelo menos os mesmos parâmetros que o construtor da classe base e passe os parâmetros do construtor para o construtor da classe base.

     Por exemplo, o construtor de uma classe derivada da <xref:Microsoft.VisualStudio.Package.Source> classe pode ser semelhante ao seguinte:

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_5.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_5.vb)]

6. No menu **Editar**, **IntelliSense** , selecione **implementar classe abstrata** se a classe base tiver quaisquer métodos abstratos que devam ser implementados.

7. Caso contrário, posicione o cursor dentro da classe e insira o método a ser substituído.

     Por exemplo, digite `public override` para ver uma lista de todos os métodos que podem ser substituídos nessa classe.

## <a name="see-also"></a>Confira também
- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)

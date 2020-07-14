---
title: Windows Communication Foundation e WCF Data Services
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- services, WCF Data
- WCF services, binding to
- WCF services, asynchronous service methods
- service references [Visual Studio]
- WCF Data Services
- asynchronous calls
- service references [Visual Studio], type sharing
- endpoints [WCF]
- asynchronous service methods
- service references [Visual Studio] endpoints
- WCF services, type sharing
- Windows Communication Foundation, in Visual Studio
- services, WCF
- WCF service, Visual Studio
- data services, WCF
- services, in Visual Studio
- data binding [Visual Studio], WCF
- service endpoints [Visual Studio]
- service references [Visual Studio], asynchronous calls
- services, Windows Communication Foundation
- type sharing in WCF services
- WCF services, endpoints
- service method, called asynchronously[Visual Studio]
ms.assetid: d56f12cb-e139-4fec-b3e4-488383356642
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c1f24a33a482b1994d0d8667b4fc71cf968e4625
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281039"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio

O Visual Studio fornece ferramentas para trabalhar com Windows Communication Foundation (WCF) e WCF Data Services, tecnologias da Microsoft para a criação de aplicativos distribuídos. Este tópico fornece uma introdução aos serviços de uma perspectiva do Visual Studio. Para obter a documentação completa, consulte [WCF Data Services 4,5](/dotnet/framework/data/wcf/index).

## <a name="what-is-wcf"></a>O que é o WCF?

O Windows Communication Foundation (WCF) é uma estrutura unificada para criar aplicativos distribuídos seguros, confiáveis, transacionados e interoperáveis. Ele substitui as tecnologias de comunicação entre processos mais antigas, como serviços Web ASMX, .NET Remoting, serviços corporativos (DCOM) e MSMQ. O WCF reúne a funcionalidade de todas essas tecnologias em um modelo de programação unificado. Isso simplifica a experiência de desenvolvimento de aplicativos distribuídos.

### <a name="what-are-wcf-data-services"></a>O que são WCF Data Services

WCF Data Services é uma implementação do padrão de protocolo OData (Open Data).  WCF Data Services permite que você exponha dados tabulares como um conjunto de APIs REST, permitindo que você retorne dados usando verbos HTTP padrão, como GET, POST, PUT ou DELETE. No lado do servidor, WCF Data Services estão sendo substituídas por [ASP.NET Web API](https://dotnet.microsoft.com/apps/aspnet/apis) para criar novos serviços OData. A biblioteca de cliente do WCF Data Services continua sendo uma boa opção para consumir serviços OData em um aplicativo .net do Visual Studio (**Project**  >  **Adicionar referência de serviço**). Para obter mais informações, consulte [WCF Data Services 4,5](/dotnet/framework/data/wcf).

### <a name="wcf-programming-model"></a>Modelo de programação do WCF

O modelo de programação do WCF se baseia na comunicação entre duas entidades: um serviço WCF e um cliente WCF. O modelo de programação é encapsulado no <xref:System.ServiceModel> namespace no .net.

### <a name="wcf-service"></a>Serviço WCF

Um serviço WCF é baseado em uma interface que define um contrato entre o serviço e o cliente. Ele é marcado com um <xref:System.ServiceModel.ServiceContractAttribute> atributo, conforme mostrado no código a seguir:

[!code-csharp[WCFWalkthrough#6](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.cs)]
[!code-vb[WCFWalkthrough#6](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.vb)]

Você define funções ou métodos que são expostos por um serviço WCF marcando-os com um <xref:System.ServiceModel.OperationContractAttribute> atributo.

[!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.cs)]
[!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.vb)]

Além disso, você pode expor dados serializados marcando um tipo composto com um <xref:System.Runtime.Serialization.DataContractAttribute> atributo. Isso habilita a vinculação de dados em um cliente.

Depois que uma interface e seus métodos são definidos, eles são encapsulados em uma classe que implementa a interface. Uma única classe de serviço WCF pode implementar vários contratos de serviço.

Um serviço WCF é exposto para consumo por meio do que é conhecido como um *ponto de extremidade*. O ponto de extremidade fornece a única maneira de se comunicar com o serviço; Você não pode acessar o serviço por meio de uma referência direta como faria com outras classes.

Um ponto de extremidade consiste em um endereço, uma associação e um contrato. O endereço define onde o serviço está localizado; pode ser uma URL, um endereço FTP ou uma rede ou um caminho local. Uma associação define a maneira como você se comunica com o serviço. As associações do WCF fornecem um modelo versátil para especificar um protocolo como HTTP ou FTP, um mecanismo de segurança, como autenticação do Windows ou nomes de usuário e senhas, e muito mais. Um contrato inclui as operações que são expostas pela classe de serviço do WCF.

Vários pontos de extremidade podem ser expostos para um único serviço WCF. Isso permite que diferentes clientes se comuniquem com o mesmo serviço de diferentes maneiras. Por exemplo, um serviço bancário pode fornecer um ponto de extremidade para funcionários e outro para clientes externos, cada um usando um endereço, associação e/ou contrato diferente.

### <a name="wcf-client"></a>Cliente de WCF

Um cliente WCF consiste em um *proxy* que permite que um aplicativo se comunique com um serviço WCF e um ponto de extremidade que corresponde a um ponto de extremidade definido para o serviço. O proxy é gerado no lado do cliente no arquivo de *app.config* e inclui informações sobre os tipos e métodos que são expostos pelo serviço. Para serviços que expõem vários pontos de extremidade, o cliente pode selecionar aquele que melhor atenda às suas necessidades, por exemplo, para se comunicar via HTTP e usar a autenticação do Windows.

Após a criação de um cliente WCF, você faz referência ao serviço em seu código, assim como faria com qualquer outro objeto. Por exemplo, para chamar o `GetData` método mostrado anteriormente, você escreveria um código semelhante ao seguinte:

[!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.cs)]
[!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.vb)]

## <a name="wcf-tools-in-visual-studio"></a>Ferramentas do WCF no Visual Studio

O Visual Studio fornece ferramentas para ajudá-lo a criar serviços WCF e clientes WCF. Para um passo a passo que demonstra as ferramentas, consulte [instruções passo a passo: Criando um serviço WCF simples no Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md).

### <a name="create-and-test-wcf-services"></a>Criar e testar serviços WCF

Você pode usar os modelos do Visual Studio do WCF como uma base para criar rapidamente seu próprio serviço. Em seguida, você pode usar o cliente de teste do WCF e o host automático do WCF para depurar e testar o serviço. Essas ferramentas juntas fornecem um ciclo de depuração e teste rápido e conveniente e eliminam a necessidade de se comprometer com um modelo de hospedagem em um estágio inicial.

#### <a name="wcf-templates"></a>Modelos do WCF

Os modelos do WCF Visual Studio fornecem uma estrutura de classe básica para o desenvolvimento de serviços. Vários modelos WCF estão disponíveis na caixa de diálogo **Adicionar novo projeto** . Isso inclui projetos do serviço WCF lLibrary, sites de serviço WCF e modelos de item de serviço WCF.

Quando você seleciona um modelo, os arquivos são adicionados a um contrato de serviço, uma implementação de serviço e uma configuração de serviço. Todos os atributos necessários já foram adicionados, criando um tipo simples de serviço "Olá, Mundo" e você não precisou escrever nenhum código. Você certamente vai querer adicionar código para fornecer funções e métodos para seu serviço real, mas os modelos fornecem a base básica.

Para saber mais sobre os modelos do WCF, confira [modelos do WCF do Visual Studio](/dotnet/framework/wcf/wcf-vs-templates).

#### <a name="wcf-service-host"></a>Host de serviço do WCF

Quando você inicia o depurador do Visual Studio (pressionando **F5**) para um projeto de serviço WCF, a ferramenta host de serviço do WCF é iniciada automaticamente para hospedar o serviço localmente. O host de serviço WCF enumera os serviços em um projeto de serviço WCF, carrega a configuração do projeto e cria uma instância de um host para cada serviço que ele encontra.

Usando o host de serviço do WCF, você pode testar um serviço WCF sem gravar código extra ou confirmá-lo em um host específico durante o desenvolvimento.

Para saber mais sobre o host de serviço WCF, consulte [host de serviço WCF (WcfSvcHost.exe)](/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe).

#### <a name="wcf-test-client"></a>Cliente de teste do WCF

A ferramenta de cliente de teste do WCF permite que você insira parâmetros de teste, envie essa entrada para um serviço WCF e exiba a resposta que o serviço envia de volta. Ele fornece uma experiência de teste de serviço conveniente quando você a combina com o host de serviço WCF. Localize a ferramenta na pasta *% ProgramFiles (x86)% \ Microsoft Visual Studio\2017\Enterprise\Common7\IDE* .

Quando você pressiona **F5** para depurar um projeto de serviço WCF, o cliente de teste do WCF é aberto e exibe uma lista de pontos de extremidade de serviço que são definidos no arquivo de configuração. Você pode testar os parâmetros e iniciar o serviço e repetir esse processo para testar e validar continuamente seu serviço.

Para saber mais sobre o cliente de teste do WCF, consulte [WCF Test Client (WcfTestClient.exe)](/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe).

### <a name="accessing-wcf-services-in-visual-studio"></a>Acessando serviços WCF no Visual Studio

O Visual Studio simplifica a tarefa de criar clientes WCF, gerando automaticamente um proxy e um ponto de extremidade para os serviços que você adiciona usando a caixa de diálogo **Adicionar referência de serviço** . Todas as informações de configuração necessárias são adicionadas ao arquivo de *app.config* . Na maioria das vezes, tudo o que você precisa fazer é instanciar o serviço para usá-lo.

A caixa de diálogo **Adicionar referência de serviço** permite que você insira o endereço de um serviço ou procure um serviço que esteja definido em sua solução. A caixa de diálogo retorna uma lista de serviços e as operações fornecidas por esses serviços. Ele também permite que você defina o namespace pelo qual você fará referência aos serviços no código.

A caixa de diálogo **Configurar referências de serviço** permite que você personalize a configuração de um serviço. Você pode alterar o endereço de um serviço, especificar o nível de acesso, o comportamento assíncrono e os tipos de contrato de mensagem e configurar a reutilização de tipo.

## <a name="how-to-select-a-service-endpoint"></a>Como: selecionar um ponto de extremidade de serviço

Alguns serviços do Windows Communication Foundation (WCF) expõem vários pontos de extremidade por meio dos quais um cliente pode se comunicar com o serviço. Por exemplo, um serviço pode expor um ponto de extremidade que usa associação HTTP e nome de usuário e segurança de senha e um segundo ponto de extremidade que usa autenticação FTP e Windows. O primeiro ponto de extremidade pode ser usado por aplicativos que acessam o serviço de fora de um firewall, enquanto o segundo pode ser usado em uma intranet.

Nesse caso, você pode especificar o `endpointConfigurationName` como um parâmetro para o construtor para uma referência de serviço.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-select-a-service-endpoint"></a>Para selecionar um ponto de extremidade de serviço

1. Adicione uma referência a um serviço WCF clicando com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e escolhendo **Adicionar referência de serviço**.

2. No editor de código, adicione um construtor para a referência de serviço:

    ```vb
    Dim proxy As New ServiceReference.Service1Client(
    ```

    ```csharp
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(
    ```

    > [!NOTE]
    > Substitua o *inreference* pelo namespace para a referência de serviço e substitua *Service1Client* pelo nome do serviço.

3. Uma lista do IntelliSense é exibida, incluindo as sobrecargas do construtor. Selecione a `endpointConfigurationName As String` sobrecarga.

4. Após a sobrecarga, digite `=` *ConfigurationName*, em que *ConfigurationName* é o nome do ponto de extremidade que você deseja usar.

    > [!NOTE]
    > Se você não souber os nomes dos pontos de extremidade disponíveis, poderá encontrá-los no arquivo de *app.config* .

### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>Para localizar os pontos de extremidade disponíveis para um serviço WCF

1. No **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo **app.config** do projeto que contém a referência de serviço e clique em **abrir**. O arquivo aparece no editor de código.

2. Procure a `<Client>` marca no arquivo.

3. Pesquise abaixo da `<Client>` marca para obter uma marca que comece com `<Endpoint>` .

     Se a referência de serviço fornecer vários pontos de extremidade, haverá duas ou mais `<Endpoint` marcas.

4. Dentro da `<EndPoint>` marca, você encontrará um `name="` parâmetro *SomeService* `"` (em que *SomeService* representa um nome de ponto de extremidade). Esse é o nome do ponto de extremidade que pode ser passado para a `endpointConfigurationName As String` sobrecarga de um construtor para uma referência de serviço.

## <a name="how-to-call-a-service-method-asynchronously"></a>Como: chamar um método de serviço de forma assíncrona

A maioria dos métodos nos serviços Windows Communication Foundation (WCF) pode ser chamada de forma síncrona ou assíncrona. Chamar um método de forma assíncrona permite que seu aplicativo continue funcionando enquanto o método está sendo chamado quando ele opera em uma conexão lenta.

Por padrão, quando uma referência de serviço é adicionada a um projeto, ela é configurada para chamar métodos de forma síncrona. Você pode alterar o comportamento para chamar métodos de forma assíncrona alterando uma configuração na caixa de diálogo **Configurar referência de serviço** .

> [!NOTE]
> Essa opção é definida em uma base por serviço. Se um método para um serviço for chamado de forma assíncrona, todos os métodos deverão ser chamados de forma assíncrona.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-call-a-service-method-asynchronously"></a>Para chamar um método de serviço de forma assíncrona

1. Em **Gerenciador de soluções**, selecione a referência de serviço.

2. No menu **projeto** , clique em **Configurar referência de serviço**.

3. Na caixa de diálogo **Configurar referência de serviço** , marque a caixa de seleção **gerar operações assíncronas** .

## <a name="how-to-bind-data-returned-by-a-service"></a>Como associar dados retornados por um serviço

Você pode associar dados retornados por um serviço de Windows Communication Foundation (WCF) a um controle, assim como você pode associar qualquer outra fonte de dados a um controle. Quando você adiciona uma referência a um serviço WCF, se o serviço contiver tipos compostos que retornam dados, eles serão adicionados automaticamente à janela **fontes de dados** .

### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>Para associar um controle a um único campo de dados retornado por um serviço WCF

1. No menu **Dados**, clique em **Mostrar Fontes de Dados**.

   A janela **Fontes de Dados** é exibida.

2. Na janela **fontes de dados** , expanda o nó para a referência de serviço. Todos os tipos compostos retornados pela exibição do serviço.

3. Expanda um nó para um tipo. Os campos de dados para esse tipo são exibidos.

4. Selecione um campo e clique na seta suspensa para exibir uma lista de controles que estão disponíveis para o tipo de dados.

5. Clique no tipo de controle ao qual você deseja associar.

6. Arraste o campo para um formulário. O controle é adicionado ao formulário, junto com um <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.

7. Repita as etapas 4 a 6 para todos os outros campos que você deseja associar.

### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>Para associar um controle ao tipo composto retornado por um serviço WCF

1. No menu **dados** , selecione **mostrar fontes de dados**. A janela **Fontes de Dados** é exibida.

2. Na janela **fontes de dados** , expanda o nó para a referência de serviço. Todos os tipos compostos retornados pela exibição do serviço.

3. Selecione um nó para um tipo e clique na seta suspensa para exibir uma lista de opções disponíveis.

4. Clique em **DataGridView** para exibir os dados em uma grade ou **detalhes** para exibir os dados em controles individuais.

5. Arraste o nó para o formulário. Os controles são adicionados ao formulário, junto com um <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.

## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>Como: configurar um serviço para reutilizar tipos existentes

Quando uma referência de serviço é adicionada a um projeto, todos os tipos definidos no serviço são gerados no projeto local. Em muitos casos, isso cria tipos duplicados quando um serviço usa tipos .NET comuns ou quando os tipos são definidos em uma biblioteca compartilhada.

Para evitar esse problema, os tipos em assemblies referenciados são compartilhados por padrão. Se você quiser desabilitar o compartilhamento de tipo para um ou mais assemblies, poderá fazer isso na caixa de diálogo **Configurar referências de serviço** .

### <a name="to-disable-type-sharing-in-a-single-assembly"></a>Para desabilitar o compartilhamento de tipo em um único assembly

1. Em **Gerenciador de soluções**, selecione a referência de serviço.

2. No menu **projeto** , clique em **Configurar referência de serviço**.

3. Na caixa de diálogo **Configurar referências de serviço** , selecione **reutilizar tipos em assemblies referenciados especificados**.

4. Marque a caixa de seleção para cada assembly no qual você deseja habilitar o compartilhamento de tipo. Para desabilitar o compartilhamento de tipo para um assembly, deixe a caixa de seleção desmarcada.

### <a name="to-disable-type-sharing-in-all-assemblies"></a>Para desabilitar o compartilhamento de tipo em todos os assemblies

1. Em **Gerenciador de soluções**, selecione a referência de serviço.

2. No menu **projeto** , clique em **Configurar referência de serviço**.

3. Na caixa de diálogo **Configurar referências de serviço** , desmarque a caixa de seleção **reutilizar tipos em assemblies referenciados** .

## <a name="related-topics"></a>Tópicos relacionados

| Title | Descrição |
| - | - |
| [Passo a passo: criando um Serviço WCF em Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md) | Fornece uma demonstração passo a passo de como criar e usar serviços WCF no Visual Studio. |
| [Walkthrough: Criando um serviço de dados WCF com o WPF e Entity Framework](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md) | Fornece uma demonstração passo a passo de como criar e usar WCF Data Services no Visual Studio. |
| [Usando as ferramentas de desenvolvimento do WCF](/dotnet/framework/wcf/using-the-wcf-development-tools) | Discute como criar e testar serviços WCF no Visual Studio. |
| | [Como: Adicionar, atualizar ou remover uma referência do WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md) |
| [Solucionando problemas de referências de serviço](../data-tools/troubleshooting-service-references.md) | Apresenta alguns erros comuns que podem ocorrer com referências de serviço e como evitá-los. |
| [Depurando serviços WCF](../debugger/debugging-wcf-services.md) | Descreve problemas comuns de depuração e técnicas que você pode encontrar ao depurar serviços WCF. |
| [Walkthrough: Criando um aplicativo de dados de n camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md) | Fornece instruções passo a passo para criar um conjunto de dados tipado e separar o código do TableAdapter e do conjunto de dados em vários projetos. |
| [Caixa de diálogo Configurar Referência de Serviço](../data-tools/configure-service-reference-dialog-box.md) | Descreve os elementos da interface do usuário da caixa de diálogo **Configurar referência de serviço** . |

## <a name="reference"></a>Referência

- <xref:System.ServiceModel>
- <xref:System.Data.Services>

## <a name="see-also"></a>Veja também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)

---
title: Windows Communication Foundation e WCF Data Services
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: b9f2202c96799fcc2e258e79f050d15fb474d0aa
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305501"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio

Visual Studio fornece ferramentas para trabalhar com o Windows Communication Foundation (WCF) e o WCF Data Services, tecnologias da Microsoft para criar aplicativos distribuídos. Este tópico fornece uma introdução aos serviços de uma perspectiva do Visual Studio. Para obter a documentação completa, consulte [WCF Data Services 4.5](/dotnet/framework/data/wcf/index).

## <a name="what-is-wcf"></a>O que é o WCF?

Windows Communication Foundation (WCF) é uma estrutura unificada para criar aplicativos distribuídos seguros, confiáveis, transacionados e interoperáveis. Ele substitui as tecnologias mais antigas de comunicação entre processos, como serviços web ASMX, .NET Remoting, Enterprise Services (DCOM) e MSMQ. WCF reúne a funcionalidade de todas essas tecnologias em um modelo de programação unificado. Isso simplifica a experiência de desenvolvimento de aplicativos distribuídos.

### <a name="what-are-wcf-data-services"></a>Quais são o WCF Data Services

WCF Data Services é uma implementação do protocolo OData (Open Data) padrão.  WCF Data Services permite expor dados tabulares como um conjunto de APIs REST, permitindo que você retornar dados usando verbos HTTP como GET, POST, PUT ou DELETE. No lado do servidor, o WCF Data Services estão sendo substituídos pelos [API Web ASP.NET](http://www.asp.net/web-api) para a criação de novos serviços OData. A biblioteca de cliente do WCF Data Services continua a ser uma boa opção para consumir serviços OData em um aplicativo .NET do Visual Studio (**Project** > **Add Service Reference**). Para obter mais informações, consulte [WCF Data Services 4.5](http://go.microsoft.com/fwlink/?LinkID=119952).

### <a name="wcf-programming-model"></a>Modelo de programação do WCF

O modelo de programação do WCF baseia-se a comunicação entre duas entidades: um serviço WCF e um cliente do WCF. O modelo de programação é encapsulado no <xref:System.ServiceModel> namespace no .NET Framework.

### <a name="wcf-service"></a>Serviço WCF

Um serviço WCF baseia-se em uma interface que define um contrato entre o serviço e o cliente. Ele é marcado com um <xref:System.ServiceModel.ServiceContractAttribute> de atributo, conforme mostrado no código a seguir:

[!code-csharp[WCFWalkthrough#6](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.cs)]
[!code-vb[WCFWalkthrough#6](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.vb)]

Definir funções ou métodos que são expostos por um serviço WCF marcando-as com um <xref:System.ServiceModel.OperationContractAttribute> atributo.

[!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.cs)]
[!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.vb)]

Além disso, você pode expor os dados serializados marcando um tipo composto com um <xref:System.Runtime.Serialization.DataContractAttribute> atributo. Isso permite que a associação de dados em um cliente.

Depois que uma interface e seus métodos são definidos, eles são encapsulados em uma classe que implementa a interface. Uma única classe de serviço do WCF pode implementar vários contratos de serviço.

Um serviço WCF é exposto para consumo por meio do que é conhecido como um *ponto de extremidade*. O ponto de extremidade fornece a única maneira de se comunicar com o serviço; não é possível acessar o serviço por meio de uma referência direta, como você faria com outras classes.

Um ponto de extremidade consiste em um endereço, uma ligação e um contrato. O endereço define em que o serviço está localizado; Isso pode ser uma URL, um endereço FTP, ou uma rede ou o caminho local. Uma associação define a maneira que você se comunica com o serviço. Associações do WCF fornecem um modelo versátil para especificar um protocolo como HTTP ou FTP, um mecanismo de segurança como autenticação do Windows ou nomes de usuário e senhas e muito mais. Um contrato inclui as operações que são expostas pela classe de serviço WCF.

Vários pontos de extremidade podem ser expostos para um único serviço do WCF. Isso permite que clientes diferentes para se comunicar com o mesmo serviço de maneiras diferentes. Por exemplo, um serviço de serviços bancários pode fornecer um ponto de extremidade para os funcionários e outro para clientes externos, cada um com um endereço diferente, associação, e/ou de contrato.

### <a name="wcf-client"></a>Cliente de WCF

Um cliente WCF consiste em uma *proxy* que permite que um aplicativo para se comunicar com um serviço WCF e um ponto de extremidade que corresponde a um ponto de extremidade definido para o serviço. O proxy é gerado no lado do cliente na *App. config* de arquivo e inclui informações sobre os tipos e métodos que são expostos pelo serviço. Para serviços que expõem vários pontos de extremidade, o cliente pode selecionar aquele que melhor atenda às suas necessidades, por exemplo, para se comunicar por HTTP e usar a autenticação do Windows.

Depois que um cliente WCF tiver sido criado, você referenciar o serviço em seu código exatamente como faria com qualquer outro objeto. Por exemplo, para chamar o `GetData` método mostrado anteriormente, você escreveria código semelhante ao seguinte:

[!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.cs)]
[!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.vb)]

## <a name="wcf-tools-in-visual-studio"></a>Ferramentas do WCF no Visual Studio

Visual Studio fornece ferramentas para ajudá-lo a criar serviços WCF e clientes do WCF. Para um passo a passo que demonstra as ferramentas, consulte [instruções passo a passo: Criando um serviço WCF simples no Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md).

### <a name="create-and-test-wcf-services"></a>Criar e testar os serviços WCF

Você pode usar modelos do Visual Studio do WCF como uma base para criar rapidamente seu próprio serviço. Em seguida, você pode usar o Host de automático de serviço do WCF e o cliente de teste do WCF para depurar e testar o serviço. Juntos, essas ferramentas fornecem um rápido e conveniente de depuração e ciclo de testes e eliminam a necessidade de se comprometer com um modelo de hospedagem em um estágio inicial.

#### <a name="wcf-templates"></a>Modelos do WCF

Modelos do Visual Studio do WCF fornecem uma estrutura de classe básica para o desenvolvimento de serviço. Vários modelos WCF estão disponíveis na **adicionar novo projeto** caixa de diálogo. Isso inclui projetos de lLibrary de serviço do WCF, sites de serviço WCF e modelos de item de serviço do WCF.

Quando você seleciona um modelo, os arquivos são adicionados para um contrato de serviço, uma implementação de serviço e uma configuração de serviço. Todos os atributos necessários já foram adicionados, criando um tipo de "Hello World" simples do serviço, e você não tivesse de escrever nenhum código. É claro, convém adicionar código para fornecer funções e métodos para o serviço do mundo real, mas os modelos fornecem os princípios básicos.

Para saber mais sobre os modelos WCF, consulte [modelos do Visual Studio do WCF](/dotnet/framework/wcf/wcf-vs-templates).

#### <a name="wcf-service-host"></a>Host de serviço do WCF

Quando você inicia o depurador do Visual Studio (pressionando **F5**) para um projeto de serviço do WCF, a ferramenta de Host de serviço WCF é iniciada automaticamente para hospedar o serviço localmente. Host de serviço WCF enumera os serviços em um projeto de serviço do WCF, carrega a configuração do projeto e cria uma instância de um host para cada serviço que encontrar.

Usando o Host de serviço WCF, você pode testar um serviço WCF sem gravar código extra ou confirmar a um host específico durante o desenvolvimento.

Para saber mais sobre o Host de serviço WCF, consulte [host de serviço do WCF (WcfSvcHost.exe)](/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe).

#### <a name="wcf-test-client"></a>Cliente de teste do WCF

A ferramenta de cliente de teste do WCF lhe permite parâmetros de teste, enviem essa entrada para um serviço WCF e exibir a resposta que o serviço envia de volta. Ele fornece um serviço conveniente testar a experiência quando combiná-lo com o Host de serviço WCF. Encontrar a ferramenta na *% ProgramFiles (x86) %\Microsoft Visual Studio\2017\Enterprise\Common7\IDE* pasta.

Quando você pressiona **F5** para depurar um projeto de serviço do WCF, o cliente de teste do WCF é aberta e exibe uma lista de pontos de extremidade de serviço que são definidos no arquivo de configuração. Você pode testar os parâmetros e iniciar o serviço e repita esse processo para testar e validar seu serviço continuamente.

Para saber mais sobre o cliente de teste do WCF, consulte [(WcfTestClient.exe) do cliente de teste do WCF](/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe).

### <a name="accessing-wcf-services-in-visual-studio"></a>Acessando os serviços WCF no Visual Studio

Visual Studio simplifica a tarefa de criação de clientes do WCF, geração automática de um proxy e um ponto de extremidade para serviços que você adicionar usando o **adicionar referência de serviço** caixa de diálogo. Todas as informações de configuração necessária são adicionadas para o *App. config* arquivo. A maioria das vezes, tudo o que você precisa fazer é instanciar o serviço para usá-lo.

O **adicionar referência de serviço** caixa de diálogo permite que você insira o endereço de um serviço ou para pesquisar um serviço que é definido em sua solução. A caixa de diálogo retorna uma lista de serviços e as operações fornecidas por esses serviços. Ele também permite que você defina o espaço para nome pelo qual você fará referência os serviços no código.

O **configurar referências de serviço** caixa de diálogo permite que você personalize a configuração para um serviço. Alterar o endereço para um serviço, especifique o nível de acesso, o comportamento assíncrono e tipos de contrato de mensagem e configurar a reutilização de tipo.

## <a name="how-to-select-a-service-endpoint"></a>Como: selecione um ponto de extremidade de serviço

Alguns serviços do Windows Communication Foundation (WCF) expõem vários pontos de extremidade por meio do qual um cliente pode se comunicar com o serviço. Por exemplo, um serviço pode expor um ponto de extremidade que usa uma associação HTTP e o nome de usuário e a segurança de senha e um segundo ponto de extremidade que usa a autenticação do Windows e FTP. O primeiro ponto de extremidade pode ser usado por aplicativos que acessam o serviço de fora de um firewall, enquanto o segundo pode ser usado em uma intranet.

Nesse caso, você pode especificar o `endpointConfigurationName` como um parâmetro para o construtor para uma referência de serviço.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-select-a-service-endpoint"></a>Para selecionar um ponto de extremidade de serviço

1.  Adicione uma referência a um serviço WCF clicando com o nó do projeto no **Gerenciador de soluções** e escolhendo **adicionar referência de serviço**.

2.  No Editor de códigos, adicione um construtor para a referência de serviço:

    ```vb
    Dim proxy As New ServiceReference.Service1Client(
    ```

    ```csharp
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(
    ```

    > [!NOTE]
    > Substitua *ServiceReference* com o namespace para a referência de serviço e a substituição *Service1Client* com o nome do serviço.

3.  Uma lista do IntelliSense exibe que inclui as sobrecargas do construtor. Selecione o `endpointConfigurationName As String` de sobrecarga.

4.  Após a sobrecarga, digite `=` *ConfigurationName*, onde *ConfigurationName* é o nome do ponto de extremidade que você deseja usar.

    > [!NOTE]
    > Se você não souber os nomes dos pontos de extremidade disponíveis, você pode encontrá-los de *App. config* arquivo.

### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>Para localizar pontos de extremidade disponíveis para um serviço WCF

1.  No **Gerenciador de soluções**, com o botão direito do **App. config** de arquivos para o projeto que contém a referência de serviço e, em seguida, clique em **abrir**. O arquivo aparece no Editor de códigos.

2.  Pesquise o `<Client>` marca no arquivo.

3.  Pesquisar sob o `<Client>` marca para uma marca que começa com `<Endpoint>`.

     Se a referência de serviço fornece vários pontos de extremidade, haverá duas ou mais `<Endpoint` marcas.

4.  Dentro de `<EndPoint>` marca, você encontrará um `name="` *SomeService* `"` parâmetro (onde *SomeService* representa um nome de ponto de extremidade). Esse é o nome para o ponto de extremidade que pode ser passado para o `endpointConfigurationName As String` sobrecarga de um construtor para uma referência de serviço.

## <a name="how-to-call-a-service-method-asynchronously"></a>Como: chamar um método de serviço de forma assíncrona

A maioria dos métodos em serviços Windows Communication Foundation (WCF) pode ser chamado de forma síncrona ou assíncrona. Chamando um método de forma assíncrona permite que seu aplicativo para continuar trabalhando enquanto o método está sendo chamado quando ele opera sobre uma conexão lenta.

Por padrão, quando uma referência de serviço é adicionada a um projeto, ele é configurado para chamar métodos de forma síncrona. Você pode alterar o comportamento para chamar os métodos de forma assíncrona, alterando uma configuração na **Configure Service Reference** caixa de diálogo.

> [!NOTE]
> Essa opção é definida em uma base por serviço. Se um método para um serviço é chamado de forma assíncrona, todos os métodos devem ser chamados de forma assíncrona.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-call-a-service-method-asynchronously"></a>Para chamar um método de serviço de forma assíncrona

1.  Na **Gerenciador de soluções**, selecione a referência de serviço.

2.  Sobre o **Project** menu, clique em **Configure Service Reference**.

3.  No **Configure Service Reference** caixa de diálogo, selecione o **gerar operações assíncronas** caixa de seleção.

## <a name="how-to-bind-data-returned-by-a-service"></a>Como: associar dados retornados por um serviço

Você pode associar os dados retornados por um serviço do Windows Communication Foundation (WCF) a um controle, assim como você pode vincular qualquer outra fonte de dados a um controle. Quando você adiciona uma referência a um serviço WCF, se o serviço contiver tipos compostos que retornam dados, eles são adicionados automaticamente para o **fontes de dados** janela.

### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>Para associar um controle a único campo de dados retornado por um serviço WCF

1.  No menu **Dados**, clique em **Mostrar Fontes de Dados**.

   A janela **Fontes de Dados** é exibida.

2.  No **fontes de dados** janela, expanda o nó para sua referência de serviço. Quaisquer tipos compostos retornados pela exibição do serviço.

3.  Expanda um nó para um tipo. Os campos de dados para esse tipo aparecem.

4.  Selecione um campo e clique na seta suspensa para exibir uma lista de controles que estão disponíveis para o tipo de dados.

5.  Clique no tipo de controle ao qual você deseja associar.

6.  Arraste o campo um formulário. O controle é adicionado ao formulário, juntamente com uma <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.

7.  Repita as etapas 4, embora a 6 para todos os outros campos que você deseja associar.

### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>Para associar um controle a tipo composto retornado por um serviço WCF

1.  Sobre o **dados** menu, selecione **Show Data Sources**. A janela **Fontes de Dados** é exibida.

2.  No **fontes de dados** janela, expanda o nó para sua referência de serviço. Quaisquer tipos compostos retornados pela exibição do serviço.

3.  Selecione um nó para um tipo e clique na seta suspensa para exibir uma lista das opções disponíveis.

4.  Clique em **DataGridView** para exibir os dados em uma grade ou **detalhes** para exibir os dados em controles individuais.

5.  Arraste o nó para o formulário. Os controles são adicionados ao formulário, juntamente com uma <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.

## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>Como: configurar um serviço para reutilizar os tipos existentes

Quando uma referência de serviço é adicionada a um projeto, quaisquer tipos definidos no serviço são gerados no projeto local. Em muitos casos, isso cria tipos duplicados quando um serviço usa tipos comuns do .NET Framework ou quando os tipos são definidos em uma biblioteca compartilhada.

Para evitar esse problema, os tipos em assemblies referenciados são compartilhados por padrão. Se você quiser desabilitar o compartilhamento para um ou mais assemblies de tipo, você pode fazer isso na **configurar referências de serviço** caixa de diálogo.

### <a name="to-disable-type-sharing-in-a-single-assembly"></a>Para desabilitar o compartilhamento de tipo em um único assembly

1.  Na **Gerenciador de soluções**, selecione a referência de serviço.

2.  Sobre o **Project** menu, clique em **Configure Service Reference**.

3.  No **configurar referências de serviço** caixa de diálogo, selecione **reutilizar os tipos em assemblies referenciados especificados**.

4.  Marque a caixa de seleção para cada assembly no qual você deseja habilitar o compartilhamento de tipo. Para desabilitar o compartilhamento para um assembly de tipo, deixe a caixa de seleção desmarcada.

### <a name="to-disable-type-sharing-in-all-assemblies"></a>Para desabilitar o compartilhamento de tipo em todos os assemblies

1.  Na **Gerenciador de soluções**, selecione a referência de serviço.

2.  Sobre o **Project** menu, clique em **Configure Service Reference**.

3.  No **configurar referências de serviço** caixa de diálogo, desmarque a **reutilizar os tipos em assemblies referenciados** caixa de seleção.

## <a name="related-topics"></a>Tópicos relacionados

| Título | Descrição |
| - | - |
| [Passo a passo: criando um Serviço WCF em Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md) | Fornece uma demonstração passo a passo de criação e uso de serviços WCF no Visual Studio. |
| [Passo a passo: criando um serviço de dados WCF com WPF e Entity Framework](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md) | Fornece uma demonstração passo a passo de como criar e usar o WCF Data Services no Visual Studio. |
| [Usando as ferramentas de desenvolvimento do WCF](/dotnet/framework/wcf/using-the-wcf-development-tools) | Discute como criar e testar os serviços WCF no Visual Studio. |
| | [Como adicionar, atualizar ou remover uma referência de WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md) |
| [Solução de problemas de referências de serviço](../data-tools/troubleshooting-service-references.md) | Apresenta alguns erros comuns que podem ocorrer com referências de serviço e como evitá-los. |
| [Depurando serviços WCF](../debugger/debugging-wcf-services.md) | Descreve problemas comuns de depuração e técnicas que você pode encontrar ao depurar serviços WCF. |
| [Passo a passo: criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md) | Fornece instruções passo a passo para criar um conjunto de dados tipado e separar o código do TableAdapter e do conjunto de dados em vários projetos. |
| [Configurar a caixa de diálogo de referência de serviço](../data-tools/configure-service-reference-dialog-box.md) | Descreve os elementos de interface do usuário para o **Configure Service Reference** caixa de diálogo. |

## <a name="reference"></a>Referência

- <xref:System.ServiceModel>
- <xref:System.Data.Services>

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
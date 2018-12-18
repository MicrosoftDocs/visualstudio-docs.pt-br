---
title: Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 55b6ddc1d0e8e3a3caaee89547874e9e38115a17
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49194682"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual Studio fornece ferramentas para trabalhar com o Windows Communication Foundation (WCF) e [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)], tecnologias da Microsoft para a criação de aplicativos distribuídos. Este tópico fornece uma introdução aos serviços de um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] perspectiva. Para obter a documentação completa, consulte [WCF Data Services 4.5](http://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a).  
  
## <a name="what-is-wcf"></a>O que é o WCF?  
 [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] é uma estrutura unificada para criar aplicativos distribuídos seguros, confiáveis, transacionados e interoperáveis. Ele substitui as tecnologias mais antigas de comunicação entre processos, como serviços Web ASMX, .NET Remoting, Enterprise Services (DCOM) e MSMQ. WCF reúne a funcionalidade de todas essas tecnologias em um modelo de programação unificado. Isso simplifica a experiência de desenvolvimento de aplicativos distribuídos.  
  
#### <a name="what-are-wcf-data-services"></a>Quais são o WCF Data Services  
 [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] é uma implementação do protocolo OData (Open Data) padrão.  WCF Data Services permite expor dados tabulares como um conjunto de APIs REST, permitindo que você retornar dados usando verbos HTTP como GET, POST, PUT ou DELETE. No lado do servidor, o WCF Data Services estão sendo substituídos pelos [API Web ASP.NET](http://www.asp.net/web-api) para a criação de novos serviços OData. A biblioteca de cliente do WCF Data Services continua a ser uma boa opção para consumir serviços OData em um aplicativo .NET do Visual Studio (**projeto &#124; adicionar referência de serviço**). Para obter mais informações, consulte [WCF Data Services 4.5](http://go.microsoft.com/fwlink/?LinkID=119952).  
  
### <a name="wcf-programming-model"></a>Modelo de programação do WCF  
 O modelo de programação do WCF baseia-se a comunicação entre duas entidades: um serviço WCF e um cliente do WCF. O modelo de programação é encapsulado na <xref:System.ServiceModel> namespace no [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
#### <a name="wcf-service"></a>Serviço WCF  
 Um serviço WCF baseia-se em uma interface que define um contrato entre o serviço e o cliente. Ele é marcado com um <xref:System.ServiceModel.ServiceContractAttribute> de atributo, conforme mostrado no código a seguir:  
  
 [!code-csharp[WCFWalkthrough#6](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1.cs#6)]
 [!code-vb[WCFWalkthrough#6](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1.vb#6)]  
  
 [!code-csharp[WCFWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1.cs#1)]
 [!code-vb[WCFWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1.vb#1)]  
  
 Definir funções ou métodos que são expostos por um serviço WCF marcando-as com um <xref:System.ServiceModel.OperationContractAttribute> atributo. Além disso, você pode expor os dados serializados marcando um tipo composto com um <xref:System.Runtime.Serialization.DataContractAttribute> atributo. Isso permite que a associação de dados em um cliente.  
  
 Depois que uma interface e seus métodos são definidos, eles são encapsulados em uma classe que implementa a interface. Uma única classe de serviço do WCF pode implementar vários contratos de serviço.  
  
 Um serviço WCF é exposto para consumo por meio do que é conhecido como um *ponto de extremidade*. O ponto de extremidade fornece a única maneira de se comunicar com o serviço; não é possível acessar o serviço por meio de uma referência direta, como você faria com outras classes.  
  
 Um ponto de extremidade consiste em um endereço, uma ligação e um contrato. O endereço define em que o serviço está localizado; Isso pode ser uma URL, um endereço FTP, ou uma rede ou o caminho local. Uma associação define a maneira que você se comunica com o serviço. Associações do WCF fornecem um modelo versátil para especificar um protocolo como HTTP ou FTP, um mecanismo de segurança como autenticação do Windows ou nomes de usuário e senhas e muito mais. Um contrato inclui as operações que são expostas pela classe de serviço WCF.  
  
 Vários pontos de extremidade podem ser expostos para um único serviço do WCF. Isso permite que clientes diferentes para se comunicar com o mesmo serviço de maneiras diferentes. Por exemplo, um serviço de serviços bancários pode fornecer um ponto de extremidade para os funcionários e outro para clientes externos, cada um com um endereço diferente, associação, e/ou de contrato.  
  
#### <a name="wcf-client"></a>Cliente do WCF  
 Um cliente WCF consiste em uma *proxy* que permite que um aplicativo para se comunicar com um serviço WCF e um ponto de extremidade que corresponde a um ponto de extremidade definido para o serviço. O proxy é gerado no lado do cliente no arquivo App. config e inclui informações sobre os tipos e métodos que são expostos pelo serviço. Para serviços que expõem vários pontos de extremidade, o cliente pode selecionar aquele que melhor atenda às suas necessidades, por exemplo, para se comunicar por HTTP e usar a autenticação do Windows.  
  
 Depois que um cliente WCF tiver sido criado, você referenciar o serviço em seu código exatamente como faria com qualquer outro objeto. Por exemplo, para chamar o `GetData` método mostrado anteriormente, você escreveria código semelhante ao seguinte:  
  
 [!code-csharp[WCFWalkthrough#3](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/form1.cs#3)]
 [!code-vb[WCFWalkthrough#3](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/form1.vb#3)]  
  
## <a name="wcf-tools-in-visual-studio"></a>Ferramentas do WCF no Visual Studio  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece ferramentas para ajudá-lo a criar serviços WCF e clientes do WCF. Para um passo a passo que demonstra as ferramentas, consulte [instruções passo a passo: Criando um serviço WCF simples no Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md).  
  
### <a name="creating-and-testing-wcf-services"></a>Criando e Testando serviços WCF  
 Você pode usar o WCF [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelos como base para criar rapidamente seu próprio serviço. Em seguida, você pode usar o Host de automático de serviço do WCF e o cliente de teste do WCF para depurar e testar o serviço. Juntos, essas ferramentas fornecem um rápido e conveniente de depuração e ciclo de testes e eliminam a necessidade de se comprometer com um modelo de hospedagem em um estágio inicial.  
  
#### <a name="wcf-templates"></a>Modelos do WCF  
 WCF [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelos fornecem uma estrutura de classe básica para o desenvolvimento de serviço. Vários modelos WCF estão disponíveis na **adicionar novo projeto** caixa de diálogo. Isso inclui projetos de biblioteca de serviço WCF, Sites de Web do serviço WCF e modelos de Item de serviço do WCF.  
  
 Quando você seleciona um modelo, os arquivos são adicionados para um contrato de serviço, uma implementação de serviço e uma configuração de serviço. Todos os atributos necessários já foram adicionados, criando um tipo de "Hello World" simples do serviço, e você não tivesse de escrever nenhum código. É claro, convém adicionar código para fornecer funções e métodos para o serviço do mundo real, mas os modelos fornecem os princípios básicos.  
  
 Para saber mais sobre os modelos WCF, consulte [modelos do Visual Studio WCF](http://msdn.microsoft.com/library/6a608575-3535-4190-89da-911e24c8374f).  
  
#### <a name="wcf-service-host"></a>Host de serviço WCF  
 Quando você inicia o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] do depurador (pressionando F5) para um projeto de serviço do WCF, o Host de serviço do WCF é iniciada automaticamente para hospedar o serviço localmente. Host de serviço WCF enumera os serviços em um projeto de serviço do WCF, carrega a configuração do projeto e cria uma instância de um host para cada serviço que encontrar.  
  
 Usando o Host de serviço WCF, você pode testar um serviço WCF sem gravar código extra ou confirmar a um host específico durante o desenvolvimento.  
  
 Para saber mais sobre o Host de serviço WCF, consulte [Host de serviço do WCF (WcfSvcHost.exe)](http://msdn.microsoft.com/library/8643a63d-a357-4c39-bd6c-cdfdf71e370e).  
  
#### <a name="wcf-test-client"></a>Cliente de teste do WCF  
 A ferramenta de cliente de teste do WCF lhe permite parâmetros de teste, enviem essa entrada para um serviço WCF e exibir a resposta que o serviço envia de volta. Ele fornece um serviço conveniente testar a experiência quando combiná-lo com o Host de serviço WCF. A ferramenta pode ser encontrada na pasta \Common7\IDE, que, para o Visual Studio 2015 instalado na unidade c: é aqui: **C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\\**.  
  
 Quando você pressiona F5 para depurar um projeto de serviço do WCF, o cliente de teste do WCF abre e exibe uma lista de pontos de extremidade de serviço que são definidos no arquivo de configuração. Você pode testar os parâmetros e iniciar o serviço e repita esse processo para testar e validar seu serviço continuamente.  
  
 Para saber mais sobre o cliente de teste do WCF, consulte [cliente de teste do WCF (WcfTestClient.exe)](http://msdn.microsoft.com/library/d4302855-677f-4640-aa90-c5d785d72fb7).  
  
### <a name="accessing-wcf-services-in-visual-studio"></a>Acessando os serviços WCF no Visual Studio  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] simplifica a tarefa de criação de clientes do WCF, geração automática de um proxy e um ponto de extremidade para serviços que você adicionar usando o **adicionar referência de serviço** caixa de diálogo. Todas as informações de configuração necessária são adicionadas ao arquivo App. config. A maioria das vezes, tudo o que você precisa fazer é instanciar o serviço para usá-lo.  
  
 O **adicionar referência de serviço** caixa de diálogo permite que você insira o endereço de um serviço ou para pesquisar um serviço que é definido em sua solução. A caixa de diálogo retorna uma lista de serviços e as operações fornecidas por esses serviços. Ele também permite que você defina o espaço para nome pelo qual você fará referência os serviços no código.  
  
 O **configurar referências de serviço** caixa de diálogo permite que você personalize a configuração para um serviço. Alterar o endereço para um serviço, especifique o nível de acesso, o comportamento assíncrono e tipos de contrato de mensagem e configurar a reutilização de tipo.  
  
## <a name="how-to-select-a-service-endpoint"></a>Como: selecione um ponto de extremidade de serviço  
 Alguns serviços do Windows Communication Foundation (WCF) expõem vários pontos de extremidade por meio do qual um cliente pode se comunicar com o serviço. Por exemplo, um serviço pode expor um ponto de extremidade que usa um nome de usuário e a associação de HTTP / segurança de senha e um segundo ponto de extremidade que usa a autenticação do Windows e FTP. O primeiro ponto de extremidade pode ser usado por aplicativos que acessam o serviço de fora de um firewall, enquanto o segundo pode ser usado em uma intranet.  
  
 Nesse caso, você pode especificar o `endpointConfigurationName` como um parâmetro para o construtor para uma referência de serviço.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-select-a-service-endpoint"></a>Para selecionar um ponto de extremidade de serviço  
  
1.  Adicione uma referência a um serviço WCF clicando duas vezes no nó do projeto no Gerenciador de soluções e escolhendo **adicionar referência de serviço**  
  
2.  No Editor de códigos, adicione um construtor para a referência de serviço:  
  
    ```vb  
    Dim proxy As New ServiceReference.Service1Client(  
    ```  
  
    ```csharp  
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(  
    ```  
  
    > [!NOTE]
    >  Substitua *ServiceReference* com o namespace para a referência de serviço e a substituição *Service1Client* com o nome do serviço.  
  
3.  Uma lista do IntelliSense será exibida com as sobrecargas do construtor. Selecione o `endpointConfigurationName As String` de sobrecarga.  
  
4.  Após a sobrecarga, digite `=` *ConfigurationName*, onde *ConfigurationName* é o nome do ponto de extremidade que você deseja usar.  
  
    > [!NOTE]
    >  Se você não souber os nomes dos pontos de extremidade disponíveis, você pode encontrá-los no arquivo App. config.  
  
#### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>Para localizar pontos de extremidade disponíveis para um serviço WCF  
  
1.  Na **Gerenciador de soluções**, clique no arquivo App. config para o projeto que contém a referência de serviço e, em seguida, clique em **abrir**. O arquivo será exibido no Editor de códigos.  
  
2.  Pesquise o `<Client>` marca no arquivo.  
  
3.  Pesquisar sob o `<Client>` marca para uma marca que começa com `<Endpoint>`.  
  
     Se a referência de serviço fornece vários pontos de extremidade, haverá duas ou mais `<Endpoint` marcas.  
  
4.  Dentro de `<EndPoint>` marca, você encontrará uma `name="` *SomeService* `"` parâmetro (onde *SomeService* representa um nome de ponto de extremidade). Esse é o nome para o ponto de extremidade que pode ser passado para o `endpointConfigurationName As String` sobrecarga de um construtor para uma referência de serviço.  
  
## <a name="how-to-call-a-service-method-asynchronously"></a>Como: chamar um método de serviço de forma assíncrona  
 A maioria dos métodos em serviços Windows Communication Foundation (WCF) pode ser chamado de forma síncrona ou assíncrona. Chamando um método de forma assíncrona permite que seu aplicativo para continuar trabalhando enquanto o método está sendo chamado quando ele opera sobre uma conexão lenta.  
  
 Por padrão, quando uma referência de serviço é adicionada a um projeto ele é configurado para chamar métodos de forma síncrona. Você pode alterar o comportamento para chamar os métodos de forma assíncrona, alterando uma configuração na **Configure Service Reference** caixa de diálogo.  
  
> [!NOTE]
>  Essa opção é definida em uma base por serviço. Se um método para um serviço é chamado de forma assíncrona, todos os métodos devem ser chamados de forma assíncrona.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-call-a-service-method-asynchronously"></a>Para chamar um método de serviço de forma assíncrona  
  
1.  Na **Gerenciador de soluções**, selecione a referência de serviço.  
  
2.  Sobre o **Project** menu, clique em **Configure Service Reference**.  
  
3.  No **Configure Service Reference** caixa de diálogo, selecione o **gerar operações assíncronas** caixa de seleção.  
  
## <a name="how-to-bind-data-returned-by-a-service"></a>Como: associar dados retornados por um serviço  
 Você pode associar os dados retornados por um serviço do Windows Communication Foundation (WCF) a um controle, assim como você pode vincular qualquer outra fonte de dados a um controle. Quando você adiciona uma referência a um serviço WCF, se o serviço contiver tipos compostos que retornam dados, eles são adicionados automaticamente para o **fontes de dados** janela.  
  
#### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>Para associar um controle a único campo de dados retornado por um serviço WCF  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**. O **fontes de dados** janela será exibida.  
  
2.  No **fontes de dados** janela, expanda o nó para sua referência de serviço. Quaisquer tipos compostos retornados pelo serviço serão exibidos.  
  
3.  Expanda um nó para um tipo. Os campos de dados para esse tipo serão exibidos.  
  
4.  Selecione um campo e clique na seta suspensa para exibir uma lista de controles que estão disponíveis para o tipo de dados.  
  
5.  Clique no tipo de controle que você deseja associar.  
  
6.  Arraste o campo um formulário. O controle será adicionado ao formulário junto com um <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.  
  
7.  Repita as etapas 4, embora a 6 para todos os outros campos que você deseja associar.  
  
#### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>Para associar um controle a tipo composto retornado por um serviço WCF  
  
1.  Sobre o **dados** menu, selecione **Show Data Sources**. O **fontes de dados** janela será exibida.  
  
2.  No **fontes de dados** janela, expanda o nó para sua referência de serviço. Quaisquer tipos compostos retornados pelo serviço serão exibidos.  
  
3.  Selecione um nó para um tipo e clique na seta suspensa para exibir uma lista das opções disponíveis.  
  
4.  Clique em **DataGridView** para exibir os dados em uma grade ou **detalhes** para exibir os dados em controles individuais.  
  
5.  Arraste o nó para o formulário. Os controles serão adicionados ao formulário junto com um <xref:System.Windows.Forms.BindingSource> componente e um <xref:System.Windows.Forms.BindingNavigator> componente.  
  
## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>Como: configurar um serviço para reutilizar os tipos existentes  
 Quando uma referência de serviço é adicionada a um projeto, quaisquer tipos definidos no serviço são gerados no projeto local. Em muitos casos, isso cria tipos duplicados quando usa um serviço comum [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] tipos ou quando os tipos são definidos em uma biblioteca compartilhada.  
  
 Para evitar esse problema, os tipos em assemblies referenciados são compartilhados por padrão. Se você quiser desabilitar o compartilhamento para um ou mais assemblies de tipo, você pode fazer isso na **configurar referências de serviço** caixa de diálogo.  
  
#### <a name="to-disable-type-sharing-in-a-single-assembly"></a>Para desabilitar o compartilhamento de tipo em um único assembly  
  
1.  Na **Gerenciador de soluções**, selecione a referência de serviço.  
  
2.  Sobre o **Project** menu, clique em **Configure Service Reference**.  
  
3.  No **configurar referências de serviço** caixa de diálogo, selecione **reutilizar os tipos em assemblies referenciados especificados**.  
  
4.  Marque a caixa de seleção para cada assembly no qual você deseja habilitar o compartilhamento de tipo. Para desabilitar o compartilhamento para um assembly de tipo, deixe a caixa de seleção desmarcada.  
  
#### <a name="to-disable-type-sharing-in-all-assemblies"></a>Para desabilitar o compartilhamento de tipo em todos os assemblies  
  
1.  Na **Gerenciador de soluções**, selecione a referência de serviço.  
  
2.  Sobre o **Project** menu, clique em **Configure Service Reference**.  
  
3.  No **configurar referências de serviço** caixa de diálogo, desmarque a **reutilizar os tipos em assemblies referenciados** caixa de seleção.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Passo a passo: criando um Serviço WCF em Windows Forms](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md)|Fornece uma demonstração passo a passo de criação e uso de serviços do WCF em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|[Passo a passo: criando um Serviço de Dados WCF com WPF e Entity Framework](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md)|Fornece uma demonstração passo a passo de como criar e usar [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|[Usando as ferramentas de desenvolvimento do WCF](http://msdn.microsoft.com/library/054adb87-c244-4d5a-83d1-0b2b44bd454b)|Discute como criar e testar os serviços WCF em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|[Como: adicionar, atualizar ou remover uma referência de serviço](http://msdn.microsoft.com/library/cacc14bd-4455-4a44-be78-d2ac16113dd9)|Descreve como adicionar, atualizar ou remover os serviços WCF de um projeto.|  
|[Como adicionar, atualizar ou remover uma referência de WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)|Discute como referenciar e usar [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|[Solução de problemas de referências de serviço](../data-tools/troubleshooting-service-references.md)|Apresenta alguns erros comuns que podem ocorrer com referências de serviço e como evitá-los.|  
|[Depurando serviços WCF](../debugger/debugging-wcf-services.md)|Descreve problemas comuns de depuração e técnicas que você pode encontrar ao depurar serviços WCF.|  
|[Visão geral do serviço de autenticação do Windows Communication Foundation](http://msdn.microsoft.com/library/6e121a28-89e8-4974-88a8-70aaa6a7d52b)|Descreve como usar o WCF para fornecer um serviço de função para um site da Web.|  
|[Passo a passo: criando um aplicativo de dados de N camadas](../data-tools/walkthrough-creating-an-n-tier-data-application.md)|Fornece instruções passo a passo para criar um conjunto de dados tipado e separar o código do TableAdapter e do conjunto de dados em vários projetos.|  
|[Caixa de diálogo Configurar Referência de Serviço](../data-tools/configure-service-reference-dialog-box.md)|Descreve os elementos de interface do usuário para o **Configure Service Reference** caixa de diálogo.|  
  
## <a name="reference"></a>Referência  
 <xref:System.ServiceModel>  
  
 <xref:System.Data.Services>  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)


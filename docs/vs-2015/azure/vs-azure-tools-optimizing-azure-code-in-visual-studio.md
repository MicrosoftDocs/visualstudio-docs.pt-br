---
title: Otimizando o código do Azure
description: Saiba mais sobre como as ferramentas de otimização de código do Azure no Visual Studio ajudam a tornar o código mais robusto e com melhor desempenho.
author: ghogen
manager: jillfra
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.topic: conceptual
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 11/11/2016
ms.author: ghogen
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: e34c51db062528c83e08e2cb463a1cc44ab476f7
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75915754"
---
# <a name="optimizing-your-azure-code"></a>Otimizando o código do Azure
Quando você está programando aplicativos que usam o Microsoft Azure, existem algumas práticas de codificação que você deve seguir para ajudar a evitar problemas de escalabilidade, comportamento e desempenho do aplicativo em um ambiente de nuvem. A Microsoft fornece uma ferramenta de análise de código do Azure que reconhece e identifica vários desses problemas comumente encontrados e ajuda a resolvê-los. Você pode baixar a ferramenta no Visual Studio, via NuGet.

## <a name="azure-code-analysis-rules"></a>Regras de análise de código do Azure
A ferramenta de análise de código do Azure usa as seguintes regras para sinalizar automaticamente seu código do Azure quando encontra problemas conhecidos de impacto no desempenho. Os problemas detectados aparecem como avisos ou erros do compilador. Correções de código ou sugestões para resolver o erro ou aviso geralmente são fornecidos por meio de um ícone de lâmpada.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Evitar o uso do modo de estado de sessão padrão (em processo)
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Descrição
Se você usar o modo de estado de sessão padrão (em processo) para aplicativos em nuvem, poderá perder o estado da sessão.

### <a name="reason"></a>Reason
Por padrão, o modo de estado de sessão especificado no arquivo web.config está em processo. Além disso, se nenhuma entrada for especificada no arquivo de configuração, o modo de estado de sessão assume o padrão de em processo. O modo em processo armazena o estado de sessão na memória, no servidor Web. Quando uma instância é reiniciada ou uma nova instância é usada para balanceamento de carga ou suporte a failover, o estado de sessão armazenado na memória no servidor Web não é salvo. Essa situação impede que o aplicativo seja escalonável na nuvem.

O estado da sessão ASP.NET dá suporte a várias opções diferentes de armazenamento para dados de estado de sessão: InProc, StateServer, SQLServer, Personalizado e Desativado. É recomendável que você use o modo Personalizado para hospedar dados em um armazenamento de estado da sessão externo, como [Provedor de estado de sessão do Azure para Redis](https://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

### <a name="solution"></a>{1&gt;&lt;1} Solução
É uma solução recomendada armazenar o estado de sessão em um serviço de cache gerenciado. Saiba como usar [provedor de Estado de Sessão do Azure para Redis](https://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) para armazenar o estado de sessão. Você também pode armazenar o estado de sessão em outros locais para garantir que seu aplicativo seja escalonável na nuvem. Para saber mais sobre as soluções alternativas, leia [Modos de estado de sessão](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>O método de execução não deve ser assíncrono
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Descrição
Crie métodos assíncronos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fora do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e, em seguida, chamar os métodos assíncronos de [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). A declaração do método [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) como assíncrono faz com que a função de trabalho insira um loop de reinicialização.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](https://social.msdn.microsoft.com/Forums/en-US/home).

### <a name="reason"></a>Reason
A chamada de métodos assíncronos dentro do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que o runtime do serviço de nuvem recicle a função de trabalho. Quando uma função de trabalho é iniciada, todas as execuções do programa ocorrem dentro do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) . Sair do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) faz com que a função de trabalho reinicie. Quando o runtime da função de trabalho atinge o método assíncrono, ele envia todas as operações posteriores ao método assíncrono e retorna. Isso faz com que a função de trabalho saia do método [[[[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e reinicialize. Na próxima iteração da execução, a função de trabalho atinge o método assíncrono novamente e reinicia, fazendo com que a função de trabalho seja reciclada novamente.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Coloque todas as operações assíncronas fora do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) . Chame o método async refatorado de dentro do método [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) , como RunAsync().wait. A ferramenta de análise de código do Azure pode ajudá-lo a corrigir esse problema.

O snippet de código a seguir demonstra a correção de código para esse problema:

```csharp
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("https://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Autenticação de assinatura de acesso compartilhado com barramento de serviço
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Descrição
Use SAS (Assinatura de Acesso Compartilhado) para autenticação. ACS (Serviço de Controle de Acesso) está sendo preterido para autenticação do barramento de serviço.

### <a name="reason"></a>Reason
Para mais segurança, o Active Directory do Azure está substituindo a autenticação do ACS pela autenticação SAS. Consulte [Active Directory do Azure é o futuro do ACS](https://cloudblogs.microsoft.com/enterprisemobility/2013/06/22/azure-active-directory-is-the-future-of-acs/) para obter informações sobre o plano de transição.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Use autenticação de SAS em seus aplicativos. O exemplo a seguir mostra como usar um token SAS existente para acessar um namespace do barramento de serviço ou uma entidade.

```csharp
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Para obter mais informações, consulte os tópicos a seguir.

* [Como usar a autenticação de assinatura de acesso compartilhado com barramento de serviço](/azure/service-bus-messaging/service-bus-sas)

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a>Considerar o uso do método OnMessage para evitar "loop de recebimento"
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Descrição
Para evitar o início de um "loop de recebimento" a chamada ao método **OnMessage** é a melhor solução para receber mensagens do que chamar o método **Receive**. No entanto, se você deve usar o método **Receive** e especificar um tempo de espera de servidor não padrão, verifique se o tempo de espera do servidor é mais de um minuto.

### <a name="reason"></a>Reason
Ao chamar **OnMessage**, o cliente inicia uma bomba de mensagens internas que monitora constantemente a fila ou assinatura. Essa bomba de mensagens contém um loop infinito que emite uma chamada para receber mensagens. Se a chamada alcançar o tempo limite, ele emitirá uma nova chamada. O intervalo de tempo limite é determinado pelo valor da propriedade [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) do [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx) que está sendo usado.

A vantagem de usar o **OnMessage** em comparação com **Receive** é que os usuários não precisarão manualmente pesquisar mensagens, manipular exceções, processar várias mensagens em paralelo e concluir mensagens.

Se você chamar **Receive** sem usar o valor padrão, não se esqueça que o valor de *ServerWaitTime* é a mais de um minuto. A definição de *ServerWaitTime* para mais de um minuto impede que o servidor alcance o tempo limite antes que a mensagem seja recebida totalmente.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Consulte exemplos de código a seguir para usos recomendados. Para obter mais detalhes, consulte o método [QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e o método [QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

Para melhorar o desempenho da infraestrutura de mensagens do Azure, consulte o padrão de design [Prévia de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

A seguir, um exemplo de uso de **OnMessage** para receber mensagens.

```csharp
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is received, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

A seguir, um exemplo de uso de **Receive** com o tempo de espera de servidor padrão.

```csharp
string connectionString =
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)
{
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

A seguir, um exemplo de uso de **Receive** com o tempo de espera de servidor não padrão.

```csharp
while (true)
{
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```

## <a name="consider-using-asynchronous-service-bus-methods"></a>Considere o uso de métodos assíncronos de barramento de serviço
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Descrição
Use os métodos assíncronos do barramento de serviço para melhorar o desempenho com sistema de mensagens agenciado.

### <a name="reason"></a>Reason
O uso de métodos assíncronos permite a simultaneidade do programa aplicativo porque a execução de cada chamada não bloqueia o thread principal. Ao usar os métodos de mensagens do Barramento de Serviço, a execução de uma operação (enviar, receber, excluir, etc.) leva tempo. Esse tempo inclui o processamento da operação pelo serviço do barramento de serviço, além da latência da solicitação e resposta. Para aumentar o número de operações por hora, elas devem ser executadas simultaneamente. Para obter mais informações, consulte [Práticas recomendadas para melhorias de desempenho usando o sistema de mensagens agenciado do Barramento de Serviço](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>{1&gt;&lt;1} Solução
Consulte [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obter informações sobre como usar o método assíncrono recomendado.

Para melhorar o desempenho da infraestrutura de mensagens do Azure, consulte o padrão de design [Prévia de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Considerar o particionamento de tópicos e filas do barramento de serviço
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Descrição
Particione filas e tópicos do barramento de serviço para um melhor desempenho com as mensagens do barramento de serviço.

### <a name="reason"></a>Reason
O particionamento de tópicos e filas do barramento de serviço aumenta a taxa de transferência do desempenho e a disponibilidade do serviço porque a taxa de transferência geral de uma fila ou tópico particionado não é mais limitada pelo desempenho de um único agente ou repositório de mensagens. Além disso, uma falha temporária de um repositório de mensagens não torna uma fila ou tópico particionado indisponível. Para saber mais, confira [Particionamento de entidades de mensagens](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>{1&gt;&lt;1} Solução
O snippet de código a seguir mostra como particionar entidades de mensagens.

```csharp
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Para obter mais informações, consulte [Tópicos e filas do barramento de serviço particionado | Blog do Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) e confira a amostra [Fila particionada do Barramento de Serviço do Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f).

## <a name="do-not-set-sharedaccessstarttime"></a>Não definir SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Descrição
Você deve evitar usar SharedAccessStartTimeset para a hora atual para iniciar imediatamente a política de acesso compartilhado. Você só precisa definir essa propriedade se quiser iniciar a política de acesso compartilhado em um momento posterior.

### <a name="reason"></a>Reason
A sincronização do relógio causa uma pequena diferença de hora entre os data centers. Por exemplo, você pensaria logicamente que definir a hora de início de uma política SAS de armazenamento como a hora atual usando o método DateTime.Now ou semelhante faria com que a política SAS entrasse em vigor imediatamente. No entanto, as pequenas diferenças de horário entre data centers podem causar problemas com isso, já que alguns horários de data center podem ser ligeiramente posteriores ou anteriores à hora de início. Como resultado, a política de SAS pode expirar rapidamente (ou até mesmo imediatamente) se o tempo de vida da política definido for muito curto.

Para orientação de como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [Apresentando SAS (Assinatura de Acesso Compartilhado) de tabela, SAS de fila e atualização de SAS de blob - Blog da equipe de Armazenamento do Microsoft Azure - Home page do site - Blogs MSDN](https://blogs.msdn.microsoft.com/windowsazurestorage/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas/).

### <a name="solution"></a>{1&gt;&lt;1} Solução
Remova a instrução que define a hora de início da política de acesso compartilhado. A ferramenta de análise de código do Azure fornece uma correção para esse problema. Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [Padrão de chave de manobrista](https://msdn.microsoft.com/library/dn568102.aspx).

O snippet de código a seguir demonstra a correção de código para esse problema.

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>O tempo de expiração da Política de Acesso Compartilhado deve ser mais de cinco minutos
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Descrição
Pode haver até cinco minutos de diferença em relógios dos data centers em locais diferentes devido a uma condição conhecida como "defasagem horária". Para impedir que o token da política de SAS expire antes do planejado, defina a hora de expiração para mais de cinco minutos.

Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](https://social.msdn.microsoft.com/Forums/en-US/home).

### <a name="reason"></a>Reason
Data centers em locais diferentes no mundo sincronizam por um sinal de relógio. Como o sinal de relógio demora em viajar para locais diferentes, pode haver uma variação de tempo entre data centers em locais geográficos diferentes, embora supostamente tudo esteja sincronizado. Essa diferença de tempo pode afetar o intervalo de expiração e a hora de início da política de acesso compartilhado. Portanto, para garantir a política de acesso compartilhado entre em vigor imediatamente, não especifique a hora de início. Além disso, verifique se que a hora de expiração é de mais de 5 minutos para evitar antecipação do tempo limite.

Para obter instruções sobre como usar assinatura de acesso compartilhado no armazenamento do Azure, consulte [Apresentando SAS (Assinatura de Acesso Compartilhado) de tabela, SAS de fila e atualização de SAS de blob - Blog da equipe de Armazenamento do Microsoft Azure - Home page do site - Blogs MSDN](https://blogs.msdn.microsoft.com/windowsazurestorage/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas/).

### <a name="solution"></a>{1&gt;&lt;1} Solução
Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [Padrão de chave de manobrista](https://msdn.microsoft.com/library/dn568102.aspx).

Este é um exemplo de não especificar uma hora de início da política de acesso compartilhado.

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Este é um exemplo de especificação de uma hora de início da política de acesso compartilhado com uma duração de expiração de política superior a cinco minutos.

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Para obter mais informações, consulte [Criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Use CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Descrição
O uso da classe [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) para projetos como o site do Azure e serviços móveis do Azure não introduzirá problemas de runtime. Como melhor prática, no entanto, é uma boa ideia usar Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como uma forma unificada de gerenciamento de configurações para todos os aplicativos de nuvem do Azure.

### <a name="reason"></a>Reason
CloudConfigurationManager lê o arquivo de configuração apropriado para o ambiente do aplicativo.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>{1&gt;&lt;1} Solução
Refatore seu código para usar a classe [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Uma correção de código para esse problema é fornecida pela ferramenta de análise de código do Azure.

O snippet de código a seguir demonstra a correção de código para esse problema. {1&gt;Substituir&lt;1}

`var settings = ConfigurationManager.AppSettings["mySettings"];`

Com

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Eis um exemplo de como armazenar a definição de configuração em um arquivo App.config ou Web.config. Adicione as configurações à seção appSettings do arquivo de configuração. Este é o arquivo Web.config para o exemplo de código anterior.

```xml
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Evitar o uso de cadeias de conexão embutidas em código
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Descrição
Se você usar cadeias de conexão embutidas em código e precisar atualizá-las mais tarde, terá de fazer alterações em seu código-fonte e recompilar o aplicativo. No entanto, se você armazenar as cadeias de conexão em um arquivo de configuração, poderá alterá-las posteriormente simplesmente atualizando o arquivo de configuração.

### <a name="reason"></a>Reason
Cadeias de conexão hard-coding é uma prática ruim, porque apresenta problemas quando as cadeias de conexão precisam ser alteradas rapidamente. Além disso, se o projeto precisar ser verificado no controle do código-fonte, as cadeias de conexão embutidas em código introduzirão vulnerabilidades de segurança, já que podem ser exibidas no código-fonte.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Armazene cadeias de conexão em arquivos de configuração ou ambientes do Azure.

* Para aplicativos autônomos, use o app.config para armazenar configurações de cadeia de conexão.
* Para aplicativos autônomos, use o web.config para armazenar cadeias de conexão.
* Para aplicativos do vNext do ASP.NET, use configuration.json para armazenar cadeias de conexão.

Para obter informações sobre como usar arquivos de configurações, como web.config ou app.config, consulte [Diretrizes de configuração Web do ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Para obter informações sobre como variáveis de ambiente do Azure funcionam, consulte [Sites do Azure: como as cadeias de aplicativo e cadeias de conexão funcionam](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Para obter informações sobre o armazenamento de cadeia de conexão no controle do código-fonte, consulte [Evitar colocar informações confidenciais, como cadeias de conexão em arquivos armazenados no repositório de código-fonte](/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Usar arquivo de configuração de diagnóstico
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Descrição
Em vez de definir as configurações de diagnóstico em seu código usando a API de programação Microsoft.WindowsAzure.Diagnostics, você deve configurar as definições de diagnóstico no arquivo diagnostics.wadcfg. (Ou diagnostics.wadcfgx se você usar o SDK 2.5 do Azure). Fazendo isso, você pode alterar as configurações de diagnóstico sem recompilar o código.

### <a name="reason"></a>Reason
Antes do SDK 2.5 do Azure (que usa o diagnóstico do Azure 1.3), o diagnóstico do Azure (WAD) podia ser configurado usando vários métodos diferentes: adicionando-o ao blob de configuração no armazenamento, usando código obrigatório, configuração declarativa ou a configuração padrão. No entanto, a maneira preferencial de configurar diagnósticos é usar um arquivo de configuração XML (diagnostics.wadcfg ou diagnostics.wadcfgx para o SDK 2.5 e posterior) no projeto de aplicativo. Nessa abordagem, o arquivo diagnostics.wadcfg define completamente a configuração e pode ser atualizado e reimplantado à vontade. Misturar o uso do arquivo de configuração Diagnostics. wadcfg com os métodos programáticos de configuração de configurações usando as classes [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) pode levar à confusão. Consulte [Inicializar ou alterar configuração de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obter mais informações.

A partir do WAD 1.3 (incluído com o SDK 2.5 do Azure), não é possível usar o código para configurar diagnóstico. Como resultado, você só pode fornecer a configuração ao aplicar ou atualizar a extensão de diagnóstico.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Use o designer de configuração de diagnóstico para mover as configurações de diagnóstico para o arquivo de configuração de diagnóstico (diagnostics.wadcfg ou diagnostics.wadcfgx para SDK 2.5 e posterior). Também é recomendável que você instale [SDK 2.5 do Azure](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/VWDOrVs2015AzurePack.appids) e usar o recurso de diagnóstico mais recente.

1. No menu de atalho da função que você deseja configurar, escolha Propriedades e, em seguida, escolha a guia Configuração.
2. Na seção **Diagnóstico**, verifique se a caixa de seleção **Habilitar Diagnóstico** está marcada.
3. Escolha o botão **Configurar** .

   ![Acessando a opção Habilitar diagnóstico](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Consulte [Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obter mais informações.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Evitar declarar objetos DbContext como estáticos
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Descrição
Para economizar memória, evite declarar objetos DbContext como estáticos.

### <a name="reason"></a>Reason
Objetos DBContext mantêm os resultados da consulta de cada chamada. Os objetos estáticos DBContext não são descartados até que o domínio de aplicativo seja descarregado. Portanto, um objeto DBContext estático pode consumir grandes quantidades de memória.

### <a name="solution"></a>{1&gt;&lt;1} Solução
Declare DBContext como uma variável local ou um campo de instância não estático, use-o para uma tarefa e deixe-o ser descartado após o uso.

O exemplo a seguir de classe de controlador MVC mostra como usar o objeto DBContext.

```csharp
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}
Para saber mais sobre a otimização e solução de problemas de aplicativos do Azure, consulte [Solucionar problemas de um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio).

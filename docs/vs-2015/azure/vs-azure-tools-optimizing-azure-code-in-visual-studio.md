---
title: Otimizando o código do Azure no Visual Studio | Microsoft Docs
description: Saiba mais sobre o código do Azure como ferramentas de otimização no Visual Studio ajudam a tornar seu código mais robusto e com melhor desempenho.
author: ghogen
manager: douge
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.topic: conceptual
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 11/11/2016
ms.author: ghogen
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: d1d0f5a69015a6c6596e1a2b7ee85b12f4116d6b
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001177"
---
# <a name="optimizing-your-azure-code"></a>Otimizando o código do Azure
Quando você está programando aplicativos que usam o Microsoft Azure, há algumas práticas de codificação que você deve seguir para ajudar a evitar problemas de escalabilidade do aplicativo, comportamento e desempenho em um ambiente de nuvem. A Microsoft fornece uma ferramenta de análise de código do Azure que reconhece e identifica vários desses problemas comumente encontrados e ajuda você a resolvê-los. Você pode baixar a ferramenta no Visual Studio por meio do NuGet.

## <a name="azure-code-analysis-rules"></a>Regras de análise de código do Azure
A ferramenta de análise de código do Azure usa as seguintes regras para sinalizar automaticamente seu código do Azure quando encontra problemas conhecidos que afetam o desempenho. Problemas detectados aparecem como avisos ou erros do compilador. Correções de código ou sugestões para resolver o erro ou aviso geralmente são fornecidos por meio de um ícone de lâmpada.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Evite usar o modo de estado de sessão (em processo) padrão
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Descrição
Se você usar o modo de estado de sessão (em processo) padrão para aplicativos em nuvem, você poderá perder o estado de sessão.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Por padrão, o modo de estado de sessão especificado no arquivo Web. config está no processo. Além disso, se nenhuma entrada for especificada no arquivo de configuração, o modo de estado de sessão padrão no processo. O modo em processo armazena o estado de sessão na memória no servidor web. Quando uma instância é reiniciada ou uma nova instância é usada para balanceamento de carga ou suporte a failover, o estado de sessão armazenado na memória no servidor web não é salvo. Essa situação impede que o aplicativo seja escalonável na nuvem.

Estado de sessão ASP.NET dá suporte a várias opções diferentes de armazenamento para dados de estado de sessão: InProc, StateServer, SQLServer, personalizado e Off. É recomendável que você use o modo personalizado para hospedar dados em um repositório externo de estado de sessão, como [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Solução
É uma solução recomendada armazenar o estado de sessão em um serviço de cache gerenciado. Saiba como usar [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) para armazenar o estado da sessão. Você também pode armazenar o estado de sessão em outros locais para garantir que seu aplicativo seja escalonável na nuvem. Para saber mais sobre as soluções alternativas, leia [modos de estado de sessão](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>Método de execução não deve ser assíncrono
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Descrição
Crie métodos assíncronos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fora do [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e, em seguida, chamar os métodos assíncronos de [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Declarando o [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método como assíncrono faz com que a função de trabalho inserir um loop de reinicialização.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Chamando métodos assíncronos dentro de [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que o tempo de execução do serviço de nuvem recicle a função de trabalho. Quando uma função de trabalho é iniciado, o toda a execução de programa ocorre dentro de [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. Saindo do [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que a função de trabalho reiniciar. Quando o tempo de execução de função de trabalho atinge o método assíncrono, ele envia todas as operações posteriores ao método assíncrono e, em seguida, retorna. Isso faz com que a função de trabalho sair das [ [ [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e a reinicialização. Na próxima iteração da execução, a função de trabalho atinge o método assíncrono novamente e reinicia, fazendo com que a função de trabalho reciclada novamente.

### <a name="solution"></a>Solução
Colocar todas as operações assíncronas fora das [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. Em seguida, chame o método async refatorado de dentro de [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, como RunAsync () wait. A ferramenta de análise de código do Azure pode ajudar você a corrigir esse problema.

O trecho de código a seguir demonstra o código para corrigir esse problema:

```
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

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Usar a autenticação de assinatura de acesso compartilhado do Service Bus
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Descrição
Use assinatura de acesso compartilhado (SAS) para autenticação. Access Control Service (ACS) está sendo preterido para autenticação do barramento de serviço.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Para maior segurança, Active Directory do Azure está substituindo a autenticação ACS com a autenticação de SAS. Ver [Azure Active Directory é o futuro do ACS](https://cloudblogs.microsoft.com/enterprisemobility/2013/06/22/azure-active-directory-is-the-future-of-acs/) para obter informações sobre o plano de transição.

### <a name="solution"></a>Solução
Use a autenticação SAS em seus aplicativos. O exemplo a seguir mostra como usar um token SAS existente para acessar um namespace do barramento de serviço ou uma entidade.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Consulte os tópicos a seguir para obter mais informações.

* Para obter uma visão geral, consulte [autenticação de assinatura de acesso compartilhado com barramento de serviço](https://msdn.microsoft.com/library/dn170477.aspx)
* [Como usar a autenticação de assinatura de acesso compartilhado com barramento de serviço](https://msdn.microsoft.com/library/dn205161.aspx)
* Para um projeto de exemplo, consulte [autenticação usando SAS Shared Access Signature () com assinaturas do barramento de serviço](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a>Considere o uso do método OnMessage para evitar "loop de recebimento"
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Descrição
Para evitar o início de um "loop de recebimento" chamando o **OnMessage** método é a melhor solução para o recebimento de mensagens do que chamar o **Receive** método. No entanto, se você precisar usar o **Receive** método e você especificar um tempo de espera de servidor não padrão, verifique se o tempo de espera de servidor é a mais de um minuto.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Ao chamar **OnMessage**, o cliente inicia uma bomba de mensagens internas que monitora constantemente a fila ou assinatura. Essa bomba de mensagens contém um loop infinito que emite uma chamada para receber mensagens. Se a chamada de tempo limite, ele emite uma nova chamada. O intervalo de tempo limite é determinado pelo valor da [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propriedade da [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)que está sendo usado.

A vantagem de usar **OnMessage** em comparação com **Receive** é que os usuários não precisarão manualmente sondar mensagens, manipular exceções, processar várias mensagens em paralelo e concluir as mensagens.

Se você chamar **Receive** sem usar o valor padrão, certifique-se a *ServerWaitTime* valor é a mais de um minuto. Definindo *ServerWaitTime* para mais de um minuto impede que o servidor de tempo limite antes que a mensagem seja recebida totalmente.

### <a name="solution"></a>Solução
Consulte os exemplos de código a seguir para usos recomendados. Para obter mais detalhes, consulte [Queueclient onMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)e [método Queueclient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

Para melhorar o desempenho da infra-estrutura de mensagens do Azure, consulte o padrão de design [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

A seguir está um exemplo de uso **OnMessage** para receber mensagens.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

A seguir está um exemplo de uso **Receive** tempo de espera com o servidor padrão.

```
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

A seguir está um exemplo de uso **Receive** tempo de espera com um servidor diferente do padrão.

```
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
Use métodos assíncronos do barramento de serviço para melhorar o desempenho com mensagens orientadas.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Usar métodos assíncronos permite a simultaneidade do programa aplicativo porque a execução de cada chamada não bloqueia o thread principal. Ao usar o barramento de serviço, métodos de mensagens, a execução de uma operação (enviar, receber, excluir, etc.) leva tempo. Esse tempo inclui o processamento da operação pelo serviço do barramento de serviço, além da latência da solicitação e resposta. Para aumentar o número de operações por hora, elas devem ser executadas simultaneamente. Para obter mais informações, consulte [práticas recomendadas para desempenho melhorias usando o serviço de mensagens Agenciado do barramento](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Solução
Ver [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obter informações sobre como usar o método assíncrono recomendado.

Para melhorar o desempenho da infra-estrutura de mensagens do Azure, consulte o padrão de design [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Considere particionamento de tópicos e filas do barramento de serviço
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Descrição
As filas do barramento de serviço de partição e tópicos para obter melhor desempenho com o sistema de mensagens do barramento de serviço.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Particionamento de tópicos e filas do barramento de serviço aumenta o desempenho taxa de transferência e disponibilidade do serviço, porque a taxa de transferência geral de uma fila ou tópico particionado não é mais limitada pelo desempenho de um único agente ou repositório de mensagens. Além disso, uma interrupção temporária de um repositório de mensagens não faz uma fila ou tópico particionado indisponível. Para obter mais informações, consulte [particionamento de entidades de mensagens](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Solução
O trecho de código a seguir mostra como particionar entidades de mensagens.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Para obter mais informações, consulte [tópicos e filas de barramento de serviço particionado | Blog do Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) e conferir as [fila particionada do Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) exemplo.

## <a name="do-not-set-sharedaccessstarttime"></a>Não definir SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Descrição
Você deve evitar usar SharedAccessStartTimeset para a hora atual para iniciar imediatamente a política de acesso compartilhado. Você só precisará definir essa propriedade se você deseja iniciar a política de acesso compartilhado em um momento posterior.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Sincronização do relógio causa uma pequena diferença de hora entre os data centers. Por exemplo, você pensaria logicamente que definir a hora de início de uma política SAS de armazenamento como a hora atual, usando DateTime. Now ou um método semelhante fará com que a política de SAS entrem em vigor imediatamente. No entanto, as pequenas diferenças de horário entre data centers podem causar problemas com isso, já que algumas vezes de datacenter podem estar um pouco posteriores à hora de início, enquanto outros à sua frente. Como resultado, a política de SAS pode expirar rapidamente (ou até mesmo imediatamente) se o tempo de vida de política for definido muito curto.

Para obter instruções sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado), SAS de fila e atualização para SAS de Blob - Blog de equipe de armazenamento do Microsoft Azure - página inicial - Site Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solução
Remova a instrução que define a hora de início da política de acesso compartilhado. A ferramenta de análise de código do Azure fornece uma correção para esse problema. Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [padrão Valet Key](https://msdn.microsoft.com/library/dn568102.aspx).

O trecho de código a seguir demonstra o código para corrigir esse problema.

```
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

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Hora de expiração deve ser mais de cinco minutos de política de acesso compartilhado
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Descrição
Pode haver como cinco minutos de diferença em relógios dos data centers em locais diferentes devido a uma condição conhecida como "defasagem horária". Para impedir que a SAS o token da política de expiração antes do planejado, defina a hora de expiração para mais de cinco minutos.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Data centers em locais diferentes em todo o mundo sincronizem por um sinal de relógio. Como demora para o sinal de relógio viajar para locais diferentes, pode haver uma variação de tempo entre data centers em locais geográficos diferentes embora supostamente tudo esteja sincronizado. Essa diferença de tempo pode afetar o intervalo de expiração e a hora de início do diretiva acesso compartilhado. Portanto, para garantir que a política de acesso compartilhado entra em vigor imediatamente, não especifique a hora de início. Além disso, certifique-se de que o tempo de expiração é de mais de 5 minutos para impedir que o antecipação do tempo limite.

Para obter mais informações sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado), SAS de fila e atualização para SAS de Blob - Blog de equipe de armazenamento do Microsoft Azure - página inicial - Site Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solução
Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [padrão Valet Key](https://msdn.microsoft.com/library/dn568102.aspx).

O exemplo a seguir é um exemplo de não especificar uma hora de início da política de acesso compartilhado.

```
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

O exemplo a seguir é um exemplo de especificação de uma hora de início da política de acesso compartilhado com uma duração de expiração da política maior do que cinco minutos.

```
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

Para obter mais informações, consulte [criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Usar o CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Descrição
Usando o [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) para projetos de classe, como o site do Azure e serviços móveis do Azure não introduzirá problemas de tempo de execução. Como prática recomendada, no entanto, é uma boa ideia usar Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como uma forma unificada de gerenciamento de configurações para todos os aplicativos de nuvem do Azure.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
CloudConfigurationManager lê o arquivo de configuração apropriado para o ambiente do aplicativo.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Solução
Refatorar seu código para usar o [classe CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Um código para corrigir esse problema é fornecido pela ferramenta de análise de código do Azure.

O trecho de código a seguir demonstra o código para corrigir esse problema. Substituir

`var settings = ConfigurationManager.AppSettings["mySettings"];`

with

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Aqui está um exemplo de como armazenar a definição de configuração em um arquivo App. config ou Web. config. Adicione as configurações para a seção appSettings do arquivo de configuração. A seguir está o arquivo Web. config para o exemplo de código anterior.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Evite usar cadeias de caracteres de conexão embutida
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Descrição
Se você usar cadeias de caracteres de conexão embutida e você precisará atualizá-las posteriormente, você precisará fazer alterações em seu código-fonte e recompilar o aplicativo. No entanto, se você armazenar as cadeias de conexão em um arquivo de configuração, você pode alterá-las posteriormente simplesmente atualizando o arquivo de configuração.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Codificar cadeias de caracteres de conexão é uma prática ruim, porque apresenta problemas quando as cadeias de caracteres de conexão precisam ser alteradas rapidamente. Além disso, se o projeto precisa ser verificado no controle do código-fonte, cadeias de caracteres de conexão embutido em código introduzirão vulnerabilidades de segurança, pois as cadeias de caracteres podem ser exibidas no código-fonte.

### <a name="solution"></a>Solução
Store cadeias de caracteres de conexão em arquivos de configuração ou ambientes do Azure.

* Para aplicativos autônomos, use o App. config para armazenar configurações de cadeia de caracteres de conexão.
* Para aplicativos web hospedados no IIS, use o Web. config para armazenar cadeias de caracteres de conexão.
* Para aplicativos do ASP.NET vNext, use Configuration para armazenar cadeias de conexão.

Para obter informações sobre como usar arquivos de configurações, como Web. config ou App. config, consulte [diretrizes de configuração do ASP.NET Web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Para obter informações sobre o trabalho de variáveis de ambiente como o Azure, consulte [Sites do Azure: como cadeias de caracteres de aplicativo e cadeias de caracteres de Conexão funcionam](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Para obter informações sobre como armazenar a cadeia de caracteres de conexão no controle de origem, consulte [evitar colocar informações confidenciais, como cadeias de caracteres de conexão em arquivos que são armazenados no repositório de código fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Usar arquivo de configuração de diagnóstico
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Descrição
Em vez de configurar as configurações de diagnóstico em seu código, como usando a API de programação de windowsazure, você deve configurar as configurações de diagnóstico no arquivo Diagnostics. wadcfg. (Ou Diagnostics. wadcfgx se você usar o SDK do Azure 2.5). Ao fazer isso, você pode alterar as configurações de diagnóstico sem ter que recompilar seu código.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Antes que o Azure SDK 2.5 (que usa o diagnóstico do Azure 1.3), o diagnóstico do Azure (WAD) pode ser configurado usando vários métodos diferentes: adicioná-lo para o blob de configuração no armazenamento, usando código obrigatório, configuração declarativa ou o padrão configuração. No entanto, a maneira preferencial para configurar diagnósticos é usar um arquivo de configuração XML (Diagnostics. wadcfg ou diagnositcs para SDK 2.5 e posterior) no projeto de aplicativo. Nessa abordagem, o arquivo Diagnostics. wadcfg completamente define a configuração e pode ser atualizado e reimplantado à vontade. Combinar o uso do arquivo de configuração Diagnostics. wadcfg com os métodos de programação de definir configurações usando o [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes podem gerar confusão. Ver [inicializar ou alterar configuração de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obter mais informações.

A partir do WAD 1.3 (incluído no SDK do Azure 2.5), não é possível usar código para configurar o diagnóstico. Como resultado, você só pode fornecer a configuração ao aplicar ou atualizar a extensão de diagnóstico.

### <a name="solution"></a>Solução
Use o designer de configuração de diagnóstico para mover as configurações de diagnóstico para o arquivo de configuração de diagnóstico (diagnositcs. wadcfg ou diagnositcs para SDK 2.5 e posterior). Também é recomendável que você instale [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) e usar o recurso de diagnóstico mais recente.

1. No menu de atalho para a função que você deseja configurar, escolha Propriedades e, em seguida, escolha a guia Configuração.
2. No **diagnósticos** seção, certifique-se de que o **habilitar diagnóstico** caixa de seleção está selecionada.
3. Escolha o **configurar** botão.

   ![Acessando a opção Habilitar diagnóstico](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Ver [Configurando o diagnóstico para serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obter mais informações.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Evite declarar objetos DbContext como estáticos
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Descrição
Para economizar memória, evite declarar objetos DBContext como estáticos.

Compartilhe suas ideias e comentários no [comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Objetos DBContext mantêm os resultados da consulta de cada chamada. Os objetos estáticos DBContext não são descartados até que o domínio do aplicativo seja descarregado. Portanto, um objeto DBContext estático pode consumir grandes quantidades de memória.

### <a name="solution"></a>Solução
Declare DBContext como uma variável local ou um campo de instância não estático, usá-lo para uma tarefa e, em seguida, deixe-a ser descartado após o uso.

O exemplo a seguir classe do controlador MVC mostra como usar o objeto DBContext.

```
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

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre a otimização e solução de problemas de aplicativos do Azure, consulte [solucionar problemas de um aplicativo web no serviço de aplicativo do Azure usando o Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio).

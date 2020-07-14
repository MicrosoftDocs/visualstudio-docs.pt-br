---
title: 'Tutorial: Verificação de'
description: Usando o Azure Functions no Visual Studio para Mac.
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.technology: vs-ide-install
ms.assetid: 38FD2070-5151-482E-B0A9-993715128736
ms.topic: tutorial
ms.openlocfilehash: 144580b0ebe0eb3615c5cf55c1bee03ff2a614fa
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938978"
---
# <a name="tutorial-getting-started-with-azure-functions"></a>Tutorial: Introdução ao Azure Functions

Neste laboratório, você aprenderá a começar a criar no Azure Functions usando o Visual Studio para Mac. Você também fará a integração com as tabelas de armazenamento do Azure, que representam um dos muitos tipos de associações e gatilhos disponíveis para os desenvolvedores no Azure Functions.

## <a name="objectives"></a>Objetivos

> [!div class="checklist"]
> * Criar e depurar funções do Azure locais
> * Integrar com recursos de armazenamento do Azure e da Web
> * Organizar um fluxo de trabalho envolvendo várias funções do Azure

## <a name="requirements"></a>Requisitos

- Visual Studio para Mac 7.5 ou posterior.
- Uma assinatura do Azure (disponível gratuitamente em [https://azure.com/free](https://azure.com/free) ).

## <a name="exercise-1-creating-an-azure-functions-project"></a>Exercício 1: Criar um projeto do Azure Functions

1. Iniciar **Visual Studio para Mac**.

2. Selecione **Arquivo > Nova Solução**.

3. Na categoria **Nuvem > Geral**, selecione o modelo do **Azure Functions**. Você usará o C# para criar uma biblioteca de classes .NET que hospeda o Azure Functions. Clique em **Próximo**.

    ![Seleção de modelo do Azure Functions](media/azure-functions-lab-image1.png)

4. Definir o **Nome do Projeto** como **"AzureFunctionsLab"** e clique em **Criar**.

    ![Nomeando e criando seu projeto de função do Azure](media/azure-functions-lab-image2.png)

5. Expanda os nós no **Painel de Soluções**. O modelo de projeto padrão inclui referências de NuGet a uma variedade de pacotes do Azure WebJobs, bem como ao pacote Newtonsoft.Json.

     Também há três arquivos: - **host.json** para descrever as opções de configuração globais para o host - **local.settings.json** para definir as configurações de serviço.
        - O modelo de projeto também cria um HttpTrigger padrão. Para este laboratório, você deve excluir o arquivo **HttpTrigger.cs** do projeto.

    Abra **local.settings.json**. O padrão é ter duas configurações de cadeia de conexão vazias.

    ![Painel de Soluções exibindo o arquivo local.settings.json](media/azure-functions-lab-image3.png)

## <a name="exercise-2-creating-an-azure-storage-account"></a>Exercício 2: Criar uma Conta de Armazenamento do Azure

1. Faça logon em sua conta do Azure em [https://portal.azure.com](https://portal.azure.com) .

1. Na seção **Favoritos**, localizada à esquerda na tela, selecione **Contas de Armazenamento**:

    ![Seção Favoritos do portal do Azure mostrando o item de contas de armazenamento](media/azure-functions-lab-image4.png)

1. Selecione **Adicionar** para criar uma nova conta de armazenamento:

    ![Botão para adicionar nova conta de armazenamento](media/azure-functions-lab-image5.png)

1. Insira um nome global exclusivo em **Nome** e reutilize-o para o **Grupo de recursos**. Você pode manter todos os outros itens com os valores padrão.

    ![Detalhes da nova conta de armazenamento](media/azure-functions-lab-image6.png)

1. Clique em **Criar**. Pode levar alguns minutos para criar a conta de armazenamento. Você receberá uma notificação quando ela tiver sido criada com êxito.

    ![Notificação de implantação bem-sucedida](media/azure-functions-lab-image7.png)

1. Selecione o botão **Ir para o recurso** na notificação.

1. Selecione a guia **Chaves de acesso**.

    ![Configuração de chave de acesso](media/azure-functions-lab-image8.png)

1. Copie a primeira **Cadeia de conexão**. Essa cadeia de caracteres é usada para integrar o Armazenamento do Azure com o Azure Functions posteriormente.

    ![Informações sobre a chave 1](media/azure-functions-lab-image9.png)

1. Retorne ao **Visual Studio para Mac** e cole a cadeia de conexão completa como a configuração **AzureWebJobsStorage** em **local.settings.json**. Agora, você pode referenciar o nome da configuração nos atributos para funções que precisam de acesso a seus recursos.

    ![Arquivo de configurações local com a chave de conexão inserida](media/azure-functions-lab-image10.png)

## <a name="example-3-creating-and-debugging-an-azure-function"></a>Exemplo 3: Criar e depurar uma função do Azure

1. Agora, você está pronto para começar a adicionar algum código. Ao trabalhar com uma biblioteca de classes .NET, funções do Azure são adicionadas como métodos estáticos. Em **painel de soluções**, clique com o botão direito do mouse no nó do projeto **AzureFunctions** e selecione **Adicionar > Adicionar função**:

    ![Opção Adicionar Função](media/azure-functions-lab-image11.png)

1. Na caixa de diálogo Novas Funções do Azure, selecione o modelo de webhook Genérico. Definir o **Nome** a **Adicionar** e clique em **OK** para criar a função:

    ![Caixa de diálogo Novas Funções do Azure](media/azure-functions-lab-image12.png)

1. Na parte superior do novo arquivo, adicione as diretivas **using** abaixo:

    ```csharp
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using System.Web;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Remova o método `Run` existente e adicione o método a seguir à classe como sua função do Azure:

    ```csharp
    [FunctionName("Add")]
    public static int Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
    HttpRequestMessage req,
    TraceWriter log)
    {
        int x = 1;
        int y = 2;

        return x + y;
    }
    ```

1. Vamos examinar a definição do método detalhadamente.

    A primeira coisa que você verá é o atributo **FunctionName**, que marca este método como uma função do Azure. O atributo designa o nome público da função. O nome do atributo não precisa corresponder ao nome real do método.

    ![Novo método de execução com o atributo FunctionName realçado](media/azure-functions-lab-image13.png)

1. Em seguida, o método é marcado como um método **estático público**, o que é obrigatório. Você também observará que o valor de retorno é um **int**. A menos que especificado em contrário usando atributos de método, qualquer valor de retorno não void de uma função do Azure é retornado ao cliente como texto. Por padrão, ele é retornado como **XML**, mas pode ser alterado para **JSON**, o que você fará mais tarde no laboratório.

    ![Novo método de execução com a inicialização do método realçada](media/azure-functions-lab-image14.png)

1. O primeiro parâmetro é marcado com o atributo **HttpTrigger**, que indica que esse método é invocado por uma solicitação HTTP. O atributo também especifica o nível de autorização do método, bem como os verbos a que ele dá suporte (apenas **"GET"** nesse caso). Você também pode definir um **Rota** que substitui o caminho para o método e oferece uma forma de extrair automaticamente variáveis do caminho. Como o **Rota** é nula aqui, o caminho para este método terá o valor padrão **/api/Add**.

    ![Novo método de execução com parâmetro realçado](media/azure-functions-lab-image15.png)

1. O parâmetro final do método é um **TraceWriter**, que pode ser usado para registrar mensagens para erros e diagnóstico.

    ![Novo método de execução com TraceWriter realçado](media/azure-functions-lab-image16.png)

1. Defina um ponto de interrupção na linha de **retorno** do método clicando na margem da linha:

    ![Ponto de interrupção definido na linha de retorno](media/azure-functions-lab-image17.png)

1. Crie e execute o projeto em uma sessão de depuração pressionando **F5** ou selecionando **Depurar > Iniciar a Depuração**. Também é possível clicar no botão **Executar**. Todas essas opções executam a mesma tarefa. O restante deste laboratório faz referência a **F5**, mas você pode usar o método que considerar mais confortável.

    ![Criar e executar o projeto](media/azure-functions-lab-image18.png)

1. Executar o projeto abrirá automaticamente o aplicativo de Terminal.

1. O projeto passa por um processo de detecção de funções do Azure com base em atributos de método e em uma convenção de arquivo que será abordada posteriormente neste artigo. Nesse caso, ele detecta uma única função do Azure e "gera" 1 função de trabalho.

    ![Saída da função do Azure no Terminal](media/azure-functions-lab-image19.png)

1. Na parte inferior das mensagens de inicialização, o host do Azure Functions imprime as URLs de qualquer API de gatilho HTTP. Deve haver apenas uma. Copie essa URL e cole-a em uma nova guia do navegador.

    ![URL de API de função do Azure](media/azure-functions-lab-image20.png)

1. O ponto de interrupção deve ser disparado imediatamente. A solicitação da Web foi encaminhada para a função e agora pode ser depurada. Passe o mouse sobre a variável **x** para ver seu valor.

    ![Ponto de interrupção disparado](media/azure-functions-lab-image21.png)

1. Remova o ponto de interrupção usando o mesmo método usado para adicioná-lo anteriormente (clique na margem ou selecione a linha e pressione **F9**).

1. Pressione **F5** para continuar a execução.

1. No navegador, será renderizado o resultado XML do método. Como esperado, a operação de adição codificada produz uma soma plausível. Observe que, se você vir apenas "3" no Safari, vá até **Safari > Preferências > Avançado**, marque a caixa de seleção "**Exibir menu Desenvolver na barra de menus**" e recarregue a página.

1. No **Visual Studio para Mac**, clique no botão **Parar** para encerrar a sessão de depuração. Para garantir que as novas alterações entrem em vigor, não se esqueça de reiniciar (interromper e retomar) a sessão de depuração.

    ![Opção Parar depuração](media/azure-functions-lab-image22.png)

1. No método **Run**, substitua as definições de **x** e **y** pelo código abaixo. Esse código extrai valores cadeia de consulta da URL para que a operação de adição possa ser realizada de forma dinâmica com base nos parâmetros fornecidos.

    ```csharp
    var query = HttpUtility.ParseQueryString(req.RequestUri.Query);

    int x = int.Parse(query["x"]);

    int y = int.Parse(query["y"]);

    return x + y;
    ```

1. Execute o aplicativo.

1. Retorne à janela do navegador e acrescente a cadeia de caracteres `/?x=2&y=3` à URL. A URL inteira agora deve ser `http://localhost:7071/api/Add?x=2&y=3`. Navegue até a nova URL.

1. Dessa vez, o resultado deve refletir os novos parâmetros. Fique à vontade para executar o projeto com valores diferentes. Observe que não há nenhuma verificação de erros, de modo que parâmetros inválidos ou ausentes gerarão um erro.

1. Interrompa a sessão de depuração.

## <a name="exercise-4-working-with-functionjson"></a>Exercício 4: Trabalhar com function.json

1. Em um exercício anterior, mencionamos que o Visual Studio para Mac “gera” uma função de trabalho para a função do Azure definida na biblioteca. Isso acontece porque o Azure Functions não usa de fato os atributos de método em runtime, mas usa uma convenção de sistema de arquivos em tempo de compilação para configurar onde e como as funções do Azure são disponibilizadas. No **Painel de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Revelar no Localizador**.

     ![Opção de menu Revelar no Localizador](media/azure-functions-lab-image23.png)

1. Navegue pelo sistema de arquivos até alcançar **bin/Debug/netstandard2.0**. Deve haver uma pasta chamada **Add**. Essa pasta foi criada para corresponder ao atributo de nome de função no código C#. Expanda a pasta Adicionar para revelar um único arquivo **function.json**. Esse arquivo é usado pelo runtime para hospedar e gerenciar a função do Azure. Para outros modelos de linguagem sem suporte para tempo de compilação (como script em C# ou JavaScript), essas pastas precisam ser criadas e mantidas manualmente. Para desenvolvedores de C#, elas são geradas automaticamente dos metadados de atributo no momento do build. Clique com o botão direito do mouse em **function.json** e selecione para abrir no Visual Studio.

    ![function.json no diretório de arquivos](media/azure-functions-lab-image24.png)

1. Dadas as etapas anteriores deste tutorial, você deve ter uma compreensão básica dos atributos de C#. Levando isso em conta, este JSON deve ser familiar. No entanto, há alguns itens que não foram abordados em exercícios anteriores. Por exemplo, cada **binding** precisa ter seu valor de **direction** definido. Como você pode inferir, **"in"** significa que o parâmetro é uma entrada, enquanto **"out"** indica que o parâmetro é um valor retornado (via **$return**) ou um parâmetro **out** do método. Você também precisa especificar o **scriptFile** (relativo a este local final) e o método **entryPoint** (público e estático) dentro do assembly. Nas próximas etapas, você adicionará um caminho de função personalizado usando este modelo, sendo assim, copie o conteúdo desse arquivo para a área de transferência.

    ![Arquivo function.json aberto no Visual Studio para Mac](media/azure-functions-lab-image25.png)

1. No **Painel de Soluções**, clique com o botão direito do mouse no nó de projeto **AzureFunctionsLab** e selecione **Adicionar > Nova Pasta**. Nomeie a nova pasta como **Adder**. Segundo a convenção padrão, o nome desta pasta definirá o caminho para a API, como **api/Adder**.

    ![Opção Nova Pasta](media/azure-functions-lab-image26.png)

1. Clique com o botão direito do mouse na pasta **Adder** e selecione **Adicionar > Novo Arquivo**.

    ![Opção Novo Arquivo](media/azure-functions-lab-image27.png)

1. Selecione a categoria **Web** e o modelo **Arquivo JSON Vazio**. Defina o **Nome** como **function** e clique em **Novo**.

    ![Opção Arquivo JSON Vazio](media/azure-functions-lab-image28.png)

1. Copie o conteúdo do outro **function.json** (da etapa 3) para substituir o conteúdo padrão do arquivo recém-criado.

1. Remova as seguintes linhas da parte superior do arquivo json:

    ```json
    "configurationSource":"attributes",
    "generatedBy":"Microsoft.NET.Sdk.Functions-1.0.13",
    ```

1. No final da primeira associação (após a linha **"name": "req"**), adicione as propriedades abaixo. Não deixe de incluir uma vírgula na linha anterior. Essa propriedade substitui a raiz padrão, de forma que agora os parâmetros **int** serão extraídos do caminho e colocados nos parâmetros de método chamados **x** e **y**.

    ```json
    "direction": "in",
    "route": "Adder/{x:int?}/{y:int?}"
    ```

1. Adicione outra associação sob a primeira. Essa associação lida com o valor retornado da função. Não deixe de incluir uma vírgula na linha anterior:

    ```json
    {
    "name": "$return",
    "type": "http",
    "direction": "out"
    }
    ```

1. Atualize também a propriedade **entryPoint** na parte inferior do arquivo para usar um método chamado **"Add2"**, como mostrado abaixo. Isso ilustra que o caminho **api/Adder...** pode ser mapeado para um método apropriado com qualquer nome (**Add2** aqui).

    ```json
    "entryPoint": "<project-name>.<function-class-name>.Add2"
    ```

1. Seu arquivo **function.json** final deve ser semelhante ao json a seguir:

    ```json
    {
    "bindings": [
        {
        "type": "httpTrigger",
        "methods": [
            "get"
        ],
        "authLevel": "function",
        "direction": "in",
        "name": "req",
        "route": "Adder/{x:int?}/{y:int?}"
        },
        {
        "name": "$return",
        "type": "http",
        "direction": "out"
        }
    ],
    "disabled": false,
    "scriptFile": "../bin/AzureFunctionsProject.dll",
    "entryPoint": "AzureFunctionsProject.Add.Add2"
    }
    ```

1. A etapa final necessária para fazer tudo isso funcionar é instruir o Visual Studio para Mac a copiar esse arquivo para o mesmo caminho relativo no diretório de saída, sempre que ele for alterado. Com o arquivo selecionado, escolha a guia de propriedades na barra direita e, para **Copiar para diretório de saída** selecione **Copiar se mais recente**:

    ![Opções de propriedades para o arquivo json](media/azure-functions-lab-image30.png)

1. Em **Add.cs**, substitua o método `Run` (incluindo o atributo) pelo seguinte método para preencher a função esperada. Ele é muito semelhante ao método `Run`, mas não usa nenhum atributo e tem parâmetros explícitos para **x** e **y**.

    ```csharp
    public static int Add2(
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        return x + y;
    }
    ```

1. Pressione **F5** para criar e executar o projeto.

1. Conforme o build é concluído e a plataforma o executa, será indicado que há uma segunda rota disponível para as solicitações, que é mapeada para o método recém-adicionado:

    ![URL para funções Http](media/azure-functions-lab-image31.png)

1. Retorne a janela do navegador e navegue até **http://localhost:7071/api/Adder/3/5** .

1. Dessa vez, o método funciona mais uma vez, obtendo os parâmetros do caminho e produzindo uma soma.

1. Retorne ao **Visual Studio para Mac** e encerre a sessão de depuração.

## <a name="exercise-5-working-with-azure-storage-tables"></a>Exercício 5: Trabalhar com tabelas de armazenamento do Azure

Frequentemente, o serviço criado pode ser muito mais complexo do que o que criamos até o momento, e pode demandar tempo e/ou estrutura significativa para ser executado. Nesse caso, você pode achar eficiente aceitar solicitações enfileiradas para processamento quando os recursos ficarem disponíveis, e o Azure Functions dá suporte a isso. Em outros casos, você vai preferir armazenar dados centralmente. As tabelas de Armazenamento do Azure permitem fazer isso facilmente.

1. Adicione a classe abaixo a **Add.cs**. Ela deve ficar dentro do namespace, mas fora da classe atual.

    ```csharp
    public class TableRow : TableEntity
    {
        public int X { get; set; }
        public int Y { get; set; }
        public int Sum { get; set; }
    }
    ```

1. Dentro da classe **Add**, adicione o código abaixo para introduzir outra função. Observe que esta é única até o momento, pois não envolve uma resposta HTTP. A linha final retorna uma nova **TableRow** preenchida com informações de chave que facilitarão a recuperação posteriormente (**PartitionKey** e **RowKey**), bem como seus parâmetros e uma soma. O código dentro do método também usa o **TraceWriter** para ficar mais fácil saber quando a função é executada.

    ```csharp
    [FunctionName("Process")]
    [return: Table("Results")]
    public static TableRow Process(
        [HttpTrigger(AuthorizationLevel.Function, "get",
            Route = "Process/{x:int}/{y:int}")]
        HttpRequestMessage req,
        int x,
        int y,
        TraceWriter log)
    {
        log.Info($"Processing {x} + {y}");

        return new TableRow()
        {
            PartitionKey = "sums",
            RowKey = $"{x}_{y}",
            X = x,
            Y = y,
            Sum = x + y
        };
    }
    ```

1. Pressione **F5** para criar e executar o projeto.

1. Na guia navegador, navegue até **http://localhost:7071/api/Process/4/6** . Isso colocará outra mensagem na fila, o que deve fazer com que outra linha seja adicionada à tabela.

1. Retorne ao **Terminal** e observe a solicitação de entrada de **4 + 6**.

    ![Saída do Terminal mostrando solicitação de adição](media/azure-functions-lab-image32.png)

1. Retorne ao navegador para atualizar a solicitação para a mesma URL. Dessa vez, você verá um erro após o método **Process**. Isso ocorre porque o método está tentando adicionar uma linha à tabela do Armazenamento de Tabelas do Azure usando uma combinação de partição e chave de linha que já existe.

    ```
    System.Private.CoreLib: Exception while executing function: Process. Microsoft.Azure.WebJobs.Host: Error while handling parameter $return after function returned:. Microsoft.Azure.WebJobs.Host: The specified entity already exists.
    ```

1. Encerre a sessão de depuração.

1. Para mitigar o erro, adicione o seguinte parâmetro à definição de método imediatamente antes do parâmetro **TraceWriter**. Esse parâmetro instrui a plataforma do Azure Functions a tentar recuperar uma **TableRow** da tabela de **Results** na **PartitionKey** que usamos para armazenar resultados. No entanto, a magia real acontece quando você percebe que **RowKey** está sendo gerada de forma dinâmica com base nos outros parâmetros **x** e **y** do mesmo método. Se essa linha já existir, **tableRow** a terá quando o método começar sem trabalho extra necessário por parte do desenvolvedor. Se essa linha não existir, o valor será nulo. Esse tipo de eficiência permite que os desenvolvedores se concentrem na lógica de negócios importante, e não na infraestrutura.

    ```csharp
    [Table("Results", "sums", "{x}_{y}")]
    TableRow tableRow,
    ```

1. Adicione o código abaixo ao início do método. Se **tableRow** não for nulo, já teremos o resultado da operação solicitada e poderemos retorná-lo imediatamente. Caso contrário, a função continua como antes. Embora essa possa não ser a forma mais robusta de retornar dados, ela ilustra o fato de que é possível orquestrar operações extremamente sofisticadas em várias camadas escalonáveis com pouquíssimo código.

    ```csharp
    if (tableRow != null)
    {
        log.Info($"{x} + {y} already exists");
        return null;
    }
    ```

1. Pressione **F5** para criar e executar o projeto.

1. Na guia navegador, atualize a URL em **http://localhost:7071/api/Process/4/6** . Como a linha da tabela para este registro existe, ela deve ser retornada imediatamente em erros. Como não há uma saída HTTP, você pode ver a saída no Terminal.

    ![Saída do Terminal mostrando que a linha da tabela já existe](media/azure-functions-lab-image33.png)

1. Atualize a URL para refletir uma combinação ainda não testada, como **http://localhost:7071/api/Process/5/7** . Observe a mensagem no Terminal, que indica que a linha da tabela não foi encontrada (conforme esperado).

    ![Saída do Terminal mostrando novo processo](media/azure-functions-lab-image34.png)

1. Retorne ao **Visual Studio para Mac** e encerre a sessão de depuração.

<!--
1. Finally, let's take a look at what it's like to work with multiple input records. Rather than specify a specific **TableRow**, you can request an **IQueryable<TableRow>** using the same attributes, and the runtime will fill it with the appropriate resource you need. Add the code below to create a **List** function that lists all items that currently exist in the Azure table we've been working with. Also note that we're specifying that the MIME type of the response is **application/json**, so the runtime will automatically render as JSON.

    ```csharp
    [FunctionName("List")]
    public static HttpResponseMessage List(
        [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)]
        HttpRequestMessage req,
        [Table("Results", "sums")]
        IQueryable<TableRow> table,
        TraceWriter log)
    {
        return req.CreateResponse(HttpStatusCode.OK, table, "application/json");
    }
    ```
1. Press **F5** to build and run the project.

1. In the browser tab, navigate to **http://localhost:7071/api/List**. This should pull down the list of all items in the Azure table and render it as JSON.

    ![](https://user-images.githubusercontent.com/3944468/29033725-be9d5a5e-7b4a-11e7-8b55-df0a200b6320.png)
-->

## <a name="summary"></a>Resumo

Neste laboratório, você aprendeu a criar no Azure Functions com o Visual Studio para Mac.

---
title: Criar um teste de serviço Web
ms.date: 06/30/2020
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9934f48e6d5900a418995eb96d357b4ea1ea532f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814753"
---
# <a name="how-to-create-a-web-service-test"></a>Como criar um teste de serviço Web

Você pode usar um teste de desempenho na Web para testar serviços Web. Usando as opções **Inserir solicitação** e **Inserir solicitação de serviço Web**, você pode personalizar as solicitações individuais no **Editor de Testes de Desempenho Web** para localizar páginas de serviço Web. Normalmente, você não exibe essas páginas no aplicativo Web. Portanto, você deve personalizar a solicitação para acessar essas páginas.

>[!NOTE]
> A funcionalidade de teste de carga e desempenho da Web foi preterida no Visual Studio 2019. Por Application Insights, os testes na Web de várias etapas dependem de arquivos do Visual Studio WebTest. Foi [anunciado](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/) que o Visual Studio 2019 será a última versão com a funcionalidade webtest. É importante entender que, embora nenhum novo recurso seja adicionado, a funcionalidade webtest no Visual Studio 2019 ainda é suportada e continuará a ter suporte durante o ciclo de vida de suporte do produto. A equipe de produto do Azure Monitor respondeu perguntas sobre o futuro dos testes de disponibilidade de várias etapas [aqui](https://github.com/MicrosoftDocs/azure-docs/issues/26050#issuecomment-468814101).

**Requisitos**

Visual Studio Enterprise

## <a name="to-create-a-simple-web-service"></a>Para criar um serviço Web simples

Para testar, você pode usar seu próprio serviço Web ou usar o modelo ASMX (serviço Web básico) incluído no Visual Studio. Para criar um serviço Web simples usando este modelo:

1. No Visual Studio, crie um novo projeto usando o modelo de aplicativo Web ASP.NET (.NET Framework) e selecione o modelo **vazio** quando solicitado. Digite um nome e crie o projeto.

1. Em Gerenciador de soluções, clique com o botão direito do mouse no nó do projeto, escolha **Adicionar**  >  **novo item**e escolha **serviço Web (asmx)**. Adicione o serviço Web.

1. Abra *WebService1. asmx* e substitua o `HelloWorld` método Web padrão pelo código a seguir.

   ```csharp
   public string HelloWorld(string str)
   {
      return "Hello, " + str;
   }
   ```

## <a name="install-the-load-testing-component"></a>Instalar a componente de teste de carga

Se ainda não tiver o componente de ferramentas de teste de carga e de desempenho Web instalado, você precisará instalá-lo usando o Instalador do Visual Studio.

1. Abra **instalador do Visual Studio** no menu **Iniciar** do Windows. Você também pode acessá-lo no Visual Studio na caixa de diálogo novo projeto ou escolhendo **ferramentas**  >  **obter ferramentas e recursos** na barra de menus.

1. No **Instalador do Visual Studio**, escolha a guia **Componentes individuais** e role para baixo até a seção **Depuração e testes**. Selecione **Ferramentas de teste de carga e desempenho Web**.

   ![Componente de ferramentas de teste de carga e desempenho Web](media/web-perf-load-testing-tools-component.png)

1. Escolha o botão **Modificar**.

   O componente das ferramentas de teste de carga e desempenho na Web está instalado.

## <a name="create-a-web-test-project"></a>Criar um projeto de teste na Web

Um teste na Web requer o modelo de projeto de projeto de teste de carga e desempenho na Web. Nesta seção, criaremos um projeto de teste de carga em C#. Você também pode criar um projeto de teste de carga do Visual Basic se preferir.

::: moniker range="vs-2017"

1. Abra o Visual Studio.

   Se você estiver usando o modelo ASMX (serviço Web de exemplo), poderá adicionar o projeto de teste da Web à mesma solução.

2. Escolha **Arquivo** > **Novo** > **Projeto** na barra de menus.

   A caixa de diálogo **Novo Projeto** será aberta.

3. Na caixa de diálogo **Novo Projeto**, expanda **Instalado**, expanda **Visual C#** e selecione a categoria **Testar**. Escolha o modelo **Projeto de teste de carga e desempenho na Web**.

   ![Modelo de projeto de teste de carga e desempenho Web](media/web-perf-load-test-project-template.png)

4. Insira um nome para o projeto se não quiser usar o nome padrão e, em seguida, escolha **OK**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio.

   Se você estiver usando o modelo ASMX (serviço Web de exemplo), poderá adicionar o projeto de teste da Web à mesma solução.

2. Na janela iniciar, escolha **criar um novo projeto**.

3. Na página **Criar um novo projeto**, digite **teste da Web** na caixa de pesquisa e selecione o modelo **Desempenho da Web e Projeto de teste de carga \[preterido] ** para o modelo C#. Escolha **Próxima**.

4. Insira um nome para o projeto se não quiser usar o nome padrão e escolha **Criar**.

::: moniker-end

   O Visual Studio cria o projeto e exibe os arquivos em **Gerenciador de soluções**. Inicialmente, o projeto contém um arquivo de teste da Web chamado *WebTest1. WebTest*.

## <a name="to-test-a-web-service"></a>Para testar um serviço Web

1. Inicie o serviço Web e, se necessário, escolha **parar** para pausar o serviço.

1. No projeto de teste na Web, abra *WebTest1. WebTest*, que abre o editor de testes de desempenho Web. No editor de teste, clique com o botão direito do mouse no teste de desempenho da Web e selecione **Adicionar solicitação de serviço Web**.

1. Na propriedade **URL** da nova solicitação, digite o nome do serviço Web, como **https://localhost:44318/WebService1.asmx**.

1. Para o serviço Web, abra uma sessão separada do navegador e digite a URL da página *. asmx* na barra de ferramentas de **endereço** . Na parte superior da página da Web, selecione o método que você deseja testar e examine a mensagem SOAP. (No exemplo de serviço Web, o método é HelloWorld.) Ao abrir o método, você verá que ele contém um `SOAPAction` .

1. No **Editor de Testes de Desempenho Web**, clique com o botão direito do mouse na solicitação e selecione **Adicionar Cabeçalho** para adicionar um novo cabeçalho. Na propriedade **Nome**, digite `SOAPAction`. Na propriedade **valor** , digite o valor que você vê no `SOAPAction` , como *http://tempuri.org/HelloWorld* .

1. Expanda o nó URL no editor de teste, escolha o nó **corpo da cadeia de caracteres** e, na propriedade tipo de **conteúdo** , insira um valor de `text/xml` .

1. Retorne ao navegador na etapa 4, selecione a parte XML da solicitação SOAP da página de descrição do serviço Web e copie-a para a área de transferência.

   O conteúdo XML é semelhante ao seguinte exemplo:

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
       <soap:Body>
         <HelloWorld xmlns="http://tempuri.org/">
           <str>string</str>
         </HelloWorld>
       </soap:Body>
     </soap:Envelope>
     ```

1. Volte para a editor de testes de desempenho Web e escolha as reticências **(...)** na propriedade de **corpo da cadeia de caracteres** . Cole o conteúdo da área de transferência na propriedade.

1. Substitua quaisquer valores de espaço reservado no XML por valores válidos para que o teste possa passar. No exemplo anterior, você substituiria a instância de `string` por um nome.

1. Clique com o botão direito do mouse na solicitação de serviço Web e selecione **Adicionar URL do parâmetro QueryString**.

1. Atribua um nome e um valor ao parâmetro de cadeia de caracteres de consulta. No exemplo anterior, o nome é `op` e o valor é `HelloWorld`. Isso identifica a operação de serviço Web a ser executada.

    > [!NOTE]
    > Você pode usar a vinculação de dados no corpo SOAP para substituir qualquer valor de espaço reservado por valores associados a dados usando a `{{DataSourceName.TableName.ColumnName}}` sintaxe.

1. Execute o teste. No painel superior do **Visualizador de Resultados de Teste de Desempenho na Web**, selecione a solicitação de serviço Web. No painel inferior, selecione a guia **navegador da Web** . O XML que é retornado pelo serviço Web e os resultados de quaisquer operações serão exibidos.

   Procure os resultados para sua solicitação de serviço Web.

## <a name="see-also"></a>Veja também

- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)

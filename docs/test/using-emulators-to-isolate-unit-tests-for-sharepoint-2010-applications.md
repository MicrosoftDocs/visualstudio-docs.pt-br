---
title: Usando emuladores para isolar testes de unidade para aplicativos do Sharepoint 2010
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 1b139d1c1c4e91ac3a7bdd8e0b264bd4dd63a413
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55952652"
---
# <a name="using-emulators-to-isolate-unit-tests-for-sharepoint-2010-applications"></a>Usando emuladores para isolar testes de unidade para aplicativos do Sharepoint 2010

O pacote Microsoft.SharePoint.Emulators fornece um conjunto de bibliotecas que ajudam você a criar testes de unidade isolados para aplicativos do Microsoft SharePoint 2010. Os emuladores usam [shims](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md) da estrutura de isolamento do [Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) para criar objetos na memória leves que imitam os objetos e métodos da API do SharePoint mais comuns. Quando um método do SharePoint não é emulado, ou quando há a necessidade de alterar o comportamento padrão de um emulador, você pode criar shims do Fakes para obter os resultados desejados.

As classes e os métodos de teste existentes podem ser convertidos facilmente para execução no contexto do Emulador. Esse recurso permite criar testes de uso duplo. Um teste de uso duplo pode alternar entre os testes de integração com a API do SharePoint real e os testes de unidade isolados que usam os emuladores.

##  <a name="BKMK_Requirements"></a> Requisitos

-   Microsoft SharePoint 2010 (SharePoint 2010 Server ou SharePoint 2010 Foundation)

-   Microsoft Visual Studio Enterprise

-   Pacote NuGet de emuladores do Microsoft SharePoint

Você também deve estar familiarizado com as [noções básicas de teste de unidade no Visual Studio](../test/unit-test-basics.md) e saber um pouco sobre o [Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md).

##  <a name="BKMK_The_AppointmentsWebPart_example"></a> O exemplo AppointmentsWebPart

O AppointmentsWebPart permite exibir e gerenciar uma lista de seus compromissos do SharePoint.

![Web Part de Compromissos](../test/media/ut_emulators_appointmentswebpart.png)

Testaremos dois métodos da web part neste exemplo:

-   O método `ScheduleAppointment` valida os valores de item de lista passados para o método e cria uma nova entrada em uma lista na Web do SharePoint especificada.

-   O método `GetAppointmentsForToday` retorna os detalhes de compromissos de hoje.

##  <a name="convert-an-existing-test"></a>Converter um teste existente

Em um teste típico de um método em um componente do SharePoint, o método de teste cria um site temporário no SharePoint Foundation e adiciona os componentes do SharePoint ao site necessário para o código em teste. O método de teste cria e executa uma instância do componente. No final do teste, o site é interrompido.

O método `ScheduleAppointment` do nosso código em teste é provavelmente um dos primeiros métodos escritos para o componente:

```csharp
// method under test
public bool ScheduleAppointment(SPWeb web, string listName, string name,
    string phone, string email, string age, DateTime date, out string errorMsg)
{
    errorMsg = string.Empty;
    var badFormat = this.checkInput(name, phone, email, age);
    if (badFormat)
    {
        errorMsg = "Bad Format";
        return false;
    }
    var exists = this.CheckDuplicate(listName, web, name, phone, email, age, date);
    if (exists)
    {
        errorMsg = "Item already exists";
        return false;
    }
    SPListItemCollection items = web.Lists[listName].Items;
    // create item and populate fields
    SPListItem item = items.Add();
    item["Name"] = name;
    item["Phone"] = phone;
    item["Email"] = email;
    item["Age"] = age;
    item["Date"] = date.ToString("D");
    item.Update();
    return true;
}
```

O primeiro teste de funcionalidade no método `ScheduleAppointment` seria mais ou menos assim:

```csharp
[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}
```

Embora esse método de teste verifique que o método `ScheduleAppointment` adiciona uma nova entrada na lista corretamente, ele é mais um teste de integração da web part do que um teste de comportamento específico do seu código. As dependências externas para o SharePoint e a API do SharePoint podem fazer com que o teste falhe por razões diferentes do código do usuário no método `ScheduleAppointment`. A sobrecarga na criação e destruição do site do SharePoint também tornar o teste muito lento para ser executado como parte normal do processo de codificação. A execução da instalação e da destruição do site para cada método de teste só aumenta ainda mais o problema de criação de testes de unidade do desenvolvedor eficientes.

Os emuladores do Microsoft SharePoint oferecem um conjunto de “dublês” de objetos e método que imitam o comportamento das APIs do SharePoint mais comuns. Os métodos emulados são implementações leves da API do SharePoint que não exigem o SharePoint para serem executadas. Ao usar o Microsoft Fakes para desviar chamadas à API do SharePoint para os dublês de método dos emuladores do SharePoint, você isola seus testes e confirma se está testando o código desejado. Quando você chama os métodos do SharePoint que não são emulados, pode usar o Fakes diretamente para criar o comportamento desejado.

###  <a name="BKMK_Adding_the_Emulators_package_to_a_test_project"></a> Adicionar o pacote de emuladores a um projeto de teste

Para adicionar os emuladores do SharePoint a um projeto de teste:

1.  Selecione o projeto de teste no **Gerenciador de Soluções**.

2.  Escolha **Gerenciar pacotes NuGet** no menu de atalho.

3.  Pesquise `Microsoft.SharePoint.Emulators` na categoria **Online** e escolha **Instalar**.

![Pacote NuGet de Emuladores do SharePoint](../test/media/ut_emulators_nuget.png)

###  <a name="BKMK__Running_a_test_method_in_the_emulation_context"></a> Executar um método de teste com emulação

A instalação do pacote adiciona referências às bibliotecas necessárias aos seus projetos. Para facilitar o uso de emuladores em uma classe de teste existente, adicione os namespaces `Microsoft.SharePoint.Emulators` e `Microsoft.QualityTools.Testing.Emulators`.

Para habilitar a emulação de seus métodos de teste, encapsule o corpo do método em uma instrução `using` que cria um objeto `SharePointEmulationScope`. Por exemplo:

```csharp
[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    // create the emulation scope with a using statement
    using (new SharePointEmulationScope())
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}
```

Quando o método de teste é executado, o tempo de execução do Emulador chama o Microsoft Fakes para injetar o código dinamicamente nos métodos do SharePoint para desviar as chamadas a esses métodos para representantes que são declarados em *Microsoft.SharePoint.Fakes.dll*. A *Microsoft.SharePoint.Emulators.dll* implementa os representantes para os métodos emulados, imitando atentamente o comportamento real do SharePoint. Quando o método de teste ou o componente em teste chama um método do SharePoint, o comportamento resultante é o da emulação.

![Fluxo de execução de emuladores](../test/media/ut_emulators_flowchart.png)

##  <a name="create-dual-use-classes-and-methods"></a>Criar métodos e classes de uso duplo

Para criar métodos que podem ser usados nos dois testes de integração com a API do SharePoint real e em testes de unidade isolados que usam emuladores, use o construtor sobrecarregado `SharePointEmulationScope(EmulationMode)` para encapsular o código do método de teste. Os dois valores da enumeração `EmulationMode` especificam se o escopo usa emuladores (`EmulationMode.Enabled`) ou se usa a API do SharePoint (`EmulationMode.Passthrough`).

Por exemplo, eis como você pode modificar o teste anterior para ser de uso duplo:

```csharp
// class level field specifies emulation mode
private const EmulationMode emulatorMode = EmulationMode.Enabled;

[TestMethod]
public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
{
    // emulation scope determined by emulatorMode
    using( SharePointEmulationScope(emulatorMode))
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        string errorMsg = string.Empty;
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);

        // Act
        bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
            "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
            out errorMsg);
        list.Delete();

        // Assert
        Assert.IsTrue(success);
    }
}
```

## <a name="use-testinitialize-and-testcleanup-attributes-to-create-a-dual-use-test-class"></a>Usar os atributos TestInitialize e TestCleanup para criar uma classe de teste de uso duplo

Se você executar todos ou a maioria dos testes em uma classe usando `SharePointEmulationScope`, poderá tirar proveito das técnicas de nível de classe para definir o modo de emulação.

-   Os métodos da classe de teste que são atribuídos com <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute> e <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute> podem criar e destruir o escopo.

-   A definição de `EmulationMode` no nível da classe pode lhe permitir automatizar a alteração do modo entre `EmulationMode.Enabled` e `EmulationMode.Passthrough`.

Um método de classe que é atribuído com `[TestInitialize]` é executado no início de cada método de teste, e um método que é atribuído com `[TestCleanup]` é executado no final de cada método de teste. Você pode declarar um campo particular para o objeto `SharePointEmulationScope` no nível da classe, inicializá-lo no método atribuído `TestInitialize` e descartar o objeto no método atribuído `TestCleanup`.

Você pode usar qualquer método escolhido para automatizar a seleção do `EmulationMode`. Uma maneira é verificar a existência de um símbolo usando as diretivas do pré-processador. Por exemplo, para executar os métodos de teste em uma classe usando emuladores, você pode definir um símbolo como `USE_EMULATION` no arquivo de projeto de teste ou na linha de comando de compilação. Se o símbolo está definido, uma constante `EmulationMode` no nível da classe é declarada e definida como `Enabled`. Caso contrário, a constante é definida como `Passthrough`.

Aqui está um exemplo da classe de teste que demonstra como usar diretivas de pré-processador e os métodos atribuídos `TestInitialize` e `TestCleanup` para definir o modo de emulação.

```csharp
//namespace declarations
...

namspace MySPAppTests
{
    [TestClass]
    public class BookAnAppointmentWebPartTests
    {

        // emulationScope is a class level field
        private SharePointEmulationScope emulationScope;

        // preprocessor directives determine the value of emulatorMode
        #if USE_EMULATIONprivate const EmulationMode emulatorMode = EmulationMode.Enabled;#elseprivate const EmulationMode emulatorMode = EmulationMode.Passthrough;#endif

        // InitializeTest sets the emulation scope at the beginning of each test method
        [TestInitialize]public void InitializeTest(){this.emulationScope = new SharePointEmulationScope(emulatorMode);}

        // CleanupTest disposes the emulation scope at the end of each test method
        [TestCleanup]public void CleanupTest(){this.emulationScope.Dispose();}

        [TestMethod]
        public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
        {
            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                string errorMsg = string.Empty;
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);

                // Act
                bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
                    "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
                    out errorMsg);
                list.Delete()

                // Assert
                Assert.IsTrue(success);
            }
        }

        ...// More tests

    }
}
```

##  <a name="handle-non-emulated-sharepoint-methods"></a>Manipular métodos não emulados do SharePoint

Nem todos os tipos do SharePoint são emulados e nem todos os métodos em alguns tipos emulados são emulados. Se o código em teste chama um método do SharePoint que não é emulado, o método gera uma exceção `NotSupportedException`. Quando ocorre uma exceção, você pode adicionar um shim do Fakes ao método do SharePoint.

**Configurando o Sharepoint Fakes**

Para chamar explicitamente os shims do Microsoft Fakes:

1.  Caso deseje usar shim em uma classe do SharePoint que não é emulada, edite o arquivo *Microsoft.SharePoint.fakes* e adicione a classe à lista de classes corrigidas. Confira a seção [Configurar a geração de código de stubs](code-generation-compilation-and-naming-conventions-in-microsoft-fakes.md#configure-code-generation-of-stubs) de [Convenções de nomenclatura, compilação e geração de código no Microsoft Fakes](../test/code-generation-compilation-and-naming-conventions-in-microsoft-fakes.md).

     ![Pastas falsas no Gerenciador de Soluções](../test/media/ut_emulators_fakesfilefolder.png)

2.  Recompile o projeto de teste pelo menos uma vez depois de instalar o pacote Emuladores do Microsoft SharePoint e se você editou o arquivo *Microsoft.SharePoint.Fakes*. A criação do projeto cria e preenche uma pasta **FakesAssembly** na pasta raiz do projeto em disco.

     ![Pasta FakesAssembly](../test/media/ut_emulators_fakesassemblyfolder.png)

3.  Adicione uma referência ao assembly **Microsoft.SharePoint.14.0.0.0.Fakes.dll** que está localizado na pasta **FakesAssembly**.

4.  (Opcional) Adicione uma diretiva de namespace à classe de teste para `Microsoft.QualityTools.Testing.Fakes`, `Microsoft.SharePoint.Fakes` e qualquer namespace aninhado de `Microsoft.SharePoint.Fakes`que você deseja usar.

**Implementando o representante de shim em um método do SharePoint**

Em nosso projeto de exemplo, o método `GetAppointmentsForToday` chama o método da API do SharePoint [SPList.GetItems(SPQuery)](xref:Microsoft.SharePoint.SPList.GetItems%2A).

```csharp
// method under test
public string GetAppointmentsForToday(string listName, SPWeb web)
{
    SPList list = web.Lists[listName];
    DateTime today = DateTime.Now;
    var listQuery = new SPQuery{Query = String.Format("<Where><Eq><FieldRef Name='Date'/>" +"<Value Type='Text'>{0}</Value>" +"</Eq></Where>", today.ToString("D"))};
    var result = new System.Text.StringBuilder();
    foreach (SPListItem item in list.GetItems(listQuery))
    {
        result.AppendFormat("Name: {0}, Phone: {1}, Email: {2}, Age: {3}, Date: {4}\n",
            item["Name"], item["Phone"], item["Email"], item["Age"], item["Date"]);
    }
    return result.ToString();
}
```

A versão `SPList.GetItems(SPQuery)` do método sobrecarregado `GetItems` não é emulada. Portanto, o simples encapsulamento de um teste existente para `GetAppointmentsForToday` na `SharePoint.Emulation.Scope` apresentaria falha. Para criar um teste de trabalho, é necessário escrever uma implementação do representante do Fakes `ShimSPList.GetItemsSPQuery` que retorna os resultados que você deseja testar.

Aqui está uma modificação de um método de teste existente, `GetAppointmentsForTodayReturnsOnlyTodaysAppointments`, que implementa um representante do Fakes. As alterações necessárias estão destacadas nos comentários:

> [!IMPORTANT]
> Os métodos de teste que criam explicitamente shims do Fakes geram uma exceção `ShimNotSupported` quando o teste é executado no contexto `EmulationMode.Passthrough`. Para evitar esse problema, use uma variável para definir o valor `EmulationMode` e encapsular um código do Fakes em uma instrução `if` que testa o valor.

```csharp
// class level field to set emulation mode
private const EmulationMode emulatorMode = EmulationMode.Enabled

[TestMethod]
public void GetAppointmentsForTodayReturnsOnlyTodaysAppointments()
{

    // create the emulation scope with a using statement
    using (var emulationScope = new SharePointEmulationScope(emulatorMode))
    using( var site = new SPSite("http://localhost"))
    using (var webPart = new BookAnAppointmentWebPart())
    {
        // Arrange
        DateTime date = DateTime.Now;
        SPList list = AddListToSiteHelper(site);
        // insert 2 items into list
        AddItemsToListHelper(list, new string[] {"Raisa Pokrovskaya", "425-555-0163",
            "raisa@outlook.com", "55", date.ToString("D") });
        AddItemsToListHelper(list, new string[] {"Francis Totten", "313-555-0100",
            "francis@contoso.com", "42", date.AddDays(1).ToString("D") });

        // use Fakes shims only if emulation is enabled
        if (emulatorMode == EmulationMode.Enabled){var sList = new ShimSPList(list);sList.GetItemsSPQuery = (query) =>{var shim = new ShimSPListItemCollection();shim.Bind(new[] { list.Items[0] });return shim.Instance;}}

        // Act
        string result = webPart.GetAppointmentsForToday(list.Title, site.RootWeb);
        list.Delete();

        // Assert
        Assert.IsTrue(result.Contains(String.Format(
            "Name: Raisa Pokrovskaya, Phone: 425-555-0163, Email: raisa@outlook.com," +
            "Age: 55, Date: {0}", date.ToString("D"))));
        Assert.IsFalse(result.Contains("Name: Francis Totten"));
    }
}
```

Nesse método, primeiro testamos se a emulação está habilitada. Se for o caso, poderemos criar um objeto de shim do Fakes para nossa lista `SPList`, criar e atribuir um método para seu representante `GetItemsSPQuery`. O representante usa o método `Bind` do Fakes para adicionar o item de lista correta à `ShimSPListItemCollection` que é retornada ao chamador.

##  <a name="write-emulation-tests-from-scratch-and-a-summary"></a>Escrever testes de emulação do zero e um resumo

Embora as técnicas para criar emulações e testes de uso duplo descritas nas seções anteriores pressuponham que você está convertendo testes existentes, também é possível usar as técnicas para escrever testes a partir do zero. A lista abaixo resume as técnicas:

-   Para usar emuladores em um projeto de teste, adicione o pacote NuGet Microsoft.SharePoint.Emulators ao projeto.

-   Para usar emuladores em um método de teste, crie um objeto `SharePointEmulationScope` no início do método. Todas as APIs do SharePoint com suporte serão emuladas até que o escopo seja descartado.

-   Escreva seu código de teste como se estivesse escrevendo para a API do SharePoint real. O contexto de emulação desvia automaticamente as chamadas a métodos do SharePoint para seus emuladores.

-   Nem todos os objetos do SharePoint são emulados e nem todos os métodos de alguns objetos emulados são emulados. Uma exceção `NotSupportedException` é gerada quando você usa um método ou objeto não emulado. Quando isso ocorre, crie explicitamente um representante de shim do Fakes para o método a fim de retomar o comportamento necessário.

-   Para criar testes de uso duplo, use o construtor `SharePointEmulationScope(EmulationMode)` para criar o objeto de escopo da emulação. O valor `EmulationMode` especifica se as chamadas do SharePoint são emuladas ou executadas em um site do SharePoint real.

-   Se todos ou a maioria de seus métodos de teste em uma classe de teste são executados no contexto de emulação, você pode usar um método atribuído `TestInitialize` no nível da classe para criar o objeto `SharePointEmulationScope` e um campo no nível da classe para definir o modo de emulação. Isso ajudará você a automatizar a mudança do modo de emulação. Em seguida, use um método atribuído `TestCleanup` para descartar o objeto de escopo.

##  <a name="BKMK_Example"></a> Exemplo

Aqui está um exemplo final que incorpora as técnicas de emulador do SharePoint descritas acima:

```csharp
using System;
//other namespace declarations
...
// code under test
using MySPApps;
using Microsoft.SharePoint;
// unit testing and emulators
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.QualityTools.Testing.Emulators;
using Microsoft.SharePoint.Emulators;
// explicit Fakes shims
using Microsoft.QualityTools.Testing.Fakes;
using Microsoft.SharePoint.Fakes

namspace MySPAppTests
{
    [TestClass]
    public class BookAnAppointmentWebPartTests
    {

        // emulationScope is a class level field
        private SharePointEmulationScope emulationScope;

        // preprocessor directives determine the value of emulatorMode
        #if USE_EMULATION
            private const EmulationMode emulatorMode = EmulationMode.Enabled;
        #else
            private const EmulationMode emulatorMode = EmulationMode.Passthrough;
        #endif

        // InitializeTest sets the emulation scope at the beginning of each test method
        [TestInitialize]
        public void InitializeTest()
        {
            this.emulationScope = new SharePointEmulationScope(emulatorMode);
        }

        // CleanupTest disposes the emulation scope at the end of each test method
        [TestCleanup]
        public void Cleanup()
        {
            this.emulationScope.Dispose();
        }

        [TestMethod]
        public void ScheduleAppointmentReturnsTrueWhenNewAppointmentIsCreated()
        {
            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                string errorMsg = string.Empty;
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);

                // Act
                bool success = webPart.ScheduleAppointment(site.RootWeb, list.Title,
                    "Raisa Pokrovskaya", "425-555-0163", "raisa@outlook.com", "55", date,
                    out errorMsg);
                list.Delete()

                // Assert
                Assert.IsTrue(success);
            }
        }

        [TestMethod]
        public void GetAppointmentsForTodayReturnsOnlyTodaysAppointments()
        {

            // remove the SharePointEmulationScope using statement from the method
            using( var site = new SPSite("http://localhost"))
            using (var webPart = new BookAnAppointmentWebPart())
            {
                // Arrange
                DateTime date = DateTime.Now;
                SPList list = AddListToSiteHelper(site);
                // insert 2 items into list
                AddItemsToListHelper(list, new string[] {"Raisa Pokrovskaya", "425-555-0163",
                    "raisa@outlook.com", "55", date.ToString("D") });
                AddItemsToListHelper(list, new string[] {"Francis Totten", "313-555-0100",
                    "francis@contoso.com", "42", date.AddDays(1).ToString("D") });

                // use Fakes shims only if emulation is enabled
                if (emulatorMode == EmulationMode.Enabled)
                {
                    var sList = new ShimSPList(list);

                    sList.GetItemsSPQuery = (query) =>
                    {
                        var shim = new ShimSPListItemCollection();
                        shim.Bind(new[] { list.Items[0] });
                        return shim.Instance;
                    }
                }

                // Act
                string result = webPart.GetAppointmentsForToday(list.Title, site.RootWeb);
                list.Delete();

                // Assert
                Assert.IsTrue(result.Contains(String.Format(
                    "Name: Raisa Pokrovskaya, Phone: 425-555-0163, Email: raisa@outlook.com," +
                    "Age: 55, Date: {0}", date.ToString("D"))));
                Assert.IsFalse(result.Contains("Name: Francis Totten"));
            }
        }

        ...// More tests

    }
}
```

##  <a name="BKMK_Emulated_SharePoint_types"></a> Tipos de SharePoint emulados

 <xref:Microsoft.SharePoint.SPField?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFieldIndex?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFieldIndexCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFieldLink?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFieldLinkCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFieldUrlValue?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFile?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFileCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFolder?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPFolderCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPItem?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPItemEventDataCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPItemEventProperties?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPList?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPListCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPListEventProperties?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPListItem?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPListItemCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPQuery?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPRoleAssignment?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPRoleAssignmentCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPSecurableObject?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPSecurity?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPSite?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPUser?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPUserCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPView?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPViewCollection?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPViewContext?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPWeb?displayProperty=nameWithType>

 <xref:Microsoft.SharePoint.SPWebCollection?displayProperty=nameWithType>

## <a name="see-also"></a>Consulte também

- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)
- [Testar aplicativos do SharePoint 2010 com testes de IU codificados](../test/testing-sharepoint-2010-applications-with-coded-ui-tests.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)

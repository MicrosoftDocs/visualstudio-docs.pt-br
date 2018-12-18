---
title: Usando membros do Microsoft.VisualStudio.TestTools.UnitTesting em testes de unidade
ms.date: 03/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: reference
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: bad6f01a49856e44120c0dc121ee262d9d26506c
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295599"
---
# <a name="use-the-mstest-framework-in-unit-tests"></a>Usar a estrutura de MSTest em testes de unidades

O framework [MSTest](<xref:Microsoft.VisualStudio.TestTools.UnitTesting>) oferece suporte a teste de unidade no Visual Studio. Use as classes e os membros do namespace <xref:Microsoft.VisualStudio.TestTools.UnitTesting> quando você estiver codificando testes de unidade. Você também pode usá-los quando estiver refinando um teste de unidade que foi gerado a partir do código.

## <a name="framework-members"></a>Membros da estrutura

Para ajudar a fornecer uma visão geral mais clara da estrutura de teste de Unidade, esta seção organiza os membros do namespace <xref:Microsoft.VisualStudio.TestTools.UnitTesting> em grupos de funcionalidades relacionadas.

> [!NOTE]
> Os elementos de atributo, cujos nomes terminam com "Attribute", podem ser usados com ou sem "Attribute" no fim. Por exemplo, os dois exemplos de código a seguir funcionam de forma idêntica:
>
> `[TestClass()]`
>
> `[TestClassAttribute()]`

### <a name="members-used-for-data-driven-testing"></a>Membros usados para teste controlado por dados

Use os seguintes elementos para configurar testes de unidade controlados por dados. Para obter mais informações, confira [Criar um teste de unidade controlado por dados](../test/how-to-create-a-data-driven-unit-test.md) e [Usar um arquivo de configuração para definir uma fonte de dados](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md).

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataAccessMethod>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElement>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElementCollection>

## <a name="attributes-used-to-establish-a-calling-order"></a>Atributos usados para estabelecer uma ordem de chamada

Um elemento de código decorado com um dos seguintes atributos é chamado no momento em especificado por você. Para obter mais informações, confira [Anatomia de um teste de unidade](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144).

### <a name="attributes-for-assemblies"></a>Atributos para assemblies

AssemblyInitialize e AssemblyCleanup são chamados logo após o assembly ser carregado e logo antes de seu assembly ser descarregado.

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyCleanupAttribute>

### <a name="attributes-for-classes"></a>Atributos para classes

ClassInitialize e ClassCleanup são chamadas logo após a classe ser carregada e logo antes de sua classe ser descarregada.

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassCleanupAttribute>

### <a name="attributes-for-test-methods"></a>Atributos para métodos de teste

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>

## <a name="attributes-used-to-identify-test-classes-and-methods"></a>Atributos usados para identificar classes de teste e métodos

Cada classe de teste deve ter o atributo `TestClass` e cada método de teste deve ter o atributo `TestMethod`. Para obter mais informações, confira [Anatomia de um teste de unidade](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144).

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>

## <a name="assert-classes-and-related-exceptions"></a>Classes Assert e exceções relacionadas

Testes de unidade podem verificar comportamentos específicos do aplicativo pelo uso de vários tipos de asserções, exceções e atributos. Para obter mais informações, confira [Usando as classes Assert](../test/using-the-assert-classes.md).

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute>

## <a name="the-testcontext-class"></a>A classe TestContext

Os seguintes atributos e os valores atribuídos a eles aparecem na janela Propriedades do Visual Studio de um método de teste específico. Esses atributos não devem ser acessados por meio do código do teste de unidade. Em vez disso, eles afetam as maneiras pelas quais o teste de unidade é utilizado ou executado, seja por meio do IDE do Visual Studio ou pelo mecanismo de testes do Visual Studio. Por exemplo, alguns desses atributos aparecem como colunas nas janelas **Gerenciador de Testes** e **Resultados do Teste**, o que significa que é possível usá-las para agrupar e classificar testes e resultados de teste. Um desses atributos é <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>, que pode ser usado para adicionar metadados arbitrários a testes de unidade. Por exemplo, é possível usá-lo para armazenar o nome de uma passagem de teste coberta pelo teste em questão, por meio da marcação do teste de unidade com `[TestProperty("TestPass", "Accessibility")]`. Como alternativa, você pode usá-lo para armazenar um indicador de que o tipo de teste é com o `[TestProperty("TestKind", "Localization")]`. A propriedade criada por você com esse atributo e o valor da propriedade atribuído são exibidos na janela **Propriedades** do Visual Studio sob o título **Especificidades do teste**.

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DescriptionAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.WorkItemAttribute>

## <a name="test-configuration-classes"></a>Classes de configuração de teste

- <xref:Microsoft.TeamFoundation.TestManagement.Client.ObjectTypes>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection>

## <a name="attributes-used-to-generate-reports"></a>Atributos usados para gerar relatórios

Os atributos desta seção relacionam o método de teste decorados por eles a entidades na hierarquia do projeto de um projeto de equipe do Team Foundation Server.

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssIterationAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssProjectStructureAttribute>

## <a name="classes-used-with-private-accessors"></a>Classes usadas com acessadores particulares

Você pode gerar um teste de unidade para um método privado. Essa geração cria uma classe de acessador particular, que instancia um objeto da classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>. A classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject> é uma classe wrapper que usa reflexão como parte do processo do acessador particular. A classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType> é semelhante, mas é usada para chamar métodos estáticos privados em vez de chamar os métodos de instância privada.

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType>

## <a name="see-also"></a>Consulte também

- Documentação de referência do <xref:Microsoft.VisualStudio.TestTools.UnitTesting>

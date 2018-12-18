---
title: Usando membros do Microsoft.VisualStudio.TestTools.UnitTesting em testes de unidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fa335fd-e442-448f-913f-25a19df90a93
caps.latest.revision: 8
ms.author: gewarren
manager: douge
ms.openlocfilehash: 691b1e46f7657eb027fa48b31f31119cae0c7451
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49216639"
---
# <a name="using-microsoftvisualstudiotesttoolsunittesting-members-in-unit-tests"></a>Usando membros do Microsoft.VisualStudio.TestTools.UnitTesting em testes de unidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
A Estrutura de Teste de Unidade dá suporte a testes de unidade no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Use as classes e os membros do namespace <xref:Microsoft.VisualStudio.TestTools.UnitTesting> quando você estiver codificando testes de unidade. É possível usá-los ao gravar o teste de unidade do zero ou refinar um teste de unidade gerado do código em teste.

## <a name="groups-of-elements"></a>Grupos de Elementos
 Para ajudar a fornecer uma visão geral mais clara da Estrutura de Teste de Unidade, esta seção organiza os elementos do namespace UnitTesting em grupos de funcionalidades relacionadas.

> [!NOTE]
> Os elementos de atributo, cujos nomes terminam com a cadeia de caracteres Attribute, podem ser usados com ou sem a cadeia de caracteres Attribute. Por exemplo, os dois exemplos de código a seguir funcionam de forma idêntica:
>
>  `[TestClass()]`
>
>  `[TestClassAttribute()]`

### <a name="elements-used-for-data-driven-testing"></a>Elementos Usados Para Teste Controlado por Dados
 Use os seguintes elementos para configurar testes de unidade controlados por dados. Para obter mais informações, consulte [Como Criar um Teste de Unidade Controlado por Dados](../test/how-to-create-a-data-driven-unit-test.md) e [Passo a Passo: Usando um Arquivo de Configuração para Definir uma Fonte de Dados](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md).

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataAccessMethod>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElement>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElementCollection>

## <a name="attributes-used-to-establish-a-calling-order"></a>Atributos Usados para Estabelecer uma Ordem de Chamada
 Um elemento de código decorado com um dos seguintes atributos é chamado no momento em especificado por você. Para obter mais informações, consulte [Anatomia de um Teste de Unidade](http://msdn.microsoft.com/en-us/a03d1ee7-9999-4e7c-85df-7d9073976144).

### <a name="for-assemblies"></a>Para Assemblies
 AssemblyInitialize e AssemblyCleanup são chamados logo após o assembly ser carregado e logo antes de seu assembly ser descarregado.

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyInitializeAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyCleanupAttribute>

### <a name="for-classes"></a>Para Classes
 ClassInitialize e ClassCleanup são chamadas logo após a classe ser carregada e logo antes de sua classe ser descarregada.

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassInitializeAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassCleanupAttribute>

### <a name="for-test-methods"></a>Para Métodos de Teste

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>

## <a name="attributes-used-to-identify-test-classes-and-methods"></a>Atributos Usados para Identificar Classes de Teste e Métodos
 Cada classe de teste deve ter o atributo TestClass e cada método de teste deve ter o atributo TestMethod. Para obter mais informações, consulte [Anatomia de um Teste de Unidade](http://msdn.microsoft.com/en-us/a03d1ee7-9999-4e7c-85df-7d9073976144).

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>

## <a name="assert-classes-and-related-exceptions"></a>Classes Assert e Exceções Relacionadas
 Testes de unidade podem verificar comportamentos específicos do aplicativo pelo uso de vários tipos de instruções Assert, exceções e atributos. Para obter mais informações, consulte [Usando as Classes Assert](../test/using-the-assert-classes.md).

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute>

## <a name="the-testcontext-class"></a>A Classe TestContext
 Os seguintes atributos e os valores atribuídos a eles aparecem na janela Propriedades [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] de um método de teste específico. Esses atributos não devem ser acessados por meio do código do teste de unidade. Em vez disso, eles afetam as maneiras pelas quais o teste de unidade é utilizado ou executado, seja por meio do IDE de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou pelo mecanismo de testes [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Por exemplo, alguns desses atributos aparecem como colunas nas janelas Gerenciador de Testes e Resultados do Teste, o que significa que é possível usá-las para agrupar e classificar testes e resultados de teste. Um desses atributos é TestPropertyAttribute, que pode ser usado para adicionar metadados arbitrários a testes de unidade. Por exemplo, é possível usá-lo para armazenar o nome de uma passagem de teste coberta pelo teste em questão, por meio da marcação do teste de unidade com `[TestProperty("TestPass", "Accessibility")]`. Como alternativa, você pode usá-lo para armazenar um indicador de que o tipo de teste é: `[TestProperty("TestKind", "Localization")]`. A propriedade criada por você com esse atributo e o valor da propriedade atribuído são exibidos na janela Propriedades [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] sob o título **Especificidades do teste**.

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DescriptionAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.WorkItemAttribute>

## <a name="test-configuration-classes"></a>Classes de Configuração de Teste

-   <xref:Microsoft.TeamFoundation.TestManagement.Client.ObjectTypes>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection>

## <a name="attributes-used-for-generating-reports"></a>Atributos Usados para a Geração de Relatórios
 Os atributos desta seção relacionam o método de teste decorados por eles a entidades na hierarquia do projeto de um projeto de equipe [!INCLUDE[esprtfs](../includes/esprtfs-md.md)].

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssIterationAttribute>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssProjectStructureAttribute>

## <a name="classes-used-with-private-accessors"></a>Classes Usadas com Acessadores Particulares
 Conforme descrito em [Usar o Publicize para Criar um Acessador Particular](http://msdn.microsoft.com/en-us/2056c6a7-6672-42a7-8f53-fead33c56deb), é possível gerar um teste de unidade para um método particular. Essa geração cria uma classe de acessador particular, que instancia um objeto da classe PrivateObject. A classe PrivateObject é uma classe wrapper que usa reflexão como parte do processo do acessador particular. A classe PrivateType é semelhante, mas é usada para chamar métodos estáticos privados em vez de chamar os métodos de instância privada.

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>

-   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType>

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>
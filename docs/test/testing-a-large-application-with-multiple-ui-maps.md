---
title: Testar um aplicativo grande com vários mapas de interface do usuário
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- coded UI tests, multiple UI maps
- coded UI tests, for large applications
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99e703d10d2bc6ed8fd573f4973e73f7ad40a937
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286577"
---
# <a name="test-a-large-application-with-multiple-ui-maps"></a>Testar um aplicativo grande com vários Mapas de Interface do Usuário

Este tópico aborda o uso de testes de IU codificados durante o teste de um aplicativo grande usando vários Mapas de Interface do Usuário.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**Requisitos**

- Visual Studio Enterprise

Ao criar um novo teste de interface do usuário codificado, a estrutura de testes do Visual Studio gera um código para o teste em uma classe [UIMap](/previous-versions/dd580454(v=vs.140)) por padrão. Para obter mais informações sobre como gravar testes de IU codificados, confira [Criar testes de UI codificados](../test/use-ui-automation-to-test-your-code.md) e [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md).

O código gerado para o mapa de interface do usuário contém uma classe para cada objeto com o qual há interação. Para cada método gerado, é gerada uma classe complementar aos parâmetros de método especificamente para o método em questão. Se houver uma grande quantidade de objetos, páginas, formulários e controles em seu aplicativo, o mapa de interface do usuário pode ficar muito grande. Além disso, se houver diversas pessoas trabalhando nos testes, o aplicativo fica pesado com um único arquivo grande de mapa de interface do usuário.

Usando diversos arquivos desse tipo, você pode proporcionar estes benefícios:

- Cada mapa pode ser associado a um subconjunto lógico do aplicativo. Isso facilita o gerenciamento das alterações.

- Cada testador pode trabalhar em uma seção do aplicativo e fazer check-in do código sem interferir no trabalho de outros testadores em outras seções do aplicativo.

- É possível dimensionar as adições feitas na interface do usuário do aplicativo a incrementos, com efeito mínimo sobre os testes em outras seções da interface.

## <a name="do-you-need-multiple-ui-maps"></a>Você precisa de diversos mapas de interface do usuário?
Crie diversos mapas em cada uma destas situações:

- Diversos conjuntos complexos de controles de interface do usuário compostos que, juntos, executam uma operação lógica, como uma página de registro de um site ou a página de compras de um carrinho de compras.

- Um conjunto independente de controles que é acessado por diversos pontos do aplicativo, como um assistente com várias páginas de operações. Se cada página de um assistente for muito complexa, você pode criar mapas de interface do usuário para cada página.

## <a name="add-multiple-ui-maps"></a>Adicionar vários Mapas de Interface do Usuário

### <a name="to-add-a-ui-map-to-your-coded-ui-test-project"></a>Para adicionar um mapa de interface do usuário ao seu projeto de teste de IU codificado

1. No **Gerenciador de soluções**, para criar uma pasta em seu projeto de teste de interface do usuário codificado para armazenar todos os mapas da interface do usuário, clique com o botão direito do mouse no arquivo de projeto de teste de interface do usuário codificado, aponte para **Adicionar**e escolha **nova pasta**. Por exemplo, você pode atribuir o nome `UIMaps`.

    A nova pasta é exibida no projeto de teste de IU codificado.

2. Clique com o botão direito do mouse na pasta `UIMaps`, aponte para **Adicionar** e clique em **Novo Item**.

    A caixa de diálogo **Adicionar novo item** é exibida.

   > [!NOTE]
   > Você deve estar em um projeto de teste de IU codificado para adicionar um novo mapa de testes de IU codificado.

3. Selecione **Mapa de Teste de IU Codificado** na lista.

    Na caixa **Nome**, insira o nome de um novo mapa de interface do usuário. Use o nome do componente ou da página que o mapa representará, por exemplo, `HomePageMap`.

4. Escolha **Adicionar**.

    A janela do Visual Studio é minimizada e a caixa de diálogo **Construtor de Teste de IU Codificado** é exibida.

5. Registre as ações para o primeiro método e escolha **Gerar Código**.

6. Depois de registrar todas as ações e asserções do primeiro componente ou da página e agrupá-las em métodos, feche a caixa de diálogo **Construtor de Teste de IU Codificado**.

7. Continue a criar mapas de interface do usuário. Registre as ações e asserções, agrupe-as em métodos para cada componente e gere o código.

   Em muitos casos, a janela principal do aplicativo permanece uma constante para assistentes, formulários e páginas. Embora cada Mapa de Interface do Usuário tenha uma classe para a janela principal, provavelmente, todos os mapas referenciam a mesma janela principal na qual todos os componentes do aplicativo são executados. Os testes de IU codificados pesquisam controles hierarquicamente, de cima para baixo, começando na janela principal. Assim, em aplicativos complexos, é possível duplicar a janela principal em todos os Mapas de Interface do Usuário. Se a janela principal real for duplicada, essa janela sofrerá alterações com várias modificações. Isso pode resultar em problemas de desempenho quando você alterna entre os mapas de interface do usuário.

   Para minimizar esse efeito, use o método `CopyFrom()` para garantir que a nova janela principal do Mapa de Interface do Usuário seja a mesma janela principal.

## <a name="example"></a>Exemplo

O exemplo a seguir faz parte de uma classe de utilitários que fornece acesso a cada componente e seus controles filho, que são representados pelas classes geradas nos vários Mapas de Interface do Usuário.

Nesse exemplo, o aplicativo Web `Contoso` tem uma Home page, uma Página de produtos e uma Página de carrinho de compras. Cada uma dessas páginas usa a mesma janela principal, que é a janela do navegador. Há um mapa de interface do usuário para cada página e o código da classe do utilitário é parecido com este:

```csharp
using ContosoProject.UIMaps;
using ContosoProject.UIMaps.HomePageClasses;
using ContosoProject.UIMaps.ProductPageClasses;
using ContosoProject.UIMaps.ShoppingCartClasses;

namespace ContosoProject
{
    public class TestRunUtility
    {
        // Private fields for the properties
        private HomePage homePage = null;
        private ProductPage productPage = null;
        private ShoppingCart shoppingCart = null;

        public TestRunUtility()
        {
            homePage = new HomePage();
        }

        // Properties that get each UI Map
        public HomePage HomePage
        {
            get { return homePage; }
            set { homePage = value; }
        }

        // Gets the ProductPage from the ProductPageMap.
        public ProductPage ProductPageObject
        {
            get
            {
                if (productPage == null)
                {
                    // Instantiate a new page from the UI Map classes
                    productPage = new ProductPage();

                    // Since the Product Page and Home Page both use
                    // the same browser page as the top level window,
                    // get the top level window properties from the
                    // Home Page.
                    productPage.UIContosoFinalizeWindow.CopyFrom(
                        HomePage.UIContosoWindowsIWindow);
                }
                return productPage;
            }
        }

    // Continue to create properties for each page, getting the
    // page object from the corresponding UI Map and copying the
    // top level window properties from the Home Page.
}
```

## <a name="see-also"></a>Veja também

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UITesting.BrowserWindow.CopyFrom%2A>
- [Usar a automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)
- [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md)
- [Anatomia de um teste de interface do usuário codificado](../test/anatomy-of-a-coded-ui-test.md)

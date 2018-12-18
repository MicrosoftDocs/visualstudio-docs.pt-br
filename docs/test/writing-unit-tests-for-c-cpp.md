---
title: Gravar testes de unidade para C/C++ no Visual Studio
ms.date: 10/09/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: e79b65628193c7b90a03b2e1141dfc45b6b0829f
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48879195"
---
# <a name="write-unit-tests-for-cc-in-visual-studio"></a>Gravar testes de unidade para C/C++ no Visual Studio

É possível gravar e executar testes de unidade para C++ usando a janela **Gerenciador de Testes**, assim como em outras linguagens. Para saber mais sobre como usar o **Gerenciador de Testes**, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

> [!NOTE]
> Não há suporte para alguns recursos no C++, como o Live Unit Testing, Testes de Interface do Usuário Codificados e IntelliTest.

O Visual Studio inclui estas estruturas de teste para C++, sem a necessidade de fazer outros downloads:

- Microsoft Unit Testing Framework para C/C++
- Google Test
- Boost.Test
- CTest

Além das estruturas instaladas, é possível gravar seu próprio adaptador de teste em qualquer estrutura que você deseja usar no Visual Studio. Um adaptador de teste pode integrar testes de unidade à janela **Gerenciador de Testes**. Vários adaptadores de terceiros são disponibilizados no [Visual Studio Marketplace](https://marketplace.visualstudio.com). Para saber mais, consulte [Instalar estruturas de teste de unidade de terceiros](install-third-party-unit-test-frameworks.md).

**Visual Studio 2017 versão 15.7 (Professional e Enterprise)**

Os projetos de teste de unidade C++ são compatíveis com o [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md).

**Visual Studio 2017 versão 15.5**

- O **Adaptador do Google Test** está incluído como componente padrão da carga de trabalho **Desenvolvimento para área de trabalho com C++**. Ele tem um modelo de projeto que pode ser adicionado a uma solução por meio do menu de contexto **Adicionar Novo Projeto** no nó da solução, no **Gerenciador de Soluções**, além de opções que podem ser configuradas por meio de **Ferramentas** > **Opções**. Para saber mais, consulte [How to: use Google Test in Visual Studio](how-to-use-google-test-for-cpp.md) (Como usar o Google Test no Visual Studio).

- **Boost.Test** está incluído como componente padrão da carga de trabalho **Desenvolvimento para área de trabalho com C++**. Ele é integrado ao **Gerenciador de Testes**, mas, atualmente, não tem um modelo de projeto, portanto, deve ser configurado manualmente. Para saber mais, consulte [How to: use Boost.Test in Visual Studio](how-to-use-boost-test-for-cpp.md) (Como usar o Boost.Test no Visual Studio).

- O suporte para **CTest** está incluído no componente [Ferramentas CMake para Visual Studio](/cpp/ide/cmake-tools-for-visual-cpp), que faz parte da carga de trabalho **Desenvolvimento para área de trabalho com C++**. No entanto, o CTest ainda não está totalmente integrado ao **Gerenciador de Testes**. Para saber mais, consulte [How to: use CTest in Visual Studio](how-to-use-ctest-for-cpp.md) (Como usar o CTest no Visual Studio).

**Visual Studio 2015 e versões anteriores**

Baixe as extensões dos adaptadores Google Test e Boost.Test no Visual Studio Marketplace em [Adaptador de teste para Boost.Test](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforBoostTest) e [Adaptador de Teste para Google Test](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforGoogleTest).

## <a name="basic-test-workflow"></a>Fluxo de trabalho básico de teste

As seções a seguir mostram as etapas básicas para começar os testes de unidade para C++. A configuração básica é muito semelhante para as estruturas da Microsoft e do Google Test. O Boost.Test requer a criação manual de um projeto de teste.

### <a name="create-a-test-project"></a>Criar um projeto de teste

Defina e execute testes dentro de um ou mais projetos de teste que estão na mesma solução do código que você deseja testar. Para adicionar um novo projeto de teste a uma solução existente, clique com o botão direito do mouse no nó Solução, no **Gerenciador de Soluções**, e escolha **Adicionar** > **Novo Projeto**. Em seguida, no painel à esquerda, clique em **Teste, no nó Visual C++** e escolha um dos tipos de projeto no painel central. A ilustração a seguir mostra os projetos de teste disponibilizados quando a carga de trabalho **Desenvolvimento de Área de Trabalho com C++** é instalada:

![Projetos de teste C++](media/cpp-new-test-project.png)

### <a name="create-references-to-other-projects-in-the-solution"></a>Criar referências a outros projetos na solução

Para habilitar o código de teste a acessar as funções no projeto a ser testado, adicione uma referência ao projeto no projeto de teste. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó de projeto de teste e escolha **Adicionar** > **Referência**. Em seguida, na caixa de diálogo, escolha os projetos que deseja testar.

![Adicionar referência](media/cpp-add-ref-test-project.png)

### <a name="add-include-directives-for-header-files"></a>Adicionar diretivas de inclusão aos arquivos de cabeçalho

Em seguida, no arquivo *.cpp* do teste de unidade, adicione uma diretiva `#include` a todos os arquivos de cabeçalho que declaram os tipos e as funções que você deseja testar. Digite `#include "` e, depois, o IntelliSense será ativado para ajudá-lo a escolher. Repita essas etapas nos outros cabeçalhos.

![Adicionar diretivas de inclusão](media/cpp-add-includes-test-project.png)

### <a name="write-test-methods"></a>Gravar métodos de teste

> [!NOTE]
> Esta seção mostra a sintaxe da Microsoft Unit Testing Framework para C/C++. Ela está documentada na [Referência de API do Microsoft.VisualStudio.TestTools.CppUnitTestFramework](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md). Para obter a documentação do Google Test, confira [Prévia do Google Test](https://github.com/google/googletest/blob/master/googletest/docs/primer.md). Quanto ao Boost.Test, confira [Biblioteca do Boost Test: a estrutura de teste de unidade](http://www.boost.org/doc/libs/1_46_0/libs/test/doc/html/utf.html).

O arquivo *.cpp* no projeto de teste tem um método e uma classe stub definidos para você como um exemplo de como gravar um código de teste. Observe que as assinaturas usam as macros TEST_CLASS e TEST_METHOD, o que possibilita a descoberta dos métodos por meio da janela **Gerenciador de Testes**.

![Adicionar diretivas de inclusão](media/cpp-write-test-methods.png)

TEST_CLASS e TEST_METHOD fazem parte do [Framework de Teste Nativo da Microsoft](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md). O **Gerenciador de Testes** descobre os métodos de teste em outras estruturas com suporte, de maneira semelhante.

Um TEST_METHOD retorna nulo. Para produzir um resultado do teste, use os métodos estáticos na classe `Assert` para testar os resultados reais em relação a o que é esperado. No exemplo a seguir, considere que `MyClass` tem um construtor que usa uma `std::string`. É possível testar se o construtor inicializa a classe conforme o esperado da seguinte forma:

```cpp
TEST_METHOD(TestClassInit)
{
    std::string name = "Bill";
    MyClass mc(name);
    Assert::AreEqual(name, mc.GetName());
}
```

No exemplo anterior, o resultado da chamada `Assert::AreEqual` determina o resultado do teste: aprovação ou falha. A classe Assert contém vários outros métodos para comparar os resultados esperados aos resultados reais.

É possível adicionar *características* aos métodos de teste a fim de especificar os proprietários do teste, a prioridade e outras informações. Depois, é possível usar esses valores para classificar e agrupar os testes no **Gerenciador de Testes**. Para obter mais informações, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

### <a name="run-the-tests"></a>Executar os testes

1. No menu **Teste**, escolha **Windows** > **Gerenciador de Testes**. A ilustração a seguir mostra um projeto de teste cujos testes ainda não foram executados.

   ![Gerenciador de Testes antes da execução dos testes](media/cpp-test-explorer.png)

   > [!NOTE]
   > A integração do CTest com o **Gerenciador de Testes** ainda não está disponível. Execute testes de CTest no menu principal do CMake.

1. Caso todos os testes não estejam visíveis na janela, crie o projeto de teste clicando com o botão direito no mouse no nó do **Gerenciador de Soluções** e escolhendo **Criar** ou **Recompilar**.

1. No **Gerenciador de Testes**, escolha **Executar Todos** ou selecione os testes específicos que deseja executar. Clique com o botão direito do mouse para ver outras opções, incluindo a execução em modo de depuração com pontos de interrupção habilitados. Depois de executar todos os testes, a janela mostrará quais testes foram aprovados e quais falharam:

![Gerenciador de Testes depois da execução dos testes](media/cpp-test-explorer-passed.png)

Para testes com falha, a mensagem mostra detalhes que ajudam a diagnosticar a causa. É possível clicar com o botão direito do mouse no teste com falha e selecione **Depurar Testes Selecionados** para ver a etapa da função em que a falha ocorreu.

Para saber mais sobre como usar o **Gerenciador de Testes**, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

Para conhecer as melhores práticas relacionadas ao teste de unidade, confira [Noções básicas sobre o teste de unidade](unit-test-basics.md)

## <a name="use-codelens"></a>Usar o CodeLens

**Apenas Visual Studio 2017 versão 15.7 Professional e Enterprise Editions**: o [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) permite que você veja rapidamente o status de uma unidade de teste sem sair do editor de código. Você pode inicializar o CodeLens para um projeto de teste de unidade do C++ em qualquer uma das seguintes formas:

- Editar e compilar sua solução ou projeto de teste.
- Recompilar sua solução ou projeto.
- Executar o(s) teste(s) na janela do **Gerenciador de Testes**.

Após o **CodeLens** ser inicializado, os ícones de status de teste podem ser vistos acima de cada teste de unidade.

![Ícones do CodeLens C++](media/cpp-test-codelens-icons.png)

 Clique no ícone para obter mais informações ou para executar ou depurar o teste de unidade:

![Execução e depuração do CodeLens C++](media/cpp-test-codelens-run-debug.png)

## <a name="see-also"></a>Consulte também

[Efetuar teste de unidade em seu código](unit-test-your-code.md)

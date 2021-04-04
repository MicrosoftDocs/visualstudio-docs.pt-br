---
title: Escrever testes de unidade para C/C++
description: Escreva testes de unidade em C++ no Visual Studio usando várias estruturas de teste, incluindo CTest, Boost. Test e Google Test.
ms.date: 04/01/2021
ms.topic: conceptual
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: d20bcdef769d8cd751230000b0e4d4319b10e46f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217457"
---
# <a name="write-unit-tests-for-cc-in-visual-studio"></a>Gravar testes de unidade para C/C++ no Visual Studio

Você pode escrever e executar os testes de unidade do C++ usando a janela **Test Explorer** . Ele funciona exatamente como faz para outros idiomas. Para saber mais sobre como usar o **Gerenciador de Testes**, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

> [!NOTE]
> Não há suporte para alguns recursos no C++, como o Live Unit Testing, Testes de Interface do Usuário Codificados e IntelliTest.

O Visual Studio inclui estas estruturas de teste para C++, sem a necessidade de fazer outros downloads:

- Microsoft Unit Testing Framework para C/C++
- Google Test
- Boost.Test
- CTest

Juntamente com o uso das estruturas instaladas, você pode escrever seu próprio adaptador de teste para qualquer estrutura que queira usar no Visual Studio. Um adaptador de teste pode integrar testes de unidade à janela **Gerenciador de Testes**. Vários adaptadores de terceiros são disponibilizados no [Visual Studio Marketplace](https://marketplace.visualstudio.com). Para obter mais informações, consulte [instalar estruturas de teste de unidade de](install-third-party-unit-test-frameworks.md)terceiros.

**Visual Studio 2017 e posterior (Professional e Enterprise)**

Os projetos de teste de unidade C++ são compatíveis com o [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md).

**Visual Studio 2017 e posterior (todas as edições)**

- **Google Test adaptador** está incluído como um componente padrão do **desenvolvimento de desktop com** carga de trabalho do C++. Ele tem um modelo de projeto que você pode adicionar a uma solução. Use o menu **Adicionar novo projeto** clique com o botão direito do mouse no nó da solução em **Gerenciador de soluções** para adicioná-lo. Ele também tem opções que você pode configurar por meio das opções de **ferramentas**  >  . Para obter mais informações, consulte [como: usar Google Test no Visual Studio](how-to-use-google-test-for-cpp.md).

- O **Boost. Test** é incluído como um componente padrão do **desenvolvimento de desktop com** carga de trabalho do C++. Ele está integrado ao **Gerenciador de testes**, mas atualmente não tem um modelo de projeto. Ele deve ser configurado manualmente. Para obter mais informações, consulte [como: usar Boost. Test no Visual Studio](how-to-use-boost-test-for-cpp.md).

- O suporte para **CTest** está incluído no componente **Ferramentas CMake para C++**, que faz parte da carga de trabalho **Desenvolvimento para desktop com C++**. Para obter mais informações, consulte [como: usar o CTest no Visual Studio](how-to-use-ctest-for-cpp.md).

**Visual Studio 2015 e versões anteriores**

Você pode baixar o adaptador de Google Test e aumentar as extensões do adaptador de teste no Visual Studio Marketplace. Encontre-os no [adaptador de teste para o Boost. teste](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforBoostTest) e [adaptador de teste para Google Test](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforGoogleTest).

## <a name="basic-test-workflow"></a>Fluxo de trabalho básico de teste

As seções a seguir mostram as etapas básicas para começar os testes de unidade para C++. A configuração básica é semelhante para as estruturas da Microsoft e do Google Test. O Boost.Test requer a criação manual de um projeto de teste.

::: moniker range="vs-2019"

### <a name="create-a-test-project-in-visual-studio-2019"></a>Crie um projeto de teste no Visual Studio 2019

Você define e executa testes dentro de um ou mais projetos de teste. Você cria os projetos na mesma solução que o código que deseja testar. Para adicionar um novo projeto de teste a uma solução existente, clique com o botão direito do mouse no nó da solução em **Gerenciador de soluções**. No menu pop-up, escolha **Adicionar**  >  **novo projeto**. Defina **Linguagem de programação** como C++ e digite "teste" na caixa de pesquisa. A ilustração a seguir mostra os projetos de teste que estão disponíveis quando o **Desenvolvimento de área de trabalho com C++** e a carga de trabalho **Desenvolvimento de UWP** estão instalados:

![Projetos de teste C++ no Visual Studio 2019](media/vs-2019/cpp-new-test-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

### <a name="create-a-test-project-in-visual-studio-2017"></a>Crie um projeto de teste no Visual Studio 2017

Você define e executa testes dentro de um ou mais projetos de teste. Você cria os projetos na mesma solução que o código que deseja testar. Para adicionar um novo projeto de teste, clique com o botão direito do mouse no nó da solução em **Gerenciador de soluções** e escolha **Adicionar**  >  **novo projeto**. No painel esquerdo, escolha **Visual C++ teste**. Em seguida, escolha um dos tipos de projeto no painel central. A ilustração a seguir mostra os projetos de teste disponibilizados quando a carga de trabalho **Desenvolvimento de Área de Trabalho com C++** é instalada:

![Projetos de teste C++](media/cpp-new-test-project.png)

::: moniker-end

### <a name="create-references-to-other-projects-in-the-solution"></a>Criar referências a outros projetos na solução

Para habilitar o acesso às funções no projeto em teste, adicione uma referência ao projeto em seu projeto de teste. Clique com o botão direito do mouse no nó Test Project no **Gerenciador de soluções** para um menu pop-up. Escolha **Adicionar**  >  **referência**. Na caixa de diálogo Adicionar referência, escolha os projetos que você deseja testar.

![Adicionar referência](media/cpp-add-ref-test-project.png)

### <a name="link-to-object-or-library-files"></a>Vincular a arquivos de biblioteca ou objeto

Se o código de teste não exportar as funções que você deseja testar, será possível adicionar os arquivos .obj ou .lib de saída para as dependências do projeto de teste. Para obter mais informações, consulte [para vincular os testes aos arquivos de objeto ou de biblioteca](how-to-use-microsoft-test-framework-for-cpp.md#object_files).

### <a name="add-include-directives-for-header-files"></a>Adicionar diretivas de inclusão aos arquivos de cabeçalho

Em seguida, no arquivo *.cpp* do teste de unidade, adicione uma diretiva `#include` a todos os arquivos de cabeçalho que declaram os tipos e as funções que você deseja testar. Digite `#include "` e, depois, o IntelliSense será ativado para ajudá-lo a escolher. Repita essas etapas nos outros cabeçalhos.

![Captura de tela da Gerenciador de Soluções mostrando uma diretiva de #include que está sendo adicionada com o IntelliSense realçando um arquivo de cabeçalho para inclusão.](media/cpp-add-includes-test-project.png)

Para evitar a necessidade de digitar o caminho completo em cada instrução include no arquivo de origem, você pode adicionar as pastas necessárias nas propriedades do **projeto projetos** de  >    >  inclusão adicionais do **C/C++**  >  **geral**  >  .

### <a name="write-test-methods"></a>Gravar métodos de teste

> [!NOTE]
> Esta seção mostra a sintaxe da Microsoft Unit Testing Framework para C/C++. Ela está documentada na [Referência de API do Microsoft.VisualStudio.TestTools.CppUnitTestFramework](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md). Para obter a documentação do Google Test, confira [Prévia do Google Test](https://github.com/google/googletest/blob/master/docs/primer.md). Quanto ao Boost.Test, confira [Biblioteca do Boost Test: a estrutura de teste de unidade](https://www.boost.org/doc/libs/1_46_0/libs/test/doc/html/utf.html).

O arquivo *. cpp* em seu projeto de teste tem uma classe stub e um método definido para você. Eles mostram um exemplo de como escrever código de teste. As assinaturas usam as macros TEST_CLASS e TEST_METHOD, que tornam os métodos detectáveis na janela **Gerenciador de testes** .

![Captura de tela da janela Test Explorer que mostra o arquivo de código UnitTest1. cpp que contém uma classe stub e um método usando as macros TEST_CLASS e TEST_METHOD.](media/cpp-write-test-methods.png)

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

Você pode adicionar *características* a métodos de teste para especificar proprietários de teste, prioridade e outras informações. Depois, é possível usar esses valores para classificar e agrupar os testes no **Gerenciador de Testes**. Para obter mais informações, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

### <a name="run-the-tests"></a>Executar os testes

1. No menu **Teste**, escolha **Windows** > **Gerenciador de Testes**. A ilustração a seguir mostra um projeto de teste cujos testes ainda não foram executados.

   ![Test Explorer antes de executar testes](media/cpp-test-explorer.png)

   > [!NOTE]
   > A integração do CTest com o **Gerenciador de Testes** ainda não está disponível. Execute testes de CTest no menu principal do CMake.

1. Se nem todos os testes estiverem visíveis na janela, crie o projeto de teste clicando com o botão direito do mouse em seu nó em **Gerenciador de soluções** e escolhendo **Compilar** ou **Recompilar**.

1. No **Gerenciador de testes**, escolha **executar tudo** ou selecione os testes específicos que você deseja executar. Clique com o botão direito do mouse para ver outras opções, incluindo a execução em modo de depuração com pontos de interrupção habilitados. Depois de executar todos os testes, a janela mostrará quais testes foram aprovados e quais falharam:

![Gerenciador de Testes depois da execução dos testes](media/cpp-test-explorer-passed.png)

Para testes com falha, a mensagem mostra detalhes que ajudam a diagnosticar a causa. Clique com o botão direito do mouse no teste com falha de um menu pop-up. Escolha **depurar testes selecionados** para percorrer a função em que a falha ocorreu.

Para saber mais sobre como usar o **Gerenciador de Testes**, consulte [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md).

Para obter mais informações relacionadas ao teste de unidade, consulte [noções básicas de teste de unidade](unit-test-basics.md)

## <a name="use-codelens"></a>Usar o CodeLens

**Visual Studio 2017 e posterior (edições Professional e Enterprise)**

O [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) permite que você veja rapidamente o status de um teste de unidade sem sair do editor de código.

Você pode inicializar o CodeLens para um projeto de teste de unidade do C++ em qualquer uma das seguintes formas:

- Editar e compilar sua solução ou projeto de teste.
- Recompilar sua solução ou projeto.
- Execute testes na janela **Gerenciador de testes** .

Depois de inicializado, você pode ver os ícones de status de teste acima de cada teste de unidade.

![Ícones do CodeLens C++](media/cpp-test-codelens-icons.png)

Clique no ícone para obter mais informações ou para executar ou depurar o teste de unidade:

![Execução e depuração do CodeLens C++](media/cpp-test-codelens-run-debug.png)

## <a name="see-also"></a>Confira também

- [Teste de unidade em seu código](unit-test-your-code.md)

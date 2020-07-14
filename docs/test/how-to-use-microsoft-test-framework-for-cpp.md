---
title: Usar a estrutura de teste de unidade da Microsoft para C++
description: Use a estrutura de testes de unidade da Microsoft para C++ para criar testes de unidade para seu código C++.
ms.date: 01/08/2020
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: a9393fd248f4e6520c261d405bc624a75d8cf69f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287110"
---
# <a name="use-the-microsoft-unit-testing-framework-for-c-in-visual-studio"></a>Usar o Microsoft Unit Testing Framework para C/C++ no Visual Studio

O Microsoft Unit Testing Framework para C/C++ está incluído por padrão na carga de trabalho **Desenvolvimento de Área de Trabalho com C++**.

## <a name="to-write-unit-tests-in-a-separate-project"></a><a name="separate_project"></a> Gravar testes de unidade em um projeto separado

Normalmente, o código de teste é executado no próprio projeto na mesma solução que o código que você deseja testar. Para instalar e configurar um novo projeto de teste, consulte [Gravar testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md).

## <a name="to-write-unit-tests-in-the-same-project"></a><a name="same_project"></a>Para gravar testes de unidade no mesmo projeto

Em alguns casos, por exemplo, ao testar funções não exportadas em uma DLL, talvez você precise criar os testes no mesmo projeto que o programa que você está testando. Gravar testes de unidade no mesmo projeto:

1. Modifique as propriedades do projeto para incluir os cabeçalhos e os arquivos de biblioteca necessários para os testes de unidade.

   1. No Gerenciador de Soluções, no menu de atalho do projeto que você está testando, escolha **Propriedades**. A janela de propriedades do projeto aparece.

   1. Na caixa de diálogo páginas de propriedades, selecione **Propriedades de configuração**  >  **diretórios vc + +**.

   1. Clique na seta para baixo nas linhas a seguir e escolha **\<Edit>** . Adicione estes caminhos:

      | Diretório | Propriedade |
      |-| - |
      | **Incluir Diretórios** | **$(VCInstallDir)Auxiliary\VS\UnitTest\include** |
      | **Diretórios de Biblioteca** | **$(VCInstallDir)Auxiliary\VS\UnitTest\lib** |

1. Adicione um arquivo de teste de unidade C++:

   - No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Adicionar** > **Novo Item** > **Arquivo C++**.

## <a name="to-link-the-tests-to-the-object-or-library-files"></a><a name="object_files"></a>Para vincular os testes aos arquivos de biblioteca ou objeto

Se o código em teste não exportar as funções que você deseja testar, você poderá adicionar o arquivo output **. obj** ou **. lib** às dependências do projeto de teste. Modifique as propriedades do projeto de teste para incluir os cabeçalhos e os arquivos de biblioteca ou de objeto que são necessários para o teste de unidade.

1. No Gerenciador de Soluções, no menu de atalho do projeto de teste, selecione **Propriedades**. A janela de propriedades do projeto aparece.

1. Selecione a página de entrada do vinculador de **Propriedades de configuração**  >  **Linker**  >  **Input** e, em seguida, selecione **dependências adicionais**.

   Escolha **Editar**e adicione os nomes dos arquivos **.obj** ou **.lib**. Não use os nomes de caminho completos.

1. Selecione a página Geral do vinculador de **Propriedades de configuração**  >  **Linker**  >  **General** e, em seguida, selecione **diretórios de biblioteca adicionais**.

   Escolha **Editar**e adicione o caminho do diretório dos arquivos **.obj** ou **.lib**. O caminho fica geralmente dentro da pasta de compilação do projeto em teste.

1. Selecione a página de diretórios **Propriedades de configuração**  >  **vc + +** e, em seguida, selecione **incluir diretórios**.

   Escolha **Editar**e adicione o diretório de cabeçalho do projeto que está sendo testado.

## <a name="write-the-tests"></a>Gravar os testes

Qualquer arquivo *. cpp* com classes de teste deve incluir "CppUnitTest. h" e ter uma instrução using para `using namespace Microsoft::VisualStudio::CppUnitTestFramework` . O projeto de teste já está configurado para você. Uma definição de namespace e uma TEST_CLASS com um TEST_METHOD já estão incluídos para você começar. Você pode modificar o nome do namespace e os nomes entre parênteses nas macros de classe e método.

A estrutura de teste define macros especiais para inicializar módulos, classes e métodos de teste e para limpeza de recursos após a conclusão dos testes. Essas macros geram código a ser executado antes que uma classe ou um método seja acessado pela primeira vez e após a execução do último teste. Para saber mais, consulte [Inicialização e limpeza](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#Initialize_and_cleanup).

Use os métodos estáticos na classe [Assert](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#general_asserts) para definir as condições de teste. Use a classe de [Agente](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#logger) para gravar mensagens na **Janela de Saída**. Adicione atributos aos métodos de teste

## <a name="run-the-tests"></a>Executar os testes

1. No menu **Teste**, escolha **Windows** > **Gerenciador de Testes**.

1. Se nem todos os testes estiverem visíveis na janela, crie o projeto de teste clicando com o botão direito do mouse em seu nó em **Gerenciador de soluções** e escolhendo **Compilar** ou **Recompilar**.

1. No **Gerenciador de testes**, escolha **executar tudo**ou selecione os testes específicos que você deseja executar. Clique com o botão direito do mouse para ver outras opções, incluindo a execução em modo de depuração com pontos de interrupção habilitados.

1. Na **janela de saída** escolha **testes** na lista suspensa para exibir mensagens gravadas pela `Logger` classe:

   ![Janela de Saída do C++ mostrando mensagens de teste](media/cpp-test-output-window.png)

## <a name="define-traits-to-enable-grouping"></a>Definir as características para habilitar o agrupamento

Você pode definir características em métodos de teste, que permitem categorizar e agrupar testes no Gerenciador de **testes**. Para definir uma característica, use a macro `TEST_METHOD_ATTRIBUTE`. Por exemplo, para definir uma característica chamada de `TEST_MY_TRAIT`:

```cpp
#define TEST_MY_TRAIT(traitValue) TEST_METHOD_ATTRIBUTE(L"MyTrait", traitValue)
```

Para usar a característica definida em seus testes de unidade:

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
    TEST_OWNER(L"OwnerName")
    TEST_PRIORITY(1)
    TEST_MY_TRAIT(L"thisTraitValue")
END_TEST_METHOD_ATTRIBUTE()

TEST_METHOD(Method1)
{
    Logger::WriteMessage("In Method1");
    Assert::AreEqual(0, 0);
}
```

### <a name="c-trait-attribute-macros"></a>Macros de atributo de característica do C++

As seguintes características predefinidas são encontradas em `CppUnitTest.h`. Para obter mais informações, consulte [a estrutura de testes de unidade da Microsoft para referência de API do C++](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md).

|Macro|Descrição|
|-|-----------------|
|`TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)`|Use a macro TEST_METHOD_ATTRIBUTE para definir uma característica.|
|`TEST_OWNER(ownerAlias)`|Use a característica de proprietário predefinida para especificar um proprietário do método de teste.|
|`TEST_PRIORITY(priority)`|Use a característica de prioridade predefinida para atribuir prioridades relativas a seus métodos de teste.|

## <a name="see-also"></a>Veja também

- [Início Rápido: Desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md)

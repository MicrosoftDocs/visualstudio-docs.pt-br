---
title: Usar a estrutura de teste de unidade da Microsoft para C++
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: bcd75724e5124c280d5c3e54bfe870041c432790
ms.sourcegitcommit: ab06cde69d862440b4277bcd9bf02e7b50593a1b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67132124"
---
# <a name="use-the-microsoft-unit-testing-framework-for-c-in-visual-studio"></a>Usar o Microsoft Unit Testing Framework para C/C++ no Visual Studio

O Microsoft Unit Testing Framework para C/C++ está incluído por padrão na carga de trabalho **Desenvolvimento de Área de Trabalho com C++** .

## <a name="separate_project"></a> Gravar testes de unidade em um projeto separado

Normalmente, o código de teste é executado no próprio projeto na mesma solução que o código que você deseja testar. Para instalar e configurar um novo projeto de teste, consulte [Gravar testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md).

## <a name="same_project"></a> Gravar testes de unidade no mesmo projeto

Em alguns casos, por exemplo, ao testar funções não exportadas em uma DLL, talvez você precise criar os testes no mesmo projeto que o programa que você está testando. Gravar testes de unidade no mesmo projeto:

1. Modifique as propriedades do projeto para incluir os cabeçalhos e os arquivos de biblioteca necessários para os testes de unidade.

   1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto do programa que você está testando e, em seguida, escolha **Propriedades** > **Propriedades de Configuração** > **Diretórios VC++** .

   2. Clique na seta para baixo nas linhas a seguir e escolha **\<Editar>** . Adicione estes caminhos:

      | Diretório | Propriedade |
      |-| - |
      | **Incluir Diretórios** | **$(VCInstallDir)Auxiliary\VS\UnitTest\include** |
      | **Diretórios de Biblioteca** | **$(VCInstallDir)Auxiliary\VS\UnitTest\lib** |

2. Adicione um arquivo de teste de unidade C++:

   - No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Adicionar** > **Novo Item** > **Arquivo C++** .

## <a name="write-the-tests"></a>Gravar os testes

Qualquer arquivo *.cpp* com classes de teste precisa incluir "CppUnitTest.h" e ter uma instrução using para `using namespace Microsoft::VisualStudio::CppUnitTestFramework`. O projeto de teste já está configurado para você. Uma definição de namespace e uma TEST_CLASS com um TEST_METHOD já estão incluídos para você começar. É possível modificar o nome do namespace, bem como os nomes entre parênteses nas macros de classe e método.

As macros especiais são definidas para inicializar módulos de teste, classes e métodos e para a limpeza de recursos quando os testes forem concluídos. Essas macros geram código executado antes de uma classe ou método serem acessados pela primeira vez e após a execução do último teste. Para saber mais, consulte [Inicialização e limpeza](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#Initialize_and_cleanup).

Use os métodos estáticos na classe [Assert](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#general_asserts) para definir as condições de teste. Use a classe de [Agente](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#logger) para gravar mensagens na **Janela de Saída**. Adicione atributos aos métodos de teste

## <a name="run-the-tests"></a>Executar os testes

1. No menu **Teste**, escolha **Windows** > **Gerenciador de Testes**.

1. Caso todos os testes não estejam visíveis na janela, crie o projeto de teste clicando com o botão direito no mouse no nó do **Gerenciador de Soluções** e escolhendo **Criar** ou **Recompilar**.

1. No **Gerenciador de Testes**, escolha **Executar Todos** ou selecione os testes específicos que deseja executar. Clique com o botão direito do mouse para ver outras opções, incluindo a execução em modo de depuração com pontos de interrupção habilitados.

1. Na **Janela de Saída**, escolha **Testes** no menu suspenso para exibir as mensagens gravadas pela classe `Logger`:

   ![Janela de Saída do C++ mostrando mensagens de teste](media/cpp-test-output-window.png)

## <a name="define-traits-to-enable-grouping"></a>Definir as características para habilitar o agrupamento

É possível definir características nos métodos de teste que permitem categorizar e agrupar testes no **Gerenciador de Testes**. Para definir uma característica, use a macro `TEST_METHOD_ATTRIBUTE`. Por exemplo, para definir uma característica chamada de `TEST_MY_TRAIT`:

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

As seguintes características predefinidas são encontradas em `CppUnitTest.h`. Para obter mais informações, confira [A referência de API do Microsoft Unit Testing Framework para C++](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md).

|Macro|DESCRIÇÃO|
|-|-----------------|
|`TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)`|Use a macro TEST_METHOD_ATTRIBUTE para definir uma característica.|
|`TEST_OWNER(ownerAlias)`|Use a característica de proprietário predefinida para especificar um proprietário do método de teste.|
|`TEST_PRIORITY(priority)`|Use a característica de prioridade predefinida para atribuir prioridades relativas a seus métodos de teste.|

## <a name="see-also"></a>Consulte também

- [Início Rápido: Desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md)

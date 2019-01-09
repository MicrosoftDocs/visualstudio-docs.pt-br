---
title: Escrever testes de unidade para DLLs C++
ms.date: 11/04/2017
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.author: mblome
manager: douge
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: 7de21715053a91b187ccdcc1b87f042cedd1b7de
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53832444"
---
# <a name="write-unit-tests-for-c-dlls-in-visual-studio"></a>Escrever testes de unidade para DLLs em C++ no Visual Studio

 Há várias maneiras de testar o código da DLL, dependendo da exportação das funções que você deseja testar. Escolha uma das seguintes opções:

 **Os testes de unidade chamam apenas as funções exportadas da DLL:** Adicione um projeto de teste separado, conforme descrito em [Gravar testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md). No projeto de teste, adicione uma referência ao projeto de DLL.

 Vá para o procedimento [Para fazer referência a funções exportadas do projeto de DLL](#projectRef).

 **A DLL é compilada como um arquivo .exe:** Adicione um projeto de teste separado. Vincule-o ao arquivo de objeto de saída.

 Vá para o procedimento [Para vincular os testes aos arquivos de biblioteca ou objeto](#objectRef).

 **Os testes de unidade chamam funções não membro que não são exportadas da DLL e a DLL pode ser compilada como uma biblioteca estática:** Altere o projeto de DLL para que ele seja compilado em um arquivo *.lib*. Adicione um projeto de teste separado que referencia o projeto em teste.

 Essa abordagem tem a vantagem de permitir que seus testes usem membros não exportados, mas mantenham os testes em um projeto separado.

 Vá para o procedimento [Para alterar a DLL para uma biblioteca estática](#staticLink).

 **Os testes de unidade devem chamar funções não membro que não são exportadas e o código precisa ser criado como uma DLL (biblioteca de vínculo dinâmico):** Adicione testes de unidade no mesmo projeto que o código do produto.

 Vá para o procedimento [Para adicionar testes de unidade no mesmo projeto](#sameProject).

## <a name="create-the-tests"></a>Criar os testes

###  <a name="staticLink"></a> Para alterar uma DLL para uma biblioteca estática

- Se os testes devem usar membros que não são exportados pelo projeto de DLL e este é criado como uma biblioteca dinâmica, considere a possibilidade de convertê-la em uma biblioteca estática.

  1.  No **Gerenciador de Soluções**, no menu de atalho do projeto em teste, selecione **Propriedades**. A janela **Propriedades** do projeto é aberta.

  2.  Escolha **Propriedades de Configuração** > **Geral**.

  3.  Defina **Tipo de Configuração** como **Biblioteca Estática (.lib)**.

  Continue com o procedimento [Para vincular os testes aos arquivos de biblioteca ou objeto](#objectRef).

###  <a name="projectRef"></a> Para fazer referência a funções DLL exportadas do projeto de teste

- Se um projeto de DLL exporta as funções que deseja testar, você pode adicionar uma referência ao projeto de código do projeto de teste.

  1.  Criar um projeto de teste de unidade nativo.

      1.  No menu **Arquivo**, escolha **Novo** > **Projeto** > **Visual C++** > **Teste** > **Projeto de Teste de Unidade C++**.

  2.  No **Gerenciador de Soluções**, no menu de atalho do projeto de teste, selecione **Referências**. A janela **Propriedades** do projeto é aberta.

  3.  Selecione **Propriedades Comuns** > **Estrutura e Referências** e, em seguida, escolha o botão **Adicionar Nova Referência**.

  4.  Selecione **Projetos**e o projeto a ser testado.

       Escolha o botão **Adicionar**.

  5.  Nas propriedades do projeto de teste, adicione o local do projeto em teste a Incluir Diretórios.

       Escolha **Propriedades de Configuração** > **Diretórios VC++** > **Incluir Diretórios**.

       Escolha **Editar**e adicione o diretório de cabeçalho do projeto que está sendo testado.

  Acesse [Escrever os testes de unidade](#addTests).

###  <a name="objectRef"></a>Para vincular os testes aos arquivos de biblioteca ou objeto

- Se a DLL não exporta as funções que você deseja testar, é possível adicionar o arquivo de saída *.obj* ou *.lib* às dependências do projeto de teste.

  1.  Criar um projeto de teste de unidade nativo.

      1.  No menu **Arquivo**, escolha **Novo** > **Projeto** > **Visual C++** > **Teste** > **Projeto de Teste de Unidade Nativo**.

  2.  No **Gerenciador de Soluções**, no menu de atalho do projeto de teste, selecione **Propriedades**.

  3.  Escolha **Propriedades de Configuração** > **Vinculador** > **Entrada** > **Dependências Adicionais**.

       Escolha **Editar**e adicione os nomes dos arquivos **.obj** ou **.lib**. Não use os nomes de caminho completo.

  4.  Escolha **Propriedades de Configuração** > **Vinculador** > **Geral** > **Diretórios de Biblioteca Adicionais**.

       Escolha **Editar**e adicione o caminho do diretório dos arquivos **.obj** ou **.lib**. O caminho fica geralmente dentro da pasta de compilação do projeto em teste.

  5.  Escolha **Propriedades de Configuração** > **Diretórios VC++** > **Incluir Diretórios**.

       Escolha **Editar**e adicione o diretório de cabeçalho do projeto que está sendo testado.

  Acesse [Escrever os testes de unidade](#addTests).

###  <a name="sameProject"></a>Para adicionar testes de unidade no mesmo projeto

1. Modifique as propriedades do projeto do código de produto para incluir os cabeçalhos e os arquivos de biblioteca necessários aos testes de unidade.

   1.  No **Gerenciador de Soluções**, no menu de atalho do projeto em teste, escolha **Propriedades**. A janela **Propriedades** do projeto é aberta.

   2.  Escolha **Propriedades de Configuração** > **Diretórios VC++**.

   3.  Edite os diretórios Incluir e Biblioteca:

       |Diretório|Propriedade|
       |-|-|
       |**Incluir Diretórios** | **$(VCInstallDir)UnitTest\include;$(IncludePath)**|
       |**Diretórios de Biblioteca** | **$(VCInstallDir)UnitTest\lib;$(LibraryPath)**|

2. Adicione um arquivo de teste de unidade C++:

   -   No **Gerenciador de Soluções**, no menu de atalho do projeto, escolha **Adicionar** > **Novo Item** > **Teste de Unidade C++**.

   Acesse [Escrever os testes de unidade](#addTests).

##  <a name="addTests"></a> Escrever os testes de unidade

1.  Em cada arquivo de código de teste de unidade, adicione uma instrução `#include` aos cabeçalhos do projeto em teste.

2.  Adicione métodos e classes de teste aos arquivos de código do teste de unidade. Por exemplo:

    ```cpp
    #include "stdafx.h"
    #include "CppUnitTest.h"
    #include "MyProjectUnderTest.h"
    using namespace Microsoft::VisualStudio::CppUnitTestFramework;
    namespace MyTest
    {
      TEST_CLASS(MyTests)
      {
      public:
          TEST_METHOD(MyTestMethod)
          {
              Assert::AreEqual(MyProject::Multiply(2,3), 6);
          }
      };
    }
    ```

## <a name="run-the-tests"></a>Executar os testes

1.  No menu **Teste**, escolha **Windows** > **Gerenciador de Testes**.

1. Caso todos os testes não estejam visíveis na janela, crie o projeto de teste clicando com o botão direito no mouse no nó do **Gerenciador de Soluções** e escolhendo **Criar** ou **Recompilar**.

1.  No **Gerenciador de Testes**, escolha **Executar Todos** ou selecione os testes específicos que deseja executar. Clique com o botão direito do mouse para ver outras opções, incluindo a execução em modo de depuração com pontos de interrupção habilitados.

## <a name="see-also"></a>Consulte também

- [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)
- [Referência da API Microsoft.VisualStudio.TestTools.CppUnitTestFramework](../test/microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)
- [Depurar código nativo](../debugger/debugging-native-code.md)
- [Passo a passo: Criando e usando uma biblioteca de vínculo dinâmico (C++)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)
- [Importar e exportar](/cpp/build/importing-and-exporting)
- [Início Rápido: Desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md)

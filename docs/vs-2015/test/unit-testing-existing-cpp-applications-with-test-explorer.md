---
title: Teste de unidade de aplicativos do C++ existentes com Gerenciador de Testes | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 7d08de69-c32e-4f0b-89aa-75347b15fb82
caps.latest.revision: 13
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 68bff8dbe2d0e5d85c8b18eeafaeaad06ba3982e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540069"
---
# <a name="unit-testing-existing-c-applications-with-test-explorer"></a>Teste de unidade de aplicativos do C++ existentes com Gerenciador de Testes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Recomendamos que, antes de alterar um aplicativo existente, você verifique se ele tem uma boa cobertura com testes de unidade. Isso dá a garantia de que as alterações não introduziram bugs. Se o aplicativo ainda não tem testes de unidade, você pode adicioná-los usando as técnicas demonstradas neste tópico. Este tópico descreve como adicionar testes de unidade para código existente do Visual C++, iniciando com a decisão de como testar seu código e, em seguida, criando, escrevendo e executando os testes.

## <a name="deciding-how-to-test-your-code"></a>Decidindo como testar seu código
 Abra o projeto C++ existente e verifique-o para decidir como deseja adicionar os testes de unidade. Talvez você queira usar algumas ferramentas de modelagem, que ajudam a ver as dependências no código e a entender como as partes interagem. Para saber mais, confira [Visualizar código](../modeling/visualize-code.md).

 Recomendamos que você separe suas alterações em pequenas tarefas. Antes de cada pequena alteração, escreva testes de unidade para aspectos do comportamento que permanecerão iguais. Esses testes continuarão a ser aprovados depois que a alteração for feita. Por exemplo, se você pretende alterar uma função de classificação para que ela classifique uma lista de pessoas por sobrenome em vez de por nome, pode escrever um teste de unidade que verifica se todos os nomes de entrada aparecem na saída. Depois de ter feito a alteração, convém adicionar novos testes de unidade para o novo comportamento.

 Se for viável, muitos ou todos os seus testes de unidade devem usar apenas as funções que são exportadas. Mas se você estiver alterando apenas uma pequena parte de todo o aplicativo, poderá usar as funções que não são exportadas. Por exemplo, você pode querer testes que chamam funções internas ou testes que definem e obtêm os valores das variáveis internas.

 Há várias maneiras de testar o código do produto, dependendo da exposição das interfaces que você deseja testar. Escolha uma das seguintes opções:

 **Os testes de unidade usarão apenas as funções exportadas do código sob teste:** Adicione um projeto de teste separado. No projeto de teste, adicione uma referência ao projeto em teste.

 Vá para o procedimento [Para fazer referência a funções exportadas do projeto de teste](#projectRef).

 **O código em teste é criado como um arquivo. exe:** Adicione um projeto de teste separado. Vincule-o ao arquivo de objeto de saída.

 Vá para o procedimento [Para vincular os testes aos arquivos de biblioteca ou objeto](#objectRef).

 **Os testes de unidade devem usar funções e dados privados e o código em teste pode ser criado como uma biblioteca estática:** Altere o projeto em teste para que ele seja compilado em um arquivo. lib. Adicione um projeto de teste separado que referencia o projeto em teste.

 Essa abordagem tem a vantagem de permitir que seus testes usem membros privados, mas mantenham os testes em um projeto separado. No entanto, ele pode não ser adequado para alguns aplicativos em que você tenha que ter uma biblioteca de vínculo dinâmico (.dll).

 Vá para o procedimento [Para alterar o código em teste para uma biblioteca estática](#staticLink).

 **Os testes de unidade devem usar funções e dados privados e o código deve ser compilado como uma dll (biblioteca de vínculo dinâmico):** Adicione testes de unidade no mesmo projeto que o código do produto.

 Vá para o procedimento [Para adicionar testes de unidade no mesmo projeto](#sameProject).

## <a name="creating-the-tests"></a>Criando os testes

### <a name="to-change-the-code-under-test-to-a-static-library"></a><a name="staticLink"></a>Para alterar o código em teste para uma biblioteca estática

- Se os testes devem usar membros que não são exportados por um projeto em teste e este é criado como uma biblioteca dinâmica, considere a possibilidade de convertê-la em uma biblioteca estática.

  1. No Gerenciador de Soluções, no menu de atalho do projeto em teste, escolha **Propriedades**. A janela de propriedades do projeto aparece.

  2. Escolha **Propriedades de Configuração**, **Geral**.

  3. Defina **Tipo de Configuração** como **Biblioteca Estática (.lib)**.

  Continue com o procedimento [Para vincular os testes aos arquivos de biblioteca ou objeto](#objectRef).

### <a name="to-reference-exported-functions-from-the-test-project"></a><a name="projectRef"></a>Para fazer referência a funções exportadas do projeto de teste

- Se um projeto em teste exporta as funções que deseja testar, você pode adicionar uma referência ao projeto de código do projeto de teste.

  1. Criar um projeto de teste em C++.

      1. No menu **Arquivo**, escolha **Novo**, **Projeto**, **Visual C++, Teste**, **Projeto de Teste de Unidade C++**.

  2. No Gerenciador de Soluções, no menu de atalho do projeto de teste, selecione **Referências**. A janela de propriedades do projeto aparece.

  3. Selecione **Propriedades Comuns**, **Estrutura e Referências**e escolha o botão **Adicionar Nova Referência**.

  4. Selecione **Projetos**e o projeto a ser testado.

       Clique no botão **Adicionar**.

  5. Nas propriedades do projeto de teste, adicione o local do projeto em teste a Incluir Diretórios.

       Escolha **Propriedades de Configuração**, **Diretórios VC + +**, **Incluir Diretórios**.

       Escolha **Editar**e adicione o diretório de cabeçalho do projeto que está sendo testado.

  Vá para [Escrevendo testes de unidade](#addTests).

### <a name="to-link-the-tests-to-the-object-or-library-files"></a><a name="objectRef"></a>Para vincular os testes aos arquivos de biblioteca ou objeto

- Se o código em teste não exporta as funções que deseja testar, você pode adicionar o arquivo de saída **.obj** ou **.lib** às dependências do projeto de teste.

  1. Criar um projeto de teste em C++.

      1. No menu **Arquivo**, escolha **Novo**, **Projeto**, **Visual C++, Teste**, **Projeto de Teste de Unidade C++**.

  2. No Gerenciador de Soluções, no menu de atalho do projeto de teste, selecione **Propriedades**. A janela de propriedades do projeto aparece.

  3. Escolha **Propriedades de Configuração**, **Vinculador**, **Entrada**, **Dependências Adicionais**.

       Escolha **Editar**e adicione os nomes dos arquivos **.obj** ou **.lib**. Não use os nomes de caminho completo.

  4. Escolha **Propriedades de Configuração**, **Vinculador**, **Geral**, **Diretórios de Biblioteca Adicionais**.

       Escolha **Editar**e adicione o caminho do diretório dos arquivos **.obj** ou **.lib**. O caminho fica geralmente dentro da pasta de compilação do projeto em teste.

  5. Escolha **Propriedades de Configuração**, **Diretórios VC + +**, **Incluir Diretórios**.

       Escolha **Editar**e adicione o diretório de cabeçalho do projeto que está sendo testado.

  Vá para [Escrevendo testes de unidade](#addTests).

### <a name="to-add-unit-tests-in-the-same-project"></a><a name="sameProject"></a>Para adicionar testes de unidade no mesmo projeto

1. Modifique as propriedades do projeto do código de produto para incluir os cabeçalhos e os arquivos de biblioteca necessários aos testes de unidade.

   1. No Gerenciador de Soluções, no menu de atalho do projeto em teste, selecione Propriedades. A janela de propriedades do projeto aparece.

   2. Escolha **Propriedades de Configuração**, **Diretórios VC + +**.

   3. Edite os diretórios Incluir e Biblioteca:

       |Propriedade|Valor|
       |-|-|
       |**Incluir Diretórios**|**$(VCInstallDir)UnitTest\include;$(IncludePath)**|
       |**Diretórios de Biblioteca**|**$(VCInstallDir)UnitTest\lib;$(LibraryPath)**|

2. Adicione um arquivo de teste de unidade C++:

   - No Gerenciador de Soluções, no menu de atalho do projeto, escolha **Adicionar**, **Novo Item**e escolha **Teste de Unidade C++**.

   Vá para [Escrevendo testes de unidade](#addTests).

## <a name="writing-the-unit-tests"></a><a name="addTests"></a> Escrevendo testes de unidade

1. Em cada arquivo de código de teste de unidade, adicione uma instrução `#include` aos cabeçalhos do projeto em teste.

2. Adicione métodos e classes de teste aos arquivos de código do teste de unidade. Por exemplo:

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

   Para saber mais, confira [Teste de unidade de código nativo com o Gerenciador de Testes](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c).

## <a name="run-the-tests"></a>Executar os testes

1. No menu **Exibir**, escolha **Outras Janelas**, **Gerenciador de Testes**.

2. No Gerenciador de testes, escolha **executar tudo**.

   Para saber mais, confira [Início Rápido: desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md).

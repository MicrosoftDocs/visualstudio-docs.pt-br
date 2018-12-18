---
title: Criar um projeto de teste de unidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a608bfba-1a43-4a60-b73a-1fe53ef58098
caps.latest.revision: 10
ms.author: gewarren
manager: douge
ms.openlocfilehash: 92520f2b092d3ef8b3daa3f4ffa41139a18d6641
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883413"
---
# <a name="create-a-unit-test-project"></a>Crie um projeto de teste de unidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Geralmente, os testes de unidade refletem a estrutura do código que está sendo testado. Por exemplo, um projeto de teste de unidade será criado para cada projeto de código do produto. O projeto de teste pode estar na mesma solução que o código de produção ou em uma solução separada. É possível ter vários projetos de teste de unidade em uma solução.  
  
> [!NOTE]
>  O local dos testes de unidade para o código nativo e a estrutura do projeto de teste podem ser diferentes da estrutura descrita neste tópico. Para obter mais informações, consulte [Adicionando testes de unidade a aplicativos do C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md).  
  
## <a name="to-create-a-unit-test-project"></a>Para criar um projeto de teste de unidade:  
  
1.  No menu **Arquivo**, escolha **Novo** e, em seguida, escolha **Projeto** (Teclado: Ctrl + Shift + N).  
  
2.  Na caixa de diálogo Novo Projeto, expanda o nó **Instalado**, escolha o idioma que você deseja usar para o projeto de teste e escolha **Testar**.  
  
3.  Para usar uma das estruturas de teste de unidade da Microsoft, escolha **Projeto de Teste de Unidade** na lista de modelos de projeto. Caso contrário, escolha o modelo de projeto da estrutura de teste de unidade que você deseja usar. Para testar o projeto Contas de nosso exemplo, você nomeará o projeto AccountsTests.  
  
4.  No projeto de teste de unidade, adicione uma referência ao código que está sendo testado.  Veja como criar a referência a um projeto de código na mesma solução:  
  
    1.  Selecione o projeto no Gerenciador de Soluções.  
  
    2.  No menu **Projeto**, escolha **Adicionar Referência...**.  
  
    3.  Na caixa de diálogo Gerenciador de Referência, abra o nó **Solução** e escolha **Projetos**. Verifique o nome do projeto de código e feche a caixa de diálogo.  
  
5.  Se o código que você deseja testar estiver em outro local, consulte [Gerenciando referências em um projeto](../ide/managing-references-in-a-project.md) para obter informações sobre como adicionar referências.  
  
## <a name="next-steps"></a>Próximas etapas  
 **Escrevendo testes de unidade**  
  
 Consulte uma das seguintes seções:  
  
- [Escrevendo testes de unidade para .NET Framework com a estrutura de teste de unidade Microsoft para código gerenciado](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)  
  
- [Escrevendo testes de unidade para C/C++ com o Microsoft Unit Testing Framework para C++](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)  
  
  **Executando testes de unidade**  
  
  [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)




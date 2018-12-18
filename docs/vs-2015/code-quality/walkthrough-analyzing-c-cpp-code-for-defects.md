---
title: 'Passo a passo: Analisando código C / C++ em busca de defeitos | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- C/C++, code analysis
- code analysis, walkthroughs
- code, analyzing C/C++
- code analysis tool, walkthroughs
ms.assetid: eaee55b8-85fe-47c7-a489-9be0c46ae8af
caps.latest.revision: 37
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 6a5e98ee673d232065dd522b0b81a21760306979
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782304"
---
# <a name="walkthrough-analyzing-cc-code-for-defects"></a>Instruções passo a passo: analisando código do C/C++ em busca de defeitos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo demonstra como analisar o código C/C++ em busca de possíveis defeitos de código usando a ferramenta de análise de código para código C/C++.  
  
 Neste passo a passo, você percorrer o processo de usar a análise de código para analisar seu código C/C++ em busca de possíveis defeitos de código.  
  
 Você concluirá as seguintes etapas:  
  
-   Execute análise de código em código nativo.  
  
-   Analise os avisos de defeitos de código.  
  
-   Tratar aviso como erro.  
  
-   Anote o código-fonte para melhorar a análise de defeitos de código.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] ou [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)].  
  
-   Uma cópia do [amostra de demonstração](../code-quality/demo-sample.md).  
  
-   Noções básicas sobre C/C++.  
  
### <a name="to-run-code-defect-analysis-on-native-code"></a>Para executar a análise de defeitos de código em código nativo  
  
1.  Abra a solução de demonstração no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
     A solução de demonstração agora preenche **Gerenciador de soluções**.  
  
2.  Sobre o **construir** menu, clique em **recompilar solução**.  
  
     A solução é compilada sem erros ou avisos.  
  
3.  Na **Gerenciador de soluções**, selecione o projeto CodeDefects.  
  
4.  No menu **Projeto**, clique em **Propriedades**.  
  
     O **páginas de propriedade CodeDefects** caixa de diálogo é exibida.  
  
5.  Clique em **análise de código**.  
  
6.  Clique o **habilitar a análise de código para C/C++ no Build** caixa de seleção.  
  
7.  Recompile o projeto CodeDefects.  
  
     Avisos da análise de código são exibidos na **Error List**.  
  
### <a name="to-analyze-code-defect-warnings"></a>Para analisar os avisos de defeitos de código  
  
1.  Sobre o **modo de exibição** menu, clique em **lista de erros**.  
  
     Dependendo do perfil do desenvolvedor que você escolheu na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], talvez você precise apontar para **Other Windows** sobre o **exibição** menu e, em seguida, clique **lista de erros**.  
  
2.  No **Error List**, clique duas vezes o seguinte aviso:  
  
     Aviso C6230: conversão implícita entre tipos semanticamente diferentes: usando HRESULT em um contexto booleano.  
  
     O editor de código exibe a linha que causou o aviso na função `bool``ProcessDomain()`. Este aviso indica que um HRESULT está sendo usado em uma instrução 'if' em que um resultado booliano é esperado.  
  
3.  Corrigi este aviso usando a macro SUCCEEDED. Seu código deve se parecer com o código a seguir:  
  
    ```  
    if (SUCCEEDED (ReadUserAccount()) )  
    ```  
  
4.  No **Error List**, clique duas vezes o seguinte aviso:  
  
     Aviso C6282: operador incorreto: atribuição a constante no contexto do teste. Foi = = pretendido?  
  
5.  Para corrigir este aviso, testando a igualdade. Seu código deve ser semelhante ao seguinte código:  
  
    ```  
    if ((len == ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))  
    ```  
  
### <a name="to-treat-warning-as-an-error"></a>Tratar aviso como erro  
  
1.  No arquivo Bug.cpp, adicione o seguinte `#pragma` instrução para o início do arquivo para tratar o aviso C6001 como um erro:  
  
    ```  
    #pragma warning (error: 6001)  
    ```  
  
2.  Recompile o projeto CodeDefects.  
  
     No **lista de erros**, C6001 agora aparece como um erro.  
  
3.  Corrija os erros de C6001 dois restantes na **lista de erros** Inicializando `i` e `j` como 0.  
  
4.  Recompile o projeto CodeDefects.  
  
     O projeto é compilado sem avisos ou erros.  
  
### <a name="to-correct-the-source-code-annotation-warnings-in-annotationc"></a>Para corrigir os avisos de anotação do código fonte no annotation.c  
  
1.  No Gerenciador de soluções, selecione o projeto de anotações.  
  
2.  No menu **Projeto**, clique em **Propriedades**.  
  
     O **páginas de propriedades de anotações** caixa de diálogo é exibida.  
  
3.  Clique em **análise de código**.  
  
4.  Selecione o **habilitar a análise de código para C/C++ no Build** caixa de seleção.  
  
5.  Recompile o projeto de anotações.  
  
6.  No **Error List**, clique duas vezes o seguinte aviso:  
  
     Aviso C6011: Desreferenciando ponteiro NULL 'newNode'.  
  
     Este aviso indica falha pelo chamador para verificar o valor de retorno. Nesse caso, uma chamada para **AllocateNode** pode retornar um valor NULL (consulte o arquivo de cabeçalho para a declaração de função para AllocateNode annotations.h).  
  
7.  Abra o arquivo annotations.cpp.  
  
8.  Para corrigir este aviso, use uma instrução 'if' para testar o valor de retorno. Seu código deve se parecer com o código a seguir:  
  
     `if (NULL != newNode)`  
  
     `{`  
  
     `newNode->data = value;`  
  
     `newNode->next = 0;`  
  
     `node->next = newNode;`  
  
     `}`  
  
9. Recompile o projeto de anotações.  
  
     O projeto é compilado sem avisos ou erros.  
  
### <a name="to-use-source-code-annotation"></a>Para usar a anotação de código fonte  
  
1.  Anotar parâmetros formais e retornar o valor da função `AddTail` usando as condições anteriores e subsequentes, conforme mostrado neste exemplo:  
  
     `[returnvalue:SA_Post (Null=SA_Maybe)] LinkedList* AddTail`  
  
     `(`  
  
     `[SA_Pre(Null=SA_Maybe)] LinkedList* node,`  
  
     `int value`  
  
     `)`  
  
2.  Recompile o projeto de anotações.  
  
3.  No **Error List**, clique duas vezes o seguinte aviso:  
  
     Aviso C6011: Desreferenciando ponteiro NULL 'node'.  
  
     Este aviso indica que o nó passado para a função pode ser nulo e indica o número de linha em que o aviso foi gerado.  
  
4.  Para corrigir este aviso, use uma instrução 'if' para testar o valor de retorno. Seu código deve se parecer com o código a seguir:  
  
    ```  
    . . .  
    LinkedList *newNode = NULL;   
    if (NULL == node)  
    {  
         return NULL;  
        . . .  
    }  
    ```  
  
5.  Recompile o projeto de anotações.  
  
     O projeto é compilado sem avisos ou erros.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: analisando código gerenciado em busca de defeitos de código](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)




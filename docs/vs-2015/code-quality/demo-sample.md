---
title: Exemplo de demonstração | Microsoft Docs
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
- demo sample [Visual Studio ALM]
- code analysis, samples
ms.assetid: 09e1b9f7-5916-4ed6-a001-5c2d7e710682
caps.latest.revision: 23
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 2ca480078bf269e8af662d94910a5d337c13bcd8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722379"
---
# <a name="demo-sample"></a>Amostra de demonstração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Estes procedimentos a seguir mostram como criar o exemplo para [instruções passo a passo: Analisando código do C/C++ em busca de defeitos](../code-quality/walkthrough-analyzing-c-cpp-code-for-defects.md). Criam os procedimentos:  
  
- Um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução chamada CppDemo.  
  
- Um projeto de biblioteca estática denominada CodeDefects.  
  
- Um projeto de biblioteca estática denominada anotações.  
  
  Os procedimentos também fornecem o código para os arquivos de cabeçalho e. cpp para as bibliotecas estáticas.  
  
### <a name="create-the-cppdemo-solution-and-the-codedefects-project"></a>Crie a solução CppDemo e o projeto de CodeDefects  
  
1.  Clique o **arquivo** , aponte para **New**e, em seguida, clique em **novo projeto**.  
  
2.  No **tipos de projeto** lista de árvore, expanda se o Visual C++ não é o idioma padrão no VS **outros idiomas**.  
  
3.  Expandir **Visual C++** e, em seguida, clique em **geral**.  
  
4.  Na **modelos**, clique em **projeto vazio**.  
  
5.  No **nome** caixa de texto, digite **CodeDefects**.  
  
6.  Marque a caixa de seleção **Criar diretório para a solução**.  
  
7.  No **nome da solução** caixa de texto, digite **CppDemo**.  
  
### <a name="configure-the-codedefects-project-as-a-static-library"></a>Configurar o projeto CodeDefects como uma biblioteca estática  
  
1.  No Gerenciador de soluções, clique com botão direito **CodeDefects** e, em seguida, clique em **propriedades**.  
  
2.  Expandir **propriedades de configuração** e, em seguida, clique em **geral**.  
  
3.  No **gerais** , selecione o texto na coluna ao lado de **extensão de destino**e, em seguida, digite **. lib**.  
  
4.  Na **padrões de projeto**, clique na coluna ao lado de **tipo de configuração**e, em seguida, clique em **biblioteca estática (. lib)**.  
  
### <a name="add-the-header-and-source-file-to-the-codedefects-project"></a>Adicione o arquivo de cabeçalho e o código-fonte ao projeto CodeDefects  
  
1.  No Gerenciador de soluções, expanda **CodeDefects**, clique com botão direito **arquivos de cabeçalho**, clique em **Add**e, em seguida, clique em **Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, clique em **código**e, em seguida, clique em **arquivo de cabeçalho (. h)**.  
  
3.  No **nome** , digite **Bug.cpp** e, em seguida, clique em **adicionar**.  
  
4.  Copie o código a seguir e cole-o na **Bug.cpp** arquivo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor.  
  
    ```  
    #include <windows.h>  
  
    //    
    //These 3 functions are consumed by the sample  
    //  but are not defined. This project cannot be linked!  
    //  
  
    bool CheckDomain( LPCSTR );  
    HRESULT ReadUserAccount();  
  
    //  
    //These constants define the common sizes of the   
    //  user account information throughout the program  
    //  
  
    const int USER_ACCOUNT_LEN = 256;  
    const int ACCOUNT_DOMAIN_LEN = 128;  
    ```  
  
5.  No Gerenciador de soluções, clique com botão direito **arquivos de origem**, aponte para **New**e, em seguida, clique em **Novo Item**.  
  
6.  No **Adicionar Novo Item** caixa de diálogo, clique em **arquivo C++ (. cpp)**  
  
7.  No **nome** , digite **Bug.cpp** e, em seguida, clique em **adicionar**.  
  
8.  Copie o código a seguir e cole-o no arquivo Bug.h do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor.  
  
    ```  
    #include <stdlib.h>  
    #include "Bug.h"  
  
    // the user account   
    TCHAR g_userAccount[USER_ACCOUNT_LEN] = "";  
    int len = 0;  
  
    bool ProcessDomain()  
    {  
        TCHAR* domain = new TCHAR[ACCOUNT_DOMAIN_LEN];  
        // ReadUserAccount gets a 'domain\user' input from   
        //the user into the global 'g_userAccount'  
        if (ReadUserAccount() )  
        {  
  
            // Copies part of the string prior to the '\'   
            // character onto the 'domain' buffer  
            for( len = 0 ; (len < ACCOUNT_DOMAIN_LEN) && (g_userAccount[len] != '\0') ; len++  )  
            {  
                if ( g_userAccount[len] == '\\' )   
                {  
                    // Stops copying on the domain and user separator ('\')   
                    break;  
                }  
                domain[len] = g_userAccount[len];          
            }  
            if((len= ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))  
            {  
                // '\' was not found. Invalid domain\user string.  
                delete [] domain;  
                return false;  
            }  
            else  
            {  
                domain[len]='\0';  
            }  
            // Process domain string  
            bool result = CheckDomain( domain );  
  
            delete[] domain;  
            return result;  
        }  
        return false;  
    }  
  
    int path_dependent(int n)  
    {  
        int i;  
        int j;  
        if (n == 0)  
            i = 1;  
        else  
            j = 1;  
        return i+j;   
    }  
    ```  
  
9. Clique o **arquivo** menu e clique **Salvar tudo**.  
  
### <a name="add-the-annotations-project-and-configure-it-as-a-static-library"></a>Adicione o projeto de anotações e configurá-lo como uma biblioteca estática  
  
1.  No Gerenciador de soluções, clique em **CppDemo**, aponte para **Add**e, em seguida, clique em **novo projeto**.  
  
2.  No **adicionar novo projeto** diálogo caixa, expanda Visual C++, clique em **gerais**e, em seguida, clique em **projeto vazio**.  
  
3.  No **nome** caixa de texto, digite **anotações**e, em seguida, clique em **adicionar**.  
  
4.  No Gerenciador de soluções, clique com botão direito **anotações** e, em seguida, clique em **propriedades**.  
  
5.  Expandir **propriedades de configuração** e, em seguida, clique em **geral**.  
  
6.  No **gerais** , selecione o texto na coluna ao lado de **extensão de destino**e, em seguida, digite **. lib**.  
  
7.  Na **padrões de projeto**, clique na coluna ao lado de **tipo de configuração**e, em seguida, clique em **biblioteca estática (. lib)**.  
  
### <a name="add-the-header-file-and-source-file-to-the-annotations-project"></a>Adicionar o arquivo de cabeçalho e o arquivo de origem para o projeto de anotações  
  
1.  No Gerenciador de soluções, expanda **anotações**, clique com botão direito **arquivos de cabeçalho**, clique em **Add**e, em seguida, clique em **Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, clique em **arquivo de cabeçalho (. h)**.  
  
3.  No **nome** , digite **annotations.h** e, em seguida, clique em **adicionar**.  
  
4.  Copie o código a seguir e cole-o na **annotations.h** arquivo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor.  
  
    ```  
    #include <CodeAnalysis/SourceAnnotations.h>  
  
    struct LinkedList  
    {  
        struct LinkedList* next;  
        int data;  
    };  
  
    typedef struct LinkedList LinkedList;  
  
    [returnvalue:SA_Post( Null=SA_Maybe )] LinkedList* AllocateNode();  
  
    ```  
  
5.  No Gerenciador de soluções, clique com botão direito **arquivos de origem**, aponte para **New**e, em seguida, clique em **Novo Item**.  
  
6.  No **Adicionar Novo Item** caixa de diálogo, clique em **código** e, em seguida, clique em **arquivo C++ (. cpp)**  
  
7.  No **nome** , digite **annotations.cpp** e, em seguida, clique em **adicionar**.  
  
8.  Copie o código a seguir e cole-o na **annotations.cpp** arquivo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor.  
  
    ```  
    #include <CodeAnalysis/SourceAnnotations.h>  
    #include <windows.h>  
    #include <stdlib.h>    
    #include "annotations.h"  
  
    LinkedList* AddTail( LinkedList *node, int value )  
    {  
        LinkedList *newNode = NULL;   
  
        // finds the last node  
        while ( node->next != NULL )   
        {  
            node = node->next;  
        }  
  
        // appends the new node  
        newNode = AllocateNode();   
        newNode->data = value;  
        newNode->next = 0;  
        node->next = newNode;  
  
        return newNode;  
    }  
  
    ```  
  
9. Clique o **arquivo** menu e clique **Salvar tudo**.




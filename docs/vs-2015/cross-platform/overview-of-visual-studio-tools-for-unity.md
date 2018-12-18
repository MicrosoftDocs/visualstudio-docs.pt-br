---
title: Visão Geral das Ferramentas do Visual Studio para Unity | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4231bb9-45c4-4c77-ac3c-d05033b26393
caps.latest.revision: 6
ms.author: crdun
manager: crdun
ms.openlocfilehash: f403a1001cb32376b91da472acdebaa31cc91682
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744249"
---
# <a name="overview-of-visual-studio-tools-for-unity"></a>Visão Geral das Ferramentas do Visual Studio para Unity
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Nesta seção, saiba mais sobre os recursos que as Ferramentas do Visual Studio para Unity oferecem e como usá-las para ter mais produtividade no Unity.  
  
 Com as Ferramentas do Visual Studio para Unity (*VSTU*), é possível usar o Visual Studio para registrar scripts de jogos e edição no C# e, em seguida, usar seu poderoso depurador para localizar e corrigir erros. A última versão do VSTU inclui a coloração de sintaxe da linguagem de sombreador ShaderLab do Unity, melhores visualizações do depurador e geração de código aprimorada para o assistente MonoBehavior. O VSTU também leva seus arquivos de projeto do Unity, mensagens do console e a capacidade de iniciar seu jogo para o Visual Studio, para que você possa gastar menos tempo mudando do e para o Editor do Unity durante a escrita do código.  
  
 Continue para saber mais sobre esses recursos.  
  
## <a name="integration-with-unity"></a>Integração com o Unity  
 As Ferramentas do Visual Studio para Unity não melhorariam a produtividade se fosse necessário mudar entre o editor do Unity e o Visual Studio toda hora. É por isso que as Ferramentas do Visual Studio para Unity facilitam o trabalho sem sair do Visual Studio.  
  
-   O **Gerenciador de Projetos do Unity** exibe todo o projeto do Unity dentro do Visual Studio usando a mesma hierarquia exibida no editor do Unity.  
  
-   A integração de console do Unity exibe a saída do console do Unity dentro da janela de erro do Visual Studio.  
  
-   Inicie a depuração de um jogo no Visual Studio – não é necessário voltar para o Unity, apenas pressione F5.  
  
## <a name="superior-debugging"></a>Depuração Superior  
 Conecte o poderoso depurador do Visual Studio ao jogo do Unity para depurar scripts do C# e DLLs mesmo se ele estiver em execução autônoma ou no editor do Unity. É possível usar todos os recursos de depuração esperados do Visual Studio.  
  
- Pontos de interrupção, incluindo pontos de interrupção condicionais.  
  
- Avalie expressões complexas na janela Inspeção.  
  
- Inspecione e modifique o valor de variáveis e argumentos.  
  
- Analise objetos complexos e estruturas de dados.  
  
  É possível até mesmo depurar um jogo do Unity enquanto ele é executado em outro computador em sua rede.  
  
## <a name="productivity"></a>Produtividade  
 Além da produtividade estabelecida pelo Visual Studio no registro e refatoração de código no C#, as Ferramentas do Visual Studio para Unity fornecem recursos extra para desenvolvedores do Unity.  
  
-   A coloração de sintaxe para a linguagem ShaderLab do Unity ajuda a identificar erros em sombreadores antes que eles se tornem bugs. Basta abrir os arquivos do ShaderLab no Visual Studio.  
  
-   O assistente do MonoBehavior permite procurar por uma lista de comportamentos do Unity e cria código clichê para comportamentos com os quais você pode não estar familiarizado. Pressione CTRL+SHIFT+M.  
  
-   Quando estiver familiarizado com os comportamentos do Unity que você mais usa, o assistente rápido do MonoBehavior os colocará ao seu alcance. Pressione CTRL + ALT + Q.  
  
-   Acesse a documentação do Unity no Visual Studio. Basta realçar a chamada à API que você deseja conhecer e, em seguida, pressionar CTRL+ALT+M, CTRL+H.  
  
-   Acesse todos esses recursos e muito mais com os atalhos de teclado.  
  
## <a name="visual-studio-tools-for-unity-api"></a>Ferramentas do Visual Studio para API de Unity  
 Personalize e estenda o comportamento das Ferramentas do Visual Studio para Unity usando as APIs fornecidas.  
  
-   As Ferramentas do Visual Studio para Unity registram um retorno de chamada de log a fim de transmitir o console do Unity para o Visual Studio. Caso você tenha scripts de editor que registram informações, é possível colocá-los no mesmo retorno de chamada para enviar mensagens ao Visual Studio. Para obter mais informações, consulte o exemplo para Retorno de Chamada de Log.  
  
-   É possível alterar o modo como as Ferramentas do Visual Studio para Unity geram arquivos de projeto usando o estilo de retorno de chamada ProjectFileGeneration do Unity. Para obter mais informações, consulte o exemplo de Geração de Arquivo de Projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Home page do Unity](http://unity3d.com)


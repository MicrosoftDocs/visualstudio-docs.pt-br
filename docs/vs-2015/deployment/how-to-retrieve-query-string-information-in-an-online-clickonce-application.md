---
title: 'Como: recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce Online | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, query strings
- query strings, retrieving information
ms.assetid: 48ce098a-a075-481b-a5f5-c8ba11f63120
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 78b4edd85d47087033cc20189f2c9edc4d7fcd34
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49278922"
---
# <a name="how-to-retrieve-query-string-information-in-an-online-clickonce-application"></a>Como recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce online
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O *cadeia de caracteres de consulta* é a parte de uma URL que comece com um ponto de interrogação (?) que contém informações arbitrárias no formulário *nome = valor*. Suponha que você tenha um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo denominado `WindowsApp1` que você hospede em `servername`, e você deseja passar um valor para a variável `username` quando o aplicativo é iniciado. A URL pode parecer com o seguinte:  
  
 `http://servername/WindowsApp1.application?username=joeuser`  
  
 Os dois procedimentos a seguir mostram como usar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo para obter informações de cadeia de caracteres de consulta.  
  
> [!NOTE]
>  Você só pode passar informações em uma cadeia de caracteres de consulta quando seu aplicativo está sendo iniciado usando HTTP, em vez de usar um compartilhamento de arquivos ou o sistema de arquivos local.  
  
 O primeiro procedimento mostra como seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo pode usar um pequeno trecho de código para ler esses valores quando o aplicativo é iniciado.  
  
 O procedimento a seguir mostra como configurar seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] usando MageUI.exe para que ele pode aceitar parâmetros de cadeia de caracteres de consulta de aplicativo. Você precisará fazer isso sempre que você publicar seu aplicativo.  
  
> [!NOTE]
>  Antes de tomar uma decisão para habilitar esse recurso, consulte a seção "Segurança" mais adiante neste tópico.  
  
 Para obter informações sobre como criar uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação usando Mage.exe ou MageUI.exe, consulte [passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  
  
> [!NOTE]
>  A partir do .NET Framework 3.5 SP1, é possível passar argumentos de linha de comando para um offline [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Se você deseja fornecer argumentos para o aplicativo, você pode passar parâmetros para o arquivo de atalho com o. Extensão APPREF-MS.  
  
### <a name="to-obtain-query-string-information-from-a-clickonce-application"></a>Para obter informações de cadeia de caracteres de consulta de um aplicativo ClickOnce  
  
1.  Coloque o código a seguir em seu projeto. Em ordem para este código à função, você precisará ter uma referência a System. Web e adicionar `using` ou `Imports` instruções para System.Deployment.Application, Specialized e System. Web.  
  
     [!code-csharp[ClickOnceQueryString#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceQueryString/CS/Form1.cs#1)]
     [!code-vb[ClickOnceQueryString#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceQueryString/VB/Form1.vb#1)]  
  
2.  Chamar a função definida anteriormente para recuperar um <xref:System.Collections.DictionaryBase.Dictionary%2A> dos parâmetros de cadeia de caracteres de consulta, indexados pelo nome.  
  
### <a name="to-enable-query-string-passing-in-a-clickonce-application-with-mageuiexe"></a>Para habilitar a cadeia de caracteres de consulta passando em um aplicativo ClickOnce com MageUI.exe  
  
1.  Abra o Prompt de comando do .NET e digite:  
  
    ```  
    MageUI  
    ```  
  
2.  Do **arquivo** menu, selecione **abra**e abra o manifesto de implantação para seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, que é o arquivo terminando no `.application` extensão.  
  
3.  Selecione o **opções de implantação** na janela de navegação à esquerda do painel e, em seguida, selecione o **parâmetros de URL de permitir a serem passados para o aplicativo** caixa de seleção.  
  
4.  Dos **arquivo** menu, selecione **salvar**.  
  
> [!NOTE]
>  Como alternativa, você pode habilitar a cadeia de caracteres de consulta passando [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Selecione o **parâmetros de URL de permitir a serem passados para o aplicativo** caixa de seleção, que pode ser encontrada, abrindo o **propriedades do projeto**, selecionando o **publicar** guia, clicando no **Opções** botão e, em seguida, selecionando **manifestos**.  
  
## <a name="robust-programming"></a>Programação robusta  
 Quando você usa os parâmetros de cadeia de caracteres de consulta, você deve dar uma consideração cuidadosa como seu aplicativo é instalado e ativado. Se seu aplicativo está configurado para instalar no computador do usuário da Web ou de um compartilhamento de rede, é provável que o usuário ativará o aplicativo apenas uma vez por meio da URL. Depois disso, o usuário geralmente ativar seu aplicativo usando o atalho na **iniciar** menu. Como resultado, seu aplicativo é garantido que recebem argumentos de cadeia de caracteres de consulta apenas uma vez durante seu ciclo de vida. Se você optar por armazenar esses argumentos na máquina do usuário para uso futuro, você é responsável por armazená-los de maneira segura e protegida.  
  
 Se seu aplicativo só está online, ele sempre será ativado por meio de uma URL. Mesmo nesse caso, no entanto, seu aplicativo deve ser escrito para funcionar corretamente se os parâmetros de cadeia de caracteres de consulta estão ausentes ou corrompidos.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Permitir a passagem de parâmetros de URL para seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo somente se você planeja limpar a entrada de quaisquer caracteres mal-intencionados antes de usá-lo. Uma cadeia de caracteres inserida com aspas, barras ou ponto e vírgula, por exemplo, pode executar a operações de dados arbitrário se usado sem o filtro em uma consulta SQL em relação a um banco de dados. Para obter mais informações sobre a segurança da cadeia de caracteres de consulta, consulte [visão geral de explorações de Script](http://msdn.microsoft.com/library/772c7312-211a-4eb3-8d6e-eec0aa1dcc07).  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)




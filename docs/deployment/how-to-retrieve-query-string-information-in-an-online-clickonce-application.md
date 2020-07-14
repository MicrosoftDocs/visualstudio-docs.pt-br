---
title: Recuperar informações de cadeia de caracteres de consulta no aplicativo ClickOnce online
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, query strings
- query strings, retrieving information
ms.assetid: 48ce098a-a075-481b-a5f5-c8ba11f63120
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d0e177f1d41655ffa6fb6b6bbfa52cfc29d15fd6
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382179"
---
# <a name="how-to-retrieve-query-string-information-in-an-online-clickonce-application"></a>Como recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce online
A *cadeia de caracteres de consulta* é a parte de uma URL que começa com um ponto de interrogação (?) que contém informações arbitrárias no formato *nome = valor*. Suponha que você tenha um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo chamado `WindowsApp1` que você hospede em `servername` e queira passar um valor para a variável `username` quando o aplicativo for iniciado. Sua URL pode ser semelhante ao seguinte:

 `http://servername/WindowsApp1.application?username=joeuser`

 Os dois procedimentos a seguir mostram como usar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo para obter informações de cadeia de caracteres de consulta.

> [!NOTE]
> Você só pode passar informações em uma cadeia de caracteres de consulta quando seu aplicativo está sendo iniciado usando HTTP, em vez de usar um compartilhamento de arquivos ou o sistema de arquivos local.

 O primeiro procedimento mostra como seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo pode usar uma pequena parte do código para ler esses valores quando o aplicativo é iniciado.

 O procedimento a seguir mostra como configurar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando MageUI.exe para que ele possa aceitar parâmetros de cadeia de caracteres de consulta. Você precisará fazer isso sempre que publicar seu aplicativo.

> [!NOTE]
> Consulte a seção "segurança" mais adiante neste tópico antes de tomar uma decisão para habilitar esse recurso.

 Para obter informações sobre como criar uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação usando *Mage.exe* ou *MageUI.exe*, consulte [passo a passos: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).

> [!NOTE]
> A partir do .NET Framework 3,5 SP1, é possível passar argumentos de linha de comando para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo offline. Se você quiser fornecer argumentos para o aplicativo, poderá passar parâmetros para o arquivo de atalho com o. Extensão APPREF-MS.

### <a name="to-obtain-query-string-information-from-a-clickonce-application"></a>Para obter informações de cadeia de caracteres de consulta de um aplicativo ClickOnce

1. Coloque o código a seguir em seu projeto. Para que esse código funcione, você precisará ter uma referência a System. Web e adicionar `using` ou a `Imports` diretivas para System. Web, System. Collections. especializadas e System. Deployment. Application.

     [!code-csharp[ClickOnceQueryString#1](../deployment/codesnippet/CSharp/how-to-retrieve-query-string-information-in-an-online-clickonce-application_1.cs)]
     [!code-vb[ClickOnceQueryString#1](../deployment/codesnippet/VisualBasic/how-to-retrieve-query-string-information-in-an-online-clickonce-application_1.vb)]

2. Chame a função definida anteriormente para recuperar um <xref:System.Collections.DictionaryBase.Dictionary%2A> dos parâmetros de cadeia de caracteres de consulta, indexados por nome.

### <a name="to-enable-query-string-passing-in-a-clickonce-application-with-mageuiexe"></a>Para habilitar a passagem de cadeia de caracteres de consulta em um aplicativo ClickOnce com MageUI.exe

1. Abra o prompt de comando do .NET e digite:

   ```cmd
   MageUI
   ```

2. No menu **arquivo** , selecione **abrir**e abra o manifesto de implantação para seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo, que é o arquivo que termina na `.application` extensão.

3. Selecione o painel **Opções de implantação** na janela de navegação à esquerda e marque a caixa de seleção **permitir que os parâmetros de URL sejam passados para o aplicativo** .

4. No menu **arquivo** , selecione **salvar**.

> [!NOTE]
> Como alternativa, você pode habilitar a passagem da cadeia de caracteres de consulta [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] . Marque a caixa de seleção **permitir que os parâmetros de URL sejam passados para o aplicativo** , que pode ser encontrado abrindo as **Propriedades do projeto**, selecionando a guia **publicar** , clicando no botão **Opções** e, em seguida, selecionando **manifestos**.

## <a name="robust-programming"></a>Programação robusta
 Ao usar parâmetros de cadeia de caracteres de consulta, você deve dar uma consideração cuidadosa sobre como seu aplicativo está instalado e ativado. Se seu aplicativo estiver configurado para ser instalado no computador do usuário da Web ou de um compartilhamento de rede, é provável que o usuário ative o aplicativo apenas uma vez por meio da URL. Depois disso, o usuário geralmente ativará seu aplicativo usando o atalho no menu **Iniciar** . Como resultado, seu aplicativo tem a garantia de receber argumentos de cadeia de caracteres de consulta apenas uma vez durante seu tempo de vida. Se você optar por armazenar esses argumentos na máquina do usuário para uso futuro, você será responsável por armazená-los de maneira segura e protegida.

 Se seu aplicativo estiver somente online, ele sempre será ativado por meio de uma URL. No entanto, mesmo nesse caso, seu aplicativo deve ser escrito para funcionar corretamente se os parâmetros da cadeia de caracteres de consulta estiverem ausentes ou corrompidos.

## <a name="net-framework-security"></a>Segurança do .NET Framework
 Permita passar parâmetros de URL para seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo somente se você planeja limpar a entrada de qualquer caractere mal-intencionado antes de usá-lo. Uma cadeia de caracteres inserida com aspas, barras ou pontos-e-vírgulas, por exemplo, pode executar operações de dados arbitrárias se usadas não filtradas em uma consulta SQL em um banco de dados. Para obter mais informações sobre a segurança de cadeia de caracteres de consulta, consulte [visão geral de explorações de script](https://msdn.microsoft.com/Library/772c7312-211a-4eb3-8d6e-eec0aa1dcc07).

## <a name="see-also"></a>Veja também
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)

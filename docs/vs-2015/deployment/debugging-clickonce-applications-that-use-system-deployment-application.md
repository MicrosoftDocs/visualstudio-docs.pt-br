---
title: Depurando aplicativos ClickOnce que usam System.Deployment.Application | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c0b12faf451d3ed9bb70e2bb1ec6c8503cfb86d5
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58928048"
---
# <a name="debugging-clickonce-applications-that-use-systemdeploymentapplication"></a>Depurando aplicativos ClickOnce que usam System.Deployment.Application
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação permite que você configure como um aplicativo é atualizado. No entanto, se você precisar usar e personalizar advanced [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] recursos de implantação, você precisará acessar o modelo de objeto de implantação fornecido pelo <xref:System.Deployment.Application>. Você pode usar o <xref:System.Deployment.Application> APIs para tarefas avançadas, como:  
  
- Criar uma opção "Atualizar agora" em seu aplicativo  
  
- Downloads de sob demanda condicionais, de vários componentes do aplicativo  
  
- Integrado diretamente ao aplicativo de atualizações  
  
- Garantindo que o aplicativo cliente está sempre atualizado  
  
  Porque o <xref:System.Deployment.Application> APIs funcionam apenas quando um aplicativo é implantado com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] tecnologia, a única maneira de depurá-los é implantar o aplicativo usando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], anexar a ele e, em seguida, depurá-lo. Pode ser difícil anexar o depurador antecipada suficiente, pois esse código é executado com frequência quando o aplicativo é iniciado e é executado antes que você pode anexar o depurador. Uma solução é colocar quebras (ou é interrompido, para projetos do Visual Basic) antes de seu código de verificação de atualização ou o código sob demanda.  
  
  A técnica recomendada de depuração é da seguinte maneira:  
  
1. Antes de começar, verifique se o símbolo (. PDB) e arquivos de origem são arquivados.  
  
2. Implante a versão 1 do aplicativo.  
  
3. Crie uma nova solução em branco. Dos **arquivo** menu, clique em **New**, em seguida, **projeto**. No **novo projeto** caixa de diálogo, abra o **Other Project Types** nó, em seguida, selecione o **soluções do Visual Studio** pasta. No **modelos** painel, selecione **solução em branco**.  
  
4. Adicione o local de origem arquivados para as propriedades para essa nova solução. Na **Gerenciador de soluções**, clique com botão direito no nó da solução e clique **propriedades**. No **páginas de propriedades** caixa de diálogo, selecione **depurar arquivos fonte**, em seguida, adicione o diretório do código-fonte arquivado. Caso contrário, o depurador encontrará os arquivos de origem desatualizadas, uma vez que os caminhos de arquivo de origem são registrados no arquivo. PDB. Se o depurador usa arquivos de origem desatualizadas, você verá uma mensagem informando que a origem não corresponde.  
  
5. Verifique se que o depurador pode localizar os arquivos. PDB. Se você tiver implantado-los com o seu aplicativo, o depurador localiza automaticamente. Ele sempre se parece ao lado do assembly em questão pela primeira vez. Caso contrário, você precisará adicionar o caminho de arquivo morto para a **locais de arquivo (. PDB) de símbolo** (para acessar essa opção, da **ferramentas** menu, clique em **opções**, em seguida, abra o  **Depurando** nó e clique em **símbolos**).  
  
6. Depurar o que acontece entre o `CheckForUpdate` e `Download` / `Update` chamadas de método.  
  
    Por exemplo, o código de atualização pode ser da seguinte maneira:  
  
   ```  
       Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
           If My.Application.Deployment.IsNetworkDeployed Then  
  
               If (My.Application.Deployment.CheckForUpdate()) Then  
  
                   My.Application.Deployment.Update()  
                   Application.Restart()  
  
               End If  
  
           End If  
       End Sub  
   ```  
  
7. Implante a versão 2.  
  
8. Tentativa de anexar o depurador ao aplicativo versão 1, ele baixa uma atualização para a versão 2. Como alternativa, você pode usar o `System.Diagnostics.Debugger.Break` método ou simplesmente `Stop` no Visual Basic. Obviamente, você não deve deixar essas chamadas de método no código de produção.  
  
    Por exemplo, suponha que você estiver desenvolvendo um aplicativo do Windows Forms, e você tiver um manipulador de eventos para esse método com a lógica de atualização nela. Para depurar isso, basta anexar antes que o botão é pressionado e definir um ponto de interrupção (certifique-se de que você abre o arquivo morto apropriado e defina o ponto de interrupção lá).  
  
   Use o <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> propriedade para invocar o <xref:System.Deployment.Application> APIs somente quando o aplicativo é implantado; as APIs não deve ser invocadas durante a depuração em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Deployment.Application>

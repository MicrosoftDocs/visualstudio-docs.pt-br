---
title: Depurar aplicativos ClickOnce que usam System. Deployment. Application
ms.date: 11/04/2016
ms.topic: how-to
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 203f1edc2e29bbbc34fb39e6aa01c1b56bf20e91
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382647"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>Depurar aplicativos ClickOnce que usam System.Deployment.Application
No [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] , [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] a implantação permite que você configure como um aplicativo é atualizado. No entanto, se você precisar usar e personalizar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] recursos de implantação avançados, será necessário acessar o modelo de objeto de implantação fornecido pelo <xref:System.Deployment.Application> . Você pode usar as <xref:System.Deployment.Application> APIs para tarefas avançadas, como:

- Criando uma opção "atualizar agora" em seu aplicativo

- Downloads condicionais e sob demanda de vários componentes de aplicativos

- Atualizações integradas diretamente ao aplicativo

- Garantindo que o aplicativo cliente esteja sempre atualizado

  Como as <xref:System.Deployment.Application> APIs só funcionam quando um aplicativo é implantado com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] tecnologia, a única maneira de depurá-las é implantar o aplicativo usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] , anexá-lo e depurá-lo. Pode ser difícil anexar o depurador cedo o suficiente, pois esse código geralmente é executado quando o aplicativo é iniciado e executado antes que você possa anexar o depurador. Uma solução é fazer interrupções (ou interrupções, para projetos Visual Basic) antes do código de verificação de atualização ou código sob demanda.

  A técnica de depuração recomendada é a seguinte:

1. Antes de começar, verifique se o símbolo (. pdb) e os arquivos de origem estão arquivados.

2. Implante a versão 1 do aplicativo.

3. Crie uma nova solução em branco. No menu **Arquivo**, clique em **Novo** e, em seguida em **Projeto**. Na caixa de diálogo **novo projeto** , abra o nó **outros tipos de projeto** e, em seguida, selecione a pasta **soluções do Visual Studio** . No painel **modelos** , selecione **solução em branco**.

4. Adicione o local de origem arquivado às propriedades dessa nova solução. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó da solução e clique em **Propriedades**. Na caixa de diálogo **páginas de propriedades** , selecione **depurar arquivos de origem**e, em seguida, adicione o diretório do código-fonte arquivado. Caso contrário, o depurador encontrará os arquivos de origem desatualizados, já que os caminhos do arquivo de origem são registrados no arquivo. pdb. Se o depurador usar arquivos de origem desatualizados, você verá uma mensagem informando que a origem não corresponde.

5. Verifique se o depurador pode encontrar os arquivos *. pdb* . Se você os tiver implantado com seu aplicativo, o depurador os encontrará automaticamente. Ele sempre aparece ao lado do assembly em questão primeiro. Caso contrário, será necessário adicionar o caminho de arquivo morto para os **locais de arquivos de símbolo (. pdb)** (para acessar essa opção, no menu **ferramentas** , clique em **Opções**, abra o nó **depuração** e clique em **símbolos**).

6. Depurar o que acontece entre `CheckForUpdate` as `Download` / `Update` chamadas de método e.

    Por exemplo, o código de atualização pode ser o seguinte:

   ```vb
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

8. Tentativa de anexar o depurador ao aplicativo da versão 1, pois ele baixa uma atualização para a versão 2. Como alternativa, você pode usar o `System.Diagnostics.Debugger.Break` método ou simplesmente `Stop` em Visual Basic. É claro que você não deve deixar essas chamadas de método no código de produção.

    Por exemplo, suponha que você esteja desenvolvendo um aplicativo Windows Forms e tenha um manipulador de eventos para esse método com a lógica de atualização nele. Para depurar isso, basta anexar antes de o botão ser pressionado e, em seguida, definir um ponto de interrupção (certifique-se de abrir o arquivo arquivado apropriado e definir o ponto de interrupção nele).

   Use a <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> propriedade para invocar as <xref:System.Deployment.Application> APIs somente quando o aplicativo for implantado; as APIs não devem ser invocadas durante a depuração no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

## <a name="see-also"></a>Confira também
- <xref:System.Deployment.Application>
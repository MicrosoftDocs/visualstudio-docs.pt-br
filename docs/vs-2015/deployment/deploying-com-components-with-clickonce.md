---
title: Implantando componentes do COM o ClickOnce | Microsoft Docs
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
- registration-free COM deployment
- ClickOnce deployment, COM components
- COM components, deploying
- deploying applications [ClickOnce], COM components
- components, deploying
ms.assetid: 1a4c7f4c-7a41-45f2-9af4-8b1666469b89
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 8f4412c067ffd43a14a62cc722cf60ca1a883d9f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49820285"
---
# <a name="deploying-com-components-with-clickonce"></a>Implantando componentes do COM com o ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Implantação de componentes legados COM tradicionalmente tem sido uma tarefa difícil. Componentes precisam ser registrados globalmente e, portanto, podem causar efeitos colaterais indesejáveis entre aplicativos sobrepostos. Essa situação geralmente não é um problema em aplicativos .NET Framework porque componentes são completamente isolados para um aplicativo ou são compatíveis com o lado a lado. Visual Studio permite que você implante os componentes isolados no Windows XP ou o sistema de operacional superior.  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Fornece um mecanismo fácil e seguro para implantar seus aplicativos .NET. No entanto, se seus aplicativos usam componentes herdados, você precisará executar etapas adicionais para implantá-los. Este tópico descreve como implantar componentes isolados e fazer referência a componentes nativos (por exemplo, do Visual Basic 6.0 ou Visual C++).  
  
 Para obter mais informações sobre como implantar componentes do COM isolado, consulte "Simplifique a implantação de aplicativo com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] e COM sem registro" em [ http://msdn.microsoft.com/msdnmag/issues/05/04/RegFreeCOM/default.aspx ](http://msdn.microsoft.com/msdnmag/issues/05/04/RegFreeCOM/default.aspx).  
  
## <a name="registration-free-com"></a>COM sem registro  
 COM sem registro é uma tecnologia nova para implantar e ativar os componentes isolados. Ele funciona, colocando a biblioteca de tipos de todas as do componente e informações de registro que normalmente são instaladas no registro do sistema em um arquivo XML chamado um manifesto, armazenados na mesma pasta que o aplicativo.  
  
 Um componente COM o isolamento requer que ele ser registrado no computador de desenvolvedor, mas ele não precisa ser registrado no computador do usuário final. Para isolar um componente COM, tudo o que você precisa fazer é definir sua referência **isolado** propriedade **verdadeiro**. Por padrão, essa propriedade é definida como **falsos**, indicando que ele deve ser tratado como uma referência COM registrados. Se essa propriedade estiver **verdadeira**, faz com que um manifesto a ser gerado para esse componente em tempo de compilação. Ele também faz com que os arquivos correspondentes a serem copiados para a pasta do aplicativo durante a instalação.  
  
 Quando o gerador de manifesto encontra uma referência COM isolado, ele enumera todos os `CoClass` entradas na biblioteca de tipos do componente, correspondência de cada entrada com seus dados de registro correspondente e geração de manifesto definições para todos os o COM classes no arquivo de biblioteca de tipo.  
  
## <a name="deploying-registration-free-com-components-using-clickonce"></a>Implantação de componentes COM sem registro usando o ClickOnce  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] tecnologia de implantação é bem adequada para a implantação de componentes COM isolado, pois ambos [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] e COM sem registro exigem que um componente tem um manifesto para ser implantado.  
  
 Normalmente, o autor do componente deve fornecer um manifesto. Caso contrário, no entanto, o Visual Studio é capaz de gerar um manifesto automaticamente para um componente COM. A geração de manifesto é executada durante o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] processo de publicação; para obter mais informações, consulte [publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md). Esse recurso também permite que você aproveite os componentes herdados que você criou em ambientes de desenvolvimento anteriores, como Visual Basic 6.0.  
  
 Há duas maneiras que [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implanta componentes COM:  
  
-   Usar o bootstrapper para implantar seus componentes COM. Isso funciona em todas as plataformas com suporte.  
  
-   Use a implantação do componente nativo isolamento (também conhecido como COM sem registro). No entanto, isso só funcionará em um sistema de operacional superior ou o Windows XP.  
  
### <a name="example-of-isolating-and-deploying-a-simple-com-component"></a>Exemplo de isolar e implantação de um componente COM simples  
 Para demonstrar a implantação de componentes COM sem registro, este exemplo criará um aplicativo baseado em Windows no Visual Basic que faz referência a um componente COM nativo isolado criado usando o Visual Basic 6.0 e implantá-lo usando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
 Primeiro, você precisará criar o componente COM nativo:  
  
##### <a name="to-create-a-native-com-component"></a>Para criar um componente COM nativo  
  
1.  Usando o Visual Basic 6.0, do **arquivo** menu, clique em **New**, em seguida, **projeto**.  
  
2.  No **novo projeto** caixa de diálogo, selecione o **Visual Basic** nó e selecione uma **ActiveX DLL** projeto. Na caixa **Nome**, digite `VB6Hello`.  
  
    > [!NOTE]
    >  Somente tipos de projeto ActiveX DLL e o controle ActiveX são compatíveis com o COM sem registro; Não há suporte para tipos de projeto EXE ActiveX e documento ActiveX.  
  
3.  Na **Gerenciador de soluções**, clique duas vezes em **Class1.vb** para abrir o editor de texto.  
  
4.  No Class1. vb, adicione o código a seguir após o código gerado para o `New` método:  
  
    ```  
    Public Sub SayHello()  
       MsgBox "Message from the VB6Hello COM component"  
    End Sub  
    ```  
  
5.  Crie o componente. Dos **construir** menu, clique em **compilar solução**.  
  
> [!NOTE]
>  COM sem registro dá suporte somente DLLs e COM controles de tipos de projeto. É possível usar EXEs com sem registro COM.  
  
 Agora você pode criar um aplicativo baseado em Windows e adicione uma referência ao componente COM a ele.  
  
##### <a name="to-create-a-windows-based-application-using-a-com-component"></a>Para criar um aplicativo baseado em Windows usando um componente COM  
  
1. Usando o Visual Basic, do **arquivo** menu, clique em **New**, em seguida, **projeto**.  
  
2. No **novo projeto** caixa de diálogo, selecione o **Visual Basic** nó e selecione **aplicativo Windows**. Na caixa **Nome**, digite `RegFreeComDemo`.  
  
3. Na **Gerenciador de soluções**, clique no **Mostrar todos os arquivos** botão para exibir as referências do projeto.  
  
4. Clique com botão direito do **referências** nó e selecione **adicionar referência** no menu de contexto.  
  
5. No **adicionar referência** caixa de diálogo, clique o **procurar** guia, navegue até VB6Hello.dll e selecioná-lo.  
  
    Um **VB6Hello** referência será exibida na lista de referências.  
  
6. Aponte para o **caixa de ferramentas**, selecione um **botão** controlar e arraste-o para o **Form1** formulário.  
  
7. No **propriedades** janela, defina o botão **texto** propriedade a ser **Hello**.  
  
8. Clique duas vezes no botão para adicionar o código do manipulador e no arquivo de código, adicione código para que o manipulador diz o seguinte:  
  
   ```  
   Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim VbObj As New VB6Hello.Class1  
       VbObj.SayHello()  
   End Sub  
   ```  
  
9. Execute o aplicativo. Dos **Debug** menu, clique em **iniciar depuração**.  
  
   Em seguida, você precisa isolar o controle. Cada componente COM que o aplicativo usa é representado no seu projeto como uma referência COM. Essas referências são visíveis sob o **referências** nó na **Gerenciador de soluções** janela. (Observe que você pode adicionar referências diretamente usando o **adicionar referência** comando as **projeto** menu, ou indiretamente, arrastando um controle ActiveX para seu formulário.)  
  
   As etapas a seguir mostram como isolar o componente COM e publicar o aplicativo atualizado que contém o controle isolado:  
  
##### <a name="to-isolate-a-com-component"></a>Para isolar um componente COM  
  
1. Na **Gerenciador de soluções**, no **referências** nó, selecione o **VB6Hello** referência.  
  
2. No **propriedades** janela, altere o valor da **isolado** propriedade de **falso** para **True**.  
  
3. Dos **construir** menu, clique em **compilar solução**.  
  
   Agora, quando você pressionar F5, o aplicativo funciona conforme o esperado, mas ele está em execução em COM. sem registro Para provar isso, tente cancelar o registro do componente VB6Hello.dll e executando RegFreeComDemo1.exe fora do IDE do Visual Studio. Desta vez, quando o botão é clicado, ele ainda funcionará. Se você renomeie temporariamente o manifesto do aplicativo, ele novamente falhará.  
  
> [!NOTE]
>  Você pode simular a ausência de um componente COM temporariamente cancelar o registro. Abra um prompt de comando, vá para a pasta do sistema digitando `cd /d %windir%\system32`, em seguida, cancelar o registro do componente digitando `regsvr32 /u VB6Hello.dll`. Você pode registrá-lo novamente, digitando `regsvr32 VB6Hello.dll`.  
  
 A etapa final é publicar o aplicativo usando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]:  
  
##### <a name="to-publish-an-application-update-with-an-isolated-com-component"></a>Para publicar uma atualização de aplicativo com o componente isolado COM  
  
1. Dos **construir** menu, clique em **RegFreeComDemo publicar**.  
  
    O Assistente de Publicação será exibido.  
  
2. No Assistente de publicação, especifique um local no disco do computador local em que você pode acessar e examinar os arquivos publicados.  
  
3. Clique em **concluir** para publicar o aplicativo.  
  
   Se você examinar os arquivos publicados, você observará que o arquivo Sysmon seja incluído. O controle é totalmente isolado para este aplicativo, o que significa que, se o computador do usuário final tiver outro aplicativo usando uma versão diferente do controle, não possam interferir com este aplicativo.  
  
## <a name="referencing-native-assemblies"></a>Referenciando Assemblies nativos  
 Visual Studio dá suporte a referências nativas do Visual Basic 6.0 ou assemblies C++; Essas referências são chamadas referências nativas. Você pode dizer se uma referência é nativa, verificando se seu **tipo de arquivo** estiver definida como **nativo** ou **ActiveX**.  
  
 Para adicionar uma referência nativa, use o **adicionar referência** de comando, em seguida, navegue até o manifesto. Alguns componentes colocam o manifesto dentro da DLL. Nesse caso, você pode simplesmente escolher a própria DLL e o Visual Studio irá adicioná-lo como uma referência nativa se detectar que o componente contém um manifesto inserido. Visual Studio incluirá automaticamente todos os arquivos dependentes ou assemblies listados no manifesto, se eles estiverem na mesma pasta que o componente referenciado.  
  
 Isolamento de controle COM torna mais fácil de implantar os componentes COM que ainda não tenham manifestos. No entanto, se um componente é fornecido com um manifesto, você pode referenciar diretamente o manifesto. Na verdade, você sempre deve usar o manifesto fornecido pelo autor do componente, sempre que possível em vez de usar o **isolado** propriedade.  
  
## <a name="limitations-of-registration-free-com-component-deployment"></a>Limitações da implantação de componente COM sem registro  
 COM sem registro fornece vantagens claras sobre técnicas de implantação tradicionais. No entanto, há algumas limitações e restrições que também é importante ressaltar. A maior limitação é que ele só funciona no Windows XP ou superior. A implementação de COM sem registro necessárias alterações para a maneira na qual os componentes são carregados no sistema operacional principal. Infelizmente, não há nenhuma camada de suporte de nível inferior para COM. sem registro  
  
 Nem todo componente é um candidato adequado para COM. sem registro Um componente não é um adequado se qualquer uma das seguintes opções for verdadeira:  
  
- O componente é um servidor fora do processo. Não há suporte para servidores EXE; há suporte para apenas DLLs.  
  
- O componente faz parte do sistema operacional, ou é um componente do sistema, como XML, o Internet Explorer ou o Microsoft Data Access Components (MDAC). Você deve seguir a política de redistribuição do autor do componente; Verifique com seu fornecedor.  
  
- O componente faz parte de um aplicativo, como o Microsoft Office. Por exemplo, você não deve tentar isolar o modelo de objeto do Microsoft Excel. Isso faz parte do Office e só pode ser usado em um computador com o produto completo do Office instalado.  
  
- O componente é destinado para uso como um suplemento ou um snap-in, por exemplo um suplemento do Office ou um controle em um navegador da Web. Tais componentes geralmente exigem algum tipo de esquema de registro definido pelo ambiente de hospedagem está além do escopo do manifesto em si.  
  
- O componente gerencia um dispositivo físico ou virtual para o sistema, por exemplo, um driver de dispositivo para o spooler de impressão.  
  
- O componente é redistribuível de acesso a dados. Aplicativos de dados geralmente requerem separado de acesso a dados redistribuível ser instalado antes de serem executados. Você não deve tentar isolar os componentes, como o controle de dados do Microsoft ADO, OLE DB Microsoft ou Microsoft Data Access Components (MDAC). Em vez disso, se seu aplicativo usa MDAC ou SQL Server Express, você deve defini-los como pré-requisitos; ver [como: instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md).  
  
  Em alguns casos, talvez seja possível para o desenvolvedor do componente de refazer o design para COM. sem registro Se isso não for possível, você pode criar e publicar aplicativos que dependem deles por meio do esquema padrão do registro usando o Bootstrapper. Para obter mais informações, consulte [criação de pacotes de Bootstrapper](../deployment/creating-bootstrapper-packages.md).  
  
  Um componente COM só pode ser isolado uma vez por aplicativo. Por exemplo, é possível isolar o mesmo componente COM de duas diferentes **biblioteca de classes** projetos que fazem parte do mesmo aplicativo. Isso resultará em um aviso de compilação e o aplicativo falhará ao carregar o tempo de execução. Para evitar esse problema, a Microsoft recomenda que você encapsula componentes COM em uma única biblioteca de classes.  
  
  Há vários cenários que COM registro é necessário no computador de desenvolvedor, mesmo que a implantação do aplicativo não requer registro. O `Isolated` propriedade requer que o componente COM ser registrado no computador de desenvolvedor para gerar o manifesto durante a compilação. Não há nenhum recurso de registro de captura que invocam o auto-registro durante a compilação. Além disso, todas as classes não são explicitamente definidas na biblioteca de tipos não serão refletidas no manifesto. Ao usar um componente COM um manifesto já existente, como uma referência nativa, o componente não precisará ser registrado no momento do desenvolvimento. No entanto, o registro é necessário se o componente é um controle ActiveX e você desejar para incluí-lo na **caixa de ferramentas** e o designer de formulários do Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)




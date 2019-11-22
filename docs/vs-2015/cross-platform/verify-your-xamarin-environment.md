---
title: Verificar o ambiente do Xamarin | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: fd39882e-06d1-4b39-80d2-4d07b6e4f8f5
caps.latest.revision: 15
ms.author: crdun
manager: crdun
ms.openlocfilehash: 134ed47d26fb7afb50bb50ac18418b436a563eb6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297591"
---
# <a name="verify-your-xamarin-environment"></a>Verificar o ambiente do Xamarin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depois de ter concluído os instaladores (consulte [Configurar e instalar](../cross-platform/setup-and-install.md)), reserve alguns minutos para verificar se tudo está pronto para experimentar o desenvolvimento do Xamarin.  
  
 Depois de concluir essas verificações, você pode seguir uma ou ambas as instruções a seguir:  
  
- [Aprender as noções básicas de criação de aplicativos com o Xamarin.Forms no Visual Studio](../cross-platform/learn-app-building-basics-with-xamarin-forms-in-visual-studio.md)  
  
- [Criar aplicativos com interface do usuário nativa usando o Xamarin no Visual Studio](../cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md)  
  
## <a name="all-platforms"></a>Todas as Plataformas  
 Primeiro, selecione **Ferramentas > Opções**, expanda **Xamarin > Outros** e clique no link **Verificar agora** para obter as atualizações. Você precisa usar o Xamarin 4.0.3.214 ou posterior para evitar problemas de licenciamento anteriores.  
  
 Em seguida, crie uma nova solução do Xamarin no Visual Studio usando **Arquivo > Novo Projeto**, em seguida, na caixa de diálogo, expanda **Modelos > Outros Idiomas > Visual C# > Multiplataforma**, selecione **Aplicativo em Branco (Nativo Portátil)** e clique em OK. Isso cria uma solução com um projeto de biblioteca de classes portátil compartilhado e projetos individuais para Android, iOS e Windows:  
  
 ![Resultados da criação de um novo projeto do modelo portátil &#40;&#41; nativo do aplicativo em branco](../cross-platform/media/crossplat-xamarin-verify-1.png "CrossPlat Xamarin Verify 1")  
  
> [!NOTE]
> Se os modelos não estiverem lá, consulte [os modelos de projeto do Xamarin ausentes? Tente isso](#missing) na parte inferior desta página.  
  
## <a name="android"></a>Android  
  
1. Verifique se você tem as ferramentas mais recentes do SDK do Android instaladas, acessando **Ferramentas > Android > Gerenciador de SDK do Android** e instalando a versão mais recente das ferramentas do SDK do Android, ferramentas da plataforma do Android SDK e componentes de ferramentas de build do SDK do Android. Observe que não é sempre necessário instalar o nível da API do Android mais recente; a API necessária depende do nível da plataforma de destino. Em geral, a instalação do Xamarin instalará o nível de plataforma que ele exige.  

2. Valide o Android Designer: no projeto do Android no Gerenciador de Soluções, abra **Recursos &gt; Layout &gt; arquivo Main.axml**. (Se você não estiver vendo esse arquivo diretamente, tente pesquisar no Gerenciador de Soluções; ele existe somente no projeto do Android e não no projeto do iOS.)  
  
    - Se você receber um erro informando que "O SDK do Android instalado é muito antigo", clique em **Abrir SDK do Android** na mensagem para selecionar e instalar as ferramentas da versão do SDK mais recentes disponíveis como na etapa 1 acima. 
  
3. Valide o build e a depuração no emulador (ou dispositivo):  
  
    - Clique com o botão direito do mouse no projeto do Android no Gerenciador de Soluções e selecione **Definir como projeto de inicialização**.  
  
         ![Opção Visual Studio Set as StartUp Project](../cross-platform/media/crossplat-xamarin-verify-2.png "CrossPlat Xamarin Verify 2")  
  
    - Selecione um emulador apropriado com base na versão destino Android; se você tiver um dispositivo de desenvolvimento Android conectado ao seu computador, você também o encontrará listado aqui, juntamente com os emuladores:  
  
        - O Windows 8+: selecione um destino do **Emulador VS** na lista suspensa de depuração do Visual Studio conforme mostrado abaixo e inicie o depurador pressionando **F5**. Para obter mais detalhes, consulte [Introduzindo o Emulador do Visual Studio para Android](https://devblogs.microsoft.com/devops/introducing-visual-studios-emulator-for-android/) (blog do Visual Studio ALM). Se você encontrar problemas ao obter o emulador, consulte [Solução de problemas de Emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md). Você também pode criar novos perfis de dispositivo para o emulador selecionando **Ferramentas > Emulador do Visual Studio para Android...** .  
  
             ![Selecionando o emulador do Visual Studio para Android como um destino de depuração](../cross-platform/media/crossplat-xamarin-verify-3.png "Verificação do CrossPlat Xamarin 3")  
  
             Observação: se você não vir a opção de menu **Ferramentas > Emulador do Visual Studio para Android...** , você poderá não ter o emulador autoinstalado. Vá para o **Painel de Controle > Programas e Recursos**, selecione **Microsoft Visual Studio** e clique em **Alterar** para executar novamente o instalador. Clique em **Modificar** no instalador, marque a caixa de **Desenvolvimento Móveis de Multiplataforma > Emulador do Microsoft Visual Studio para Android** e clique em **Atualização**.  
  
        - Para o Windows 7 ou anterior: selecione o Xamarin Player para Android no menu suspenso em vez disso e pressione F5 para executá-lo. Para obter detalhes sobre o Xamarin Player, seu gerenciador de dispositivos e dicas de solução de problemas, leia [Xamarin Android Player](https://docs.microsoft.com/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows) (xamarin.com).  
  
> [!NOTE]
> No Visual Studio, você pode perceber a presença do botão Gerenciador de Emulador Android (AVD) na barra de ferramentas (mostrado abaixo), que abre o gerenciador de dispositivos é usado especificamente para configurar o emulador do Android da Google.  Isso não tem impacto no Emulador do Visual Studio para Android ou o Xamarin Player, cada qual com seu próprio gerenciador de dispositivos para configurar perfis.  Consulte [Introduzindo o Emulador do Visual Studio para Android](https://devblogs.microsoft.com/devops/introducing-visual-studios-emulator-for-android/) (blog do Visual Studio ALM) e [Xamarin Android Player](https://docs.microsoft.com/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows) (xamarin.com) para obter detalhes.  
> ![CrossPlat Xamarin Verificação 7](../cross-platform/media/crossplat-xamarin-verify-7.png "Verificação do CrossPlat Xamarin 7")  
  
## <a name="windows-phone"></a>Windows Phone  
  
1. Valide o designer do Windows Phone: no projeto do Windows Phone no Gerenciador de Soluções, abra o arquivo **MainPage.xaml**.  
  
2. Valide o build e a depuração no emulador ou em um dispositivo (observação: você precisará ter o emulador do Windows Phone instalado na instalação do Visual Studio para essa etapa ou um dispositivo vinculado):  
  
    - Clique com o botão direito do mouse no projeto do Windows Phone no Gerenciador de Soluções e selecione **Definir como projeto de inicialização**.  
  
    - Selecione um destino do **Emulador 8.1** ou um dispositivo anexado na lista suspensa de depuração do Visual Studio conforme mostrado abaixo e inicie o depurador pressionando F5.  
  
         ![Selecionando um emulador de Windows Phone como um destino de depuração](../cross-platform/media/crossplat-xamarin-verify-4.png "CrossPlat Xamarin verificação 4")  
  
    - Se você encontrar problemas ao obter o emulador, consulte [Solução de problemas de Emulador do Windows Phone 8](https://msdn.microsoft.com/library/windows/apps/jj681694.aspx).  
  
## <a name="ios"></a>iOS  
  
1. Verifique se seu Mac está disponível na rede e emparelhado com o Visual Studio, conforme descrito em [Conectando-se ao Mac](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/) (xamarin.com).  
  
2. Valide o designer do storyboard: no projeto do iOS no Gerenciador de Soluções, abra o arquivo **Main.storyboard**. Aqui, o Visual Studio hospeda o designer que executará remotamente o Mac.  
  
3. Validar compilação e depuração:  
  
    1. Clique com o botão direito do mouse no projeto do iOS no Gerenciador de Soluções e selecione **Definir como projeto de inicialização**.  
  
    2. Selecione o destino do **iPhoneSimulator** na lista suspensa incorporada do Visual Studio, conforme mostrado abaixo ou o destino do **iPhone** se você tiver um dispositivo vinculado. Se nenhum simulador estiver listado, inicie o Xcode no Mac, selecione **Xcode->Preferências** e clique em **Baixar**. Em **Componentes** você deve ver as versões de simulador que estão disponíveis para download. Instruções adicionais para depuração podem ser encontradas na página [Depuração](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) do Xamarin (xamarin.com).  
  
         ![Selecionando o destino de compilação iPhoneSimulator](../cross-platform/media/crossplat-xamarin-verify-5.png "Verificação do CrossPlat Xamarin 5")  
  
    3. Selecione um destino do iPhone na lista suspensa de depuração do Visual Studio conforme mostrado abaixo e inicie o depurador pressionando F5. Isso inicia o simulador no Mac em que você poderá interagir com o aplicativo enquanto a depuração acontecer no Visual Studio. Se você tiver um físico iPhone ou iPad conectado ao Mac, ele aparecerá aqui e você pode selecioná-lo em vez disso. Se você não vir dispositivos ou simuladores listados, verifique a conexão para o Mac revisando o tópico vinculado na etapa 1 acima ou indo para **Ferramentas** >**iOS** >**Agente do Xamarin Mac**  
  
         ![Selecionando um destino de depuração do iPhone](../cross-platform/media/crossplat-xamarin-verify-6.png "Verificação do CrossPlat Xamarin 6")  
  
    4. Se você encontrar problemas ao se conectar ao Mac, leia [Solução de Problemas de Conexão](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/troubleshooting) (xamarin.com).  
  
    5. Se você vir um erro informando "Nenhum perfil de provisionamento instalado corresponde às chaves de assinatura do iOS instaladas", faça o seguinte:  
  
        - Verifique se sua conta da Apple ID está adicionada no Xcode no Mac, conforme descrito em [Adicionar sua Conta ao Xcode](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/AddingYourAccounttoXcode/AddingYourAccounttoXcode.html#//apple_ref/doc/uid/TP40013839-CH40-SW1) (apple.com).  Depois de adicionar sua conta, certifique-se de reiniciar o Visual Studio e o Xcode.  
  
             ![Verificação do CrossPlat Xamarin 8](../cross-platform/media/crossplat-xamarin-verify-8.png "Verificação do CrossPlat Xamarin 8")  
  
        - Verifique se nas propriedades do projeto do iOS na guia de assinatura de pacote de iOS, se o campo de autorização personalizada está vazio para a configuração de depuração ativa.  Observação: você só deverá tentar remover essa configuração se você tiver encontrado a mensagem de erro acima.  
  
## <a name="missing"></a> Os modelos de projeto de Xamarin estão faltando? Experimente isto  
 Modelos poderão estar ausentes se você instalar o Xamarin diretamente do site de Xamarin e você tiver o Visual Studio 2013 e Visual Studio 2015 instalados lado a lado. Porém, é fácil corrigir isso: basta habilitar o recurso **Xamarin para Visual Studio 2015** no programa de instalação do Xamarin.  
  
1. No Painel de Controle, abra **Programas e Recursos**, escolha o item **Xamarin** e clique em **Alterar**.  
  
2. No Assistente de instalação para Xamarin que aparece, clique em **Avançar** e **Alterar**.  
  
3. Na lista de recursos opcionais a serem instalados, expanda **Xamarin para Visual Studio 2015**, escolha **será instalado na unidade local** e clique em **Avançar** para proceder para adicionar o recurso.

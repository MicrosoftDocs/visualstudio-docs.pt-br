---
title: Emulador do Visual Studio para Android | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 80f0104f-a4db-44dd-bd55-37bb67776c62
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 28d82c13273f18f9787104f080ed39c9c903076c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884830"
---
# <a name="visual-studio-emulator-for-android"></a>Emulador do Visual Studio para Android

O Emulador do Visual Studio para Android é um aplicativo de área de trabalho que emula um dispositivo Android. Ele fornece um ambiente virtualizado no qual você pode depurar e testar aplicativos do Android sem um dispositivo físico. Também fornece um ambiente isolado para protótipos de seu aplicativo.  

> [!IMPORTANT]
> Na maioria dos cenários, o emulador do Google Android é recomendado para uso, em vez do Emulador do Visual Studio para Android:
> - Não há suporte para o Emulador do Visual Studio para Android após o Visual Studio 2015.
> - As imagens do emulador posteriores à versão do Android 6.0 não estão disponíveis para o Emulador do Visual Studio para Android.
> - O Google Android Emulator agora é compatível com [Hyper-V](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/hardware-acceleration#hyper-v).
> - As Ferramentas do Visual Studio para Apache Cordova funcionam com o Google Android Emulator. Para obter mais informações, confira [Run your Apache Cordova app on Android](/visualstudio/cross-platform/tools-for-cordova/run-your-app/run-app-android#google-android-emulator) (Executar seu aplicativo Apache Cordova no Android) (observe que você não precisa mais desabilitar o Hyper-V, conforme explicado neste artigo).
>
> Para saber mais de como configurar e usar o Google Android Emulator, confira [Configuração do Android Emulator](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/).
  
 O Emulador do Visual Studio para Android foi projetado para fornecer um desempenho comparável a um dispositivo real. Porém, antes de publicar seu aplicativo, recomendamos que você teste-o em um dispositivo físico.  
  
 Teste seu aplicativo em um perfil de dispositivo exclusivo para cada uma das plataformas Android, resoluções de tela e outras propriedades de hardware com suporte do Emulador do Visual Studio para Android.
  
##  <a name="Installing"></a>Instalação e desinstalação  
 Instalando o  
  
 O Emulador do Visual Studio para Android é um componente das ferramentas de plataforma cruzada disponível no Visual Studio. Ele é instalado durante uma configuração personalizada do Visual Studio, selecionando Desenvolvimento Móvel Multiplataforma, Ferramentas Comuns e Kits de Desenvolvimento de Software e, depois, Emulador do Visual Studio para Android.  
  
 Desinstalando  
  
 Desinstale o Emulador do Visual Studio para Android usando Adicionar ou Remover Programas no Painel de Controle.  
  
> [!NOTE]
>  A desinstalação do Visual Studio não desinstalará o emulador. É necessário desinstalar o emulador separadamente.  
  
 Quando você desinstala o Emulador do Visual Studio para Android, os Adaptadores Virtuais de Ethernet do Hyper-V que foram criados para uso do emulador não são removidos automaticamente. Remova manualmente esses adaptadores virtuais (se não estiverem em uso) abrindo o Gerenciador do Hyper-V, selecionando uma das imagens VHD do emulador, escolhendo a guia Rede e depois **Remover** para cada uma das opções que aparecem nessa guia.  
  
##  <a name="Requirements"></a>Requisitos do sistema e compatibilidade com versões anteriores  
 Para obter informações importantes sobre os requisitos de hardware, software e de configuração do Emulador do Visual Studio para Android, confira o tópico a seguir.  
  
- [Requisitos do sistema para o Emulador do Visual Studio para Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)  
  
  O Emulador do Visual Studio para Android exige o Visual Studio 2015; ele não é compatível com versões anteriores do Visual Studio.  
  
  Novas versões do emulador são instaladas sobre as versões antigas (e podem, em alguns casos, substituir as imagens antigas, descartando as configurações, aplicativos e arquivos instalados nessas imagens).  
  
##  <a name="Networking"></a>Rede no Emulador do Visual Studio para Android  
 A conexão de rede do Emulador do Visual Studio para Android se comporta como a conexão de um computador desktop com as seguintes características:  
  
- O emulador aparece na rede como um dispositivo separado com seu próprio endereço IP.  
  
- Ele não exige qualquer software de rede adicional que não seja instalado com o emulador.  
  
- Ele não está associado a um domínio do Windows.  
  
  Para compreender os recursos de conexão de rede do emulador, pense nele como sendo semelhante a uma conexão Wi-Fi de seu telefone Android na mesma rede. Se um aplicativo em execução em seu telefone puder acessar um recurso de rede pela sua conexão Wi-Fi, um aplicativo em execução no emulador também poderá acessar o mesmo recurso de rede.  
  
  Para saber mais sobre requisitos de rede, confira [Requisitos de sistema para o Emulador do Visual Studio para Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)  
  
  Para saber mais sobre como solucionar problemas de rede, consulte [Solução de problemas do Emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md).  
  
##  <a name="Configuring"></a>Configurar o Emulador do Visual Studio para Android  
 Testar a compatibilidade de seu aplicativo Android com a incrível variedade de hardware Android pode ser um desafio. Telefones e tablets com Android no mercado abrangem uma ampla gama de versões e tamanhos de tela, e veem em muitas configurações de hardware diferentes (RAM, CPUs, arquitetura etc.). O Emulador do Visual Studio para Android simplifica isso usando perfis de dispositivo. Nosso conjunto de perfis de dispositivos representa o hardware mais popular no mercado, incluindo dispositivos da Samsung, Motorola, Sony, LG e outras.  
  
 No Visual Studio 2015, você pode instalar, desinstalar e iniciar os perfis de dispositivo usando o Gerenciador de Emulador. Acesse o Gerenciador de Emulador escolhendo **Ferramentas**, **Emulador do Visual Studio para Android**.  
  
 ![O Gerenciador do Emulador do Visual Studio para Android](../cross-platform/media/android_emu_manager.png "Android_Emu_Manager")  
  
 Por padrão, há quatro perfis de dispositivo previamente instalados (configurações KitKat e Lollipop para telefone 5" e tablets de 7"), conforme indicado pelo texto em branco e ícones. Outros perfis na lista aparecerão esmaecidos até que você escolha o botão **Instalar Perfil** e a instalação seja concluída. Você pode filtrar a lista por Nível de API e clicar na seta de detalhes no lado inferior direito de um perfil para exibir todos os detalhes da configuração.  
  
 Depois de instalar o conjunto de perfis que você gostaria de usar, inicie esses novos perfis diretamente do gerenciador pressionando o botão verde **Reproduzir**. Eles também aparecerão no menu suspenso do destino de depuração em qualquer tipo de projeto móvel de plataforma cruzada do Visual Studio.  
  
##  <a name="FeaturesTest"></a> Recursos que você pode testar no emulador  
 Para obter informações detalhadas sobre os recursos que você pode testar no emulador, confira esta [postagem no blog](https://blogs.msdn.microsoft.com/devops/2014/11/12/introducing-visual-studios-emulator-for-android/).  
  
##  <a name="FeaturesNonTest"></a> Recursos que você não pode testar no emulador  
 A lista a seguir descreve os recursos da plataforma Android que você **não pode** testar no emulador. Teste esses recursos em um dispositivo físico.  
  
-   Bússola  
  
-   Giroscópio  
  
-   Controlador de vibração  
  
-   Brilho. A alteração do nível de brilho do emulador não afetará visualmente a maneira que o dispositivo aparece na tela.  
  
##  <a name="Support"></a> Recursos de suporte  
 Se o computador host atender aos requisitos do sistema e você encontrar um problema não abordado neste guia de solução de problemas:  
  
-   Faça uma pergunta no StackOverflow usando o [emulador do android](http://stackoverflow.com/questions/tagged/android-emulator) e a marca visual-studio.  
  
-   Relate um problema usando a ferramenta Enviar um Smiley no Visual Studio ou no Gerenciador de emulador.  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos do sistema para o Emulador do Visual Studio para Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)   
 [Solução de problemas do emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)

---
title: Solução de problemas do emulador para Android | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f3fb5df4-3aae-40e4-9450-bbe15b0c5af5
caps.latest.revision: 25
ms.author: crdun
manager: crdun
ms.openlocfilehash: c1d8310cb2585dfd2041ce25fd4301b557521911
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068225"
---
# <a name="troubleshooting-the-visual-studio-emulator-for-android"></a>Solução de problemas do emulador do Visual Studio para Android
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


Este tópico contém informações para ajudá-lo a resolver problemas que podem ocorrer quando você estiver usando o emulador do Visual Studio para Android.

> [!WARNING]
>  Quando o emulador está instalado, o programa de instalação verifica os pré-requisitos para executar o software. Ele exibe avisos se os pré-requisitos não estiverem presentes, mas os requisitos não são necessários na instalação.

 Este tópico contém as seções a seguir.

-   [Antes de começar](#BeforeYouStart)

-   [Falha na instalação do emulador](#NoInstall)

-   [Não é possível conectar aos destinos de rede em um domínio ou uma rede corporativa](#DomainNetwork)

-   [Não é possível conectar aos destinos de rede quando as configurações de rede requerem configuração manual](#ManualNetworkConfig)

-   [O emulador inicia lentamente, falha ao iniciar devido a um tempo limite ou devido a erros na implantação do aplicativo](#SlowStart)

-   [O emulador falha ao iniciar](#NoStart2)

-   [O emulador falha ao iniciar (primeira utilização)](#NoStart)

-   [O emulador falha ao iniciar após a instalação do emulador](#NoBoot)

-   [O Visual Studio fica preso tentando implantar o aplicativo no emulador ou o emulador não aparece como um destino de depuração em outros IDEs](#ADB)

-   [O emulador paralisa porque não conseguiu configurar a porta UDP](#XamarinPlayer)

-   [Não é possível anexar o depurador a um projeto do Xamarin](#Skylake)

-   [Falha do emulador ao executar o aplicativo que usa o Google Play Services](#GooglePlay)

-   [A função arrastar e soltar de um arquivo, um APK ou um arquivo zip de memória flash não funcionam](#DragAndDrop)

-   [Resolução de tela incorreta](#Resolution)

-   [Falha do emulador ao renderizar o conteúdo do OpenGL](#OpenGL)

-   [O emulador não responde a gestos multitoque](#Multitouch)

-   [Recursos de suporte](#Support)

##  <a name="BeforeYouStart"></a> Antes de começar
 Antes de iniciar a solução de problemas, pode ser útil examinar os tópicos a seguir:

-   [Requisitos do sistema para o emulador do Visual Studio para Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)

##  <a name="NoInstall"></a> Falha na instalação do emulador
 Se você não tiver o Hyper-V instalado, verá a mensagem a seguir ao tentar instalar o emulador. Você deve ter um computador que esteja habilitado e dê suporte a HyperV.

 ![Android&#95;Emu&#95;Install&#95;Issue](../cross-platform/media/android-emu-install-issue.png "Android_Emu_Install_Issue")

> [!NOTE]
>  Esta mensagem aplica-se ao emulador do Visual Studio para Android e ao emulador do Windows Phone. Windows 8.1 e Windows 10 dão suporte ao emulador.

 Se você vir essa mensagem, verifique o [requisitos de sistema para o emulador do Visual Studio para Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md) para ver se é possível executar o emulador.

##  <a name="DomainNetwork"></a> Não é possível conectar aos destinos de rede em um domínio ou uma rede corporativa
 O emulador do Visual Studio para Android aparece na rede como um dispositivo separado com seu próprio endereço IP. Ele não está associado a um domínio do Windows e não compartilha credenciais de domínio ou grupo de trabalho com o computador host.

 Se sua rede exigir autorização de domínio ou grupo de trabalho para rede básica e conectividade na Internet, entre em contato com o administrador de TI para uma exceção. Essa exceção permite que o computador em desenvolvimento sirva como um computador de limite e para aceitar conexões de dispositivos de rede não ingressadas em domínio como o emulador.

 O emulador do Visual Studio para Android também usa seu próprio conjunto de endereços MAC. Se você não puder acessar recursos da rede ou da Internet do emulador, verifique com o administrador de TI para garantir que os endereços MAC do emulador sejam autorizados em sua rede.

#### <a name="to-view-the-emulators-mac-addresses"></a>Para exibir os endereços de MAC do emulador

1.  Inicialize o emulador.

2.  Na barra de ferramentas do emulador, clique no botão de divisa (>>) para abrir a janela Ferramentas Adicionais.

3.  Na janela Ferramentas Adicionais, clique na guia Rede.

4.  Na página Rede, localize as entradas do endereço físico.

##  <a name="ManualNetworkConfig"></a> Não é possível conectar aos destinos de rede quando as configurações de rede requerem configuração manual
 Para se conectar aos destinos de rede do emulador, a rede deve atender aos seguintes requisitos:

- DHCP. O emulador exige o DHCP, pois configura a si mesmo como um dispositivo separado na rede com seu próprio endereço IP.

- Definições de gateway e DNS configuradas automaticamente. Não é possível definir as configurações de gateway e DNS manualmente para o emulador.

  Se sua rede exigir definições configuradas manualmente, verifique com o administrador de TI como habilitar conectividade de rede para o emulador.

##  <a name="SlowStart"></a> O emulador inicia lentamente, falha ao iniciar devido a um tempo limite ou devido a erros na implantação do aplicativo
 Sob certas condições, o emulador leva vários minutos para iniciar ou não pode ser iniciado devido a um tempo limite. Quando o emulador falha ao iniciar, você vê a seguinte mensagem: `App deployment failed. Please try again`. As seguintes condições podem resultar neste erro.

-   Executando o emulador do Visual Studio para Android de um VHD inicializável. Essa configuração não tem suporte.

-   Um disco rígido com defeito. Considere a possibilidade de executar o programa chkdsk.

-   Um disco rígido precisa ser desfragmentado. Considere a desfragmentação da unidade.

-   Um disco rígido que está quase cheio. Verifique o espaço disponível na unidade.

-   Não há memória suficiente disponível devido a outros aplicativos em execução. Reduza o número de aplicativos que estão consumindo memória ou aumente a memória.

-   Em geral, qualquer fator que esteja contribuindo para o baixo desempenho do sistema. Inicie a solução de problemas com o componente que tem o menor subtotal no Índice de Experiência do Windows,e que pode ser encontrado na página de informações e ferramentas de desempenho do Painel de Controle.

##  <a name="NoStart2"></a> O emulador falha ao iniciar
 Se o emulador estava funcionando anteriormente, mas não funciona agora, execute as tarefas a seguir. Se você estiver usando o emulador pela primeira vez, consulte [O emulador falha ao iniciar (primeira utilização)](#NoStart) antes de tentar estas etapas.

-   Remova qualquer instância do Hyper-V do emulador.

    1.  Feche o Visual Studio.

    2.  Abra o Gerenciador do Hyper-V e interrompa todas as instâncias do Hyper-V do emulador (máquinas virtuais) que já estejam em execução e, possivelmente, em estado corrompido.

    3.  No Gerenciador do Hyper-V, exclua qualquer emulador de VMs.

    4.  Reinicie o computador.

-   Verifique se que você tem pelo menos 4 GB de memória de sistema e que não esteja sendo consumida por outros programas e processos de uso intensivo de recursos (por exemplo, tente fechar todas as janelas navegador).

-   No Gerenciador do Hyper-V, abra o Gerenciador de Comutador Virtual e verifique se você tem dois comutadores de rede; verifique se o primeiro é o comutador interno e o segundo é o externo.

     ![Android&#95;Emu&#95;V&#95;Switch&#95;Man](../cross-platform/media/android-emu-v-switch-man.png "Android_Emu_V_Switch_Man")

     Se a configuração estiver incorreta e você estiver usando o Windows 10, tente [reinstalar os dispositivos de rede usando o comando netcfg –d](http://windows.microsoft.com/windows-10/fix-network-connection-issues) (seção 6).

-   Se essas etapas não resolverem o problema, consulte [O emulador falha ao iniciar (primeira utilização)](#NoStart) para obter informações sobre softwares de terceiros que possam estar interferindo no emulador.

##  <a name="NoStart"></a> O emulador falha ao iniciar (primeira utilização)
 Se o emulador não iniciar, percorra as seguintes tarefas para identificar e corrigir o problema.

- Verifique se os requisitos mínimos de hardware foram atendidos e se as configurações de BIOS estão corretas.

   O emulador e o Windows 8 Hyper-V exigem um processador de 64 bits com SLAT (Conversão de Endereços de Segundo Nível). Para Intel, é necessário essencialmente um processador Core i3, i5 ou i7 (ou um dos muitos Xeons). Há uma lista dos chips AMD [aqui](http://support.amd.com/en-us).

  1. Verifique se o computador atende aos [requisitos do sistema](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md).

  2. Verifique o [ferramenta SLAT](https://slatstatuscheck.codeplex.com/) informa que o computador é compatível com SLAT.

  3. Dentro das configurações de BIOS do computador, verifique se a tecnologia de virtualização está habilitada. As descrições de BIOS exatas podem variar para cada fabricante de hardware. Em geral, habilite recursos relacionados a:

     -   SLAT (Conversão de Endereços de Segundo Nível)

     -   EPT (Extended Page Tables) (Intel)

     -   NPT (Nested Page Tables) (AMD)

     -   RVI (Rapid Virtualization Indexing) (AMD)

     -   VMX (um acrônimo Intel indicando suporte a virtualização assistida por hardware)

     -   SVM (um acrônimo AMD indicando suporte a virtualização assistida por hardware)

     -   XD (Execute Disable) (Intel); deve ser habilitado

     -   NX (nenhum Execute)(AMD); deve ser habilitado.

  4. Se as opções a seguir estiverem presentes no BIOS, desabilite-as.

     - Desabilitar Intel VT-d

     - Desabilitar a execução confiável

       Para obter mais informações, consulte este artigo: TechNet Hyper-V Como corrigir erros de BIOS habilitando o Hyper-V

  5. Verifique se você tem pelo menos 4 GB de memória de sistema e que não esteja sendo consumida por outros programas e processos de uso intensivo de recursos.

  6. Certifique-se de estar executando o Windows 8 Professional ou superior (não há suporte para Windows Server 2008). Há suporte para o Windows Server 2012, mas você deve habilitar o recurso Experiência da Área de Trabalho.

     Você pode inspecionar o Visualizador de Eventos para ver se há erros do Hipervisor. Para fazer isso, abra o Visualizador de Eventos (chave de inicialização + R, digite `eventvwr`) e, em seguida, selecione **Logs do Windows**, **Sistema**. Em seguida, filtre o log por origem de evento, configurando a fonte como **Hipervisor do Hyper-V**. Verifique se há erros ajudar a identificar a causa raiz.

     Se o processador atender aos requisitos mínimos, mas hipervisor ainda estiver falhando, descubra se há uma atualização do BIOS disponível para seu computador. Se houver e você optar por atualizar, observe todas as precauções do fabricante ao atualizar o BIOS (por exemplo, verificar se a atualização de firmware do BIOS não é interrompida por uma queda de energia, o que pode corromper permanentemente o BIOS).

- Verifique se você tem pelo menos 4 GB de memória de sistema e que não esteja sendo consumida por outros programas e processos de uso intensivo de recursos.

- Remover/desabilitar drivers ou software de terceiros que possam estar interferindo na rede virtual.

   Existem alguns problemas conhecidos com alguns produtos de terceiros instalados no Windows 8, como drivers/protocolos de rede que não são totalmente compatíveis com a pilha de rede do Hyper-V.

   Em geral, é responsabilidade dos desenvolvedores que os produtos a serem atualizados no software sejam compatíveis com o Windows 8 e Hyper-V.

   Os seguintes produtos podem exigir a atualização para conformidade do Windows 8: VirtualBox, Virtual PC 7, VMWare, alguns clientes VPN, firewalls de software, algumas versões do Cisco VPN clientes e outros sistemas de virtualização. Trabalhe com o desenvolvedor do software de virtualização questionável para incentivá-los a atualizar o software a fim de torná-lo compatível com o Windows 8 e o Hyper-V.

   Como um **solução alternativa**, você pode desabilitar todos os drivers e aplicativos de terceiros que possam estar interferindo na rede virtual usada pelo emulador para se comunicar com o Visual Studio. Esses aplicativos podem incluir:

  - Aplicativos antivírus (que se conectam à pilha de rede)

  - Ferramentas de monitoramento de rede

  - Ferramentas de registro em log de rede

  - Outro software de monitoramento do sistema

    Outra solução alternativa possível, sem desinstalar o produto em questão (e solicitar o desenvolvedor de produto para lançar uma versão atualizada), é seguir as etapas abaixo.

  1. Inicie o gerenciador de Conexões de rede (no menu Iniciar, digite `View Network Connections` e selecione esta opção para exibir as conexões de rede.)

  2. Para o adaptador vEthernet (comutador interno do emulador do Windows Phone na porta Ethernet interna), escolha **Propriedades** no menu de contexto.

      ![Adaptador virtual usado pelo Hyper&#45;V](../cross-platform/media/android-emu-virtual-adapter.png "Android_Emu_Virtual_Adapter")

      As propriedades do adaptador são mostradas aqui.

      ![Propriedades do adaptador virtual](../cross-platform/media/android-emu-virtual-adapter-properties.png "Android_Emu_Virtual_Adapter_Properties")

  3. Para esse adaptador, os únicos itens que devem ser selecionados em **Esta conexão utiliza os seguintes itens** devem ser os seguintes:

     -   Cliente para redes Microsoft

     -   Agendador de pacotes QoS

     -   Compartilhamento de arquivos e impressoras para redes da Microsoft

     -   Driver de protocolo LLDP da Microsoft

     -   Driver de E/S do mapeador de descoberta de topologia de camada de link

     -   Respondente de descoberta de topologia de camada de link

     -   Protocolo IP versão 6 (TCP/IPv6)

     -   Protocolo IP versão 4 (TCP/IPv4)

  4. Cancele a seleção de todos os outros itens.

     A desvantagem de usar essa técnica é que sempre que um novo produto de terceiros instala drivers sem suporte ou sempre que o emulador está instalado, essas etapas terão de ser repetidas.

     Depois de desinstalar os produtos de terceiros, talvez seja necessário restaurar o comutador interno do Emulador do Windows Phone. Para fazer isso:

  - Abra o Hyper V e vá para o Gerenciador de Comutador Virtual. Crie um comutador virtual chamado "Comutador interno do emulador do Windows Phone" e defina o tipo de conexão à **rede interna**.

     ![Gerenciador de comutador virtual](../cross-platform/media/android-emu-virtual-switch-manager.png "Android_Emu_Virtual_Switch_Manager")

    Agora inicialize o emulador. Ele deve funcionar.

##  <a name="NoBoot"></a> O computador falha ao iniciar após a instalação do emulador
 Esse problema pode ocorrer quando as seguintes condições são verdadeiras:

- O computador tem uma placa-mãe de gigabytes.

- O USB3 está habilitado na placa-mãe.

  Para resolver esse problema, desabilite o USB3 nas configurações do BIOS de placa-mãe e reinicie o computador. Verifique se o Gigabyte lançou uma atualização do BIOS da placa-mãe.

  Para obter mais informações, consulte o seguinte artigo da Base de dados de Conhecimento: [Falha ao iniciar após a instalação da função Hyper-V em sistemas de Gigabyte](https://support.microsoft.com/en-us/kb/2693144).

##  <a name="ADB"></a> O Visual Studio fica preso tentando implantar o aplicativo no emulador ou o emulador não aparece como um destino de depuração em outras IDEs
 Se o emulador estiver em execução, mas não parece não estar conectado a ADB (Android Debug Bridge) ou não aparecer nas ferramentas do Android que usam ADB (por exemplo, o Android Studio ou o Eclipse), talvez seja necessário ajustar onde o emulador deve procurar o ADB. O emulador usa uma chave do Registro para identificar o local de base do SDK do Android e procura o arquivo \platform-tools\adb.exe nesse diretório. Para modificar o caminho do SDK do Android usado pelo emulador:

- Abra o Editor do Registro, selecione **Executar** no menu de contexto dos botões Iniciar, digite `regedit` na caixa de diálogo e escolha **OK**.

- Navegue até as ferramentas do SDK HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Android na árvore de pastas à esquerda.

- Modifique a variável de Registro **Caminho** para coincidir com o caminho para o SDK do Android.

  Reinicie o emulador e agora você deve ver o emulador conectado ao ADB e às ferramentas do Android associadas.

##  <a name="XamarinPlayer"></a> O emulador paralisa porque não consegue configurar a porta UDP
 Você pode enfrentar esse problema devido a incompatibilidade com Xamarin Player. Se o emulador parece travar ou se você vir essa mensagem de erro "o emulador não consegue se conectar ao sistema operacional do dispositivo: Não foi possível configurar a porta UDP.  Algumas funcionalidades podem estar desabilitadas", você poderá estar enfrentando esse problema. Use as etapas a seguir.

1.  Desinstale o Xamarin Player.

2.  Verifique se a caixa virtual foi removida (Xamarin Player é executado sobre a caixa virtual).

3.  Vá para gerenciador de dispositivos, selecione a opção para mostrar dispositivos ocultos e, em seguida, exclua tudo, exceto as placas de rede físicas.

4.  Você pode tentar desinstalar/reinstalar o Hyper-V após a remoção de todos os adaptadores de rede não físicos.

##  <a name="Skylake"></a> Não é possível anexar o depurador a um projeto do Xamarin
 Se você estiver executando o Windows 10 com processadores Intel Skylake, os aplicativos do Xamarin poderão falhar ao serem executados no emulador ou o depurador do Visual Studio pode não ser anexado a eles. Isso ocorre devido a um problema com os processadores Hyper-V e Skylake. Execute as seguintes etapas como uma solução alternativa.

1.  Abra o Gerenciador do Hyper-V e selecione a VM para o perfil do emulador que você está usando.

2.  Selecione **Excluir Estado Salvo** (inferior direito).

3.  Escolha **Configurações...**

4.  Expanda o nó de processador e escolha **Compatibilidade**.

5.  Habilite **Migrar para um computador físico com uma versão de processador diferente**.

6.  Reinicie o serviço (em **Ações**) e tente novamente.

##  <a name="GooglePlay"></a> Falha do emulador ao executar o aplicativo que usa o Google Play Services
 O emulador não é fornecido com as bibliotecas do Google Play Services. No entanto, o emulador dá suporte a instalação do tipo "arrastar e soltar" de arquivos zip de memória flash.

##  <a name="DragAndDrop"></a> A função arrastar e soltar de um arquivo, um APK ou um arquivo zip de memória flash não funcionam
 O emulador usa ADB.exe para facilitar a transferência de arquivo quando você arrasta e solta um arquivo na tela. Se você encontrar um erro ao tentar arrastar e soltar um arquivo, isso provavelmente indica que o emulador não está conectado ao ADB.exe. Para resolver, siga as etapas em [O Visual Studio fica preso ao tentar implantar o aplicativo no emulador ou o emulador não aparece como um destino de depuração em outras IDEs](#ADB).

##  <a name="Resolution"></a> Resolução de tela incorreta
 Se você tirar uma captura de tela usando a guia Captura de tela na janela **Ferramentas Adicionais** e a imagem resultante for de tamanho inesperado, ajuste o nível de zoom da tela antes de escolher **Capturar**. O emulador usa capturas de tela com a resolução de tela no monitor do PC host.

##  <a name="OpenGL"></a> Falha do emulador ao renderizar o conteúdo do OpenGL
 O emulador renderiza conteúdo do OpenGL usando a GPU do computador host e usa o projeto de ANGLE para converter essas chamadas para e do DirectX. Se seu aplicativo renderizar corretamente em um dispositivo, mas incorretamente no emulador, é provável que o dispositivo esteja reduzindo uma chamada OpenGL incorreta (por exemplo, usando variáveis de sombreador que não correspondem).

##  <a name="Multitouch"></a> O emulador não responde a gestos multitoque
 Em alguns casos, o emulador iniciará e não responderá a multitoque, nem por interação direta em sua tela sensível ao toque nem usando a ferramenta multitoque na barra de ferramentas do emulador. Se esse for o caso, escolha o botão **Girar** na barra de ferramentas do emulador e tente usar o multitoque novamente. Se o problema persistir, leia [O emulador falha ao renderizar o conteúdo do OpenGL](#OpenGL).

##  <a name="Support"></a> Recursos de suporte
 Se o computador host atender aos requisitos do sistema e você encontrar um problema não abordado neste guia de solução de problemas:

-   Faça uma pergunta sobre o StackOverflow o [emulador do android](http://stackoverflow.com/questions/tagged/android-emulator) e marcações do visual studio.

-   Relate um problema usando a ferramenta Enviar um Smiley no Visual Studio ou no Gerenciador de emulador.

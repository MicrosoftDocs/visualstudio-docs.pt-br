---
title: Instalar o Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.about
helpviewer_keywords:
- Visual Studio, installing
- installing Visual Studio
- server installations [Visual Studio]
- Setup [Visual Studio]
- install Visual Studio
- visual studio installer
ms.assetid: da049020-cfda-40d7-8ff4-7492772b620f
caps.latest.revision: 183
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: 761264d80c04f0e2ce13a365071f56739d6961a2
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055161"
---
# <a name="install-visual-studio-2015"></a>Instalar o Visual Studio 2015

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta página inclui informações detalhadas para ajudá-lo com a instalação **Visual Studio 2015**, nosso pacote integrado de ferramentas de produtividade para desenvolvedores. Também incluímos links para ajudá-lo rapidamente para obter informações [recursos](https://www.visualstudio.com/news/vs2015-vs.aspx), [edições](http://go.microsoft.com/fwlink/?LinkID=242142), [requisitos do sistema](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs), [downloads](http://go.microsoft.com/fwlink/?LinkId=517106), e muito mais.

## <a name="quick-links"></a>Links rápidos

Antes de nos aprofundar até os detalhes, aqui está uma lista dos nossos links solicitados mais frequentemente.

|||
|------------------|----------------|
|![Baixe o Visual Studio](../install/media/downloads.png "Downloads") |**Downloads** Para instalar o Visual Studio 2015, você pode baixar um arquivo executável do produto dos [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) página (assinatura necessária), ou usar a mídia de instalação do produto Demarcado. [Saiba mais sobre como baixar versões do Visual Studio atuais ou anterior](https://www.visualstudio.com/vs/older-downloads/).|
|![Saiba mais sobre os recursos](../install/media/features.png "recursos") |**Recursos** Para saber mais sobre os recursos no Visual Studio 2015, consulte as notas de versão para [RTM](https://www.visualstudio.com/news/vs2015-vs), [atualização 1](https://www.visualstudio.com/news/vs2015-update1-vs), [atualização 2](https://www.visualstudio.com/news/vs2015-update2-vs), e [atualização 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).|
|![Descubra o que há em cada SKU](../install/media/sku.png "SKUs") |SKUs Para descobrir o que está disponível em cada edição do Visual Studio 2015, consulte nosso [Compare as ofertas do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=242142) página.|
|![Exibir requisitos do sistema](../install/media/system-requirements.png "requisitos do sistema") |**Requisitos de sistema** Para exibir os requisitos do sistema para cada edição do Visual Studio 2015, consulte o [compatibilidade do Visual Studio 2015](https://www.visualstudio.com/products/visual-studio-2015-compatibility-vs) página.|
|![Localize a chave do produto](../install/media/product-keys.png "chaves do produto") |**Chaves do Produto** Para localizar a chave do produto, consulte o [como: Localize a chave de produto do Visual Studio](../install/how-to-locate-the-visual-studio-product-key.md) tópico.|
|![Saiba mais sobre licenciamento](../install/media/licensing.png "licenciamento") |Licenciamento Para obter informações sobre opções de licenciamento para indivíduos ou os clientes corporativos, consulte o [Visual Studio e licenciamento do MSDN](https://www.microsoft.com/download/details.aspx?id=13350) white paper.|

##  <a name="custom"></a> Vs padrão. Instalação personalizada
 Quando você instala o Visual Studio 2015, você pode incluir ou excluir componentes que você deseja usar em uma base diária. Isso significa que uma instalação padrão será muitas vezes menores e instalar mais rapidamente do que uma instalação personalizada. Isso também significa que muitos componentes que foram instalados por padrão nas versões anteriores agora são considerados componentes personalizados que você deve selecionar explicitamente nesta versão.

 ![Diálogo de instalação do Visual Studio 2015](../ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

 Componentes personalizados incluem o Visual C++, Visual F#, SQL Server Data Tools, ferramentas de plataforma cruzada móveis e SDKs e SDKs de terceiros e extensões. Você pode instalar qualquer um dos componentes personalizados em um momento posterior, se você não selecionar eles durante a instalação inicial.

> [!NOTE]
>  Uma instalação personalizada inclui automaticamente os componentes que estão em uma instalação padrão.

 A lista completa de componentes personalizados é da seguinte maneira:

|Conjuntos de recursos|Componentes|
|------------------|----------------|
|**Atualizações**|Visual Studio 2015 Atualização 3|
|**Linguagens de programação**|Visual C++<br />Visual F#<br />Ferramentas Python para o Visual Studio|
|**Desenvolvimento Web e no Windows**|Ferramentas de publicação do ClickOnce<br />LightSwitch<br />Microsoft Office Developer Tools<br />Microsoft SQL Server Data Tools<br /> Ferramentas para Desenvolvedores Web da Microsoft<br />Ferramentas do PowerShell para Visual Studio (3ª parte)<br />Kit de desenvolvimento do Silverlight<br />Ferramentas de desenvolvimento de aplicativos universais do Windows<br />SDKs e ferramentas do Windows 10<br />Windows 8.1 e Windows Phone 8.0/8.1 ferramentas<br />SDKs e ferramentas do Windows 8.1|
|**Desenvolvimento móvel multiplataforma**|C# / .NET (Xamarin)<br />HTML/JavaScript (Apache Cordova)<br />Desenvolvimento do Visual C++ móvel para iOS / Android<br />Clang com o Microsoft CodeGen|
|**Ferramentas comuns e Kits de desenvolvimento de Software**|Kit de desenvolvimento nativo do Android (3ª parte)<br /> SDK do Android [3ª parte]<br />APIs de instalação do SDK do Android (3ª parte)<br />O Apache Ant (3ª parte)<br /> Java SE Development Kit (3ª parte)<br /> O joyent Node. js (3ª parte)|
|**Ferramentas comuns**|Git para Windows (3ª parte)<br />Extensão do GitHub para Visual Studio (3ª parte)<br /> Ferramentas de Extensibilidade do Visual Studio|

##  <a name="installing"></a> Instalando o Visual Studio
 Você pode instalar o Visual Studio usando a mídia de instalação (DVDs), usando o serviço de assinatura do Visual Studio a partir de [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) site, ao baixar um instalador da web a [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkId=517106) site, ou criando um layout de instalação offline (consulte a [criar uma off-line instalação do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) para obter mais detalhes).

> [!IMPORTANT]
>  Você deve ter credenciais de administrador para instalar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. No entanto, você não precisará delas para usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] depois de instalá-lo.

 Sua conta de administrador local deve ter os seguintes privilégios habilitados para instalar tudo no Visual Studio.

|Nome de exibição do objeto de diretiva local|Direito de usuário|
|--------------------------------------|----------------|
|Fazer backup de arquivos e diretórios|SeBackupPrivilege|
|Depurar programas|SeDebugPrivilege|
|Gerenciar logs de auditoria e segurança|SeSecurityPrivilege|

 Para obter mais informações sobre esse requisito de conta de administrador local, consulte o artigo da Base de dados de Conhecimento [instalação do SQL Server falhará se a conta de instalação não tiver determinados direitos de usuário](https://support.microsoft.com/en-us/kb/2000257).

###  <a name="BKMK_Media"></a> Usando a mídia de instalação
 Para instalar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no diretório raiz na mídia de instalação [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], execute o arquivo de instalação da edição que você deseja:

|Edição|Arquivo de instalação|
|-------------|-----------------------|
|Visual Studio Enterprise|vs_enterprise.exe|
|Visual Studio Professional|vs_professional.exe|
|Comunidade Visual Studio|vs_community.exe|

###  <a name="BKMK_Website"></a> Baixando do site do produto
 Visite o [Downloads do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=517106) página e, em seguida, selecione a edição do Visual Studio que você deseja.

### <a name="downloading-from-your-subscription-service"></a>Download de seu serviço de subscrição
 Visite o [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) página e, em seguida, selecione a edição do Visual Studio que você deseja.

###  <a name="BKMK_Offline"></a> Criando um layout de instalação offline
 Se você não tiver o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] mídia de instalação, ou você não tem uma assinatura do Visual Studio, ou você não deseja instalar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usando o instalador da web, você pode executar uma instalação "desconectada", criando o que é conhecido como um offline layout de instalação. Para obter mais informações, consulte o [criar uma instalação Offline do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md) página.

##  <a name="enterprise"></a> Implantação do Visual Studio em uma empresa
 Para obter informações sobre como implantar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] em uma rede, consulte a [guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md).

###  <a name="BKMK_Virtualized"></a> Instalação do Visual Studio em um ambiente virtualizado
 **Problemas de vídeo com o Hyper-V**

 Se você executar o Windows Server 2008 R2 com Hyper-V habilitado e um adaptador gráfico acelerado, é possível perceber lentidão no sistema.

 Para obter mais informações, consulte a seguinte página no site da Microsoft: [Desempenho de vídeo pode diminuir quando um Windows Server 2008 ou Windows Server 2008 R2 com base em computador tem a função Hyper-V habilitada e um adaptador de vídeo acelerado instalado](http://go.microsoft.com/fwlink/?LinkID=231084).

 **Emulando a dispositivos com o Hyper-V**

 Quando você instala o Visual Studio 2015 em hardware real sem a virtualização, você pode escolher os recursos que permitem a emulação do Windows e dispositivos Android usando o Hyper-V. Quando você instala no Hyper-V, você não poderá emular o Windows ou dispositivos Android. Isso ocorre porque os emuladores são as próprias máquinas virtuais e, no momento, você não pode hospedar uma máquina virtual dentro de outra VM. A solução é ter Windows real ou dispositivos Android para o qual você diretamente pode implantar e depurar seu aplicativo.

##  <a name="optionalComponents"></a> Instalar componentes opcionais
 Se você quiser instalar os componentes que você talvez não tenha selecionado durante a instalação original, use o procedimento a seguir.

#### <a name="to-install-optional-components"></a>Para instalar componentes opcionais

1.  No **Painel de Controle** na página **Programas e Recursos**, escolha a edição do produto à qual deseja adicionar um ou mais componentes e, em seguida, selecione **Alterar**.

2.  No Assistente de instalação, escolha **Modificar** e, em seguida, escolha os componentes que deseja instalar.

3.  Escolha **Avançar** e, em seguida, siga as instruções restantes.

##  <a name="helpContent"></a> Instalar o conteúdo da Ajuda offline
 Depois de instalar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você pode baixar o conteúdo de ajuda adicional para que ele estará disponível offline.

#### <a name="to-install-or-uninstall-help-content"></a>Para instalar ou desinstalar conteúdo da Ajuda

1. Na barra de menus do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], escolha **Ajuda**, **adicionar e remover conteúdo da Ajuda**.

2. Na guia **Gerenciar Conteúdo** do **Visualizador da Ajuda da Microsoft**, selecione a fonte de instalação do conteúdo da Ajuda.

3. Se você estiver procurando uma coleção da Ajuda específica, digite o nome ou uma palavra-chave na caixa de texto **Pesquisar** e pressione **Enter**.

4. Ao lado do nome da coleção da Ajuda que você deseja, escolha o link **Adicionar** ou **Remover**.

5. Clique o **atualização** botão.

   Para obter mais informações sobre como instalar ou implantar ajuda offline, consulte o [guia de administrador do Visualizador da Ajuda](../ide/help-viewer-administrator-guide.md).

##  <a name="serviceReleases"></a> Verificando liberações de serviço e atualizações de produto
 Como nem todas as extensões são compatíveis, o Visual Studio não atualiza extensões automaticamente quando você atualiza de versões anteriores. Você deverá reinstalar as extensões do [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=178891) ou do Editor do software.

#### <a name="to-automatically-check-for-service-releases"></a>Para verificar automaticamente as liberações de serviço

1.  Na barra de menus, escolha **Ferramentas**, **Opções**.

2.  Na caixa de diálogo **Opções**, expanda **Ambiente** e, em seguida, selecione **Extensões e Atualizações**. Confira se a caixa de seleção **Verificar atualizações automaticamente** está selecionada e, em seguida, escolha **OK**.

## <a name="registering-visual-studio"></a>Registrando o Visual Studio

1.  Na barra de menus, escolha **Ajuda**, **Sobre**.

     A caixa de diálogo **Sobre** mostra o PID (número de identificação do produto). Você será necessário as credenciais do PID e conta do Windows (por exemplo, um endereço de email do Hotmail ou Outlook.com e senha) para registrar o produto.

2.  Na barra de menus, escolha **Ajuda**, **Registrar Produto**.

##  <a name="repair"></a> Reparando o Visual Studio

#### <a name="to-repair-visual-studio"></a>Para reparar o Visual Studio

1.  Na **painel de controle**diante a **programas e recursos** , escolha a edição do produto que você deseja reparar e, em seguida, escolha **alteração**.

2.  No Assistente de instalação, escolha **Reparar**, escolha **Avançar** e, em seguida, siga as instruções restantes.

#### <a name="to-repair-visual-studio-in-silent-or-passive-modes-that-is-to-repair-from-source"></a>Para reparar o Visual Studio nos modos silencioso ou passivos (isto é, ao reparo da origem)

1.  No computador onde o Visual Studio está instalado, abra o prompt de comando do Windows.

2.  Digite os seguintes parâmetros:

     *1&gt;dvdroot&lt;1* \\< arquivo de instalação\> \</quiet&#124;/passive > [/norestart] / reparar

##  <a name="troubleshooting"></a> Solucionando problemas de instalação
 Utilize os seguintes recursos para conseguir ajuda para problemas de configuração e instalação:

-   Fórum de [Instalação e configuração do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=151190). Leia perguntas e respostas de outras pessoas na comunidade do Visual Studio. Se você não encontrar o que precisa, faça suas próprias perguntas.

-   Site do [Suporte da Microsoft para Visual Studio](http://go.microsoft.com/fwlink/?LinkID=251019). Leia artigos da base de dados de conhecimento e saiba como contatar o Suporte da Microsoft para obter informações sobre problemas com a instalação do Visual Studio.

##  <a name="relatedTopics"></a> Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Criar uma instalação do Offline do Visual Studio](../install/create-an-offline-installation-of-visual-studio.md)|Descreve como instalar o Visual Studio quando você não está conectado à Internet.
|[Instalar versões do Visual Studio lado a lado](../install/install-visual-studio-versions-side-by-side.md)|Fornece informações sobre como instalar várias versões do Visual Studio no mesmo computador.|
|[Usar parâmetros de linha de comando para instalar o Visual Studio](/visualstudio/install/use-command-line-parameters-to-install-visual-studio)|Lista os parâmetros de linha de comando que você pode usar ao instalar o Visual Studio em um prompt de comando.|
|[Desinstalar o Visual Studio](../install/uninstall-visual-studio.md)|Descreve como desinstalar o Visual Studio.|
|[Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)|Fornece informações sobre as opções de implantação do Visual Studio.|
|[A Biblioteca de Imagens do Visual Studio](../designers/the-visual-studio-image-library.md)|Fornece informações sobre como instalar os gráficos que podem ser usados em aplicativos do Visual Studio.|
|[Introdução ao desenvolvimento com o Visual Studio](../ide/get-started-developing-with-visual-studio.md)|Inclui informações e links que podem ajudar você a usar o Visual Studio com mais eficiência.|

## <a name="see-also"></a>Consulte também

- [Signing in to Visual Studio](../ide/signing-in-to-visual-studio.md) (Entrando no Visual Studio)
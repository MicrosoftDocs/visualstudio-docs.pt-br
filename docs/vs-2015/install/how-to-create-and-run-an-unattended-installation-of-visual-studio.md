---
title: 'Como: Criar e executar uma instalação autônoma | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Visual Studio, unattended
- unattended installation, Visual Studio
ms.assetid: 3867b5dc-ed34-4ee2-be32-a42e7e320517
caps.latest.revision: 44
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: bc1a6ba1a36dd7514257fcbb8ba4c26ca1ee6116
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065513"
---
# <a name="how-to-create-and-run-an-unattended-installation-of-visual-studio"></a>Como: Criar e executar uma instalação autônoma do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode executar o aplicativo de instalação para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] como autônomo (ou seja, silencioso personalizado) em uma intranet em vez de a partir de mídia como DVDs. Este tópico descreve como preparar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para esse tipo de instalação a partir de um compartilhamento de rede.

## <a name="creating-a-network-image"></a>Criando uma imagem de rede
 Primeiro, crie uma imagem de rede da mídia do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

#### <a name="to-create-a-network-image"></a>Para criar uma imagem de rede

1.  Crie uma pasta no servidor (por exemplo, *Drive*: \IDEinstall\\).

2.  Baixe o instalador do [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015)e, em seguida, execute *produto*.exe /Layout *unidade*: \IDEinstall\

3.  Compartilhe a pasta IDEinstall na rede e, em seguida, defina as configurações de segurança apropriadas.

     O caminho de rede do aplicativo para instalação [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] lembra \\ \\ *ServerName*\IDEinstall\\*produto*.exe.

    > [!NOTE]
    >  A instalação pode falhar se qualquer combinação de caminho e nome de arquivo exceder 260 caracteres. O comprimento máximo de um caminho em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é de 221 caracteres.  O nome do caminho local não deve exceder 70 caracteres, e o nome do caminho de rede não deve exceder 39 caracteres.

     Instalação também pode falhar se os nomes de pasta no caminho incluírem espaços inseridos (por exemplo, "\\\\*ServerName*\IDE install" ou \\ \\ *ServerName*\Visual studio\\).

## <a name="deploying-visual-studio-in-unattended-mode"></a>Implantando o Visual Studio no modo autônomo
 Para implantar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no modo autônomo, você deve modificar o arquivo Admindeployment XML. Para fazer isso, primeiro você deve criar o arquivo Admindeployment XML usando o `/CreateAdminFile`  *\<local do arquivo >* parâmetro de linha de comando. Em seguida, você pode usar esse arquivo para enviar por push uma implantação do Visual Studio à sua rede ou efetuar pull em uma instalação se você colocar esse arquivo na *unidade*: \ideinstall\packages. directory. O arquivo AdminDeployment.xml não é exclusivo de um sistema operacional, uma arquitetura, uma edição Visual Studio ou de um idioma de sistema operacional.

> [!CAUTION]
>  Às vezes, os itens listados como selecionado no arquivo Admindeployment são instalados. Para resolver esse problema, coloque os itens marcados como "selecionados ="yes"" no **final** do arquivo Admindeployment.
>
>  Se você não quiser instalar as dependências opcionais de um item, você deve primeiro selecionar o pai e, em seguida, desmarque as dependências opcionais após o pai, conforme mostrado na seguinte captura de tela:
>
>  ![Itens de instalação ao final do arquivo Admindeployment](../install/media/vs2015-install-endoffileadmindeploy.PNG "vs2015_Install_EndOfFileAdminDeploy")
>
>  Outra maneira de fazer isso é simplesmente omitir os filhos opcionais de um pai — em outras palavras, não incluem nenhum "selecionados ="não"" itens — mas você ainda deve colocar todos os o "selecionados ="yes"" itens no final do arquivo Admindeployment XML.

> [!IMPORTANT]
>  Durante a instalação, o computador pode reiniciar automaticamente uma ou mais vezes. Depois que ele for reiniciado, faça logon novamente com a mesma conta de usuário com a qual você estava conectado para executar a instalação antes do computador é reiniciado. Você pode evitar reinícios automáticos instalando os componentes de pré-requisito antes de executar uma instalação autônoma. Para obter mais informações, consulte a seção intitulada "Evite reiniciar durante a instalação" no [guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md).

 O esquema do arquivo AdminDeployment contém os seguintes elementos:

|Elemento|Atributo|Valores|Descrição|
|-------------|---------------|------------|-----------------|
|BundleCustomizations|TargetDir|*Path*|Comporta-se da mesma forma que a substituição do caminho na interface do usuário do aplicativo de instalação. Este elemento será ignorado se o Visual Studio já estiver instalado.|
|BundleCustomizations|NoWeb|Sim&#124;padrão|Se o valor desse elemento for sim, o aplicativo de instalação nunca tentará ir para a Web durante a ação de instalação.|
|SelectableItemCustomization|Hidden|Sim&#124;não|Se o valor desse elemento for Sim, oculta um item Selecionável na árvore de personalização.|
|SelectableItemCustomization|Selecionado|Sim&#124;não|Marca ou desmarca um item selecionável na árvore de personalização.|
|BundleCustomizations|Feed|Caminho|Localização do feed que o usuário deseja usar.  Esse feed é usado para subsequentes modificar operações no computador ("Default" por padrão).|
|BundleCustomizations|SuppressRefreshPrompt|Sim&#124;padrão|Impedirá que o usuário seja solicitado para a instalação de atualização, se houver uma mais recente disponível.|
|BundleCustomizations|NoRefresh|Sim&#124;padrão|Não atualizar a instalação, se houver uma mais recente disponível.|
|BundleCustomizations|NoCacheOnlyMode|Sim&#124;padrão|Impede pré-população do cache de pacote.|

> [!WARNING]
>  O aplicativo de instalação respeitará o estado Selecionado de um SelectableItem, mesmo se estiver oculto. Por exemplo, se você quiser instalar sempre um item selecionável, poderá marcá-lo como oculto e selecionado.

#### <a name="to-create-an-unattended-installation-of-visual-studio"></a>Para criar uma instalação autônoma do Visual Studio

1.  No arquivo *Drive*:\IDEinstall\AdminDeployment.xml, altere o valor do atributo NoWeb do elemento BundleCustomizations de "default" para "yes" como mostra o exemplo a seguir:

     Altere `<BundleCustomizations TargetDir="default" NoWeb="default"/>` para `<BundleCustomizations TargetDir="default" NoWeb="yes"/>`

2.  Altere o atributo SelectableItemCustomization conforme necessário para componentes opcionais e então salve o arquivo.

## <a name="running-unattended-setup"></a>Executando a instalação autônoma
 Você pode executar a instalação autônoma ao executar automaticamente o aplicativo de instalação do Visual Studio em computadores cliente ou ao permitir que os usuários executem o aplicativo por conta própria usando as configurações definidas por você.

#### <a name="to-run-an-unattended-installation-on-a-client-computer"></a>Para executar uma instalação autônoma em um computador cliente

- Abra o **inicie** menu, escolha **executar**e, em seguida, insira \\ \\ *ServerName*\IDEinstall\vs_*produto*.exe /adminfile *PathOfTheAdmindeployment.xmlFile*<em>AdditionalParametersAsNeeded</em>

   Por exemplo, você pode especificar a seguinte linha de comando: `\\server1\IDEinstall\vs_enterprise.exe /adminfile \\server1\ IDEinstall\AdminDeployment.xml /quiet /norestart`

#### <a name="to-enable-clients-to-manually-install-visual-studio-with-pre-defined-settings"></a>Para permitir que clientes instalem manualmente o Visual Studio com configurações predefinidas

1.  Copie o arquivo Admindeployment XML personalizado para um compartilhamento de rede que é somente leitura (por exemplo, \\ \\ *ServerName*\IDEinstall\packages\AdminDeployment.xml).

2.  Permita que usuários instalem deste compartilhamento.

## <a name="maintaining-an-installation"></a>Mantendo uma instalação
 Ao abrir o **Painel de Controle** e executar novamente o aplicativo de instalação, você poderá modificar os recursos do Visual Studio, desinstalar linguagens de programação e reparar ou desinstalar o Visual Studio.

> [!NOTE]
>  Você deve ter credenciais administrativas no computador local para usar o modo de manutenção.

#### <a name="to-maintain-an-installation-on-a-client-computer"></a>Para manter uma instalação em um computador cliente

-   Abra o **Painel de Controle** e, em seguida, escolha **Programas e Recursos**.

-   Escolha [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e, em seguida, escolha **Alterar**.

#### <a name="to-change-admindeployment-settings-on-a-client-computer-after-visual-studio-has-been-installed"></a>Para alterar as configurações de AdminDeployment em um computador cliente após o Visual Studio ter sido instalado

1. Atualize AdminDeployment.xml, conforme o necessário.

2. Abra o menu **Iniciar** e, em seguida, escolha **Executar**.

3. Digite o seguinte texto: \\\\*ServerName*\IDEinstall\vs_*produto*.exe /AdminFile PathToAdmindeployment.xml arquivo

    AdditionalParametersAsNeeded

    Por exemplo, você pode especificar a seguinte linha de comando: `\\server1\IDEinstall\vs_enterprise.exe /adminfile \\server1\IDEinstall\AdminDeployment.xml /quiet /norestart`

   Reparar é o parâmetro padrão depois que o Visual Studio está instalado. Se você reparar o Visual Studio com um /AdminFile atualizado, você substituirá as configurações de implantação do Admin atual com aqueles que invoca o arquivo Admindeployment XML atualizado.

## <a name="updating-an-installation"></a>Atualizando uma instalação
 A Microsoft lançou várias atualizações para o Visual Studio 2015. Esta seção explica como atualizar sua imagem de instalação autônoma do Visual Studio 2015, para que ele inclua as atualizações.

#### <a name="to-update-an-unattended-installation-of-visual-studio"></a>Para atualizar uma instalação autônoma do Visual Studio

1. Localize o arquivo de Product.exe na imagem de rede existente, clique duas vezes e, em seguida, clique em **propriedades**.

2. Clique o **detalhes** guia e, em seguida, anote as **versão do produto** propriedade.

    ![Exemplo de caixa de diálogo de propriedades em uma instalação autônoma do Visual Studio](../install/media/unattended-install-properties-dialog-box.PNG "autônoma Install - caixa de diálogo Propriedades")

3. ###### <a name="if-the-product-version-is-140247200-or-140247201-follow-these-steps"></a>Se a versão do produto é 14.0.24720.0 ou 14.0.24720.1, siga estas etapas:
4. 1.  Execute *Product.exe* /Layout *Drive:* \IDEinstall em um computador que tenha acesso à Internet. (Por exemplo, execute: `vs_enterprise.exe /Layout d:\IDEinstall`.)

   2.  Depois que o /Layout for concluído, copie a nova imagem para um novo local.

   3.  Criar e modificar o arquivo Admindeployment XML. Para fazer isso, use o `/CreateAdminFile`  *\<local do arquivo >* parâmetro de linha de comando. (Para obter mais informações, consulte a seção "Implantando Visual Studio no modo autônomo" deste artigo.)

   4.  O computador cliente, execute o seguinte comando para atualizar a cópia do Visual Studio que você instalou anteriormente: "\\\\*server1*\IDEinstall_Updated_1\\*Product.exe*  /adminfile \\\server1\ IDEinstall_Updated_1\AdminDeployment.xml lightweightserver /quiet /norestart ".

        Por exemplo, execute: `\\server1\IDEinstall_Updated_1\vs_enterprise.exe /adminfile \\server1\IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart`
5. ###### <a name="for-other-product-version-values-follow-these-steps"></a>Para outros valores de versão do produto, siga estas etapas:
6. 1.  Execute *Product.exe* /Layout *Drive:* \IDEinstall em um computador que tenha acesso à Internet. (Por exemplo, execute `vs-enterprise.exe /Layout d:\IDEinstall`.)

   2.  Depois que o /Layout for concluído, copie a nova imagem para um novo local. (Ou, você pode substituir a imagem de rede existente em vez disso.)

   3.  Crie e modifique o arquivo Admindeployment XML. Para fazer isso, use o `/CreateAdminFile`  *\<local do arquivo >* parâmetro de linha de comando. (Para obter mais informações, consulte a seção "Implantando Visual Studio no modo autônomo" deste artigo.)

   4.  Se você copiar a imagem para um novo local, você deve executar o comando a seguir no computador cliente para atualizar a cópia do Visual Studio que você instalou anteriormente: "\\\\*server1*\IDEinstall_Updated_1\\ *Product.exe* /adminfile \\\server1\ IDEinstall_Updated_1\AdminDeployment.xml lightweightserver /quiet /norestart ".

        Por exemplo, execute: `\\server1\IDEinstall_Updated_1\vs_enterprise.exe /adminfile \\server1\IDEinstall_Updated_1\AdminDeployment.xml /quiet /norestart`

   5.  Se você substituir a imagem de rede existente, você pode executar o comando, conforme listado na etapa anterior, ou você pode fazer o seguinte:

   6.  1.  Abra o **Painel de Controle** e, em seguida, escolha **Programas e Recursos**.

       2.  Escolher **Visual Studio**e, em seguida, escolha **alteração**.

       3.  Depois que o Visual Studio é iniciado no modo de manutenção, clique em **modificar**.

       4.  A atualização mais recente deve aparecer na página de recursos. Selecione os outros recursos que você deseja instalar, clique em **próxima**e, em seguida, clique em **atualizar** para instalar a atualização e os novos recursos.

## <a name="registering-the-product"></a>Registrando o produto
 Após a instalação ter sido concluída, será possível registrar sua cópia do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] de dentro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

#### <a name="to-register"></a>Para registrar

1.  Abra o menu **Ajuda** e, em seguida, escolha **Registrar Produto**.

2.  Insira a chave do produto.

     (Para obter mais informações, consulte o [como: Localize a chave de produto do Visual Studio](../install/how-to-locate-the-visual-studio-product-key.md) e o [como: Aplicar chaves de produto durante a implantação do Visual Studio](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md) tópicos.)

## <a name="see-also"></a>Consulte também
 [Instalar o Visual Studio](../install/install-visual-studio-2015.md)
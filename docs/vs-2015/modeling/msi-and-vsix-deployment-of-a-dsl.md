---
title: Implantação por MSI e VSIX de uma DSL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 81b027e9834fccadcc572cad8fae4d721be9dd56
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49922035"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>Implantação de uma DSL por MSI e VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode instalar uma linguagem específica de domínio em seu próprio computador ou em outros computadores. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] já deve estar instalado no computador de destino.  
  
##  <a name="which"></a> Escolhendo entre a implantação de MSI e VSIX  
 Há dois métodos de implantação de uma linguagem específica de domínio:  
  
|Método|Benefícios|  
|------------|--------------|  
|VSX ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão)|Muito fácil de implantar: cópia e executar o **VSIX** arquivo do projeto DslPackage.<br /><br /> Para obter mais informações, consulte [instalando e desinstalando uma DSL usando a VSX](#Installing).|  
|MSI (arquivo do instalador)|-Permite que o usuário abra [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] clicando duas vezes em um arquivo DSL.<br />-Associa um ícone com o tipo de arquivo DSL no computador de destino.<br />-Associa um XSD (esquema XML) com o tipo de arquivo DSL. Isso evita avisos quando o arquivo é carregado no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].<br /><br /> Você deve adicionar um projeto de instalação à sua solução para criar um MSI.<br /><br /> Para obter mais informações, consulte [a implantação de uma DSL usando um arquivo MSI](#msi).|  
  
##  <a name="Installing"></a> Instalação e desinstalação de uma DSL usando a VSX  
 Quando sua DSL é instalada por esse método, o usuário pode abrir um arquivo DSL no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], mas não é possível abrir o arquivo do Windows Explorer.  
  
#### <a name="to-install-a-dsl-by-using-the-vsx"></a>Para instalar uma DSL por meio do VSX  
  
1.  No seu computador, localize o **VSIX** arquivo que foi criado pelo seu projeto de pacote DSL.  
  
    1.  No **Gerenciador de soluções**, clique com botão direito do **DslPackage** do projeto e, em seguida, clique em **Abrir pasta no Windows Explorer**.  
  
    2.  Localize o arquivo **bin\\\*\\**_Seuprojeto_**. DslPackage.vsix**  
  
2.  Cópia de **VSIX** arquivo para o computador de destino no qual você deseja instalar a DSL. Isso pode ser seu próprio computador ou outro.  
  
    -   O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que dá suporte a DSLs em tempo de execução. Para obter mais informações, consulte [suporte para edições do Visual Studio de visualização e o SDK de modelagem](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md).  
  
    -   O computador de destino deve ter uma das edições do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] especificado no **DslPackage\source.extensions.manifest**.  
  
3.  No computador de destino, clique duas vezes o **VSIX** arquivo.  
  
     **Instalador de extensão do Visual Studio** abre e instala a extensão.  
  
4.  Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
5.  Para testar o DSL, use [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para criar um novo arquivo que tem a extensão que você definiu para sua DSL.  
  
#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>Para desinstalar uma DSL que foi instalada usando VSX  
  
1. Sobre o **ferramentas** menu, clique em **Gerenciador de extensões**.  
  
2. Expandir **extensões instaladas**.  
  
3. Selecione a extensão no qual a DSL é definida e clique **desinstalação**.  
  
   Raramente, uma extensão defeituosa Falha ao carregar e cria um relatório na janela de erros, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:  
  
   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**  
  
##  <a name="msi"></a> Implantando uma DSL em um MSI  
 Definindo um arquivo MSI (Windows Installer) para sua DSL, você pode permitir aos usuários abrir arquivos DSL a partir do Windows Explorer. Você também pode associar um ícone e uma descrição curta com sua extensão de nome de arquivo. Além disso, o MSI pode instalar um XSD que pode ser usado para validar os arquivos de DSL. Se você quiser, você pode adicionar outros componentes no MSI que será instalado ao mesmo tempo.  
  
 Para obter mais informações sobre arquivos MSI e outras opções de implantação, consulte [implantação de aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md).  
  
 Para criar um MSI, você adiciona um projeto de instalação para seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução. O método mais fácil de criar um projeto de instalação é usar o modelo CreateMsiSetupProject.tt, que pode ser baixado do [site do VMSDK](http://go.microsoft.com/fwlink/?LinkID=186128).  
  
#### <a name="to-deploy-a-dsl-in-an-msi"></a>Para implantar uma DSL em um MSI  
  
1. Definir `InstalledByMsi` no manifesto da extensão. Isso impede que o VSX que está sendo instalado e desinstalado, exceto pelo MSI. Isso é importante se você incluirá outros componentes do MSI.  
  
   1.  Abra DslPackage\source.extension.tt  
  
   2.  Insira a seguinte linha antes de `<SupportedProducts>`:  
  
       ```  
       <InstalledByMsi>true</InstalledByMsi>  
       ```  
  
2. Crie ou edite um ícone que representa sua DSL no Windows Explorer. Por exemplo, editar **DslPackage\Resources\File.ico**  
  
3. Certifique-se de que os seguintes atributos de sua DSL estão corretos:  
  
   -   No Gerenciador de DSL, clique no nó raiz e na janela Propriedades, examine:  
  
       -   Descrição  
  
       -   Versão  
  
   -   Clique o **Editor** nó e na janela Propriedades, clique em **ícone**. Defina o valor para fazer referência a um arquivo de ícone em **DslPackage\Resources**, como **File.ico**  
  
   -   No **Build** menu, abra **Configuration Manager**e selecione a configuração que você deseja criar, como **versão** ou **depurar** .  
  
4. Vá para [homepage do SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=186128)e para o **Downloads** guia, baixe **CreateMsiSetupProject.tt**.  
  
5. Adicione **CreateMsiSetupProject.tt** ao seu projeto de Dsl.  
  
    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] criará um arquivo chamado **CreateMsiSetupProject.vdproj**.  
  
6. No Windows Explorer, copie Dsl\\\*.vdproj para uma nova pasta denominada programa de instalação.  
  
    (Se você quiser, você pode excluir CreateMsiSetupProject.tt do seu projeto de Dsl.)  
  
7. Na **Gerenciador de soluções**, adicione **instalação\\\*. vdproj** como um projeto existente.  
  
8. Sobre o **Project** menu, clique em **dependências do projeto**.  
  
    No **dependências do projeto** caixa de diálogo, selecione o projeto de instalação.  
  
    Marque a caixa ao lado **DslPackage**.  
  
9. Recompile a solução.  
  
10. No Windows Explorer, localize o arquivo MSI criado em seu projeto de instalação.  
  
     Copie o arquivo MSI para um computador no qual você deseja instalar a DSL. Clique duas vezes no arquivo MSI. O instalador é executado.  
  
11. No computador de destino, crie um novo arquivo que tem a extensão de arquivo de sua DSL. Verifique se:  
  
    -   Na exibição de lista do Windows Explorer, o arquivo aparece com o ícone e a descrição que você definiu.  
  
    -   Quando você clica duas vezes o arquivo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciado e abre o arquivo DSL em seu editor de DSL.  
  
    Se você preferir, você pode criar o projeto de instalação manualmente, em vez de usar o modelo de texto. Para obter uma explicação que inclui esse procedimento consulte o capítulo 5 do [laboratório do SDK de modelagem e visualização](http://go.microsoft.com/fwlink/?LinkId=208878).  
  
#### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>Para desinstalar uma DSL que foi instalada de um MSI  
  
1.  No Windows, abra o **programas e recursos** painel de controle.  
  
2.  Desinstale a DSL.  
  
3.  Reinicie o Visual Studio.




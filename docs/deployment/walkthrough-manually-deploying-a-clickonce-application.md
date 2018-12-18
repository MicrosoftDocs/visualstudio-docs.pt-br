---
title: 'Passo a passo: Implantando um aplicativo ClickOnce manualmente | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Mage.exe, manual ClickOnce deployments
- MageUI.exe, manual ClickOnce deployments
- deploying applications [ClickOnce], manual ClickOnce deployments
- ClickOnce deployment, manually
- ClickOnce deployment, SDK tools
- manual ClickOnce deployments
- manifests [ClickOnce]
ms.assetid: ccee6551-a1b9-4ca2-8845-9c1cf4ac2560
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e9f25c0e0b60a3b0f52df534db8f3593a26a435a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49902864"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application"></a>Passo a passo: Implantar um aplicativo ClickOnce manualmente
Se você não pode usar o Visual Studio para implantar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo ou você precisa usar recursos de implantação avançada, como implantação de aplicativos confiáveis, você deve usar o *Mage.exe* ferramenta de linha de comando para criar o seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos. Este passo a passo descreve como criar uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação usando a versão de linha de comando (*Mage.exe*) ou a versão gráfica (*MageUI.exe*) da geração de manifesto e Ferramenta de edição.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este passo a passo tem alguns pré-requisitos e opções que você precisa escolher antes de criar uma implantação.  
  
- Instale *Mage.exe* e *MageUI.exe*.  
  
   *Mage.exe* e *MageUI.exe* fazem parte do [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]. Você deve ter o [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] instalado ou a versão do [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] incluídos no Visual Studio. Para obter mais informações, consulte [SDK do Windows](http://go.microsoft.com/fwlink/?LinkId=158044) no MSDN.  
  
- Forneça um aplicativo para implantação.  
  
   Este passo a passo pressupõe que você tenha um aplicativo do Windows que você está pronto para implantar. Este aplicativo será referenciado como AppToDeploy.  
  
- Determine como a implantação será distribuída.  
  
   As opções de distribuição incluem: Web, compartilhamento de arquivos ou de CD. Para obter mais informações, consulte [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md).  
  
- Determine se o aplicativo requer um nível elevado de confiança.  
  
   Se seu aplicativo requer confiança total — por exemplo, acesso completo ao sistema do usuário — você pode usar o `-TrustLevel` opção de *Mage.exe* defini-lo. Se você quiser definir uma permissão personalizada definida para o seu aplicativo, você pode copiar a seção de permissão de Internet ou intranet do manifesto do outro, modificá-lo para atender às suas necessidades e adicioná-lo ao manifesto do aplicativo usando um editor de texto ou  *MageUI.exe*. Para obter mais informações, consulte [visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md).  
  
- Obtenha um certificado Authenticode.  
  
   Você deve entrar sua implantação com um certificado Authenticode. Você pode gerar um certificado de teste usando o Visual Studio, *MageUI.exe*, ou *MakeCert.exe* e *Pvk2Pfx.exe* ferramentas, ou você pode obter um certificado de um certificado Autoridade (CA). Se você optar por usar a implantação de aplicativos confiáveis, você também deve executar uma única instalação do certificado em todos os computadores cliente. Para obter mais informações, consulte [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md).  
  
  > [!NOTE]
  >  Você também pode entrar sua implantação com um certificado CNG que você pode obter de uma autoridade de certificação.  
  
- Certifique-se de que o aplicativo não tem um manifesto com informações do UAC.  
  
   Você precisa determinar se o seu aplicativo contém um manifesto com informações de controle de conta de usuário (UAC), como um `<dependentAssembly>` elemento. Para examinar um manifesto de aplicativo, você pode usar o Windows Sysinternals [Sigcheck](http://go.microsoft.com/fwlink/?LinkId=158035) utilitário.  
  
   Se seu aplicativo contém um manifesto com detalhes do UAC, você deve criá-la novamente sem as informações de UAC. Para um projeto c# no Visual Studio, abra as propriedades do projeto e selecione a guia do aplicativo. No **manifesto** lista suspensa, selecione **criar aplicativo sem um manifesto**. Para um projeto do Visual Basic no Visual Studio, abra as propriedades do projeto, selecione a guia aplicativo e clique em **exibir configurações de UAC**. No arquivo de manifesto aberto, remover todos os elementos dentro do único `<asmv1:assembly>` elemento.  
  
- Determine se o aplicativo requer os pré-requisitos no computador cliente.  
  
   [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] os aplicativos implantados do Visual Studio podem incluir um bootstrapper de instalação de pré-requisito (*setup.exe*) com sua implantação. Este passo a passo cria os dois manifestos necessários para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Você pode criar um bootstrapper pré-requisito usando o [tarefa GenerateBootstrapper](../msbuild/generatebootstrapper-task.md).  
  
### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>Para implantar um aplicativo com a ferramenta de linha de comando Mage.exe  
  
1. Crie um diretório onde você armazenará seus [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de implantação.  
  
2. No diretório de implantação que você acabou de criar, crie um subdiretório de versão. Se essa for a primeira vez que você está implantando o aplicativo, nomeie o subdiretório de versão **1.0.0.0**.  
  
   > [!NOTE]
   >  A versão da sua implantação pode ser distinta da versão do seu aplicativo.  
  
3. Copie todos os arquivos de aplicativo para o subdiretório de versão, incluindo arquivos executáveis, assemblies, recursos e arquivos de dados. Se necessário, você pode criar subpastas adicionais que contêm arquivos adicionais.  
  
4. Abra o [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] ou comando do Visual Studio solicitará e altere para o subdiretório de versão.  
  
5. Crie o manifesto do aplicativo com uma chamada para *Mage.exe*. A instrução a seguir cria um manifesto de aplicativo para o código compilado para execução no processador Intel x86.  
  
   ```cmd
   mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .   
   ```  
  
   > [!NOTE]
   >  Certifique-se de incluir o ponto (.) após o `-FromDirectory` opção, que indica o diretório atual. Se você não incluir o ponto, você deve especificar o caminho para os arquivos do aplicativo.  
  
6. Assinar o manifesto de aplicativo com seu certificado Authenticode. Substitua *mycert* com o caminho para o arquivo de certificado. Substitua *passwd* com a senha para o arquivo de certificado.  
  
   ```cmd
   mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd  
   ```  
  
   Começando com o SDK do .NET Framework 4.6.2, o que é distribuído com o Visual Studio e com o SDK do Windows, *mage.exe* assina os manifestos com CNG, bem como com certificados Authenticode. Use os mesmos parâmetros de linha de comando, assim como acontece com certificados Authenticode.
    
7. Altere para a raiz do diretório de implantação.  
  
8. Gere o manifesto de implantação com uma chamada para *Mage.exe*. Por padrão, *Mage.exe* marcará sua [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação como um aplicativo instalado, para que ele pode ser executado tanto online e offline. Para disponibilizar o aplicativo somente quando o usuário está online, use o `-Install` opção com um valor de `false`. Se você usar o padrão e os usuários instalarão o aplicativo de um site da Web ou compartilhamento de arquivos, verifique se o valor da `-ProviderUrl` de manifesto no servidor Web ou compartilhamento de pontos de opção para o local do aplicativo.  
  
   ```cmd  
   mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application  
   ```  
  
9. Assinar o manifesto de implantação com o seu certificado Authenticode ou CNG.  
  
    ```cmd  
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd  
    ```  
  
10. Copie todos os arquivos no diretório de implantação para o destino de implantação ou a mídia. Isso pode ser uma pasta em um site da Web ou site FTP, um compartilhamento de arquivos ou um CD-ROM.  
  
11. Fornece aos usuários com a URL, UNC ou necessárias para instalar o aplicativo de mídia física. Se você fornecer uma URL ou um UNC, você deve dar aos usuários o caminho completo para o manifesto de implantação. Por exemplo, se AppToDeploy é implantado http://webserver01/ no diretório AppToDeploy, o caminho da URL completo seria http://webserver01/AppToDeploy/AppToDeploy.application.  
  
### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>Para implantar um aplicativo com a ferramenta gráfica do MageUI.exe  
  
1. Crie um diretório onde você armazenará seus [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de implantação.  
  
2. No diretório de implantação que você acabou de criar, crie um subdiretório de versão. Se essa for a primeira vez que você está implantando o aplicativo, nomeie o subdiretório de versão **1.0.0.0**.  
  
   > [!NOTE]
   >  A versão da sua implantação é provavelmente diferente da versão do seu aplicativo.  
  
3. Copie todos os arquivos de aplicativo para o subdiretório de versão, incluindo arquivos executáveis, assemblies, recursos e arquivos de dados. Se necessário, você pode criar subpastas adicionais que contêm arquivos adicionais.  
  
4. Iniciar o *MageUI.exe* ferramenta gráfica.  
  
   ```cmd  
   MageUI.exe  
   ```  
  
5. Criar um novo manifesto de aplicativo, selecionando **arquivo**, **New**, **manifesto do aplicativo** no menu.  
  
6. No padrão **nome** guia, digite o número de versão e o nome dessa implantação. Especifique também o **processador** que seu aplicativo é compilado, como x86.  
  
7. Selecione o **arquivos** guia e clique no botão de reticências (**...** ) botão ao lado de **diretório de aplicativo** caixa de texto. Um **Procurar pasta** caixa de diálogo é exibida.  
  
8. Selecione o subdiretório de versão que contém os arquivos do aplicativo e, em seguida, clique em **Okey**.  
  
9. Se você implantará a partir dos serviços de informações da Internet (IIS), selecione a **quando preencher adiciona a extensão. Deploy em qualquer arquivo que não tenha** caixa de seleção.  
  
10. Clique o **popular** botão para adicionar todos os arquivos de aplicativo à lista de arquivos. Se seu aplicativo contiver mais de um arquivo executável, marcar o arquivo executável principal para essa implantação como o aplicativo de inicialização, selecionando **ponto de entrada** da **tipo de arquivo** lista suspensa. (Se seu aplicativo contiver apenas um arquivo executável, *MageUI.exe* marcará para você.)  
  
11. Selecione o **permissões necessárias** guia e selecione o nível de confiança que você precisa declarar seu aplicativo. O padrão é **FullTrust**, que será adequado para a maioria dos aplicativos.  
  
12. Selecione **arquivo**, **Salvar como** no menu. Uma caixa de diálogo Opções de assinatura é exibida solicitando que você assine o manifesto do aplicativo.  
  
13. Se você tiver um certificado armazenado como um arquivo em seu sistema de arquivos, use o **assinar com arquivo de certificado** opção e, em seguida, selecione o certificado do sistema de arquivos usando o botão de reticências (**...** ) botão. Em seguida, digite sua senha do certificado.  
  
     -ou-  
  
     Se seu certificado é mantido em um repositório de certificados acessível em seu computador, selecione o **assinar com certificado armazenado** opção e, em seguida, selecione o certificado na lista fornecida.  
  
14. Clique em **Okey** para assinar o manifesto do aplicativo. O **Salvar como** caixa de diálogo é exibida.  
  
15. No **Salvar como** caixa de diálogo, especifique o diretório de versão e, em seguida, clique em **salvar**.  
  
16. Selecione **arquivo**, **New**, **manifesto de implantação** no menu para criar o manifesto de implantação.  
  
17. Sobre o **nome** , especifique um nome e número de versão para essa implantação (**1.0.0.0** neste exemplo). Especifique também o **processador** que seu aplicativo é compilado, como x86.  
  
18. Selecione o **descrição** guia e especifique valores para **Publisher** e **produto**. (**Produto** é o nome dado ao seu aplicativo no menu Iniciar do Windows quando seu aplicativo é instalado em um computador cliente para uso offline.)  
  
19. Selecione o **opções de implantação** guia e, nas **local inicial** texto, especifique o local do manifesto do aplicativo no servidor Web ou compartilhamento. Por exemplo,  *\\\myServer\myShare\AppToDeploy.application*.  
  
20. Se você tiver adicionado a *Deploy* extensão em uma etapa anterior, também selecione **usar a extensão de nome de arquivo. Deploy** aqui.  
  
21. Selecione o **as opções de atualização** guia e, em seguida, especifique a frequência com que você gostaria que esse aplicativo para atualizar. Se seu aplicativo usa <xref:System.Deployment.Application.UpdateCheckInfo> para verificar se há atualizações em si, desmarque as **esse aplicativo deve verificar por atualizações** caixa de seleção.  
  
22. Selecione o **referência de aplicativo** guia e, em seguida, clique o **selecionar manifesto** botão. Uma caixa de diálogo Abrir é exibida.  
  
23. Selecione o manifesto do aplicativo que você criou anteriormente e, em seguida, clique em **aberto**.  
  
24. Selecione **arquivo**, **Salvar como** no menu. Um **opções de assinatura** caixa de diálogo será exibida solicitando que você assine o manifesto de implantação.  
  
25. Se você tiver um certificado armazenado como um arquivo em seu sistema de arquivos, use o **assinar com arquivo de certificado** opção e, em seguida, selecione o certificado do sistema de arquivos usando o botão de reticências (**...** ) botão. Em seguida, digite sua senha do certificado.  
  
     -ou-  
  
     Se seu certificado é mantido em um repositório de certificados acessível em seu computador, selecione o **assinar com certificado armazenado** opção e, em seguida, selecione o certificado na lista fornecida.  
  
26. Clique em **Okey** para assinar o manifesto de implantação. O **Salvar como** caixa de diálogo é exibida.  
  
27. No **Salvar como** caixa de diálogo Mover para cima um diretório para a raiz da sua implantação e clique **salvar**.  
  
28. Copie todos os arquivos no diretório de implantação para o destino de implantação ou a mídia. Isso pode ser uma pasta em um site da Web ou site FTP, um compartilhamento de arquivos ou um CD-ROM.  
  
29. Fornece aos usuários com a URL, UNC ou necessárias para instalar o aplicativo de mídia física. Se você fornecer uma URL ou um UNC, você deve dar aos usuários o caminho completo, o manifesto de implantação. Por exemplo, se AppToDeploy é implantado http://webserver01/ no diretório AppToDeploy, o caminho da URL completo seria http://webserver01/AppToDeploy/AppToDeploy.application.  
  
## <a name="next-steps"></a>Próximas etapas  
 Quando você precisa implantar uma nova versão do aplicativo, crie um novo diretório chamado após a nova versão — por exemplo, 1.0.0.1—and copiar novos arquivos de aplicativo para o novo diretório. Em seguida, você precisará seguir as etapas anteriores para criar e assinar um manifesto de aplicativo novo e atualizar e assinar o manifesto de implantação. Tenha cuidado para especificar a mesma versão superior em ambos os *Mage.exe* `-New` e `-Update` chamadas, como [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] atualiza somente as versões posteriores, com o mais significativo de número inteiro mais à esquerda. Se você usou *MageUI.exe*, você pode atualizar o manifesto de implantação ao abri-lo, selecionando a **referência de aplicativo** guia, clicando no **selecione manifesto** botão, e em seguida, selecionando o manifesto de aplicativo atualizado.  
  
## <a name="see-also"></a>Consulte também  
 [Mage.exe (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)   
 [MageUI.exe (Manifest Generation and Editing Tool, Cliente Gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)   
 [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)   
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
---
title: Segurança e implantação do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployment
- deploying applications [ClickOnce]
- ClickOnce deployment
- publishing, ClickOnce
ms.assetid: abab6d34-c3c2-45c1-a8b6-43c7d3131e7a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d33e99d11007ca4684f3d875620e2baeb7ddc1e7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285488"
---
# <a name="clickonce-security-and-deployment"></a>Segurança e implantação do ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]o é uma tecnologia de implantação que permite que você crie aplicativos baseados em Windows de atualização automática que podem ser instalados e executados com a interação mínima do usuário. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]fornece suporte completo para publicar e atualizar aplicativos implantados com a tecnologia ClickOnce se você tiver desenvolvido seus projetos com o Visual Basic e o Visual C#. Para obter informações sobre a implantação de aplicativos Visual C++, consulte [implantação do ClickOnce para aplicativos Visual C++](/cpp/windows/clickonce-deployment-for-visual-cpp-applications).

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]a implantação supera três problemas principais na implantação:

- **Dificuldades na atualização de aplicativos.** Com a implantação do Microsoft Windows Installer, sempre que um aplicativo é atualizado, o usuário pode instalar uma atualização, um arquivo MSP e aplicá-lo ao produto instalado; com a [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação, você pode fornecer atualizações automaticamente. Somente as partes do aplicativo que foram alteradas são baixadas e, em seguida, o aplicativo completo e atualizado é reinstalado a partir de uma nova pasta lado a lado.

- **Impacto no computador do usuário.** Com a implantação do Windows Installer, os aplicativos geralmente dependem de componentes compartilhados, com potencial para conflitos de controle de versão; com a [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação, cada aplicativo é independente e não pode interferir em outros aplicativos.

- **Permissões de segurança.** Windows Installer implantação requer permissões administrativas e permite apenas a instalação limitada do usuário; [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]a implantação permite que usuários não administrativos instalem e conceda apenas as permissões de segurança de acesso de código necessárias para o aplicativo.

  No passado, esses problemas às vezes fizeram com que os desenvolvedores optassem por criar aplicativos Web em vez de aplicativos baseados em Windows, sacrificando uma rica interface do usuário para facilitar a instalação. Usando aplicativos implantados usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o, você pode ter o melhor de ambas as tecnologias.

## <a name="what-is-a-clickonce-application"></a>O que é um aplicativo ClickOnce?
 Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é qualquer Windows Presentation Foundation (*. XBAP*), Windows Forms (*. exe*), aplicativo de console (*. exe*) ou solução do Office (*. dll*) publicado usando a [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] tecnologia. Você pode publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo de três maneiras diferentes: de uma página da Web, de um compartilhamento de arquivos de rede ou de mídia, como um CD-ROM. Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo pode ser instalado no computador de um usuário final e ser executado localmente mesmo quando o computador estiver offline ou pode ser executado em um modo somente online sem a instalação permanente de qualquer coisa no computador do usuário final. Para obter mais informações, consulte [escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md).

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]os aplicativos podem ser atualizados automaticamente; Eles podem verificar se há versões mais recentes à medida que se tornam disponíveis e substituir automaticamente todos os arquivos atualizados. O desenvolvedor pode especificar o comportamento da atualização; um administrador de rede também pode controlar estratégias de atualização, marcando uma atualização como obrigatória, por exemplo. As atualizações também podem ser revertidas para uma versão anterior pelo usuário final ou por um administrador. Para obter mais informações, consulte [escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md).

 Como [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] os aplicativos são isolados, a instalação ou a execução de um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo não pode interromper os aplicativos existentes. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]os aplicativos são independentes; cada [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é instalado e executado em um cache seguro por usuário por aplicativo. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]os aplicativos são executados nas zonas de segurança da Internet ou da intranet. Se necessário, o aplicativo poderá solicitar permissões de segurança elevadas. Para obter mais informações, consulte [proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).

## <a name="how-clickonce-security-works"></a>Como funciona a segurança do ClickOnce
 A [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] segurança principal é baseada em certificados, políticas de segurança de acesso a código e no prompt de confiança do ClickOnce.

### <a name="certificates"></a>Certificados
 Os certificados Authenticode são usados para verificar a autenticidade do editor do aplicativo. Usando Authenticode para implantação de aplicativos, o ClickOnce ajuda a impedir que um programa prejudicial se defunda como um programa legítimo proveniente de uma fonte confiável e estabelecida. Opcionalmente, os certificados também podem ser usados para assinar os manifestos de aplicativo e de implantação para provar que os arquivos não foram adulterados. Para obter mais informações, consulte [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md). Os certificados também podem ser usados para configurar os computadores cliente para que tenham uma lista de editores confiáveis. Se um aplicativo vier de um editor confiável, ele poderá ser instalado sem qualquer interação do usuário. Para obter mais informações, consulte [visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md).

### <a name="code-access-security"></a>Segurança de acesso do código
 A segurança de acesso ao código ajuda a limitar o acesso que o código tem aos recursos protegidos. Na maioria dos casos, você pode escolher as zonas da Internet ou da intranet local para limitar as permissões. Use a página **segurança** no **ProjectDesigner** para solicitar a zona apropriada para o aplicativo. Você também pode depurar aplicativos com permissões restritas para emular a experiência do usuário final. Para obter mais informações, consulte [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md).

### <a name="clickonce-trust-prompt"></a>Prompt de confiança do ClickOnce
 Se o aplicativo solicitar mais permissões do que a zona permite, o usuário final poderá ser solicitado a tomar uma decisão de confiança. O usuário final pode decidir se aplicativos ClickOnce, como Windows Forms aplicativos, Windows Presentation Foundation aplicativos, aplicativos de console, aplicativos de navegador XAML e soluções do Office são confiáveis para execução. Para obter mais informações, consulte [como: configurar o comportamento do prompt de confiança do ClickOnce](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md).

## <a name="how-clickonce-deployment-works"></a>Como funciona a implantação do ClickOnce
 A [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquitetura de implantação principal baseia-se em dois arquivos de manifesto XML: um manifesto de aplicativo e um manifesto de implantação. Os arquivos são usados para descrever onde os aplicativos ClickOnce são instalados, como eles são atualizados e quando são atualizados.

### <a name="publish-clickonce-applications"></a>Publicar aplicativos ClickOnce
 O manifesto do aplicativo descreve o próprio aplicativo. Isso inclui os assemblies, as dependências e os arquivos que compõem o aplicativo, as permissões necessárias e o local em que as atualizações estarão disponíveis. O desenvolvedor do aplicativo cria o manifesto do aplicativo usando o assistente de publicação no Visual Studio ou o Manifest Generation and Editing Tool (*Mage.exe*) no [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] . Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

 O manifesto de implantação descreve como o aplicativo é implantado. Isso inclui o local do manifesto do aplicativo e a versão do aplicativo que os clientes devem executar.

### <a name="deploy-clickonce-applications"></a>Implantar aplicativos ClickOnce
 Depois de criado, o manifesto de implantação é copiado para a localização de implantação. Pode ser um servidor Web, um compartilhamento de arquivo de rede ou uma mídia como um CD. O manifesto do aplicativo e todos os arquivos de aplicativo também são copiados para um local de implantação especificado no manifesto de implantação. Pode ser igual à localização de implantação ou não. Ao usar o **Assistente de publicação** no Visual Studio, as operações de cópia são executadas automaticamente.

### <a name="install-clickonce-applications"></a>Instalar aplicativos ClickOnce
 Depois de colocado na localização de implantação, os usuários finais podem baixar e instalar o aplicativo clicando em um ícone que representa o arquivo de manifesto de implantação em uma página da Web ou em uma pasta. Na maioria dos casos, o usuário final recebe uma caixa de diálogo simples solicitando que o usuário confirme a instalação, depois que a instalação continua e o aplicativo é iniciado sem intervenção adicional. Nos casos em que o aplicativo requer permissões elevadas ou se o aplicativo não está assinado por um certificado confiável, a caixa de diálogo também solicita que o usuário Conceda permissão antes que a instalação possa continuar. Embora as instalações do ClickOnce sejam por usuário, a elevação de permissão pode ser necessária se houver pré-requisitos que exijam privilégios de administrador. Para obter mais informações sobre permissões elevadas, consulte [Securing ClickOnce Applications](../deployment/securing-clickonce-applications.md).

 Os certificados podem ser confiáveis no nível da máquina ou da empresa, para que os aplicativos ClickOnce assinados com um certificado confiável possam ser instalados silenciosamente. Para obter mais informações sobre certificados confiáveis, consulte [visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md).

 O aplicativo pode ser adicionado ao menu **Iniciar** do usuário e ao grupo **Adicionar ou remover programas** no **painel de controle**. Ao contrário de outras tecnologias de implantação, nada é adicionado à pasta **arquivos de programas** ou ao registro, e nenhum direito administrativo é necessário para a instalação

> [!NOTE]
> Também é possível impedir que o aplicativo seja adicionado ao menu **Iniciar** e **Adicionar ou remover** o grupo de programas, de forma que ele se comporte como um aplicativo Web. Para obter mais informações, consulte [escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md).

### <a name="update-clickonce-applications"></a>Atualizar aplicativos ClickOnce
 Quando os desenvolvedores de aplicativos criam uma versão atualizada do aplicativo, eles geram um novo manifesto do aplicativo e copiam arquivos para um local de implantação — geralmente uma pasta irmã para a pasta de implantação do aplicativo original. O administrador atualiza o manifesto de implantação para que ele aponte para a localização da nova versão do aplicativo.

> [!NOTE]
> O **Assistente de publicação** no Visual Studio pode ser usado para executar essas etapas.

 Além da localização da implantação, o manifesto de implantação também contém uma localização de atualização (uma página da Web ou um compartilhamento de arquivo na rede), em que o aplicativo verifica a existência de versões atualizadas. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]As propriedades de **publicação** são usadas para especificar quando e com que frequência o aplicativo deve verificar se há atualizações. O comportamento de atualização pode ser especificado no manifesto de implantação ou pode ser apresentado como opções de usuário na interface do usuário do aplicativo por meio das [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] APIs. Além disso, as propriedades **Publish** podem ser empregadas para tornar as atualizações obrigatórias ou para a reversão para uma versão anterior. Para obter mais informações, consulte [escolhendo uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md).

### <a name="third-party-installers"></a>Instaladores de terceiros
 Você pode personalizar o instalador do ClickOnce para instalar componentes de terceiros junto com seu aplicativo. Você deve ter o pacote redistribuível (arquivo. exe ou. msi) e descrever o pacote com um manifesto de produto com neutralidade de idioma e um manifesto de pacote específico de idioma. Para obter mais informações, consulte [Creating bootstrapper Packages](../deployment/creating-bootstrapper-packages.md).

## <a name="clickonce-tools"></a>Ferramentas do ClickOnce
 A tabela a seguir mostra as ferramentas que você pode usar para gerar, editar, assinar e assinar novamente o aplicativo e os manifestos de implantação.

|Ferramenta|Descrição|
|----------|-----------------|
|[Página Segurança, Designer de Projeto](../ide/reference/security-page-project-designer.md)|Assina os manifestos de aplicativo e implantação.|
|[Página de Publicação, Designer de Projeto](../ide/reference/publish-page-project-designer.md)|Gera e edita os manifestos de aplicativo e implantação para aplicativos Visual Basic e Visual C#.|
|[*Mage.exe* (manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|Gera os manifestos de aplicativo e implantação para aplicativos Visual Basic, Visual C# e Visual C++.<br /><br /> Assina e assina novamente os manifestos de aplicativo e implantação.<br /><br /> Pode ser executado de scripts do lote e do prompt de comando.|
|[*MageUI.exe* (manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|Gera e edita os manifestos de aplicativo e implantação.<br /><br /> Assina e assina novamente os manifestos de aplicativo e implantação.|
|[Tarefa GenerateApplicationManifest](../msbuild/generateapplicationmanifest-task.md)|Gera o manifesto do aplicativo.<br /><br /> Pode ser executado do MSBuild. Para mais informações, confira veja [Referência do MSBuild](../msbuild/msbuild-reference.md).|
|[Tarefa GenerateDeploymentManifest](../msbuild/generatedeploymentmanifest-task.md)|Gera o manifesto de implantação.<br /><br /> Pode ser executado do MSBuild. Para mais informações, confira veja [Referência do MSBuild](../msbuild/msbuild-reference.md).|
|[Tarefa SignFile](../msbuild/signfile-task.md)|Assina os manifestos de aplicativo e implantação.<br /><br /> Pode ser executado do MSBuild. Para mais informações, confira veja [Referência do MSBuild](../msbuild/msbuild-reference.md).|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|Desenvolva seu próprio aplicativo para gerar os manifestos de aplicativo e implantação.|

 A tabela a seguir mostra a versão .NET Framework necessária para dar suporte a aplicativos ClickOnce nesses navegadores.

|Navegador|Versão do .NET Framework|
|-------------|----------------------------|
|Internet Explorer|2.0, 3.0, 3.5, 3.5 SP1, 4|
|Firefox|2.0 SP1, 3.5 SP1, 4|
|Chrome|3,5|
|Microsoft Edge|3,5|

## <a name="see-also"></a>Veja também
- [Implantação do ClickOnce no Windows Vista](../deployment/clickonce-deployment-on-windows-vista.md)
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Implantar componentes COM o ClickOnce](../deployment/deploying-com-components-with-clickonce.md)
- [Compilar aplicativos ClickOnce usando a linha de comando](../deployment/building-clickonce-applications-from-the-command-line.md)
- [Depurar aplicativos ClickOnce que usam System. Deployment. Application](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)

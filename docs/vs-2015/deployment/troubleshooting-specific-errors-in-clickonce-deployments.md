---
title: Solução de problemas de erros específicos nas implantações do ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.UncRequired
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.NoInstallUrl
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
ms.assetid: 22dfe8f1-8271-4708-9c25-6bbb13920ac8
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: d0b7e53eba21372641bad683c442e796648a4765
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49213636"
---
# <a name="troubleshooting-specific-errors-in-clickonce-deployments"></a>Solução de problemas com erros específicos nas implantações do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico lista os seguintes erros comuns que podem ocorrer quando você implanta um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo e fornece etapas para resolver cada problema.  
  
## <a name="general-errors"></a>Erros gerais  
  
#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>Quando você tentar localizar um arquivo. Application, nada ocorre, renderiza o XML no Internet Explorer ou você receberá uma caixa de diálogo Executar ou salvar como  
 Esse erro provavelmente é causado por tipos de conteúdo (também conhecido como tipos de MIME) não está sendo registrados corretamente no servidor ou cliente.  
  
 Primeiro, certifique-se de que o servidor está configurado para associar a extensão. Application "application/x-ms-application" tipo de conteúdo.  
  
 Se o servidor está configurado corretamente, certifique-se de que o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] é instalado em seu computador. Se o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] estiver instalado, e você ainda estiver vendo esse problema, tente desinstalar e reinstalar o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] para registrar novamente o tipo de conteúdo no cliente.  
  
#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>Mensagem de erro afirma, "não é possível recuperar o aplicativo. Arquivos ausentes na implantação"ou"download do aplicativo foi interrompido, verifique se há erros de rede e tente novamente mais tarde"  
 Esta mensagem indica que um ou mais arquivos que está sendo referenciados pelo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos não podem ser baixados. A maneira mais fácil para depurar esse erro é tentar baixar a URL que [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] diz que ele não é possível baixar. Aqui estão algumas das possíveis causas:  
  
-   Se o arquivo de log diz "(403) proibido" ou "(404) não é encontrada," Verifique se o servidor Web é configurado para que ele não bloqueia o download deste arquivo. Para obter mais informações, consulte [Problemas de configuração de servidor e cliente em implantações do ClickOnce](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md).  
  
-   Se o arquivo. config está sendo bloqueado pelo servidor, consulte a seção "Erro de Download quando você tenta instalar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo que tem um arquivo. config" mais adiante neste tópico.  
  
-   Determinar se isso ocorreu porque o `deploymentProvider` URL no manifesto de implantação está apontando para um local diferente que a URL usada para ativação.  
  
-   Certifique-se de que todos os arquivos estão presentes no servidor. o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] log deve informar a qual arquivo não foi encontrado.  
  
-   Se houver problemas de conectividade de rede; Você pode receber essa mensagem se o computador cliente ficou offline durante o download.  
  
#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>Erro de download quando você tenta instalar um aplicativo ClickOnce que tem um arquivo. config  
 Por padrão, um aplicativo baseado em Windows do Visual Basic inclui um arquivo App. config. Haverá um problema quando um usuário tenta instalar de um servidor Web que usa o Windows Server 2003, porque o sistema operacional bloqueia a instalação de arquivos. config por motivos de segurança. Para habilitar o arquivo. config ser instalado, clique em **usar a extensão de arquivo. Deploy"** na **opções de publicação** caixa de diálogo.  
  
 Você também deve definir os tipos de conteúdo (também conhecido como tipos de MIME) adequadamente para arquivos. Deploy,. Application e. manifest. Para obter mais informações, consulte a documentação do servidor Web.  
  
 Para obter mais informações, consulte "Windows Server 2003: outra tipos de conteúdo" em [problemas de configuração de cliente em implantações do ClickOnce e servidor](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md).  
  
#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>Mensagem de erro: "Aplicativo está formatado incorretamente;" Arquivo de log contém "assinatura XML é inválida"  
 Certifique-se de que você atualizou o arquivo de manifesto e assinado novamente. Republique o aplicativo usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou use Mage para assinar o aplicativo novamente.  
  
#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>Você atualizou seu aplicativo no servidor, mas o cliente não baixa a atualização  
 Esse problema poderá ser resolvido executando uma das seguintes tarefas:  
  
-   Examinar o `deploymentProvider` URL no manifesto de implantação. Certifique-se de que você está atualizando os bits no mesmo local que `deploymentProvider` aponta.  
  
-   Verifique se o intervalo de atualização no manifesto de implantação. Se esse intervalo é definido para um intervalo periódico, como uma vez a cada seis horas, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] não examinará uma atualização até que esse intervalo tenha passado. Você pode alterar o manifesto para procurar uma atualização sempre que o aplicativo for iniciado. Alterar o intervalo de atualização é uma opção conveniente durante o tempo de desenvolvimento para verificar se estão sendo instaladas atualizações, mas ele desacelera a ativação do aplicativo.  
  
-   Tente reiniciar o aplicativo no menu Iniciar. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] pode ter detectado a atualização em segundo plano, mas solicitará que você instale os bits na próxima ativação.  
  
#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>Durante a atualização, você recebe um erro com a seguinte entrada de log: "a referência na implantação não coincide com a identidade definida no manifesto do aplicativo"  
 Esse erro pode ocorrer porque você editar manualmente os manifestos de implantação e o aplicativo e ter causado a descrição da identidade de um assembly em um manifesto para que fiquem fora de sincronia com as outras. A identidade de um assembly consiste em seu nome, versão, cultura e token de chave pública. Examine as descrições de identidade em seus manifestos e corrigir quaisquer diferenças.  
  
#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>Primeira vez que a ativação do CD-ROM ou disco local for bem-sucedida, mas subsequente ativação do Menu Iniciar não tiver êxito  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] usa a URL do provedor de implantação para receber atualizações para o aplicativo. Verifique se o local que aponta para a URL está correto.  
  
#### <a name="error-cannot-start-the-application"></a>Erro: "não é possível iniciar o aplicativo"  
 Essa mensagem de erro geralmente indica que há um problema ao instalar esse aplicativo para o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] armazenar. O aplicativo tem um erro ou o repositório está corrompido. O arquivo de log pode informar onde ocorreu o erro.  
  
 Você deve fazer o seguinte:  
  
-   Verifique se a identidade do manifesto de implantação, identidade do manifesto de aplicativo e identidade do aplicativo principal EXE são exclusivos.  
  
-   Verifique se seus caminhos de arquivo não estão mais de 100 caracteres. Se seu aplicativo contém os caminhos de arquivo que são muito longos, você poderá exceder as limitações do caminho máximo que você pode armazenar. Tente encurtar os caminhos e reinstale.  
  
#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>PrivatePath configurações no arquivo de configuração de aplicativo não são consideradas  
 Para usar PrivatePath (caminhos de investigação do Fusion), o aplicativo deve solicitar permissão de confiança total. Tente alterar o manifesto do aplicativo para solicitar confiança total e, em seguida, tente novamente.  
  
#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>Durante a desinstalação será exibida uma mensagem dizendo, "Falha ao desinstalar o aplicativo"  
 Essa mensagem geralmente indica que o aplicativo já foi removido ou o repositório está corrompido. Depois de clicar em **Okey**, o **adicionar ou remover programa** entrada será removida.  
  
#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>Durante a instalação, será exibida uma mensagem que diz que as dependências de plataforma não estão instaladas  
 Falta um pré-requisito no GAC (cache de assembly global) que o aplicativo precisa para executar.  
  
## <a name="publishing-with-visual-studio"></a>Publicação com o Visual Studio  
  
#### <a name="publishing-in-visual-studio-fails"></a>Falha de publicação no Visual Studio  
 Certifique-se de que você tenha o direito de publicar no servidor de destino. Por exemplo, se você está conectado a um computador de servidor de terminal como um usuário comum, não como um administrador, você provavelmente não terá os direitos necessários para publicar no servidor Web local.  
  
 Se você estiver publicando com uma URL, certifique-se de que o computador de destino tem o FrontPage Server Extensions habilitado.  
  
#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>Mensagem de erro: Não é possível criar o site da Web '\<site >'. Os componentes para se comunicar com as extensões FrontPage Server Extensions não estão instalados.  
 Certifique-se de que você tenha o Microsoft Visual Studio Web criação componente instalado no computador em que você está publicando da. Para usuários do Express, esse componente não está instalado por padrão. Para obter mais informações, consulte [http://go.microsoft.com/fwlink/?LinkId=102310](http://go.microsoft.com/fwlink/?LinkId=102310).  
  
#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>Mensagem de erro: Não foi possível encontrar o arquivo ' Microsoft.Windows.Common-controles, versão = 6.0.0.0, Culture = *, PublicKeyToken = 6595b64144ccf1df, ProcessorArchitecture =\*, tipo = win32'  
 Essa mensagem de erro aparece quando você tentar publicar um aplicativo WPF com estilos visuais habilitados. Para resolver esse problema, consulte [como: publicar um aplicativo WPF com estilos visuais habilitados](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md).  
  
## <a name="using-mage"></a>Usando o Mage  
  
#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>Você tentou entrar com um certificado no repositório de certificados e uma caixa de mensagem em branco recebidos  
 No **Signing** caixa de diálogo, você deve:  
  
-   Selecione **assinar com um certificado armazenado**, e  
  
-   Selecione um certificado da lista; o primeiro certificado não é a seleção padrão.  
  
#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>Clicar no botão "Entrar não" faz com que uma exceção  
 Esse problema é um bug conhecido. Todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos são necessários a serem assinados. Basta selecionar uma das opções de assinatura e, em seguida, clique em **Okey**.  
  
## <a name="additional-errors"></a>Outros erros  
 A tabela a seguir mostra algumas mensagens de erro comuns que um usuário do computador cliente pode receber quando o usuário instala um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Cada mensagem de erro é listada ao lado de uma descrição do que a causa mais provável do erro.  
  
|mensagem de erro|Descrição|  
|-------------------|-----------------|  
|Aplicativo não pode ser iniciado. Entre em contato com o Editor do aplicativo.<br /><br /> Não é possível iniciar o aplicativo. Para obter assistência, entre em contato com o fornecedor do aplicativo.|Essas são mensagens de erro genérico que ocorrem quando o aplicativo não pode ser iniciado, e nenhum outro motivo específico pode ser encontrado. Com frequência isso significa que o aplicativo está corrompido de alguma forma, ou que o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] repositório está corrompido.|  
|Não é possível continuar. O aplicativo está formatado incorretamente. Para obter assistência, entre em contato com o Editor do aplicativo.<br /><br /> Validação de aplicativo não foi bem-sucedida. Não é possível continuar.<br /><br /> Não é possível recuperar arquivos do aplicativo. Arquivos corrompidos na implantação.|Um dos arquivos de manifesto na implantação sintaticamente não é válido ou contém um hash que não pode ser reconciliado com o arquivo correspondente. Esse erro também pode indicar que o manifesto inserido dentro de um assembly está corrompido. Crie novamente sua implantação e recompilar seu aplicativo, ou encontrar e corrigir os erros manualmente em seus manifestos.|  
|Não é possível recuperar o aplicativo. Erro de autenticação.<br /><br /> Instalação do aplicativo não foi bem-sucedida. Não é possível localizar arquivos de aplicativos no servidor. Entre em contato com o Editor do aplicativo ou o administrador para obter assistência.|Não não possível baixar um ou mais arquivos na implantação porque você não tem permissão para acessá-los. Isso pode ser causado por um erro proibido 403, que está sendo retornado por um servidor Web, que pode ocorrer se um dos arquivos em sua implantação terminar com uma extensão que faz com que o servidor Web tratá-lo como um arquivo protegido. Além disso, um diretório que contém um ou mais dos arquivos do aplicativo pode exigir um nome de usuário e senha para acessar.|  
|Não é possível baixar o aplicativo. O aplicativo não tem os arquivos necessários. Entre em contato com o fornecedor do aplicativo ou o administrador do sistema para obter assistência.|Um ou mais dos arquivos listados no manifesto do aplicativo não podem ser encontrado no servidor. Verifique se que você carregou todos os arquivos de implantação dependentes e tente novamente.|  
|Download do aplicativo não foi bem-sucedida. Verifique sua conexão de rede ou contate o administrador do sistema ou o provedor de serviços de rede.|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] não é possível estabelecer uma conexão de rede para o servidor. Examine a disponibilidade do servidor e o estado da sua rede.|  
|URLDownloadToCacheFile falhou com HRESULT '\<número >'. Ocorreu um erro ao tentar baixar '\<arquivo >'.|Se um usuário tiver definido a opção de segurança avançada do Internet Explorer "Avisar se a alteração entre o modo de segurança" no computador de destino de implantação, e se a URL de instalação do aplicativo ClickOnce que está sendo instalado é redirecionada do não seguro para um site seguro (ou vice-versa), a instalação falhará porque o aviso do Internet Explorer interrompe-lo.<br /><br /> Para resolver esse problema, siga um destes procedimentos:<br /><br /> – Desmarque a opção de segurança.<br />-Certifique-se de que a URL de instalação não é redirecionada de forma que altera os modos de segurança.<br />-Remova o redirecionamento completamente e apontar para a URL de instalação real.|  
|Ocorreu um erro gravando no disco rígido. Pode haver espaço suficiente disponível no disco. Entre em contato com o fornecedor do aplicativo ou o administrador do sistema para obter assistência.|Isso pode indicar um espaço em disco insuficiente para armazenar o aplicativo, mas ele também pode indicar um erro de e/s mais geral, quando você está tentando salvar os arquivos de aplicativo para a unidade.|  
|Não é possível iniciar o aplicativo. Não há espaço suficiente disponível no disco.|O disco rígido está cheio. Limpar espaço e tente executar o aplicativo novamente.|  
|Número excessivo de ativações implantadas estão tentando carregar ao mesmo tempo.|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] limita o número de aplicativos diferentes que pode começar ao mesmo tempo. Isso é basicamente para ajudar a proteger contra tentativas mal-intencionadas de que haja ataques de negação de serviço contra local [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] serviço; os usuários que tentem iniciar o mesmo aplicativo várias vezes, em sucessão rápida, só acabará com uma única instância das aplicativo.|  
|Atalhos não podem ser ativados pela rede.|Atalhos para um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo só pode ser iniciado no disco rígido local. Eles não podem ser iniciados, abrindo uma URL que aponta para um arquivo de atalho em um servidor remoto.|  
|O aplicativo é muito grande para ser executado online em confiança parcial. Entre em contato com o fornecedor do aplicativo ou o administrador do sistema para obter assistência.|Um aplicativo executado em confiança parcial não pode ser maior do que a metade do tamanho da cota de aplicativo online, que é de 250 MB por padrão.|  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Solução de problemas de implantações ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)




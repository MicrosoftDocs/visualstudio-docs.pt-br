---
title: Solucionando problemas de erros específicos em implantações do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66a98a822cd9aac6d93b4964e2e8bdadc98972e5
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381893"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>Solucionar erros específicos em implantações do ClickOnce
Este artigo lista os seguintes erros comuns que podem ocorrer quando você implanta um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo e fornece etapas para resolver cada problema.

## <a name="general-errors"></a>Erros gerais

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>Quando você tenta localizar um arquivo de aplicativo, nada acontece ou renderizações XML no Internet Explorer, ou você recebe uma caixa de diálogo Executar ou salvar como
 Esse erro é provavelmente causado por tipos de conteúdo (também conhecidos como tipos MIME) que não estão sendo registrados corretamente no servidor ou cliente.

 Primeiro, verifique se o servidor está configurado para associar a extensão *. Application* ao tipo de conteúdo "application/x-MS-Application".

 Se o servidor estiver configurado corretamente, verifique se o .NET Framework 2,0 está instalado no computador. Se o .NET Framework 2,0 estiver instalado e você ainda estiver vendo esse problema, tente desinstalar e reinstalar o .NET Framework 2,0 para registrar novamente o tipo de conteúdo no cliente.

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>Mensagem de erro informa "não é possível recuperar o aplicativo. Arquivos ausentes na implantação "ou" o download do aplicativo foi interrompido, verifique se há erros de rede e tente novamente mais tarde "
 Essa mensagem indica que um ou mais arquivos sendo referenciados pelos [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos não podem ser baixados. A maneira mais fácil de depurar esse erro é tentar baixar a URL que diz que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] não é possível baixar. Aqui estão algumas causas possíveis:

- Se o arquivo de log disser "(403) proibido" ou "(404) não encontrado", verifique se o servidor Web está configurado para que ele não bloqueie o download desse arquivo. Para obter mais informações, consulte [Problemas de configuração de servidor e cliente em implantações do ClickOnce](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md).

- Se o arquivo *. config* estiver sendo bloqueado pelo servidor, consulte a seção "erro de download ao tentar instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que tenha um arquivo. config", mais adiante neste artigo.

- Determine se esse erro ocorreu porque a `deploymentProvider` URL no manifesto de implantação está apontando para um local diferente da URL usada para ativação.

- Verifique se todos os arquivos estão presentes no servidor; o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] log deve informar qual arquivo não foi encontrado.

- Veja se há problemas de conectividade de rede; Você poderá receber essa mensagem se o computador cliente ficou offline durante o download.

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>Erro de download ao tentar instalar um aplicativo ClickOnce que tem um arquivo. config
 Por padrão, um aplicativo baseado no Windows Visual Basic inclui um arquivo de App.config. Haverá um problema quando um usuário tentar instalar a partir de um servidor Web que usa o Windows Server 2003, porque esse sistema operacional bloqueia a instalação de arquivos *. config* por motivos de segurança. Para habilitar o arquivo *. config* a ser instalado, clique em **usar extensão de arquivo ". Deploy"** na caixa de diálogo **Opções de publicação** .

 Você também deve definir os tipos de conteúdo (também conhecidos como tipos MIME) adequadamente para os arquivos. Application,. manifest e. Deploy. Para obter mais informações, consulte a documentação do seu servidor Web.

 Para obter mais informações, consulte "Windows Server 2003: tipos de conteúdo bloqueados" em [problemas de configuração de servidor e cliente em implantações do ClickOnce](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md).

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>Mensagem de erro: "o aplicativo está formatado incorretamente;" O arquivo de log contém "a assinatura XML é inválida"
 Verifique se você atualizou o arquivo de manifesto e o assinou novamente. Republique o aplicativo usando [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou use o Mage para assinar o aplicativo novamente.

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>Você atualizou seu aplicativo no servidor, mas o cliente não baixa a atualização
 Esse problema pode ser resolvido com a conclusão de uma das seguintes tarefas:

- Examine a `deploymentProvider` URL no manifesto de implantação. Verifique se você está atualizando os bits no mesmo local que `deploymentProvider` aponta para o.

- Verifique o intervalo de atualização no manifesto de implantação. Se esse intervalo for definido como um intervalo periódico, como uma vez a cada seis horas, o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] não verificará se há uma atualização até que esse intervalo tenha passado. Você pode alterar o manifesto para verificar se há uma atualização toda vez que o aplicativo for iniciado. A alteração do intervalo de atualização é uma opção conveniente durante o tempo de desenvolvimento para verificar se as atualizações estão sendo instaladas, mas reduz a ativação do aplicativo.

- Tente iniciar o aplicativo novamente no menu iniciar. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]pode ter detectado a atualização em segundo plano, mas solicitará que você instale os bits na próxima ativação.

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>Durante a atualização, você recebe um erro com a seguinte entrada de log: "a referência na implantação não corresponde à identidade definida no manifesto do aplicativo"
 Esse erro pode ocorrer porque você editou manualmente a implantação e os manifestos do aplicativo, e fez com que a descrição da identidade de um assembly em um manifesto fique fora de sincronia com a outra. A identidade de um assembly consiste em seu nome, versão, cultura e token de chave pública. Examine as descrições de identidade em seus manifestos e corrija as diferenças.

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>A ativação pela primeira vez do disco local ou do CD-ROM é realizada com sucesso, mas a ativação subsequente do menu Iniciar não é concluída
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]usa a URL do provedor de implantação para receber atualizações para o aplicativo. Verifique se o local ao qual a URL está apontando está correto.

#### <a name="error-cannot-start-the-application"></a>Erro: "não é possível iniciar o aplicativo"
 Essa mensagem de erro geralmente indica que há um problema ao instalar esse aplicativo na [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] loja. O aplicativo tem um erro ou o repositório está corrompido. O arquivo de log pode informar onde ocorreu o erro.

 Você deve fazer o seguinte:

- Verifique se a identidade do manifesto de implantação, a identidade do manifesto do aplicativo e a identidade do aplicativo EXE principal são exclusivas.

- Verifique se os caminhos de arquivo não têm mais de 100 caracteres. Se seu aplicativo contiver caminhos de arquivo que são muito longos, você poderá exceder as limitações no caminho máximo que você pode armazenar. Tente encurtar os caminhos e reinstalar.

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>As configurações de PrivatePath no arquivo de configuração de aplicativo não são respeitadas
 Para usar PrivatePath (caminhos de investigação de fusão), o aplicativo deve solicitar a permissão de confiança total. Tente alterar o manifesto do aplicativo para solicitar confiança total e tente novamente.

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>Durante a desinstalação, aparece uma mensagem dizendo "falha ao desinstalar o aplicativo"
 Essa mensagem geralmente indica que o aplicativo já foi removido ou o repositório está corrompido. Depois de clicar em **OK**, a entrada **Adicionar/remover programa** será removida.

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>Durante a instalação, aparece uma mensagem dizendo que as dependências de plataforma não estão instaladas
 Você não tem um pré-requisito no GAC (cache de assembly global) que o aplicativo precisa para ser executado.

## <a name="publishing-with-visual-studio"></a>Publicando com o Visual Studio

#### <a name="publishing-in-visual-studio-fails"></a>Falha na publicação no Visual Studio
 Verifique se você tem o direito de publicar no servidor de destino. Por exemplo, se você estiver conectado a um computador do Terminal Server como um usuário comum, e não como um administrador, provavelmente não terá os direitos necessários para publicar no servidor Web local.

 Se você estiver publicando com uma URL, verifique se o computador de destino tem as extensões de servidor do FrontPage habilitadas.

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>Mensagem de erro: não é possível criar o site ' \<site> '. Os componentes para comunicação com as extensões de servidor do FrontPage não estão instalados.
 Verifique se você tem o Microsoft Visual Studio Web Authoring Component instalado no computador do qual você está publicando. Para usuários expressos, esse componente não é instalado por padrão. Para obter mais informações, consulte [http://go.microsoft.com/fwlink/?LinkId=102310](https://support.microsoft.com/help/945358).

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>Mensagem de erro: não foi possível encontrar o arquivo ' Microsoft. Windows. Common-Controls, Version = 6.0.0.0, cultura = *, PublicKeyToken = 6595b64144ccf1df, ProcessorArchitecture = \* , Type = Win32 '
 Essa mensagem de erro é exibida quando você tenta publicar um aplicativo WPF com estilos visuais habilitados. Para resolver esse problema, consulte [como: publicar um aplicativo WPF com estilos visuais habilitados](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md).

## <a name="using-mage"></a>Usando o Mage

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>Você tentou assinar com um certificado em seu repositório de certificados e uma caixa de mensagem em branco recebida
 Na caixa de diálogo **assinatura** , você deve:

- Selecione **assinar com um certificado armazenado**e

- Selecione um certificado da lista; o primeiro certificado não é a seleção padrão.

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>Clicar no botão "não assinar" causa uma exceção
 Esse problema é um bug conhecido. Todos os [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos devem ser assinados. Basta selecionar uma das opções de assinatura e clicar em **OK**.

## <a name="additional-errors"></a>Erros adicionais
 A tabela a seguir mostra algumas mensagens de erro comuns que um usuário do computador cliente pode receber quando o usuário instala um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Cada mensagem de erro é listada ao lado de uma descrição da causa mais provável para o erro.

| Mensagem de erro | Descrição |
| - | - |
| Não é possível iniciar o aplicativo. Contate o editor do aplicativo.<br /><br /> Não é possível iniciar o aplicativo. Contate o fornecedor do aplicativo para obter assistência. | Essas são mensagens de erro genéricas que ocorrem quando o aplicativo não pode ser iniciado, e nenhum outro motivo específico pode ser encontrado. Frequentemente, isso significa que o aplicativo está de alguma forma corrompido ou que o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] repositório está corrompido. |
| Não é possível continuar. O aplicativo está formatado incorretamente. Contate o editor de aplicativos para obter assistência.<br /><br /> A validação do aplicativo não teve sucesso. Não é possível continuar.<br /><br /> Não é possível recuperar os arquivos do aplicativo. Arquivos corrompidos na implantação. | Um dos arquivos de manifesto na implantação é sintaticamente inválido ou contém um hash que não pode ser reconciliado com o arquivo correspondente. Esse erro também pode indicar que o manifesto inserido dentro de um assembly está corrompido. Recrie a implantação e recompile seu aplicativo, ou localize e corrija os erros manualmente em seus manifestos. |
| Não é possível recuperar o aplicativo. Erro de autenticação.<br /><br /> A instalação do aplicativo não teve sucesso. Não é possível localizar os arquivos de aplicativos no servidor. Contate o editor do aplicativo ou o administrador para obter assistência. | Um ou mais arquivos na implantação não podem ser baixados porque você não tem permissão para acessá-los. Isso pode ser causado por um erro proibido 403 sendo retornado por um servidor Web, o que pode ocorrer se um dos arquivos em sua implantação terminar com uma extensão que faz com que o servidor Web o trate como um arquivo protegido. Além disso, um diretório que contém um ou mais arquivos do aplicativo pode exigir um nome de usuário e uma senha para acessar o. |
| Não é possível baixar o aplicativo. Os arquivos necessários estão ausentes no aplicativo. Contate o fornecedor do aplicativo ou o administrador do sistema para obter assistência. | Um ou mais dos arquivos listados no manifesto do aplicativo não podem ser encontrados no servidor. Verifique se você carregou todos os arquivos dependentes da implantação e tente novamente. |
| O download do aplicativo não teve sucesso. Verifique sua conexão de rede ou contate o administrador do sistema ou o provedor de serviços de rede. | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]Não é possível estabelecer uma conexão de rede com o servidor. Examine a disponibilidade do servidor e o estado da sua rede. |
| URLDownloadToCacheFile falhou com HRESULT ' \<number> '. Ocorreu um erro ao tentar baixar ' \<file> '. | Se um usuário tiver definido a opção de segurança avançada do Internet Explorer "avisar se estiver mudando entre o modo seguro e não seguro" no computador de destino da implantação, e se a URL de instalação do aplicativo ClickOnce que está sendo instalado for redirecionada de um site não seguro para um local seguro (ou vice-versa), a instalação falhará porque o aviso do Internet Explorer o interrompe.<br /><br /> Para resolver esse erro, você pode executar uma das seguintes tarefas:<br /><br /> -Desmarque a opção de segurança.<br />-Certifique-se de que a URL de instalação não seja redirecionada de forma que altere os modos de segurança.<br />-Remova completamente o redirecionamento e aponte para a URL de instalação real. |
| Ocorreu um erro ao gravar no disco rígido. Pode haver espaço insuficiente disponível no disco. Contate o fornecedor do aplicativo ou o administrador do sistema para obter assistência. | Isso pode indicar espaço em disco insuficiente para armazenar o aplicativo, mas ele também pode indicar um erro de e/s mais geral quando você estiver tentando salvar os arquivos de aplicativo na unidade. |
| Não é possível iniciar o aplicativo. Não há espaço disponível suficiente no disco. | O disco rígido está cheio. Desmarque o espaço e tente executar o aplicativo novamente. |
| Muitas ativações implantadas estão tentando carregar de uma vez. | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]limita o número de aplicativos diferentes que podem ser iniciados ao mesmo tempo. Isso é amplamente útil para ajudar a proteger contra tentativas mal-intencionadas de provocar ataques de negação de serviço contra o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] serviço local. os usuários que tentarem iniciar o mesmo aplicativo repetidamente, em sucessão rápida, acabarão com uma única instância do aplicativo. |
| Os atalhos não podem ser ativados pela rede. | Os atalhos para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo só podem ser iniciados no disco rígido local. Eles não podem ser iniciados abrindo uma URL que aponta para um arquivo de atalho em um servidor remoto. |
| O aplicativo é muito grande para ser executado online em confiança parcial. Contate o fornecedor do aplicativo ou o administrador do sistema para obter assistência. | Um aplicativo que é executado em confiança parcial não pode ser maior que metade do tamanho da cota do aplicativo online, que por padrão é 250 MB. |

## <a name="see-also"></a>Veja também
- [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)
- [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)
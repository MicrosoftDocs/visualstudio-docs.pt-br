---
title: Solucionar problemas de implantação de solução do Office
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 679a6e753e61ecb1af9097692a741c35e531c7cc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545737"
---
# <a name="troubleshoot-office-solution-deployment"></a>Solucionar problemas de implantação de solução do Office
  Este tópico contém informações sobre como resolver problemas comuns que você pode encontrar ao implantar soluções do Office.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="troubleshoot-office-solutions-by-using-the-event-viewer"></a>Solucionar problemas de soluções do Office usando o Visualizador de eventos
 Você pode usar o Visualizador de eventos no Windows para ver as mensagens de erro que são capturadas pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] quando você instala ou desinstala as soluções do Office. Você pode usar essas mensagens do agente de log de eventos para resolver problemas de instalação e implantação. Para obter mais informações, consulte [log de eventos para soluções do Office](../vsto/event-logging-for-office-solutions.md).

## <a name="change-the-assembly-name-causes-conflicts"></a>Alterar o nome do assembly causa conflitos
 Se você alterar o valor do **nome do assembly** na página do **aplicativo** do **Designer de projeto** depois de ter implantado uma solução, as ferramentas de publicação modificarão o pacote de instalação para ter um arquivo de *Setup.exe* e dois manifestos de implantação. Se você implantar dois arquivos de manifesto, as seguintes condições poderão ocorrer:

- Se o usuário final instalar ambas as versões, o aplicativo carregará ambos os suplementos do VSTO.

- Se o suplemento do VSTO foi instalado antes da alteração do nome do assembly, o usuário final nunca receberá atualizações.

  Para evitar essas condições, não altere o valor do **nome do assembly** da solução depois de implantar a solução.

## <a name="check-for-updates-takes-a-long-time"></a>Verificar se há atualizações leva muito tempo
 O tempo de execução das ferramentas do Visual Studio 2010 para Office fornece uma entrada de registro que os administradores podem usar para definir o valor de tempo limite para baixar os manifestos e a solução.

#### <a name="to-set-the-time-out-value"></a>Para definir o valor de tempo limite

1. No registro, navegue até a seguinte chave:

     **HKEY_CURRENT_USER \Software\Microsoft\VSTA**

2. Na subchave **AddInTimeout** , defina o valor de tempo limite em milissegundos.

     Se a subchave **AddInTimeout** não existir, crie-a como um DWORD.

## <a name="cant-update-or-publish-to-a-network-file-share"></a>Não é possível atualizar ou publicar em um compartilhamento de arquivos de rede
 As soluções do Office que estão em um compartilhamento de arquivos de rede podem exibir uma mensagem enganosa durante as atualizações se o arquivo de *Setup.exe* da solução estiver bloqueado em um processo enquanto a atualização estiver sendo publicada. A mensagem pode dizer o seguinte: "não é possível adicionar ' setup.exe ' à Web. O arquivo ' setup.exe ' já existe nesta Web. "

 Para ajudar a evitar o bloqueio de arquivos, você pode tornar o compartilhamento somente leitura para os usuários finais. No entanto, se os documentos estiverem no compartilhamento, eles também se tornarão somente leitura para os usuários finais.

## <a name="prerequisites-for-microsoft-office-arent-installed"></a>Os pré-requisitos para o Microsoft Office não estão instalados
 Você pode adicionar o .NET Framework, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] e os assemblies de interoperabilidade primária do Office ao seu pacote de instalação como pré-requisitos que são implantados com sua solução do Office. Para obter informações sobre como instalar os assemblies de interoperabilidade primária, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md) e [como instalar assemblies de interoperabilidade primária do Office](../vsto/how-to-install-office-primary-interop-assemblies.md).

## <a name="publish-using-localhost-can-cause-installation-problems"></a>Publicar usando localhost pode causar problemas de instalação
 Quando você usa `http://localhost` o como o local de publicação ou instalação para soluções em nível de documento, o **Assistente de publicação** não converte a cadeia de caracteres para o nome do computador real. Nesse caso, a solução deve ser instalada no computador de desenvolvimento. Para fazer com que as soluções implantadas usem o IIS no computador de desenvolvimento, use o nome totalmente qualificado para todos os locais HTTP/HTTPS/FTP em vez de localhost.

## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>Assemblies armazenados em cache são carregados em vez de assemblies atualizados
 Fusion, o carregador do assembly .NET Framework, carrega a cópia armazenada em cache de assemblies quando o caminho de saída do projeto está em um compartilhamento de arquivos de rede, o assembly é assinado com um nome forte e a versão do assembly da personalização não é alterada. Se você atualizar um assembly que atenda a essas condições, a atualização não aparecerá na próxima vez que você executar o projeto, pois a cópia armazenada em cache é carregada.

 Você pode configurar o Visual Studio para que o Fusion Baixe os assemblies toda vez que o projeto for executado.

### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>Para baixar assemblies em vez de carregar cópias armazenadas em cache

1. Na barra de menus, escolha **Project**, _ProjectName_**Propriedades**ProjectName.

2. Na página do **aplicativo** , escolha **informações do assembly**.

3. Defina o número de revisão, terceiro campo, da **versão do assembly**, para um curinga ( \* ). Por exemplo, "1,0. *".  Em seguida, escolha o botão **OK** .

   Depois de alterar a versão do assembly, você pode continuar a assinar seu assembly com um nome forte e a fusão carregará a versão mais recente da personalização.

 [!NOTE]
> A partir do Visual Studio 2017, se você tentar usar curingas na versão do assembly, ocorrerá um erro de compilação.  Isso ocorre porque curingas na versão do assembly interromperão o recurso determinístico do MSBuild. Você será instruído a remover os curingas da versão do assembly ou desabilitar o determinante.  Para saber mais sobre o recurso determinístico, consulte: [Propriedades comuns do projeto MSBuild](../msbuild/common-msbuild-project-properties.md) e [personalizar sua compilação](../msbuild/customize-your-build.md)

## <a name="installation-fails-when-the-uri-has-characters-that-arent-us-ascii"></a>A instalação falha quando o URI tem caracteres que não são US-ASCII
 Quando você publica uma solução do Office em um local HTTP/HTTPS/FTP, o caminho não pode ter nenhum caractere Unicode que não esteja em US-ASCII. Esses caracteres podem causar comportamento inconsistente no programa de instalação. Use caracteres US-ASCII para o caminho de instalação.

## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>A solicitação para desinstalar manualmente aparece quando você publica e instala uma solução no computador de desenvolvimento
 Quando você cria uma solução do Office, a versão compilada é automaticamente registrada. Se você já publicou e instalou a mesma solução em seu computador de desenvolvimento, [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] o detectará que o caminho de instalação para a versão publicada e a versão compilada são diferentes após a solução ser compilada, recriada ou publicada. A mensagem de erro diz "a personalização não pode ser instalada porque outra versão está atualmente instalada e não pode ser atualizada neste local." As chaves do registro são atualizadas sempre que uma solução é recriada. Portanto, você deve desinstalar a versão anterior antes de publicar, depurar ou executar a nova versão.

 Para impedir que a mensagem apareça, crie outra conta de usuário no computador de desenvolvimento para testar a implantação. Como alternativa, você pode desinstalar a versão da lista de programas instalados no computador antes de publicar, depurar ou recompilar a solução.

## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>Erro de exceção não percebida ou método não encontrado ao instalar uma solução
 Quando você instala as soluções do Office abrindo o manifesto de implantação (um arquivo *. vsto* ), um aplicativo do Office, um documento ou uma pasta de trabalho, as mensagens de erro das seguintes condições podem aparecer:

- Método não encontrado.

- MissingMethodException.

- Exceção não percebida.

  Para evitar essas mensagens de erro, instale a solução executando o programa de instalação.

  Quando você instala a solução sem executar o programa de instalação, o instalador não verifica ou instala os pré-requisitos. O programa de instalação verifica a versão correta dos pré-requisitos e instala-os conforme necessário.

## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>As chaves do registro de manifesto para suplementos são alteradas depois que um projeto do InstallShield Limited Edition é criado
 A chave do registro do manifesto que faz parte de um programa de instalação do suplemento do VSTO às vezes muda de *. vsto* para *. dll. manifest* quando você cria um projeto do InstallShield Limited Edition.

 Para contornar esse problema, crie o projeto do InstallShield Limited Edition em uma solução diferente ou use CompanyName. AddinName como o valor da chave do registro que contém o nome do suplemento do VSTO.

## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>O instalador do ClickOnce para sua solução do Office não instala os assemblies de interoperabilidade primários
 Quando você executar o programa de instalação que o ClickOnce cria para sua solução do Office, o instalador para os assemblies de interoperabilidade primária do Office (PIAs) será executado somente se nenhum PIAs já estiver instalado.

 Se o programa de instalação não instalar os PIAs corretamente, instale-os manualmente executando o arquivo do instalador chamado *o2007pia.msi* no diretório de instalação.

## <a name="reinstall-office-solutions-causes-an-argument-out-of-range-exception"></a>Reinstalar soluções do Office causa um argumento fora da exceção de intervalo
 Quando você reinstala uma solução do Office, uma <xref:System.ArgumentOutOfRangeException> exceção pode aparecer com a seguinte mensagem de erro: o argumento especificado estava fora do intervalo de valores válidos.

 Essa situação ocorre se a capitalização da URL para o local de instalação for diferente. Por exemplo, esse erro seria exibido se você tiver instalado uma solução do Office a partir da `http://fabrikam.com/ExcelSolution.vsto` primeira vez e usada `http://fabrikam.com/excelsolution.vsto` na segunda vez.

 Para impedir que a mensagem apareça, use o mesmo uso de maiúsculas ao instalar as soluções do Office.

## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>Não é possível instalar uma solução ClickOnce abrindo o manifesto de implantação da Web
 Os usuários podem instalar soluções do Office abrindo o manifesto de implantação da Web. No entanto, algumas instalações do Serviços de Informações da Internet (IIS) bloqueiam a extensão de nome de arquivo *. vsto* . Você deve definir o tipo MIME no IIS antes de usá-lo para implantar uma solução do Office.

 Para obter informações sobre como definir o tipo MIME no IIS 7, consulte [Adicionar um tipo de MIME (IIS7)](https://technet.microsoft.com/library/cc725608(WS.10).aspx).

 Defina a extensão para **. vsto** e o tipo MIME como **Application/x-MS-VSTO**.

## <a name="see-also"></a>Consulte também

- [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)

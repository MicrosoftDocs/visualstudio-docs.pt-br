---
title: Solucionar problemas de implantação de solução do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bba978da26a2aa7b7263fa5d2e88fa8acdc272f0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885997"
---
# <a name="troubleshoot-office-solution-deployment"></a>Solucionar problemas de implantação de solução do Office
  Este tópico contém informações sobre como resolver problemas comuns que você pode encontrar ao implantar soluções do Office.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="troubleshoot-office-solutions-by-using-the-event-viewer"></a>Solucionar problemas de soluções do Office usando o Visualizador de eventos  
 Você pode usar o Visualizador de eventos no Windows para ver mensagens de erro que são capturadas pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ao instalar ou desinstalar soluções do Office. Você pode usar essas mensagens do agente de log de eventos para solucionar problemas de implantação e instalação. Para obter mais informações, consulte [log de eventos para soluções do Office](../vsto/event-logging-for-office-solutions.md).  
  
## <a name="change-the-assembly-name-causes-conflicts"></a>Altere o nome de assembly faz com que os conflitos  
 Se você alterar o **nome do Assembly** valor na **aplicativo** página da **Project Designer** depois que você já implantou uma solução, as ferramentas de publicação irá modificar o Pacote de instalação para ter um *Setup.exe* arquivo e dois manifestos de implantação. Se você implantar dois arquivos de manifesto, as condições a seguir podem ocorrer:  
  
- Se o usuário final instalar ambas as versões, o aplicativo carregará os dois suplementos do VSTO.  
  
- Se o suplemento do VSTO que foi instalado antes que o nome do assembly foi alterado, o usuário final nunca receberá atualizações.  
  
  Para evitar essas condições, não altere a solução **nome do Assembly** valor depois de implantar a solução.  
  
## <a name="check-for-updates-takes-a-long-time"></a>Verifique se há atualizações leva muito tempo  
 Visual Studio 2010 Tools for Office runtime fornece uma entrada de registro que os administradores podem usar para definir o valor de tempo limite para baixar os manifestos e a solução.  
  
#### <a name="to-set-the-time-out-value"></a>Para definir o valor de tempo limite  
  
1.  No registro, navegue até a seguinte chave:  
  
     **HKEY_CURRENT_USER\Software\Microsoft\VSTA**  
  
2.  No **AddInTimeout** subchave, defina o valor de tempo limite em milissegundos.  
  
     Se o **AddInTimeout** subchave não existir, crie-o como um DWORD.  
  
## <a name="cant-update-or-publish-to-a-network-file-share"></a>Não é possível atualizar ou publicar em um compartilhamento de arquivos de rede  
 Soluções do Office que estão em um compartilhamento de arquivos de rede podem exibir uma mensagem enganosa durante as atualizações, se a solução *Setup.exe* arquivo está bloqueado em um processo, enquanto a atualização está sendo publicada. A mensagem pode dizer o seguinte: "não é possível adicionar 'setup.exe' para a Web. O arquivo 'setup.exe' já existe nesta Web".  
  
 Para ajudar a evitar o bloqueio de arquivos, você pode tornar o compartilhamento somente leitura para os usuários finais. No entanto, se documentos forem no compartilhamento, eles também se tornará somente leitura para os usuários finais.  
  
## <a name="prerequisites-for-microsoft-office-arent-installed"></a>Pré-requisitos para o Microsoft Office não estão instalados  
 Você pode adicionar o .NET Framework, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]e os Office assemblies de interoperabilidade primários para seu pacote de instalação como pré-requisitos que são implantados com sua solução do Office. Para obter informações sobre como instalar assemblies de interoperabilidade primários, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md) e [como: assemblies de interoperabilidade primários do Office Instale](../vsto/how-to-install-office-primary-interop-assemblies.md).  
  
## <a name="publish-using-localhost-can-cause-installation-problems"></a>Publicar usando 'Localhost' pode causar problemas de instalação  
 Quando você usa "<http://localhost>" como o local de instalação ou de publicação para soluções de nível de documento, o **Assistente de publicação** não converte a cadeia de caracteres ao nome do computador real. Nesse caso, a solução deve ser instalada no computador de desenvolvimento. Para usar IIS no computador de desenvolvimento, use o nome totalmente qualificado para todos os locais HTTP/HTTPS/FTP em vez do localhost soluções implantadas.  
  
## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>Armazenados em cache de assemblies é carregado em vez de assemblies atualizados  
 Fusion, o carregador de assembly do .NET Framework, carrega a cópia armazenada em cache de assemblies quando o caminho de saída do projeto é um compartilhamento de rede, o assembly é assinado com um nome forte e a versão do assembly da personalização não muda. Se você atualizar um assembly que atende a essas condições, a atualização não aparecerá na próxima vez que você executar o projeto porque a cópia armazenada em cache é carregada.  
  
 Você pode configurar o Visual Studio para que a fusão baixar assemblies toda vez que o projeto é executado.  
  
### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>Para baixar os assemblies em vez de carregar cópias armazenadas em cache  
  
1. Na barra de menus, escolha **Project**, _ProjectName_**propriedades**.  
  
2. Sobre o **Application** , escolha **informações de Assembly**.  
  
3. No primeiro **versão do Assembly** , digite um asterisco (\*) e, em seguida, escolha o **Okey** botão.  
  
   Depois de alterar a versão do assembly, você pode continuar a assinar o assembly com um nome forte e Fusion carregará a versão mais recente da personalização.  
  
## <a name="installation-fails-when-the-uri-has-characters-that-arent-us-ascii"></a>A instalação falha quando o URI tem caracteres que não são de US-ASCII  
 Quando você publica uma solução do Office em um local HTTP/HTTPS/FTP, o caminho não pode ter quaisquer caracteres Unicode que não estão em US-ASCII. Esses caracteres podem causar um comportamento inconsistente no programa de instalação. Use caracteres US-ASCII para o caminho de instalação.  
  
## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>Prompt para desinstalar manualmente aparece quando você publica e instala uma solução no computador de desenvolvimento  
 Quando você compila uma solução do Office, a versão compilada é registrado automaticamente. Se você tiver publicado anteriormente e instalado a mesma solução em seu computador de desenvolvimento, [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] detecta que o caminho de instalação para a versão publicada e a versão compilada são diferentes depois que a solução é criada em seguida, recriado, ou publicado. A mensagem de erro informar que "a personalização não pode ser instalada porque outra versão instalada no momento e não pode ser atualizada a partir deste local." As chaves do registro são atualizadas sempre que uma solução é reconstruída. Portanto, você deve desinstalar a versão anterior antes de publicar, depurar ou executar a nova versão.  
  
 Para impedir que a mensagem que aparece, crie outra conta de usuário no computador de desenvolvimento para testar sua implantação. Como alternativa, você pode desinstalar a versão da lista de programas instalados no computador antes de você em seguida publica, depura ou recompile a solução.  
  
## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>Exceção não percebida ou método não encontrado erro quando você instala uma solução  
 Quando você instala soluções do Office abrindo o manifesto de implantação (um *VSTO* arquivo), mensagens de erro de aplicativo, documento ou pasta de trabalho do Office em para as seguintes condições podem aparecer:  
  
- Método não encontrado.  
  
- MissingMethodException.  
  
- Exceção não capturada.  
  
  Para evitar essas mensagens de erro, instale a solução executando o programa de instalação.  
  
  Quando você instala a solução sem executar o programa de instalação, o instalador não verificar ou instalar os pré-requisitos. O programa de instalação verifica a versão correta dos pré-requisitos e instala-os conforme necessário.  
  
## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>Depois que um projeto InstallShield Limited Edition é construído de manifesto chaves do registro de alteração de suplementos  
 A chave do registro de manifesto que faz parte de uma instalação de suplemento do VSTO do programa, às vezes, as alterações do *VSTO* à *. manifest* quando você compila um projeto do InstallShield Limited Edition.  
  
 Para contornar esse problema, crie o projeto do InstallShield Limited Edition em uma solução diferente ou usar CompanyName.AddinName como o valor da chave do registro que contém o nome do suplemento do VSTO.  
  
## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>O instalador do ClickOnce para sua solução do Office não instala os assemblies de interoperabilidade primários  
 Quando você executa o programa de instalação ClickOnce cria para sua solução do Office, o instalador do Office assemblies de interoperabilidade primários (PIAs) é executado somente se nenhuma PIAs já estão instalados.  
  
 Se o programa de instalação não instala corretamente os PIAs, instalá-los manualmente executando o arquivo do instalador chamado *o2007pia.msi* do diretório de instalação.  
  
## <a name="reinstall-office-solutions-causes-an-argument-out-of-range-exception"></a>Reinstalar um argumento de exceção fora do intervalo de causas de soluções do Office  
 Quando uma solução do Office, você reinstalar um <xref:System.ArgumentOutOfRangeException> exceção pode aparecer com a seguinte mensagem de erro: argumento especificado estava fora do intervalo de valores válidos.  
  
 Essa situação ocorrerá se as maiusculas e minúsculas para a URL para o local de instalação é diferente. Por exemplo, esse erro apareceria se você tiver instalado a partir de uma solução do Office [ http://fabrikam.com/ExcelSolution.vsto ](http://fabrikam.com/ExcelSolution.vsto) na primeira vez e, em seguida, usado [ http://fabrikam.com/excelsolution.vsto ](http://fabrikam.com/excelsolution.vsto) na segunda vez.  
  
 Para impedir que a mensagem que aparece, use as mesmas maiusculas e minúsculas quando você instala as soluções do Office.  
  
## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>Não é possível instalar uma solução do ClickOnce, abrindo o manifesto de implantação da web  
 Os usuários podem instalar soluções do Office abrindo o manifesto de implantação da web. No entanto, bloqueiam algumas instalações do Internet Information Services (IIS) a *VSTO* extensão de nome de arquivo. Você deve definir o tipo MIME no IIS antes de usá-lo para implantar uma solução do Office.  
  
 Para obter informações sobre como definir o tipo MIME no IIS 7, consulte [adicionar um tipo de MIME (IIS7)](http://technet.microsoft.com/library/cc725608(WS.10).aspx).  
  
 A extensão do conjunto **VSTO** e o tipo MIME para **application/x-ms-vsto**.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de implantações do ClickOnce](/visualstudio/deployment/troubleshooting-clickonce-deployments)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  
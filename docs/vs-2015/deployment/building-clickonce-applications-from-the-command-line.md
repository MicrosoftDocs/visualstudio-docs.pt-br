---
title: Compilando aplicativos ClickOnce a partir da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, from command line
- publishing
- publishing, ClickOnce
ms.assetid: d9bc6212-c584-4f72-88c9-9a4b998c555e
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: c9a9b2e248e4f10e9b5d3f045c67a9622edd2c2b
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220011"
---
# <a name="building-clickonce-applications-from-the-command-line"></a>Compilando aplicativos ClickOnce a partir da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], você pode compilar projetos da linha de comando, mesmo se eles são criados no ambiente de desenvolvimento integrado (IDE). Na verdade, você pode recompilar um projeto criado com [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] em outro computador que tem apenas o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] instalado. Isso permite que você reproduza uma compilação usando um processo automatizado, por exemplo, em uma compilação de central de laboratório ou usando scripts avançados técnicas além do escopo da criação do projeto em si.  
  
## <a name="using-msbuild-to-reproduce-clickonce-application-deployments"></a>Usando o MSBuild para reproduzir as implantações de aplicativos ClickOnce  
 Quando você invoca o msbuild /target:publish na linha de comando, ele informa o sistema de MSBuild para compilar o projeto e criar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo na pasta publish. Isso é equivalente a selecionar o **publicar** comando no IDE.  
  
 Esse comando executa msbuild.exe, que está no caminho de ambiente de prompt de comando do Visual Studio.  
  
 "target" é um indicador para o MSBuild sobre como processar o comando. Os destinos de chave são o destino de "build" e o destino de "Publicar". O destino de build é o equivalente a selecionar a compilação comando (ou pressionando F5) no IDE. Se você quiser criar seu projeto, pode fazer isso digitando `msbuild`. Esse comando funciona porque o destino de compilação é o destino padrão para todos os projetos gerados pelo [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Isso significa que você explicitamente não precisa especificar o destino de build. Portanto, digitando `msbuild` é a mesma operação que digitar `msbuild /target:build`.  
  
 O `/target:publish` comando informa ao MSBuild para invocar o destino de publicação. O destino de publicação depende do destino de build. Isso significa que a operação de publicação é um superconjunto da operação de compilação. Por exemplo, se você fez uma alteração em um dos seus arquivos de origem do Visual Basic ou c#, o assembly correspondente automaticamente ser recriado por operação de publicação.  
  
 Para obter informações sobre como gerar uma completa [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação usando a ferramenta de linha de comando Mage.exe para criar sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto, consulte [passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  
  
## <a name="creating-and-building-a-basic-clickonce-application-using-msbuild"></a>Criando e compilando um aplicativo ClickOnce básico usando o MSBuild  
  
#### <a name="to-create-and-publish-a-clickonce-project"></a>Para criar e publicar um projeto do ClickOnce  
  
1. Clique em **novo projeto** da **arquivo** menu. A caixa de diálogo **Novo Projeto** é exibida.  
  
2. Selecione **aplicativo do Windows** e nomeie-o `CmdLineDemo`.  
  
3. Dos **construir** menu, clique no **publicar** comando.  
  
    Essa etapa garante que o projeto está configurado corretamente para produzir um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação de aplicativos.  
  
    O Assistente de Publicação será exibido.  
  
4. No Assistente de publicação, clique em **concluir**.  
  
    Visual Studio gera e exibe a página da Web padrão, chamada Publish. htm.  
  
5. Salve seu projeto e anote o local da pasta na qual ele está armazenado.  
  
   As etapas acima criam um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] projeto que foi publicado pela primeira vez. Agora você pode reproduzir o build fora do IDE.  
  
#### <a name="to-reproduce-the-build-from-the-command-line"></a>Para reproduzir a compilação da linha de comando  
  
1. Saia do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
2. Do Windows **inicie** menu, clique em **todos os programas**, em seguida, **Microsoft Visual Studio**, em seguida, **ferramentas do Visual Studio**, então **Prompt de comando do visual Studio**. Isso deve abrir um prompt de comando na pasta raiz do usuário atual.  
  
3. No **Prompt de comando do Visual Studio**, altere o diretório atual para o local do projeto que você acabou de criar acima. Por exemplo, digite `chdir My Documents\Visual Studio\Projects\CmdLineDemo`.  
  
4. Para remover os arquivos existentes produzidos em "criar e publicar uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] projeto," tipo `rmdir /s publish`.  
  
    Esta etapa é opcional, mas garante que os novos arquivos foram todos produzidos pela compilação de linha de comando.  
  
5. Digite `msbuild /target:publish` no terminal integrado.  
  
   As etapas acima produzirá uma completa [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação de aplicativos em uma subpasta do projeto chamada **publicar**. CmdLineDemo.application é o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto de implantação. A pasta CmdLineDemo_1.0.0.0 contém os arquivos CmdLineDemo.exe e CmdLineDemo.exe.manifest, o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo. Setup.exe é o bootstrapper, que, por padrão, está configurado para instalar o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. A pasta DotNetFX contém os redistribuíveis para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Isso é todo o conjunto de arquivos que você precisa para implantar seu aplicativo na Web ou por meio de UNC ou CD/DVD.  
  
## <a name="publishing-properties"></a>Propriedades de publicação  
 Quando você publica o aplicativo em procedimentos anteriores, as propriedades a seguir são inseridas no seu arquivo de projeto, o Assistente de publicação. Essas propriedades influenciam diretamente como o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo é produzido.  
  
 No CmdLineDemo.vbproj / CmdLineDemo.csproj:  
  
```  
<AssemblyOriginatorKeyFile>WindowsApplication3.snk</AssemblyOriginatorKeyFile>  
<GenerateManifests>true</GenerateManifests>  
<TargetZone>LocalIntranet</TargetZone>  
<PublisherName>Microsoft</PublisherName>  
<ProductName>CmdLineDemo</ProductName>  
<PublishUrl>http://localhost/CmdLineDemo</PublishUrl>  
<Install>true</Install>  
<ApplicationVersion>1.0.0.*</ApplicationVersion>  
<ApplicationRevision>1</ApplicationRevision>  
<UpdateEnabled>true</UpdateEnabled>  
<UpdateRequired>false</UpdateRequired>  
<UpdateMode>Foreground</UpdateMode>  
<UpdateInterval>7</UpdateInterval>  
<UpdateIntervalUnits>Days</UpdateIntervalUnits>  
<UpdateUrlEnabled>false</UpdateUrlEnabled>  
<IsWebBootstrapper>true</IsWebBootstrapper>  
<BootstrapperEnabled>true</BootstrapperEnabled>  
```  
  
 Você pode substituir qualquer uma dessas propriedades na linha de comando sem alterar o arquivo de projeto. Por exemplo, o seguinte criará o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação de aplicativo sem o bootstrapper:  
  
```  
msbuild /target:publish /property:BootstrapperEnabled=false  
```  
  
 Propriedades de publicação são controladas em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] do **Publish**, **segurança**, e **Signing** páginas de propriedades do **Designer de projeto** . Abaixo está uma descrição das propriedades de publicação, junto com uma indicação de como cada um é definida em várias páginas de propriedade do designer do aplicativo:  
  
- `AssemblyOriginatorKeyFile` Determina o arquivo de chave usado para assinar seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos de aplicativo. Essa mesma chave também pode ser usado para atribuir um nome forte a seus assemblies. Essa propriedade é definida a **Signing** página do **Designer de projeto**.  
  
  As seguintes propriedades são definidas na **segurança** página:  
  
- **Habilitar configurações de segurança do ClickOnce** determina se [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos são gerados. Quando um projeto é criado inicialmente, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] geração de manifesto está desativado por padrão. O assistente automaticamente desativa esse sinalizador nos quando você publica pela primeira vez.  
  
- **TargetZone** determina o nível de confiança para ser emitida no seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo. Os valores possíveis são "Internet", "LocalIntranet" e "Custom". Internet e LocalIntranet fará com que um conjunto de permissões padrão para ser emitida no seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo. LocalIntranet é o padrão e, basicamente, significa confiança total. Personalizada Especifica que somente as permissões explicitamente especificadas no arquivo manifest base devem ser emitida no [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo. O arquivo App. manifest é um arquivo de manifesto parcial que contém apenas as definições de informações de confiança. É um arquivo oculto, adicionado automaticamente ao seu projeto quando você configurar permissões na **segurança** página.  
  
  As seguintes propriedades são definidas na **publicar** página:  
  
- `PublishUrl` é o local em que o aplicativo será publicado no IDE. Ele é inserido na [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo se nem a `InstallUrl` ou `UpdateUrl` propriedade for especificada.  
  
- `ApplicationVersion` Especifica a versão do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Este é um número de versão de quatro dígitos. Se o último dígito é um "*", em seguida, a `ApplicationRevision` substituirá o valor inserido no manifesto no momento da compilação.  
  
- `ApplicationRevision` Especifica a revisão. Esse é um inteiro que é incrementado toda vez que você publica no IDE. Observe que não é incrementado automaticamente para compilações executadas na linha de comando.  
  
- `Install` Determina se o aplicativo é um aplicativo instalado ou um aplicativo de execução da Web.  
  
- `InstallUrl` (não mostrado) é o local em que os usuários instalarão o aplicativo. Se for especificado, esse valor é gravado no bootstrapper setup.exe se o `IsWebBootstrapper` propriedade está habilitada. Ele também é inserido no manifesto-se aplicativo a `UpdateUrl` não for especificado.  
  
- `SupportUrl` (não mostrado) é o local vinculado a **adicionar ou remover programas** caixa de diálogo para um aplicativo instalado.  
  
  As seguintes propriedades são definidas **atualizações do aplicativo** caixa de diálogo, acessada a partir de **publicar** página.  
  
- `UpdateEnabled` Indica se o aplicativo deve verificar se há atualizações.  
  
- `UpdateMode` Especifica as atualizações de primeiro plano ou atualizações em segundo plano.  
  
- `UpdateInterval` Especifica a frequência com que o aplicativo deve verificar se há atualizações.  
  
- `UpdateIntervalUnits` Especifica se o `UpdateInterval` valor está em unidades de horas, dias ou semanas.  
  
- `UpdateUrl` (não mostrado) é o local em que o aplicativo receberá atualizações. Se for especificado, esse valor é inserido no manifesto do aplicativo.  
  
- As seguintes propriedades são definidas **opções de publicação** caixa de diálogo, acessada a partir de **publicar** página.  
  
- `PublisherName` Especifica o nome do publicador exibido no prompt mostrado durante a instalação ou execução do aplicativo. No caso de um aplicativo instalado, ele também é usado para especificar o nome da pasta na **iniciar** menu.  
  
- `ProductName` Especifica o nome do produto exibido no prompt mostrado durante a instalação ou execução do aplicativo. No caso de um aplicativo instalado, ele também é usado para especificar o nome do atalho na **iniciar** menu.  
  
- As seguintes propriedades são definidas **pré-requisitos** caixa de diálogo, acessada a partir de **publicar** página.  
  
- `BootstrapperEnabled` Determina se deve gerar o bootstrapper setup.exe.  
  
- `IsWebBootstrapper` Determina se o bootstrapper setup.exe funciona pela Web ou no modo baseado em disco.  
  
## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL, SupportUrl, PublishURL e UpdateURL  
 A tabela a seguir mostra as quatro opções de URL para a implantação do ClickOnce.  
  
|Opção de URL|Descrição|  
|----------------|-----------------|  
|`PublishURL`|Necessário se você estiver publicando seu aplicativo ClickOnce para um site da Web.|  
|`InstallURL`|Opcional. Defina essa opção de URL se o site de instalação é diferente de `PublishURL`. Por exemplo, você pode definir as `PublishURL` para um caminho FTP e definir o `InstallURL` para uma URL da Web.|  
|`SupportURL`|Opcional. Defina essa opção de URL se o site de suporte é diferente de `PublishURL`. Por exemplo, você pode definir o `SupportURL` para o site de suporte ao cliente da sua empresa.|  
|`UpdateURL`|Opcional. Defina essa opção de URL se o local de atualização é diferente de `InstallURL`. Por exemplo, você pode definir as `PublishURL` para um caminho FTP e definir o `UpdateURL` para uma URL da Web.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.Build.Tasks.GenerateBootstrapper>   
 <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>   
 <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>   
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Passo a passo: implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)




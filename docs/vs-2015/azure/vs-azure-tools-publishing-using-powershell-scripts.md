---
title: Usando Scripts do Windows PowerShell para publicar em ambientes de desenvolvimento e teste | Microsoft Docs
description: Saiba como usar scripts do PowerShell do Windows do Visual Studio para publicar para desenvolvimento e ambientes de teste.
author: ghogen
manager: douge
assetId: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: 9d0142c52fbe40256fc0ab6ec0d5d9fdade243b7
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001217"
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a>Usando scripts do Windows PowerShell para publicar em ambientes de desenvolvimento e teste

Quando você cria um aplicativo web no Visual Studio, você pode gerar um script do Windows PowerShell que você pode usar posteriormente para automatizar a publicação do seu site no Azure como um aplicativo Web no serviço de aplicativo do Azure ou uma máquina virtual. Você pode editar e estender o script do Windows PowerShell no editor do Visual Studio para atender às suas necessidades ou integrar o script de compilação existente, teste e scripts de publicação.

Usando esses scripts, você pode provisionar versões personalizadas (também conhecido como ambientes de desenvolvimento e teste) do seu site para uso temporário. Por exemplo, você pode configurar uma versão específica do seu site em uma máquina virtual do Azure ou no slot de preparo em um site para executar um conjunto de testes, reproduzir um bug, testar uma correção de bug, avaliar uma alteração proposta ou configurar um ambiente personalizado para uma demonstração ou apresentação. Depois de criar um script que publica seu projeto, você pode recriar ambientes idênticos ao executar novamente o script conforme necessário ou executar o script com sua própria compilação do seu aplicativo web para criar um ambiente personalizado de teste.

## <a name="prerequisites"></a>Pré-requisitos

* Azure SDK 2.3 ou posterior. Ver [Downloads do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384). (Você não precisa do SDK do Azure para gerar scripts para projetos web. Esse recurso é para projetos web, não as funções web nos serviços de nuvem.)
* O Azure PowerShell 0.7.4 ou posterior. Ver [como instalar e configurar o Azure PowerShell](/powershell/azure/overview).
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou posterior.

## <a name="additional-tools"></a>Ferramentas adicionais

Ferramentas e recursos para trabalhar com o PowerShell no Visual Studio para desenvolvimento do Azure adicionais estão disponíveis. Ver [ferramentas do PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-the-publish-scripts"></a>Gerando scripts de publicação

Você pode gerar scripts de publicação para uma máquina virtual que hospeda seu site quando você cria um novo projeto seguindo [estas instruções](/azure/virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Você também pode [gerar scripts para aplicativos web de publicação no serviço de aplicativo do Azure](/azure/app-service/scripts/app-service-powershell-deploy-github).

## <a name="scripts-that-visual-studio-generates"></a>Scripts gerados pelo Visual Studio

O Visual Studio gera uma pasta de nível de solução chamada **PublishScripts** que contém dois arquivos do Windows PowerShell, um script de publicação para sua máquina virtual ou site e um módulo que contém funções que você pode usar o scripts. Visual Studio também gera um arquivo no formato JSON que especifica os detalhes do projeto que você está implantando.

### <a name="windows-powershell-publish-script"></a>Script de publicação do Windows PowerShell

O script de publicação contém etapas específicas de publicação para a implantação em um site ou máquina virtual. O Visual Studio fornece sintaxe colorida para o desenvolvimento do Windows PowerShell. A Ajuda para as funções estão disponíveis, e você pode editar livremente as funções no script para atender às suas necessidades em constante mudanças.

### <a name="windows-powershell-module"></a>Módulo do Windows PowerShell

O módulo do Windows PowerShell que o Visual Studio gera contém funções que usa o script de publicação. Essas funções do PowerShell do Azure não se destinam a ser modificado. Ver [como instalar e configurar o Azure PowerShell](/powershell/azure/overview).

### <a name="json-configuration-file"></a>Arquivo de configuração JSON

O arquivo JSON é criado na **configurações** pasta e contém dados de configuração que especificam exatamente quais recursos implantar no Azure. O nome do arquivo que o Visual Studio gera é project-nome-WAWS-dev se você tiver criado um site ou o nome do projeto-VM-dev, se você tiver criado uma máquina virtual. Aqui está um exemplo de um arquivo de configuração JSON que é gerado quando você cria um site. A maioria dos valores são auto-explicativos. O nome do site é gerado pelo Azure, portanto, ele pode não corresponder ao nome do seu projeto.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```

Quando você cria uma máquina virtual, o arquivo de configuração JSON é semelhante ao seguinte. Um serviço de nuvem é criado como um contêiner para a máquina virtual. A máquina virtual contém os pontos de extremidade comuns para acesso à web via HTTP e HTTPS, bem como pontos de extremidade para a implantação da Web, que permite que você publicar o site do seu computador local, a área de trabalho remota e o Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Você pode editar a configuração de JSON para alterar o que acontece quando você executar os scripts de publicação. O `cloudService` e `virtualMachine` seções são necessárias, mas você pode excluir o `databases` seção se você não precisa dela. As propriedades que estão vazias no arquivo de configuração padrão que o Visual Studio gera são opcionais. as propriedades que têm valores no arquivo de configuração padrão são necessárias.

Se você tiver um site que tem vários ambientes de implantação (conhecidos como slots) em vez de um único site de produção no Azure, você pode incluir o nome do slot no nome do site no arquivo de configuração JSON. Por exemplo, se você tiver um site que é denominado **mysite** e um slot para ele chamado **testar** e em seguida, o URI é `mysite-test.cloudapp.net`, mas o nome correto a ser usado no arquivo de configuração é MySite (Test). Você só pode fazer isso se o site e slots já existirem em sua assinatura. Se não existirem, crie o site executando o script sem especificar o slot e, em seguida, crie o slot na [portal do Azure](https://portal.azure.com/), e execute o script com o nome do site modificado. Para obter mais informações sobre os slots de implantação para aplicativos web, consulte [configurar ambientes de preparo para aplicativos web no serviço de aplicativo do Azure](/azure/app-service/web-sites-staged-publishing).

## <a name="how-to-run-the-publish-scripts"></a>Como executar scripts de publicação

Se você nunca executou um script do Windows PowerShell antes, você deve primeiro definir a política de execução para habilitar a execução de scripts. A política é um recurso de segurança para impedir que os usuários executem scripts do Windows PowerShell se estiverem vulneráveis a malware ou vírus que envolvem a execução de scripts.

### <a name="run-the-script"></a>Execute o script

1. Crie o pacote de implantação da Web para seu projeto. Um pacote de implantação da Web é um arquivo compactado (arquivo. zip) que contêm arquivos que você deseja copiar para seu site ou máquina virtual. Você pode criar pacotes de implantação da Web no Visual Studio para qualquer aplicativo da web.

   ![Criar Web implantar pacote](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

   Para obter mais informações, consulte [como: criar um pacote de implantação da Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Você também pode automatizar a criação de seu pacote de implantação da Web, conforme descrito em [personalizando e estendendo scripts de publicação](#customizing-and-extending-publish-scripts).

1. Na **Gerenciador de soluções**, abra o menu de contexto para o script e, em seguida, escolha **abrir com o PowerShell ISE**.
1. Se a execução de scripts do Windows PowerShell neste computador pela primeira vez, abra uma janela de prompt de comando com privilégios de administrador e digite o seguinte comando:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

1. Entrar no Azure usando o comando a seguir.

    ```powershell
    Add-AzureAccount
    ```

    Quando solicitado, forneça seu nome de usuário e senha.

    Observe que, quando você automatiza o script, esse método para fornecer as credenciais do Azure não funciona. Em vez disso, você deve usar o `.publishsettings` arquivo para fornecer credenciais. Uma vez apenas, você use o comando **Get-AzurePublishSettingsFile** para baixar o arquivo do Azure e depois usa **Import-AzurePublishSettingsFile** para importar o arquivo. Para obter instruções detalhadas, consulte [como instalar e configurar o Azure PowerShell](/powershell/azure/overview).

1. (Opcional) Se você quiser criar recursos do Azure como a máquina virtual, banco de dados e site sem publicar seu aplicativo web, usam o **Publish-WebApplication.ps1** com o **-Configuration**argumento é definido para o arquivo de configuração JSON. Essa linha de comando usa o arquivo de configuração JSON para determinar quais recursos criar. Porque ele usa as configurações padrão para outros argumentos de linha de comando, ele cria os recursos, mas não publica seu aplicativo web. – Verbose opção fornece mais informações sobre o que está acontecendo.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

1. Use o **Publish-WebApplication.ps1** comando conforme mostrado em um dos exemplos a seguir para invocar o script e publicar seu aplicativo web. Se você precisar substituir as configurações padrão para qualquer um dos outros argumentos, como o nome da assinatura, nome do pacote, as credenciais de máquina virtual ou credenciais do servidor de banco de dados de publicação, você pode especificar esses parâmetros. Use o **– Verbose** opção para obter mais informações sobre o andamento do processo de publicação.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Se você estiver criando uma máquina virtual, o comando é semelhante ao seguinte. Este exemplo também mostra como especificar as credenciais para vários bancos de dados. Para as máquinas virtuais que esses scripts criam, o certificado SSL não é de uma autoridade raiz confiável. Portanto, você precisa usar o **– AllowUntrusted** opção.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    O script pode criar bancos de dados, mas ele não cria servidores de banco de dados. Se você quiser criar um servidor de banco de dados, você pode usar o **New-AzureSqlDatabaseServer** função no módulo do Azure.

## <a name="customizing-and-extending-the-publish-scripts"></a>Personalizando e estendendo scripts de publicação

Você pode personalizar o script de publicação e o arquivo de configuração JSON. As funções no módulo do Windows PowerShell **AzureWebAppPublishModule.psm1** não se destina a ser modificado. Se você quiser especificar um banco de dados diferente ou alterar algumas das propriedades da máquina virtual, edite o arquivo de configuração JSON. Se você quiser estender a funcionalidade de script para automatizar a criação e teste seu projeto, você pode implementar stubs de função em **Publish-WebApplication.ps1**.

Para automatizar a criação de seu projeto, adicione o código que chama o MSBuild para `New-WebDeployPackage` conforme mostrado neste exemplo de código. O caminho para o comando MSBuild é diferente dependendo da versão do Visual Studio que você instalou. Para obter o caminho correto, você pode usar a função **Get-MSBuildCmd**, conforme mostrado neste exemplo.

### <a name="to-automate-building-your-project"></a>Para automatizar a criação de seu projeto

1. Adicionar o `$ProjectFile` parâmetro na seção de parâmetros globais.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

1. Copie a função `Get-MSBuildCmd` em seu arquivo de script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

1. Substitua `New-WebDeployPackage` com o seguinte código e substitua os espaços reservados na construção de linha `$msbuildCmd`. Esse código é para o Visual Studio 2015. Se você estiver usando o Visual Studio 2017, altere o **VisualStudioVersion** propriedade `15.0` (`12.0` para Visual Studio 2013).

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    Para criar seu aplicativo web, use MsBuild.exe. Para obter ajuda, consulte a referência de linha de comando do MSBuild em: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a>Iniciar a execução do comando de compilação

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Chame o `New-WebDeployPackage` função antes dessa linha: `$Config = Read-ConfigFile $Configuration` para aplicativos web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuais.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

1. Invoque o script personalizado da linha de comando usando a passagem de `$Project` argumento, como no exemplo a seguir:

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    Para automatizar o teste do seu aplicativo, adicione código ao `Test-WebApplication`. Certifique-se de não comentar as linhas no **Publish-WebApplication.ps1** onde essas funções são chamadas. Se você não fornecer uma implementação, você pode compilar manualmente seu projeto com o Visual Studio e, em seguida, execute o script de publicação para publicar no Azure.

## <a name="publishing-function-summary"></a>Resumo da função de publicação
Para obter ajuda para funções que você pode usar o prompt de comando do Windows PowerShell, use o comando `Get-Help function-name`. A Ajuda inclui exemplos e ajuda de parâmetro. O mesmo texto de Ajuda está também nos arquivos de origem de script **AzureWebAppPublishModule.psm1** e **Publish-WebApplication.ps1**. O script e obter ajuda está localizada em sua linguagem do Visual Studio.

**AzureWebAppPublishModule**

| Nome da função | Descrição |
| --- | --- |
| Add-AzureSQLDatabase |Cria um novo banco de dados SQL do Azure. |
| Add-AzureSQLDatabases |Cria os bancos de dados SQL do Azure dos valores no arquivo de configuração JSON que o Visual Studio gera. |
| Add-AzureVM |Cria uma máquina virtual do Azure e retorna a URL da VM implantada. A função configura os pré-requisitos e, em seguida, chama o **New-AzureVM** função (módulo do Azure) para criar uma nova máquina virtual. |
| Add-AzureVMEndpoints |Adiciona novos pontos de extremidade de entrada a uma máquina virtual e retorna a máquina virtual com o novo ponto de extremidade. |
| Add-AzureVMStorage |Cria uma nova conta de armazenamento do Azure na assinatura atual. O nome da conta começa com "devtest", seguido por uma cadeia de caracteres alfanumérica exclusiva. A função retorna o nome da nova conta de armazenamento. Especifique um local ou um grupo de afinidade para a nova conta de armazenamento. |
| Add-AzureWebsite |Cria um site com o nome e local especificados. Essa função chama o **New-AzureWebsite** função no módulo do Azure. Se a assinatura ainda não incluir um site com o nome especificado, essa função cria o site e retorna um objeto de site. Caso contrário, retornará `$null`. |
| Assinatura de backup |Salva a assinatura atual do Azure na `$Script:originalSubscription` variável no escopo do script. Essa função salva a assinatura do Azure atual (conforme obtidas pelo `Get-AzureSubscription -Current`) e sua conta de armazenamento e a assinatura é alterada por esse script (armazenado na variável `$UserSpecifiedSubscription`) e sua conta de armazenamento, no escopo do script. Ao salvar os valores, você pode usar uma função, como `Restore-Subscription`, para restaurar a conta de armazenamento e a assinatura atual original para o status atual, se o status atual foi alterado. |
| Find-AzureVM |Obtém a máquina virtual do Azure especificada. |
| Format-DevTestMessageWithTime |Precede a data e hora a uma mensagem. Essa função foi projetada para as mensagens gravadas para os fluxos de erro e detalhado. |
| Get-AzureSQLDatabaseConnectionString |Monta uma cadeia de caracteres de conexão para se conectar a um banco de dados SQL do Azure. |
| Get-AzureVMStorage |Retorna o nome da primeira conta de armazenamento com o nome padrão "devtest *" (diferencia maiusculas de minúsculas) no local especificado ou grupo de afinidade. Se o "devtest*" conta de armazenamento não corresponde ao local ou grupo de afinidade, a função o ignora. Especifique um local ou um grupo de afinidade. |
| Get-MSDeployCmd |Retorna um comando para executar a ferramenta MsDeploy.exe. |
| New-AzureVMEnvironment |Localiza ou cria uma máquina virtual na assinatura que corresponde aos valores no arquivo de configuração JSON. |
| Publish-WebPackage |Usa MsDeploy.exe e uma web publicar o pacote. Arquivo zip para implantar recursos em um site. Essa função não gera nenhuma saída. Se a chamada para MSDeploy.exe falhar, a função gera uma exceção. Para obter uma saída mais detalhada, use o **-Verbose** opção. |
| Publish-WebPackageToVM |Verifica os valores de parâmetro e, em seguida, chama o **Publish-WebPackage** função. |
| Read-ConfigFile |Valida o arquivo de configuração JSON e retorna uma tabela de hash de valores selecionados. |
| Restore-Subscription |Redefine a assinatura atual para a assinatura original. |
| Teste-AzureModule |Retorna `$true` se a versão do módulo do Azure instalado for 0.7.4 ou posterior. Retorna `$false` se o módulo não está instalado ou é uma versão anterior. Essa função não tem parâmetros. |
| Teste AzureModuleVersion |Retorna `$true` se a versão do módulo do Azure for 0.7.4 ou posterior. Retorna `$false` se o módulo não está instalado ou é uma versão anterior. Essa função não tem parâmetros. |
| Teste HttpsUrl |Converte a URL de entrada em um objeto System. URI. Retorna `$True` se a URL for absoluta e seu esquema for https. Retorna `$false` se a URL for relativa, seu esquema não for HTTPS ou a cadeia de caracteres de entrada não pode ser convertida para uma URL. |
| Membro de teste |Retorna `$true` se uma propriedade ou método é um membro do objeto. Caso contrário, retornará `$false`. |
| Gravação ErrorWithTime |Grava uma mensagem de erro prefixada com a hora atual. Essa função chama o **Format-DevTestMessageWithTime** para prefixar a hora antes de gravar a mensagem para o fluxo de erro. |
| Gravação HostWithTime |Grava uma mensagem no programa host (**Write-Host**) prefixada com a hora atual. O efeito da gravação no programa host varia. A maioria dos programas que hospedam Windows PowerShell grava essas mensagens para a saída padrão. |
| Gravação VerboseWithTime |Grava uma mensagem detalhada prefixada com a hora atual. Pois ele chama **Write-Verbose**, a mensagem será exibida apenas quando o script é executado com o **Verbose** parâmetro ou quando o **VerbosePreference** preferência é definida como  **Continuar**. |

**Publicar aplicativo Web**

| Nome da função | Descrição |
| --- | --- |
| Novo AzureWebApplicationEnvironment |Cria recursos do Azure, como um site ou máquina virtual. |
| Novo WebDeployPackage |Essa função não está implementada. Você pode adicionar comandos nessa função para compilar seu projeto. |
| AzureWebApplication publicar |Publica um aplicativo web no Azure. |
| Publicar aplicativo Web |Cria e implanta aplicativos Web, máquinas virtuais, bancos de dados SQL e contas de armazenamento para um projeto de web do Visual Studio. |
| Teste-WebApplication |Essa função não está implementada. Você pode adicionar comandos nessa função para testar seu aplicativo. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre os scripts do PowerShell lendo [scripts com o Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e ver outros scripts do PowerShell do Azure na [Script Center](https://azure.microsoft.com/documentation/scripts/).

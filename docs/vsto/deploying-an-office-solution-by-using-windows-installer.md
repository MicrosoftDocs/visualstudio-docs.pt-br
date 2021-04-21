---
title: Implantar uma solução do Office usando o Windows Installer
description: Saiba que, ao usar o Visual Studio para criar um Windows Installer, você pode implantar uma solução do Office que exige acesso administrativo no computador do usuário final.
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, setup project
- Office development in Visual Studio, MSI
- deploying applications [Office development in Visual Studio], setup project
- deploying applications [Office development in Visual Studio], MSI
- ClickOnce deployment [Office development in Visual Studio], MSI
- publishing Office solutions [Office development in Visual Studio], setup project
- Office applications [Office development in Visual Studio], MSI
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f6dfa2bb4d3309420cf0a9a71e79b5d07b5477ce
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828521"
---
# <a name="deploy-an-office-solution-by-using-windows-installer"></a>Implantar uma solução do Office usando o Windows Installer

Saiba como criar um Windows Installer para sua solução do Office usando o [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] .

Usando o Visual Studio para criar um Windows Installer, você pode implantar uma solução do Office que exige acesso administrativo no computador do usuário final. Por exemplo, você pode usar esse arquivo para instalar uma solução apenas uma vez para todos os usuários de um computador. Você também pode implantar uma solução do Office usando o ClickOnce, mas essa solução deve ser instalada separadamente para cada usuário do computador.

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-topic"></a>Neste tópico

- [Baixar exemplos de suplemento do VSTO](#Download)

- [Obter o InstallShield Limited Edition](#Obtain)

- [Decidir como conceder confiança à solução](#ApplySecurity)

- [Criar um projeto de instalação](#Create)

- [Adicionar a saída do projeto](#Add)

- [Adicione os manifestos de implantação e aplicativos](#AddD)

- [Configure os componentes dependentes como pré-requisitos](#Configure)

- [Especificar onde você deseja implantar a solução no computador do usuário](#Location)

- [Configurar um suplemento do VSTO](#ConfigureRegistry)

- [Configurar uma personalização em nível de documento](#ConfigureDocument)

- [Criar o projeto de instalação](#Build)

Para obter mais informações sobre como implantar uma solução do Office usando o ClickOnce, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).

Para obter informações sobre como criar um arquivo de Windows Installer usando o [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] , consulte [implantar uma solução do Visual Studio 2010 Tools for Office usando Windows Installer](/previous-versions/visualstudio/visual-studio-2010/ff937654(v=msdn.10)).

## <a name="download-samples"></a><a name="Download"></a>Baixar amostras
Este tópico refere-se aos seguintes exemplos que você pode baixar.

|Amostra<br /><br />|Descrição<br /><br />|
|----------|---------------|
|[ExcelAddIn](https://code.msdn.microsoft.com/VSTO-Deploy-an-Office-fbcc09ad)<br /><br />|Um suplemento do VSTO do Excel que você pode instalar em um computador que executa uma versão de 32 bits ou 64 bits do Office.<br /><br />|
|[ExcelWorkbook](https://code.msdn.microsoft.com/VSTO-Deploy-a-Customization-f70fae33)<br /><br />|Uma personalização do Excel no nível de documento que você pode instalar em um computador que execute uma versão do Office de 32 bits ou de 64 bits.<br /><br />|

## <a name="decide-how-to-grant-trust-to-the-solution"></a><a name="ApplySecurity"></a>Decidir como conceder confiança à solução
Para que uma solução possa ser executada nos computadores dos usuários, você deve conceder confiança de qualquer uma das seguintes formas ou os usuários devem responder a uma solicitação de confiança quando instalam a solução.

- Assine os manifestos usando um certificado que identifica um editor conhecido e confiável. Para obter mais informações, consulte [confiar na solução assinando o aplicativo e os manifestos de implantação](../vsto/granting-trust-to-office-solutions.md#Signing).

- Instale a solução no diretório arquivos de programas no computador do usuário.

> [!NOTE]
> Para personalizações em nível de documento, a localização do documento também deve ser confiável. Para obter mais informações, consulte [Grant Trust to Documents](../vsto/granting-trust-to-documents.md).

## <a name="get-installshield-limited-edition"></a><a name="Obtain"></a>Obter o InstallShield Limited Edition

Você pode criar um arquivo do Windows Installer usando o ISLE (InstallShield Limited Edition), que é gratuito se você instalou o Visual Studio. O ISLE substitui a funcionalidade dos modelos de projeto para instalação e implantação que as versões anteriores do Visual Studio ofereceram.

### <a name="to-get-installshield-limited-edition"></a>Para obter o InstallShield Limited Edition

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

   A caixa de diálogo **Novo Projeto** será aberta.

2. No painel modelos, expanda **outros tipos de projeto** e, em seguida, escolha o modelo de **instalação e implantação** .

3. Na lista de tipos de projeto para **instalação e implantação**, escolha **habilitar InstallShield Limited Edition** e, em seguida, escolha o botão **OK** .

   Você verá uma página que fornece informações sobre como obter o InstallShield Limited Edition.

4. Nessa página, escolha o link **ir para o site de download** .

5. Na página de download do InstallShield Limited Edition, insira as informações necessárias nos campos apropriados e escolha o link **baixar agora** .

   Depois de baixar, instalar e ativar o produto, o modelo de **projeto do InstallShield Limited Edition** aparecerá no Visual Studio.

## <a name="create-a-setup-project"></a><a name="Create"></a>Criar um projeto de instalação

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], abra o projeto do Office que você deseja implantar.

   Os exemplos de suplemento do VSTO associados a este tópico contêm um projeto chamado **ExcelAddIn**. Os exemplos de personalização no nível do documento contêm um projeto chamado **ExcelWorkbook**. Este tópico se referirá ao projeto do Office em sua solução usando um desses dois nomes.

2. Na barra de menus, escolha **arquivo**  >  **Adicionar**  >  **novo projeto**.

   A caixa de diálogo **Adicionar Novo Projeto** é aberta.

3. No painel modelos, expanda **outros tipos de projeto** e, em seguida, escolha o modelo de **instalação e implantação** .

4. Na lista de tipos de projeto para **instalação e implantação**, escolha **projeto InstallShield Limited Edition**, nomeie o projeto e, em seguida, escolha o botão **OK** .

   O projeto de instalação do InstallShield que você criou aparece em sua solução.

   Os exemplos deste tópico contêm um projeto de instalação chamado **OfficeAddInSetup**. Este tópico se referirá ao projeto em sua solução usando o mesmo nome.

## <a name="add-the-project-output"></a><a name="Add"></a>Adicionar a saída do projeto

Você configura o projeto **OfficeAddInSetup** para incluir a saída do seu projeto do Office. Para projetos de suplemento do VSTO, a saída do projeto é apenas o assembly da solução. Para os projetos de personalização no nível de documento, a saída do projeto inclui não apenas o assembly da solução, mas também do próprio documento.

### <a name="to-add-the-project-output"></a>Para adicionar a saída do projeto

1. No **Gerenciador de soluções**, expanda o nó do projeto **OfficeAddInSetup** e escolha o arquivo do **Assistente de projeto** , que mostra a ilustração a seguir.

   ![Arquivo do assistente de projeto no Gerenciador de Soluções](../vsto/media/installshield-projectassistant.png "Arquivo do assistente de projeto no Gerenciador de Soluções")

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

3. Na parte inferior da página **Assistente de projeto** , escolha o botão **arquivos de aplicativo** , que a ilustração a seguir mostra.

   ![O botão arquivos do aplicativo.](../vsto/media/installshield-applicationfiles.png "O botão arquivos do aplicativo.")

4. Na página **arquivos de aplicativo** , escolha o botão **Adicionar saídas de projeto** .

5. Na caixa de diálogo **seletor de saída do Visual Studio** , marque a caixa de seleção **saída primária** e escolha o botão **OK** .

## <a name="add-the-deployment-and-application-manifests"></a><a name="AddD"></a>Adicione os manifestos de implantação e aplicativos

1. Na página **arquivos de aplicativo** , escolha o botão **Adicionar arquivos** .

2. Na caixa de diálogo **abrir** , navegue até o diretório de saída do projeto **ExcelAddIn** .

   Normalmente, o diretório de saída é a subpasta **bin\Release** do diretório raiz do projeto, dependendo da configuração de compilação que você escolher.

3. No diretório de saída, escolha os arquivos **ExcelAddIn. vsto** e **ExcelAddIn.dll. manifest** e, em seguida, escolha o botão **abrir** .

   A página **arquivos de aplicativo** agora contém o arquivo de saída do projeto, o manifesto de implantação e o manifesto do aplicativo, como mostra a ilustração a seguir.

   ![Os arquivos de saída do seu projeto de instalação.](../vsto/media/installshield-outputfiles.png "Os arquivos de saída do seu projeto de instalação.")

## <a name="configure-the-dependent-components-as-prerequisites"></a><a name="Configure"></a>Configure os componentes dependentes como pré-requisitos

Em seu aplicativo de instalação, além dos seguintes componentes, inclua todos os outros componentes que são necessários para que a sua solução seja executada.

- A versão do .NET Framework que a sua solução do Office terá como alvo.

- Microsoft Visual Studio 2010 Tools for Office Runtime.

### <a name="add-the-net-framework-4-or-the-net-framework-45-as-a-prerequisite"></a>Adicionar o .NET Framework 4 ou o .NET Framework 4,5 como um pré-requisito

1. Em **Gerenciador de soluções**, expanda o nó do projeto **OfficeAddInSetup** , expanda o nó **especificar dados do aplicativo** e escolha o arquivo **redistribuível** , que a ilustração a seguir mostra.

   ![O arquivo redistribuível no Gerenciador de Soluções](../vsto/media/installshield-redistributablesfile.png "O arquivo redistribuível no Gerenciador de Soluções")

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

   A página **redistribuíveis** é aberta.

3. Na lista de componentes redistribuíveis, marque a caixa de seleção adequada para a versão do .NET Framework de destino da sua solução.

   Por exemplo, se sua solução for direcionada para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , marque a caixa de seleção **Microsoft .NET Framework 4,5 completo** . Uma caixa de diálogo aparecerá perguntando se você deseja instalar o componente redistribuído, que o InstallShield exige antes de adicionar o componente como um pré-requisito. Se essa caixa de diálogo não aparecer, o componente já existirá no seu computador.

4. Se essa caixa de diálogo for exibida, escolha o botão **não** .

### <a name="add-the-visual-studio-2010-tools-for-office-runtime"></a><a name="AddToolsForOffice"></a>Adicionar o Visual Studio 2010 Tools for Office Runtime

A página **redistribuíveis** contém um item chamado **Microsoft VSTO 2010 Runtime**, mas se refere a uma versão mais antiga do tempo de execução. Portanto, você pode criar manualmente um arquivo de configuração que se refere à versão mais recente. Em seguida, você deve colocar esse arquivo no mesmo diretório que os arquivos de configuração para todos os outros itens que aparecem na página **redistribuível** .

#### <a name="to-add-the-visual-studio-2010-tools-for-office-runtime-as-a-prerequisite"></a>Para adicionar o tempo de execução das ferramentas do Visual Studio 2010 para Office como um pré-requisito

1. Abra o Bloco de Notas e cole o seguinte XML em um arquivo de texto.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SetupPrereq>
   <conditions>
       <condition Type="32" Comparison="2" Path="HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSTO Runtime Setup\v4R" FileName="Version" ReturnValue="10.0.50903" Bits="2"></condition>
   <condition Type="32" Comparison="2" Path="HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSTO Runtime Setup\v4R" FileName="Version" ReturnValue="10.0.50903" Bits="2"></condition>
   </conditions>
   <files>
       <file LocalFile="<ISProductFolder>\SetupPrerequisites\VSTOR\vstor_redist.exe" URL="http://download.microsoft.com/download/C/0/0/C001737F-822B-48C2-8F6A-CDE13B4B9E9C/vstor_redist.exe" CheckSum="88b8aa9e8c90818f98c80ac4dd998b88" FileSize=" 0,40117912"></file>
   </files>
   <execute file="vstor_redist.exe" returncodetoreboot="1641,3010" requiresmsiengine="1">
   </execute>
   <properties Id="{15965040-56BB-49B8-A88F-3525C48D9BA8}" Description="This prerequisite installs the most recent version of the Microsoft Visual Studio 2010 Tools for Office Runtime." >
   </properties>

   </SetupPrereq>
   ```

2. Gere uma GUID no Visual Studio. No menu **ferramentas** , escolha **Criar GUID**.

3. No programa **gerador de GUID** , escolha o botão de opção **formato de registro** , escolha o botão **copiar** e, em seguida, escolha o botão **sair** .

4. No bloco de notas, substitua o texto que **seu GUID vai aqui** colando o GUID em seu lugar.

   O elemento **&lt; Properties &gt;** do seu arquivo é semelhante ao seguinte.

   ```xml
   <properties Id="{87989B73-21DC-4403-8FD1-0C68A41A6D8C}" Description="This prerequisite installs the most recent version of the Microsoft Visual Studio 2010 Tools for Office Runtime." >
   </properties>
   ```

5. Na barra de menus no bloco de notas, escolha **arquivo**  >  **salvar**.

6. Na caixa de diálogo **salvar como** , navegue até a pasta **da área de trabalho** .

7. Na lista **salvar como tipo** , escolha **todos os arquivos (&#42;. &#42;)**.

8. Na caixa **nome do arquivo** , insira **Visual Studio 2010 Tools for Office Runtime. prq** e, em seguida, escolha o botão **salvar** .

   > [!NOTE]
   > Certifique-se de adicionar **. prq** no final do nome do arquivo para identificar esse arquivo como um arquivo de pré-requisito.

9. Feche o Bloco de notas.

10. Na pasta **da área de trabalho** , copie o arquivo *. prq do Visual Studio 2010 Tools for Office Runtime* para um dos diretórios a seguir no seu computador.

   Para sistemas operacionais de 32 bits: *%ProgramFiles%\InstallShield\2013LE\SetupPrerequisites \\*

   Para sistemas operacionais de 64 bits: *% ProgramFiles (x86)% \ 2013LE \ \\ SetupPrerequisites*

11. Na página **redistribuível** do projeto do InstallShield, escolha o botão **Atualizar** para atualizar a lista de componentes redistribuíveis, como mostra a ilustração a seguir.

   ![O botão atualizar.](../vsto/media/installshield-refreshbutton.png "O botão atualizar.")

12. Na lista de componentes redistribuíveis, marque a caixa de seleção **Visual Studio 2010 Tools for Office Runtime** .

   Uma caixa de diálogo aparecerá perguntando se você deseja instalar o componente redistribuível. Se essa caixa de diálogo não aparecer, você poderá pular para a seção [especificar onde deseja implantar a solução no computador do usuário](#Location) deste tópico.

13. Se essa caixa de diálogo for exibida, escolha o botão **não** .

## <a name="specify-where-to-install-the-solution-on-the-users-computer"></a><a name="Location"></a>Especifique o local para instalar a solução no computador do usuário

1. No **Gerenciador de soluções**, expanda o nó **OfficeAddInSetup** , expanda o nó **organizar sua instalação** e, em seguida, escolha o arquivo de **informações gerais** .

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

3. Na lista de propriedades, escolha o botão **procurar** ao lado da propriedade **installdir** .

4. Na caixa de diálogo **set installdir** , escolha uma pasta no computador do usuário onde você deseja instalar a solução.

   > [!NOTE]
   > Você também pode criar subdiretórios na caixa de diálogo **set installdir** abrindo o menu de atalho para qualquer pasta na lista.

## <a name="configure-a-vsto-add-in"></a><a name="ConfigureRegistry"></a>Configurar um suplemento do VSTO

Você pode especificar se deseja que seu suplemento do VSTO seja instalado para todos os usuários do computador (por computador) ou apenas para o usuário que está executando a instalação (por usuário).

Se você quiser oferecer suporte a instalações por computador, crie dois instaladores separados. Você pode dividir os instaladores com base na versão do Office (32 bits e 64 bits) ou na versão do Windows (32 bits e 64 bits) que o usuário está executando.

As instalações por usuário exigem apenas um instalador independente do Office ou versão do Windows.

> [!NOTE]
> Esta seção se aplica somente se você estiver implantando um suplemento do VSTO. Se você estiver implantando uma personalização em nível de documento, poderá ir imediatamente para a seção [Configurar uma personalização em nível de documento](#ConfigureDocument) .

### <a name="to-specify-whether-you-want-to-support-per-user-or-per-computer-installations"></a>Para especificar se você quer oferecer suporte a instalações por usuário ou por computador

1. Em **Gerenciador de soluções**, expanda o nó do projeto **OfficeAddInSetup** , expanda o nó **organizar sua instalação** e, em seguida, escolha o arquivo de **informações gerais** .

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

   Você verá as propriedades do projeto de instalação.

3. Na lista da propriedade **AllUSERS** , especifique se deseja que essa solução seja instalada para todos os usuários do computador ou apenas para o usuário que instala a solução.

   Para instalar o suplemento do VSTO para o usuário atual, escolha **ALLUSERS = "" (instalação por usuário)**. Para instalar o suplemento do VSTO para todos os usuários do computador, escolha **AllUsers = 1 (instalação por computador)**

   No próximo procedimento, você criará chaves do registro para habilitar o aplicativo do Office para descobrir e carregar o suplemento do VSTO. Consulte [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).

### <a name="to-create-registry-keys"></a>Para criar chaves de registro

1. Em **Gerenciador de soluções**, escolha o nó **Assistente de projeto** .

   Na barra de menus, escolha **Exibir**  >  **abrir**.

2. Na parte inferior da página **Assistente de projeto** , escolha o botão **registro do aplicativo** , que a ilustração a seguir mostra.

   ![O botão registro do aplicativo.](../vsto/media/installshield-applicationregistry.gif "O botão registro do aplicativo.")

   A página **registro do aplicativo** é exibida.

3. Em **deseja configurar os dados do registro que seu aplicativo irá instalar?**, escolha o botão de opção **Sim** .

4. Na lista **exibição do registro do computador de destino** , adicione a hierarquia de chave que habilita o tipo de instalador que você deseja criar.

   O caminho que você configura nesta seção depende da criação de um instalador por usuário ou um instalador por computador.

   **Instalador por usuário**

   **HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**

   **Os instaladores por computador baseados na versão do Office**

| Versão do Office<br /><br /> | Configuração do caminho do InstallShield<br /><br /> |
|----------------------------| - |
| 32 bits<br /><br /> | **HKEY_LOCAL_MACHINE\SOFTWARE(32-Bit)\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |
| 64 bits<br /><br /> | **HKEY_LOCAL_MACHINE\SOFTWARE(64-Bit)\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |

   **Os instaladores por computador baseados na versão do Windows**

| Versão do Windows<br /><br /> | Configuração do caminho do InstallShield<br /><br /> |
|-----------------------------| - |
| 32 bits<br /><br /> | **HKEY_LOCAL_MACHINE\SOFTWARE(32-Bit)\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |
| 64 bits<br /><br /> | **HKEY_LOCAL_MACHINE\SOFTWARE(32-Bit)\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br />**HKEY_LOCAL_MACHINE\SOFTWARE(64-Bit)\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |

   > [!NOTE]
   > Um instalador para o Windows de 64 bits requer dois caminhos de registro porque é possível para os usuários executarem versões de 32 bits e de 64 bits do Office em um computador que executa o Windows de 64 bits.

   > [!NOTE]
   > Como prática recomendada, inicie o nome do seu suplemento do VSTO com o nome da sua empresa. Essa convenção aumenta a chance de que a chave seja exclusiva e reduz a chance de conflito com um suplemento do VSTO de outro fornecedor. Os suplementos que têm o mesmo nome podem, por exemplo, substituir as chaves de registro um do outro. Essa abordagem não pode garantir que a chave será única, mas pode reduzir possíveis conflitos de nome.

5. Depois de criar a hierarquia de chaves, abra o menu de atalho da chave **SampleCompany. ExcelAddIn** , escolha **novo** e, em seguida, escolha **valor da cadeia de caracteres**.

   O novo valor de cadeia de caracteres aparece na lista **de dados do registro do computador de destino** . O nome do valor da cadeia de caracteres é realçado e você pode renomeá-lo.

6. Renomeie o valor para **Descrição**.

7. Repita esse processo para criar os seguintes valores.

|Tipo de valor<br /><br />|Nome<br /><br />|
|--------------|--------|
|Valor da cadeia de caracteres<br /><br />|**FriendlyName**<br /><br />|
|Valor DWORD<br /><br />|**LoadBehavior**<br /><br />|
|Valor da cadeia de caracteres<br /><br />|**Manifest**<br /><br />|

8. Abra o menu de atalho para o valor **Descrição** e, em seguida, escolha **Modificar**.

   A caixa de diálogo **Editar dados** é exibida.

9. Na caixa de texto **dados de valor** , insira suplemento de **demonstração do Excel** e, em seguida, escolha o botão **OK** .

   Essa descrição aparece quando o usuário abre o aplicativo do Office, abre a caixa de diálogo **Opções** e, em seguida, no painel **suplementos** , escolhe o suplemento do VSTO.

10. Abra o menu de atalho para o valor **amigável** e, em seguida, escolha **Modificar**.

   A caixa de diálogo **Editar dados** é exibida.

11. Na caixa de texto **dados de valor** , insira suplemento de **demonstração do Excel** e, em seguida, escolha o botão **OK** .

   Essa cadeia de caracteres aparece na caixa de diálogo **suplementos de com** no aplicativo do Office. Por padrão, o valor da cadeia de caracteres é a ID do suplemento do VSTO.

12. Abra o menu de atalho para o valor **LoadBehavior** e escolha **Modificar**.

   A caixa de diálogo **Editar dados** é exibida.

13. Na caixa de texto **dados de valor** , digite **3** e, em seguida, escolha o botão **OK** .

   Um valor de 3 carrega o suplemento do VSTO quando o aplicativo é iniciado. Para obter mais informações sobre valores LoadBehavior, consulte [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).

14. Abra o menu de atalho para o valor de **manifesto** e, em seguida, escolha **Modificar**.

   A caixa de diálogo **Editar dados** é exibida.

15. Na caixa de texto **dados de valor** , digite **file:///[installdir] ExcelAddIn. vsto | vstolocal** e, em seguida, escolha o botão **OK** .

   O Visual Studio 2010 Tools for Office Runtime usa esse caminho para localizar o manifesto de implantação. A parte **[installdir]** desse caminho é uma macro que é mapeada para a propriedade **installdir** na página de propriedades **General Information** do seu projeto de instalação do InstallShield. Essa propriedade especifica o local no computador de destino para instalar o suplemento do VSTO. O sufixo **| vstolocal** garante que sua solução seja carregada da pasta de instalação, não do cache do ClickOnce.

> [!IMPORTANT]
> Se você criar uma região de formulário personalizada em um suplemento do VSTO para o Outlook, deverá criar mais entradas de registro para registrar a região com o Outlook. Para obter mais informações, consulte [entradas do registro para regiões de formulário do Outlook](../vsto/registry-entries-for-vsto-add-ins.md#OutlookEntries).

## <a name="configure-a-document-level-customization"></a><a name="ConfigureDocument"></a>Configurar uma personalização em nível de documento

Esta seção se aplicará somente se você estiver implantando uma personalização em nível de documento. Se você estiver implantando um suplemento do VSTO, poderá ir imediatamente para a seção [criar o projeto de instalação](#Build) .

As personalizações no nível do documento não usam chaves do registro. Em vez disso, as propriedades personalizadas do documento contêm o local do manifesto de implantação.

Para modificar propriedades personalizadas, você cria um programa que remove a personalização no nível do documento do documento, modifica as propriedades apropriadas e anexa novamente a personalização ao documento. Crie uma ação personalizada que execute o programa, adicione essa ação ao seu projeto de instalação.

### <a name="to-create-a-program-that-modifies-document-properties"></a>Para criar um programa que modifica as propriedades do documento

1. Na barra de menus, escolha **arquivo**  >  **Adicionar**  >  **novo projeto**.

   A caixa de diálogo **Adicionar Novo Projeto** é exibida.

2. No painel modelos, no nó do idioma que você deseja usar, escolha a pasta **Windows** .

3. Na lista de tipos de projeto do **Windows**, escolha o modelo de **aplicativo de console** .

4. Nomeie o projeto **SetExcelDocumentProperties** e, em seguida, escolha o botão **OK** .

5. Em **Gerenciador de soluções**, escolha o botão **Mostrar todos os arquivos** , abra o menu de atalho para o nó do projeto **SetExcelDocumentProperties** e escolha **Adicionar referência**.

6. Na caixa de diálogo **Gerenciador de referências** , escolha a guia **extensões** e, em seguida, marque a caixa de seleção ao lado dos seguintes assemblies e escolha o botão **OK** .

   - Microsoft.VisualStudio.Tools.Applications.Runtime

   - Microsoft.VisualStudio.Tools.Applications.ServerDocument

7. Em **Gerenciador de soluções**, escolha o arquivo **Program. cs** (para aplicativos C#) ou o arquivo **Module1. vb** (para aplicativos Visual Basic).

8. Na barra de menus, escolha **Exibir**  >  **abrir**.

9. Substitua o conteúdo do arquivo inteiro pelo seguinte código.

:::code language="vb" source="../vsto/codesnippet/VisualBasic/setexceldocumentproperties/module1.vb" id="Snippet1":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/setexceldocumentproperties/program.cs" id="Snippet1":::

10. Compile o projeto.

### <a name="to-add-a-custom-action-that-runs-your-program"></a>Para adicionar uma ação personalizada que executa o seu programa

1. No **Gerenciador de soluções**, expanda o nó do projeto **OfficeAddInSetup** e escolha o arquivo do **Assistente de projeto** , que mostra a ilustração a seguir.

   ![Arquivo do assistente de projeto no Gerenciador de Soluções](../vsto/media/installshield-projectassistant.png "Arquivo do assistente de projeto no Gerenciador de Soluções")

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

3. Na parte inferior da página **Assistente de projeto** , escolha o botão **arquivos de aplicativo** , que a ilustração a seguir mostra.

   ![O botão arquivos do aplicativo.](../vsto/media/installshield-applicationfiles.png "O botão arquivos do aplicativo.")

4. Na página **arquivos de aplicativo** , escolha o botão **Adicionar saídas de projeto** .

   A caixa de diálogo **seletor de saída do Visual Studio** é exibida.

5. No nó **SetExcelDocumentProperties** , marque a caixa de seleção **saída primária** e escolha o botão **OK** .

6. No **Gerenciador de soluções**, no nó **OfficeAddInSetup** , expanda o nó **definir os requisitos e as ações de instalação** e escolha a pasta **ações personalizadas** .

7. Na barra de menus, escolha **Exibir**  >  **abrir**.

   A lista de eventos aparece em um painel na lateral da tela.

   > [!NOTE]
   > Apenas alguns eventos que aparecem nessa lista estão disponíveis no InstallShield Limited Edition. Neste procedimento, você executará o programa usando o evento de **diálogo após a conclusão da configuração de êxito** .

8. Na lista de eventos, em **ações personalizadas durante a instalação**, abra o menu de atalho do evento de **diálogo após a instalação concluída com êxito** e, em seguida, escolha **novo exe**.

   Uma ação personalizada denominada **NewCustomAction1** aparece no evento de **diálogo após a conclusão da configuração de êxito** . Um conjunto de propriedades para a ação personalizada é exibido em um painel ao lado dos eventos.

   > [!IMPORTANT]
   > Dois **após a conclusão da instalação** eventos de diálogo de êxito aparecem na lista de eventos. Verifique se você escolheu a instância do evento de **diálogo após a instalação concluída com êxito** que aparece sob as **ações personalizadas durante** o nó de instalação.

9. Na lista da propriedade **local de origem** , escolha **instalado com o produto**.

10. Escolha o botão **procurar** ao lado da propriedade **nome do arquivo** .

11. Na caixa **de diálogo procurar um arquivo de destino** , navegue até o arquivo **SetExcelDocumentProperties. Primary. Output** e, em seguida, escolha o botão **abrir** .

    O local desse arquivo depende da pasta que você especificou para a propriedade **installdir** do projeto de instalação. Por exemplo, se você definir essa propriedade como uma pasta denominada **[PersonalFolder] DemoWorkbookApp**, poderá encontrar o arquivo **SetExcelDocumentProperties. Primary. Output** navegando até **[ProgramFilesFolder] \DemoWorkbookApp**.

    Nas próximas etapas, você obterá a ID da solução do documento e passará essa ID como um parâmetro para o aplicativo de console. Você também passará o local do documento, o manifesto de implantação e o assembly do documento.

12. Abra o menu de atalho para o projeto **ExcelWorkbook** e, em seguida, escolha **abrir pasta no Windows Explorer** ou **abra a pasta no explorador de arquivos** , dependendo do seu sistema operacional.

    A pasta que contém a solução é aberta.

13. Abra o arquivo de projeto da sua solução no Bloco de Notas. Para projetos Visual Basic, o nome do arquivo é *ExcelWorkbook. vbproj*. Para projetos C#, o nome do arquivo é *ExcelWorkbook. csproj*.

14. No arquivo de projeto, procure o elemento **&lt; SolutionID &gt;** , copie seu valor para a área de transferência e, em seguida, feche o bloco de notas.

    Passe esse valor para o aplicativo de console como um parâmetro.

15. Na página Propriedades de **NewCustomAction1**, defina a propriedade de **linha de comando** como a linha de texto a seguir.

   ```cmd
   /assemblyLocation="[INSTALLDIR]ExcelWorkbook.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbook.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbook.xlsx" /solutionID="Your Solution ID"
   ```

16. Substitua a **ID** da solução pela ID da solução que você copiou para a área de transferência.

   > [!IMPORTANT]
   > Teste o seu instalador para verificar se o aplicativo de console que essa ação personalizada executa pode acessar os documentos no diretório [INSTALLDIR]. Alguns diretórios no computador do usuário podem exigir acesso administrativo (por exemplo, o diretório arquivos de programas). Se você estiver implantando sua solução em um diretório que requer acesso administrativo, abra a caixa de diálogo **Propriedades** do arquivo *setup.exe* , escolha a guia **compatibilidade** e marque a caixa de seleção **executar este programa como administrador** antes de distribuir o instalador. Se você não quiser que os usuários executem o programa de instalação com permissões administrativas, defina a propriedade [INSTALLDIR] como um diretório ao qual o usuário provavelmente tem acesso já, como o diretório de **documentos** . Para obter mais informações, consulte a seção [especificar onde você deseja instalar a solução no computador do usuário](#Location) deste tópico.

## <a name="build-the-setup-project"></a><a name="Build"></a>Criar o projeto de instalação

1. Em **Gerenciador de soluções**, expanda o nó **preparar para a versão** e escolha o arquivo de **versões** .

2. Na barra de menus, escolha **Exibir**  >  **abrir**.

   O **Builds** Explorer é aberto em um painel lateral para que você possa escolher o tipo de liberação que deseja criar.

3. No **Builds** Explorer, escolha a pasta **SingleImage** .

4. No painel ao lado do **Builds** Explorer, escolha a guia **Setup.exe** .

5. Na página de propriedades **Setup.exe** , na lista **local dos pré-requisitos do InstallShield** , escolha **baixar na Web**.

6. Na barra de menus, escolha **criar**  >  **Configuration Manager**.

7. Na lista **configuração de solução ativa** , escolha **SingleImage**.

8. Na tabela **contextos do projeto** , na coluna **configuração** do projeto **OfficeAddInSetup** , escolha **SingleImage** e, em seguida, escolha o botão **fechar** .

9. Na barra de menus, escolha **Build**  >  **Compilar OfficeAddInSetup**.

   Depois que a compilação for concluída, você poderá localizar o arquivo de *setup.exe* do projeto **OfficeAddInSetup** no seguinte local: <em>OfficeAddInSetupProjectRoot</em>**\OfficeAddInSetup\Express\SingleImage\DiskImages\DISK1 \\**

## <a name="see-also"></a>Consulte também

- [Pré-requisitos da solução do Office para implantação](/previous-versions/bb608617(v=vs.110))
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Entradas de registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md)
- [Visão geral das propriedades do documento personalizado](../vsto/custom-document-properties-overview.md)
- [Conceder confiança às soluções do Office](../vsto/granting-trust-to-office-solutions.md)
- [Conceder confiança aos documentos](../vsto/granting-trust-to-documents.md)
- [Implantar uma solução do Visual Studio 2010 Tools for Office usando o Windows Installer](/previous-versions/visualstudio/visual-studio-2010/ff937654(v=msdn.10))
---
title: Implantar uma solução do Office usando o Windows Installer
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 3e811fac767e8b89f0a6958511c54642f07190cf
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50673049"
---
# <a name="deploy-an-office-solution-by-using-windows-installer"></a>Implantar uma solução do Office usando o Windows Installer
Saiba como criar um instalador do Windows para sua solução do Office usando [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)].  

Usando o Visual Studio para criar um instalador do Windows, você pode implantar uma solução do Office que exige acesso administrativo no computador do usuário final. Por exemplo, você pode usar esse arquivo para instalar uma solução apenas uma vez para todos os usuários de um computador. Você também pode implantar uma solução do Office usando o ClickOnce, mas essa solução deve ser instalada separadamente para cada usuário do computador.  


## <a name="in-this-topic"></a>Neste tópico  

- [Baixe amostras de suplemento do VSTO](#Download)  

- [Obter o InstallShield Limited Edition](#Obtain)  

- [Decidir como conceder confiança à solução](#ApplySecurity)  

- [Criar um projeto de instalação](#Create)  

- [Adicionar a saída do projeto](#Add)  

- [Adicione os manifestos de aplicativo e implantação](#AddD)  

- [Configurar os componentes dependentes como pré-requisitos](#Configure)  

- [Especifique onde você deseja implantar a solução no computador do usuário](#Location)  

- [Configurar um suplemento do VSTO](#ConfigureRegistry)  

- [Configurar uma personalização no nível de documento](#ConfigureDocument)  

- [Compile o projeto de instalação](#Build)  

Para obter mais informações sobre como implantar uma solução do Office usando o ClickOnce, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  

Para obter informações sobre como criar um arquivo do Windows Installer por meio [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)], consulte [implantar um Visual Studio 2010 Tools para soluções do Office usando o Windows Installer](http://go.microsoft.com/fwlink/?LinkId=201807).  


## <a name="Download"></a>Baixar exemplos  
Este tópico refere-se aos seguintes exemplos que você pode baixar.  



|Amostra<br /><br />|Descrição<br /><br />|  
|----------|---------------|  
|[ExcelAddIn](http://go.microsoft.com/fwlink/?LinkID=275492)<br /><br />|Um Add-in do VSTO do Excel que você pode instalar em um computador que executa uma versão de 32 bits ou 64 bits do Office.<br /><br />|  
|[ExcelWorkbook](http://go.microsoft.com/fwlink/?LinkID=275493)<br /><br />|Uma personalização do Excel no nível de documento que você pode instalar em um computador que execute uma versão do Office de 32 bits ou de 64 bits.<br /><br />|  

## <a name="ApplySecurity"></a>Decidir como conceder confiança à solução  
Para que uma solução possa ser executada nos computadores dos usuários, você deve conceder confiança de qualquer uma das seguintes formas ou os usuários devem responder a uma solicitação de confiança quando instalam a solução.  


- Assine os manifestos usando um certificado que identifica um editor conhecido e confiável. Para obter mais informações, consulte [confiar a solução ao assinar os manifestos de aplicativo e implantação](../vsto/granting-trust-to-office-solutions.md#Signing).  

- Instale a solução para o diretório de arquivos de programas no computador do usuário.  

> [!NOTE]  
> Para personalizações em nível de documento, a localização do documento também deve ser confiável. Para obter mais informações, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).  


## <a name="Obtain"></a>Obter o InstallShield Limited Edition  
Você pode criar um arquivo do Windows Installer usando o ISLE (InstallShield Limited Edition), que é gratuito se você instalou o Visual Studio. O ISLE substitui a funcionalidade dos modelos de projeto para instalação e implantação que as versões anteriores do Visual Studio ofereceram.  


### <a name="to-get-installshield-limited-edition"></a>Para obter o InstallShield Limited Edition  

1. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  

   A caixa de diálogo **Novo Projeto** é aberta.  

2. No painel de modelos, expanda **Other Project Types**e, em seguida, escolha o **instalação e implantação** modelo.  

3. Na lista de tipos de projeto para **Setup and Deployment**, escolha **habilitar InstallShield Limited Edition**e, em seguida, escolha o **Okey** botão.  

   Você verá uma página que fornece informações sobre como obter o InstallShield Limited Edition.  

4. Nessa página, escolha o **ir para o site de download da** link.  

5. Na página de download do InstallShield Limited Edition, insira as informações necessárias nos campos apropriados e, em seguida, escolha o **baixar agora** link.  

   Depois de baixar, instalar e ativar o produto, o **projeto InstallShield Limited Edition** modelo aparece no Visual Studio.  


## <a name="Create"></a>Criar um projeto de instalação  

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], abra o projeto do Office que você deseja implantar.  

   Os exemplos de suplemento do VSTO que estão associados este tópico contém um projeto chamado **ExcelAddIn**. Os exemplos de personalização no nível de documento contêm um projeto chamado **ExcelWorkbook**. Este tópico se referirá ao projeto do Office em sua solução usando um desses dois nomes.  

2. Na barra de menus, escolha **arquivo** > **Add** > **novo projeto**.  

   A caixa de diálogo **Adicionar Novo Projeto** é aberta.  

3. No painel de modelos, expanda **Other Project Types**e, em seguida, escolha o **instalação e implantação** modelo.  

4. Na lista de tipos de projeto para **Setup and Deployment**, escolha **projeto InstallShield Limited Edition**, nomeie o projeto e, em seguida, escolha o **Okey** botão.  

   O projeto de instalação do InstallShield que você criou aparecerá na sua solução.  

   Os exemplos deste tópico contêm um projeto de instalação que é denominado **OfficeAddInSetup**. Este tópico se referirá ao projeto em sua solução usando o mesmo nome.  


## <a name="Add"></a>Adicionar a saída do projeto  
Você configura a **OfficeAddInSetup** projeto para incluir a saída do seu projeto do Office. Para projetos de suplemento do VSTO, a saída do projeto é somente o assembly da solução. Para os projetos de personalização no nível de documento, a saída do projeto inclui não apenas o assembly da solução, mas também do próprio documento.  


### <a name="to-add-the-project-output"></a>Para adicionar a saída do projeto  

1. Na **Gerenciador de soluções**, expanda o **OfficeAddInSetup** nó do projeto e, em seguida, escolha o **Assistente de projeto** arquivo, que mostra a ilustração a seguir.  

   ![Assistente de arquivo no Gerenciador de soluções de projeto](../vsto/media/installshield-projectassistant.png "Assistente de arquivo no Gerenciador de soluções de projeto")  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

3. Na parte inferior a **Assistente de projeto** , escolha o **arquivos de aplicativo** botão, que mostra a ilustração a seguir.  

   ![O botão de arquivos do aplicativo. ](../vsto/media/installshield-applicationfiles.png "Botão o arquivos do aplicativo.")  

4. No **arquivos de aplicativo** , escolha o **adicionar saídas do projeto** botão.  

5. No **seletor de saída do Visual Studio** caixa de diálogo, selecione o **saída primária** caixa de seleção e, em seguida, escolha o **Okey** botão.  


## <a name="AddD"></a>Adicione os manifestos de aplicativo e implantação  

###  
1. No **arquivos de aplicativo** , escolha o **adicionar arquivos** botão.  

2. No **aberto** caixa de diálogo, navegue até o diretório de saída da **ExcelAddIn** projeto.  

   Geralmente, o diretório de saída é o **bin\release** subpasta do diretório raiz do projeto, dependendo da configuração de compilação que você escolher.  

3. No diretório de saída, escolha o **Exceladdin** e **Exceladdin** arquivos e, em seguida, escolha o **abrir** botão.  

   O **arquivos de aplicativo** página agora contém o arquivo de saída do projeto, o manifesto de implantação e o manifesto do aplicativo, como mostra a ilustração a seguir.  

   ![Os arquivos de saída do seu projeto de instalação. ](../vsto/media/installshield-outputfiles.png "Os arquivos de saída do seu projeto de instalação.")  


## <a name="Configure"></a>Configurar os componentes dependentes como pré-requisitos  
Em seu aplicativo de instalação, além dos seguintes componentes, inclua todos os outros componentes que são necessários para que a sua solução seja executada.  


- A versão do .NET Framework que a sua solução do Office terá como alvo.  

- Microsoft Visual Studio 2010 Tools for Office Runtime.  


### <a name="add-the-net-framework-4-or-the-net-framework-45-as-a-prerequisite"></a>Adicionar o .NET Framework 4 ou o .NET Framework 4.5 como um pré-requisito  

1. Na **Gerenciador de soluções**, expanda o **OfficeAddInSetup** nó do projeto, expanda o **especificar dados do aplicativo** nó e, em seguida, escolha o  **Pacotes redistribuíveis** arquivo, que mostra a ilustração a seguir.  

   ![Os arquivos redistribuíveis no Gerenciador de soluções](../vsto/media/installshield-redistributablesfile.png "redistribuíveis o arquivo no Gerenciador de soluções")  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

   O **redistribuíveis** página será aberta.  

3. Na lista de componentes redistribuíveis, marque a caixa de seleção adequada para a versão do .NET Framework de destino da sua solução.  

   Por exemplo, se sua solução tem como destino o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], selecione o **Microsoft .NET Framework 4.5 Full** caixa de seleção. Uma caixa de diálogo aparecerá perguntando se você deseja instalar o componente redistribuído, que o InstallShield exige antes de adicionar o componente como um pré-requisito. Se essa caixa de diálogo não aparecer, o componente já existe em seu computador.  

4. Se essa caixa de diálogo for exibida, escolha o **não** botão.  


### <a name="AddToolsForOffice"></a>Adicionar o Visual Studio 2010 Tools for Office Runtime  
O **redistribuíveis** página contém um item chamado **Microsoft VSTO 2010 Runtime**, mas ele se refere a uma versão mais antiga do tempo de execução. Portanto, você pode criar manualmente um arquivo de configuração que se refere à versão mais recente. Você deve, em seguida, colocar esse arquivo no mesmo diretório que os arquivos de configuração para todos os outros itens que aparecem na **redistribuíveis** página.  


#### <a name="to-add-the-visual-studio-2010-tools-for-office-runtime-as-a-prerequisite"></a>Para adicionar o Visual Studio 2010 Tools for Office runtime como um pré-requisito  

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

2. Gere uma GUID no Visual Studio. Sobre o **ferramentas** menu, escolha **criar GUID**.  

3. No **gerador de GUID** de programa, escolha o **formato de registro** botão de opção, escolha o **cópia** botão e, em seguida, escolha o **sair** botão.  

4. No bloco de notas, substitua o texto **seu GUID é inserido aqui** colando a GUID em seu lugar.  

   O **&lt;properties&gt;** elemento do seu arquivo semelhante ao seguinte.  


   ```xml  
   <properties Id="{87989B73-21DC-4403-8FD1-0C68A41A6D8C}" Description="This prerequisite installs the most recent version of the Microsoft Visual Studio 2010 Tools for Office Runtime." >  
   </properties>  
   ```  

5. Na barra de menu no bloco de notas, escolha **arquivo** > **salvar**.  

6. No **Salvar como** caixa de diálogo, navegue até seu **área de trabalho** pasta.  

7. No **Salvar como tipo** , escolha **todos os arquivos (&#42;.&#42;)** .  

8. No **nome do arquivo** , digite **Visual Studio 2010 Tools for Office prq**e, em seguida, escolha o **salvar** botão.  

   > [!NOTE]  
   >    Certifique-se de que você adicione **prq** no final do nome do arquivo para identificar o arquivo como um arquivo de pré-requisito.  

9. Feche o Bloco de Notas.  

10. De seu **área de trabalho** pasta, copie o *Visual Studio 2010 Tools for Office prq* arquivo a um dos seguintes diretórios em seu computador.  

   Para sistemas operacionais de 32 bits: *%ProgramFiles%\InstallShield\2013LE\SetupPrerequisites\\*  

   Para sistemas operacionais de 64 bits: *% ProgramFiles (x86) %\2013LE\SetupPrerequisites\\*  

11. No **Redistributable** página do projeto do InstallShield, escolha o **atualizar** botão para atualizar a lista de componentes redistribuíveis, como mostra a ilustração a seguir.  

   ![O botão de atualização. ](../vsto/media/installshield-refreshbutton.png "No botão Atualizar.")  

12. Na lista de componentes redistribuíveis, selecione a **Visual Studio 2010 Tools for Office Runtime** caixa de seleção.  

   Uma caixa de diálogo aparecerá perguntando se você deseja instalar o componente redistribuível. Se essa caixa de diálogo não aparecer, você poderá pular para o [especifique onde você deseja implantar a solução no computador do usuário](#Location) seção deste tópico.  

13. Se essa caixa de diálogo for exibida, escolha o **não** botão.  


## <a name="Location"></a>Especifique onde instalar a solução no computador do usuário  

1. Na **Gerenciador de soluções**, expanda o **OfficeAddInSetup** nó, expanda o **organizar sua instalação** nó e, em seguida, escolha o **asinformaçõesgerais** arquivo.  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

3. Na lista de propriedades, escolha o **navegue** lado a **INSTALLDIR** propriedade.  

4. No **definir INSTALLDIR** caixa de diálogo caixa, escolha uma pasta no computador do usuário em que você deseja instalar a solução.  

   > [!NOTE]  
   >    Você também pode criar subdiretórios na **definir INSTALLDIR** caixa de diálogo, abrindo o menu de atalho para qualquer pasta na lista.  


## <a name="ConfigureRegistry"></a>Configurar um suplemento do VSTO  
Você pode especificar se deseja que o suplemento do VSTO para ser instalado para todos os usuários do computador (por computador), ou apenas para o usuário que está executando a instalação (por usuário).  

Se você quiser oferecer suporte a instalações por computador, crie dois instaladores separados. Você pode dividir os instaladores com base na versão do Office (32 bits e 64 bits) ou na versão do Windows (32 bits e 64 bits) que o usuário está executando.  

As instalações por usuário exigem apenas um instalador independente do Office ou versão do Windows.  

> [!NOTE]  
> Esta seção se aplica somente se você estiver implantando um suplemento do VSTO. Se você estiver implantando uma personalização no nível de documento, você pode ir imediatamente para o [configurar uma personalização no nível de documento](#ConfigureDocument) seção.  


### <a name="to-specify-whether-you-want-to-support-per-user-or-per-computer-installations"></a>Para especificar se você quer oferecer suporte a instalações por usuário ou por computador  

1. Na **Gerenciador de soluções**, expanda o **OfficeAddInSetup** nó do projeto, expanda o **organizar a instalação** nó e, em seguida, escolha o **informações gerais**  arquivo.  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

   Você verá as propriedades do projeto de instalação.  

3. Na lista para o **AllUSERS** propriedade, especifique se deseja que essa solução seja instalada para todos os usuários do computador ou somente para o usuário que instala a solução.  

   Para instalar o suplemento do VSTO para o usuário atual, escolha **ALLUSERS = "" (instalação por usuário)**. Para instalar o suplemento do VSTO para todos os usuários do computador, escolha **ALLUSERS = 1 (instalação por máquina)**  

   No próximo procedimento, você criará as chaves do registro para habilitar o aplicativo do Office para descobrir e carregar o suplemento do VSTO. Ver [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  


### <a name="to-create-registry-keys"></a>Para criar chaves de registro  

1. Na **Gerenciador de soluções**, escolha o **Assistente de projeto** nó.  

   Na barra de menus, escolha **modo de exibição** > **abrir**.  

2. Na parte inferior a **Assistente de projeto** , escolha o **registro do aplicativo** botão, que mostra a ilustração a seguir.  

   ![O botão de registro do aplicativo. ](../vsto/media/installshield-applicationregistry.gif "Botão o registro do aplicativo.")  

   O **registro de aplicativo** página será exibida.  

3. Sob **você deseja configurar os dados de registro que o aplicativo instalará?**, escolha o **Sim** botão de opção.  

4. No **exibição do registro do computador de destino** lista, adicione a hierarquia de chave que permite que o tipo de instalador que você deseja criar.  

   O caminho que você configura nesta seção depende da criação de um instalador por usuário ou um instalador por computador.  

   **Instalador por usuário**  

   **HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**  

   **Instaladores por computador baseados na versão do Office**  



| Versão do Office<br /><br /> | Configuração do caminho do InstallShield<br /><br /> |
|----------------------------| - |
| 32 bits<br /><br /> | **HKEY_LOCAL_MACHINE\Software(32-bit) \Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |
| 64 bits<br /><br /> | **HKEY_LOCAL_MACHINE\Software(64-bit) \Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |

   **Instaladores por computador baseados na versão do Windows**  



| Versão do Windows<br /><br /> | Configuração do caminho do InstallShield<br /><br /> |
|-----------------------------| - |
| 32 bits<br /><br /> | **HKEY_LOCAL_MACHINE\Software(32-bit) \Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |
| 64 bits<br /><br /> | **HKEY_LOCAL_MACHINE\Software(32-bit) \Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br />**HKEY_LOCAL_MACHINE\Software(64-bit) \Microsoft\Office\Excel\Addins\SampleCompany.ExcelAddIn**<br /><br /> |

   > [!NOTE]  
   >    Um instalador para Windows de 64 bits exige dois caminhos de registro, pois é possível que os usuários executem as versões de 32 bits e 64 bits do Office em um computador que executa o Windows de 64 bits.  

   > [!NOTE]  
   >    Como prática recomendada, inicie o nome do seu suplemento do VSTO com o nome da sua empresa. Esta convenção aumenta a chance de que a chave será exclusiva e diminui a chance de conflito com um suplemento do VSTO de outro fornecedor. Os suplementos que têm o mesmo nome podem, por exemplo, substituir as chaves de registro um do outro. Essa abordagem não pode garantir que a chave será única, mas pode reduzir possíveis conflitos de nome.  

5. Depois de criar a hierarquia de chaves, abra o menu de atalho para o **Samplecompany** da chave, escolha **New**e, em seguida, escolha **valor de cadeia de caracteres**.  

   O novo valor de cadeia de caracteres aparece na **dados do registro do computador de destino** lista. O nome do valor da cadeia de caracteres é realçado e você pode renomeá-lo.  

6. Renomeie o valor como **descrição**.  

7. Repita esse processo para criar os seguintes valores.  



|Tipo do Valor<br /><br />|Nome<br /><br />|  
|--------------|--------|  
|Valor da cadeia de caracteres<br /><br />|**Nome amigável**<br /><br />|  
|Valor DWORD<br /><br />|**LoadBehavior**<br /><br />|  
|Valor da cadeia de caracteres<br /><br />|**Manifesto**<br /><br />|  

8. Abra o menu de atalho para o **descrição** valor e, em seguida, escolha **modificar**.  

   O **editar dados** caixa de diálogo é exibida.  

9. No **dados do valor** texto, digite **Excel Add-In Demo**e, em seguida, escolha o **Okey** botão.  

   Essa descrição é exibida quando o usuário abre o aplicativo do Office, abre o **opções** caixa de diálogo e, em seguida, no **Add-Ins** painel, escolhe o suplemento do VSTO.  

10. Abra o menu de atalho para o **FriendlyName** valor e, em seguida, escolha **modificar**.  

   O **editar dados** caixa de diálogo é exibida.  

11. No **dados do valor** texto, digite **Excel Add-In Demo**e, em seguida, escolha o **Okey** botão.  

   Essa cadeia de caracteres aparece na **suplementos COM** caixa de diálogo no aplicativo do Office. Por padrão, o valor da cadeia de caracteres é a ID de suplemento do VSTO  

12. Abra o menu de atalho para o **LoadBehavior** valor e, em seguida, escolha **modificar**.  

   O **editar dados** caixa de diálogo é exibida.  

13. No **dados do valor** texto, digite **3**e, em seguida, escolha o **Okey** botão.  

   Um valor de 3 carrega o suplemento do VSTO, quando o aplicativo é iniciado. Para obter mais informações sobre valores LoadBehavior, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  

14. Abra o menu de atalho para o **manifesto** valor e, em seguida, escolha **modificar**.  

   O **editar dados** caixa de diálogo é exibida.  

15. No **dados do valor** texto, digite **file:///[INSTALLDIR]ExcelAddIn.vsto|vstolocal**e, em seguida, escolha o **Okey** botão.  

   O Visual Studio 2010 Tools for Office Runtime usa esse caminho para localizar o manifesto de implantação. O **[INSTALLDIR]** parte desse caminho é uma macro que mapeia para o **INSTALLDIR** propriedade no **informações gerais** página de propriedades do seu projeto de instalação do InstallShield. Essa propriedade especifica o local no computador de destino para instalar o suplemento do VSTO. O **| vstolocal** sufixo garante que sua solução seja carregada na pasta de instalação, não o cache do ClickOnce.  

> [!IMPORTANT]  
> Se você criar uma região de formulário personalizada em um suplemento do VSTO para Outlook, você deve criar mais entradas de registro para registrar a região com o Outlook. Para obter mais informações, consulte [regiões do formulário de entradas do registro para o Outlook](../vsto/registry-entries-for-vsto-add-ins.md#OutlookEntries).  


## <a name="ConfigureDocument"></a>Configurar uma personalização no nível de documento  
Esta seção se aplica somente se você estiver implantando uma personalização no nível de documento. Se você estiver implantando um suplemento do VSTO, você poderá ir imediatamente para o [compilar o projeto de instalação](#Build) seção.  

Personalizações no nível do documento não usam as chaves do registro. Em vez disso, as propriedades personalizadas do documento contêm o local do manifesto de implantação.  

Para modificar as propriedades personalizadas, você deve criar um programa que remove a personalização de nível de documento do documento, modifique as propriedades adequadas e, em seguida, anexa novamente personalização ao documento. Crie uma ação personalizada que execute o programa, adicione essa ação ao seu projeto de instalação.  

### <a name="to-create-a-program-that-modifies-document-properties"></a>Para criar um programa que modifica as propriedades do documento  

1. Na barra de menus, escolha **arquivo** > **Add** > **novo projeto**.  

   A caixa de diálogo **Adicionar Novo Projeto** é exibida.  

2. No painel modelos, sob o nó para o idioma que você deseja usar, escolha o **Windows** pasta.  

3. Na lista de tipos de projeto para **Windows**, escolha o **aplicativo de Console** modelo.  

4. Nomeie o projeto **SetExcelDocumentProperties**e, em seguida, escolha o **Okey** botão.  

5. Na **Gerenciador de soluções**, escolha o **Show All Files** botão, abra o menu de atalho para o **SetExcelDocumentProperties** nó do projeto e escolha **Adicionar referência**.  

6. No **Gerenciador de referências** diálogo caixa, escolha o **extensões** guia e, em seguida, marque a caixa de seleção ao lado de assemblies a seguir e, em seguida, escolha o **Okey** botão.  


   - Microsoft.VisualStudio.Tools.Applications.Runtime  

   - Microsoft.VisualStudio.Tools.Applications.ServerDocument  

7. Na **Gerenciador de soluções**, escolha o **Program.cs** arquivo (para aplicativos em c#) ou o **Module1.vb** arquivo (para aplicativos do Visual Basic).  

8. Na barra de menus, escolha **modo de exibição** > **abrir**.  

9. Substitua o conteúdo do arquivo inteiro pelo seguinte código.  

[!code-vb[Trin_CustomAction#1](../vsto/codesnippet/VisualBasic/setexceldocumentproperties/module1.vb#1)]
[!code-csharp[Trin_CustomAction#1](../vsto/codesnippet/CSharp/setexceldocumentproperties/program.cs#1)]  

10. Compile o projeto.  


### <a name="to-add-a-custom-action-that-runs-your-program"></a>Para adicionar uma ação personalizada que executa o seu programa  

1. Na **Gerenciador de soluções**, expanda o **OfficeAddInSetup** nó do projeto e, em seguida, escolha o **Assistente de projeto** arquivo, que mostra a ilustração a seguir.  

   ![Assistente de arquivo no Gerenciador de soluções de projeto](../vsto/media/installshield-projectassistant.png "Assistente de arquivo no Gerenciador de soluções de projeto")  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

3. Na parte inferior a **Assistente de projeto** , escolha o **arquivos de aplicativo** botão, que mostra a ilustração a seguir.  

   ![O botão de arquivos do aplicativo. ](../vsto/media/installshield-applicationfiles.png "Botão o arquivos do aplicativo.")  

4. No **arquivos de aplicativo** , escolha o **adicionar saídas do projeto** botão.  

   O **seletor de saída do Visual Studio** caixa de diálogo é exibida.  

5. Sob o **SetExcelDocumentProperties** nó, selecione o **saída primária** caixa de seleção e, em seguida, escolha o **Okey** botão.  

6. No **Gerenciador de soluções**, nas **OfficeAddInSetup** nó, expanda o **definir requisitos de instalação e as ações** nó e, em seguida, escolha o **personalizado Ações** pasta.  

7. Na barra de menus, escolha **modo de exibição** > **abrir**.  

   A lista de eventos aparece em um painel na lateral da tela.  

   > [!NOTE]  
   >    Apenas alguns eventos que aparecem nessa lista estão disponíveis no InstallShield Limited Edition. Neste procedimento, você executará o programa usando o **caixa de diálogo após o êxito completo da instalação** eventos.  

8. Na lista de eventos, sob **ações personalizadas durante a instalação**, abra o menu de atalho para o **caixa de diálogo após o êxito completo da instalação** evento e, em seguida, escolha **novo EXE**.  

   Uma ação personalizada denominada **NewCustomAction1** aparece sob o **caixa de diálogo após o êxito completo da instalação** eventos. Um conjunto de propriedades para a ação personalizada é exibido em um painel ao lado dos eventos.  

   > [!IMPORTANT]  
   >    Duas **caixa de diálogo após o êxito completo da instalação** eventos aparecem na lista de eventos. Certifique-se de que você escolha a instância das **caixa de diálogo após o êxito completo da instalação** eventos que aparece sob o **ações personalizadas durante a instalação** nó.  

9. Na lista para o **local de origem** propriedade, escolha **instalados com o produto**.  

10. Escolha o **navegue** lado a **nome do arquivo** propriedade.  

11. No **procura um arquivo de destino** caixa de diálogo, navegue até a **SetExcelDocumentProperties.Primary.output** file e, em seguida, escolha o **abrir** botão.  

    O local desse arquivo depende da pasta que você especificou para o **INSTALLDIR** propriedade do projeto de instalação. Por exemplo, se você definir essa propriedade para uma pasta denominada **[PersonalFolder] DemoWorkbookApp**, você pode encontrar o **SetExcelDocumentProperties.Primary.output** navegando até o arquivo **[ ProgramFilesFolder] \DemoWorkbookApp**.  

    As próximas etapas, você obter a ID da solução do documento e, em seguida, passar essa ID como um parâmetro para o aplicativo de console. Você também passará o local do documento, o manifesto de implantação e o assembly de documentos.  

12. Abra o menu de atalho para o **ExcelWorkbook** do projeto e, em seguida, escolha **Abrir pasta no Windows Explorer** ou **Abrir pasta no Explorador de arquivos** , dependendo de seu operando sistema.  

    A pasta que contém a solução é aberta.  

13. Abra o arquivo de projeto da sua solução no Bloco de Notas. Para projetos do Visual Basic, o nome do arquivo é *Excelworkbook*. Para projetos c#, o nome do arquivo é *Excelworkbook*.  

14. No arquivo de projeto, procure o **&lt;SolutionID&gt;** elemento, copie o valor na área de transferência e, em seguida, feche o bloco de notas.  

    Passe esse valor para o aplicativo de console como um parâmetro.  

15. Na página de propriedades do **NewCustomAction1**, defina as **linha de comando** propriedade para a seguinte linha de texto.  


   ```cmd
   /assemblyLocation="[INSTALLDIR]ExcelWorkbook.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbook.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbook.xlsx" /solutionID="Your Solution ID"  
   ```  

16. Substitua **sua ID da solução** com a ID da solução que você copiou para a área de transferência.  

   > [!IMPORTANT]  
   >    Teste o seu instalador para verificar se o aplicativo de console que essa ação personalizada executa pode acessar os documentos no diretório [INSTALLDIR]. Alguns diretórios no computador do usuário podem exigir acesso administrativo (por exemplo, o diretório de arquivos de programas). Se você estiver implantando sua solução para um diretório que exige acesso administrativo, abra o **propriedades** caixa de diálogo da *setup.exe* do arquivo, escolha o **compatibilidade** guia e, em seguida, selecione o **executar este programa como administrador** caixa de seleção antes de distribuir o instalador. Se você não quiser que os usuários executem o programa de instalação com permissões administrativas, defina a propriedade [INSTALLDIR] para um diretório ao qual o usuário provavelmente tem acesso, como o **documentos** directory. Para obter mais informações, consulte o [especifique onde deseja instalar a solução no computador do usuário](#Location) seção deste tópico.  


## <a name="Build"></a>Compile o projeto de instalação  

1. Na **Gerenciador de soluções**, expanda o **preparar para a versão** nó e, em seguida, escolha o **versões** arquivo.  

2. Na barra de menus, escolha **modo de exibição** > **abrir**.  

   O **compilações** explorer será aberto em um painel lateral, para que você possa escolher o tipo de versão que você deseja criar.  

3. No **compilações** explorer, escolha o **SingleImage** pasta.  

4. No painel de Avançar para o **compilações** explorer, escolha o **Setup.exe** guia.  

5. No **Setup.exe** página de propriedades, da **local de pré-requisitos do InstallShield** , escolha **baixar da Web**.  

6. Na barra de menus, escolha **Build** > **Gerenciador de Configurações**.  

7. No **configuração da solução ativa** , escolha **SingleImage**.  

8. No **contextos do projeto** tabela, o **Configuration** coluna do **OfficeAddInSetup** do projeto, escolha **SingleImage**e, em seguida, Escolha o **fechar** botão.  

9. Na barra de menus, escolha **construir** > **Build OfficeAddInSetup**.  

   Depois que a compilação for concluída, você pode localizar o *setup.exe* arquivo da **OfficeAddInSetup** projeto no seguinte local: <em>OfficeAddInSetupProjectRoot</em> **\OfficeAddInSetup\Express\SingleImage\DiskImages\DISK1\\**  


## <a name="see-also"></a>Consulte também  
[Pré-requisitos de solução do Office para implantação](https://msdn.microsoft.com/library/9f672809-43a3-40a1-9057-397ce3b5126e)  
[Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
[Entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md)  
[Visão geral das propriedades de documento personalizadas](../vsto/custom-document-properties-overview.md)  
[Conceder confiança a soluções do Office](../vsto/granting-trust-to-office-solutions.md)  
[Conceder confiança a documentos](../vsto/granting-trust-to-documents.md)  
[Implantar um Visual Studio 2010 Tools para soluções do Office usando o Windows Installer](http://go.microsoft.com/fwlink/?LinkId=201807)  

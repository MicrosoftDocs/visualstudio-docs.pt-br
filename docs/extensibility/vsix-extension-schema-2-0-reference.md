---
title: Referência de esquema 2.0 de extensão do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e295bc8c09f41c4c1c77b216a9d91d0644d2d24e
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388537"
---
# <a name="vsix-extension-schema-20-reference"></a>Referência de esquema 2.0 de extensão do VSIX
Um arquivo de manifesto de implantação do VSIX descreve o conteúdo de um pacote VSIX. O formato de arquivo é regido por um esquema. A versão 2.0 desse esquema dá suporte a adição de atributos e tipos personalizados.  O esquema do manifesto é extensível. O carregador de manifesto ignora elementos XML e atributos que não entende.  
  
> [!IMPORTANT]
>  Visual Studio 2015 pode carregar arquivos VSIX nos formatos de Visual Studio 2010, Visual Studio 2012 ou Visual Studio 2013.  
  
## <a name="package-manifest-schema"></a>Esquema de manifesto de pacote  
 O elemento raiz do arquivo manifesto XML é `<PackageManifest>`. Ele tem um único atributo `Version`, que é a versão do formato de manifesto. Se forem feitas alterações principais para o formato, o formato da versão é alterado. Este artigo descreve a versão do formato de manifesto 2.0, que é especificado no manifesto, definindo o `Version` de atributo para o valor da versão = "2.0".  
  
### <a name="packagemanifest-element"></a>Elemento PackageManifest  
 Dentro de `<PackageManifest>` elemento raiz, você pode usar os seguintes elementos:  
  
-   `<Metadata>` -Metadados e informações de anúncio sobre o pacote propriamente dito. Apenas um `Metadata` elemento é permitido no manifesto.  
  
-   `<Installation>` -Esta seção define a maneira que este pacote de extensão pode ser instalado, incluindo se ele pode ser instalado em SKUs do aplicativo. Um único `Installation` elemento é permitido no manifesto. Um manifesto deve ter um `Installation` elemento ou esse pacote não será instalado em qualquer SKU.  
  
-   `<Dependencies>` -Uma lista opcional de dependências para esse pacote são definidos aqui.  
  
-   `<Assets>` -Esta seção contém todos os ativos contidos neste pacote. Nesta seção, esse pacote não surgir qualquer conteúdo.  
  
-   `<AnyElement>*` -O esquema de manifesto é flexível o suficiente para permitir que todos os outros elementos. Elementos filho não reconhecidos pelo carregador de manifesto são expostos na API do Gerenciador de extensões como objetos de XmlElement extras. Usando esses elementos filho, extensões VSIX podem definir dados adicionais no arquivo de manifesto que o código em execução no Visual Studio pode acessar no tempo de execução. Consulte <xref:Microsoft.VisualStudio.ExtensionManager.IExtension.AdditionalElements%2A> e <xref:Microsoft.VisualStudio.ExtensionManager.IExtension.LocalizedAdditionalElements%2A>.  
  
### <a name="metadata-element"></a>Elemento de metadados  
 Nesta seção é os metadados sobre o pacote, sua identidade e informações de publicidade. `<Metadata>` contém os seguintes elementos:  
  
-   `<Identity>` -Define as informações de identificação para esse pacote e inclui os seguintes atributos:  
  
    -   `Id` -Este atributo deve ser uma ID exclusiva para o pacote escolhido por seu autor. O nome deve ser qualificado da mesma forma que os tipos CLR são ajudaria: Company.Product.Feature.Name. O `Id` atributo é limitado a 100 caracteres.  
  
    -   `Version` -Define a versão deste pacote e seu conteúdo. Esse atributo segue o formato de controle de versão do assembly CLR: Major (1.2.40308.00). Um pacote com um maior número de versão é considerado atualizações do pacote e pode ser instalado em relação à versão instalada existente.  
  
    -   `Language` -Este atributo é o idioma padrão para o pacote e corresponde aos dados textuais neste manifesto. Esse atributo segue a convenção de código de localidade do CLR para assemblies de recurso, por exemplo: en-us, en, fr-fr. Você pode especificar `neutral` para declarar uma extensão com neutralidade de idioma que será executado em qualquer versão do Visual Studio. O valor padrão é `neutral`.  
  
    -   `Publisher` -Este atributo identifica o editor desse pacote, uma empresa ou um nome individual. O `Publisher` atributo é limitado a 100 caracteres.  
  
-   `<DisplayName>` -Este elemento Especifica o nome amigável do pacote que é exibido na UI do Gerenciador de extensões. O `DisplayName` conteúdo é limitado a 50 caracteres.  
  
-   `<Description>` -Esse elemento opcional é uma breve descrição do pacote e seu conteúdo que é exibida na UI do Gerenciador de extensões. O `Description` conteúdo pode conter qualquer texto que você deseja, mas ele tem limitado a 1000 caracteres.  
  
-   `<MoreInfo>` -Esse elemento opcional é uma URL para uma página online que contém uma descrição completa desse pacote. O protocolo deve ser especificado como o http.  
  
-   `<License>` -Esse elemento opcional é um caminho relativo para um arquivo de licença (. txt,. rtf) contido no pacote.  
  
-   `<ReleaseNotes>` -Esse elemento opcional é um caminho relativo para um arquivo de notas de versão contido no pacote (. txt,. rtf) ou então uma URL para um site da Web que exibe as notas de versão.  
  
-   `<Icon>` -Esse elemento opcional é um caminho relativo para um arquivo de imagem (png, bmp, jpeg, ico) contido no pacote. A imagem do ícone deve ter 32 x 32 pixels (ou será reduzida para que o tamanho) e é exibido na interface do usuário do listview. Se nenhum `Icon` elemento for especificado, a interface do usuário usa um padrão.  
  
-   `<PreviewImage>` -Esse elemento opcional é um caminho relativo para um arquivo de imagem (png, bmp, jpeg) contido no pacote. A imagem de visualização deve ser 200 x 200 pixels e exibido nos detalhes da interface do usuário. Se nenhum `PreviewImage` elemento for especificado, a interface do usuário usa um padrão.  
  
-   `<Tags>` -Esse elemento opcional lista marcas de texto delimitada por ponto e vírgula adicionais que são usadas para obter dicas de pesquisa. O `Tags` elemento é limitado a 100 caracteres.  
  
-   `<GettingStartedGuide>` -Esse elemento opcional é um caminho relativo para um arquivo HTML ou uma URL para um site que contém informações sobre como usar a extensão ou o conteúdo dentro desse pacote. Este guia é iniciado como parte de uma instalação.  
  
-   `<AnyElement>*` -O esquema de manifesto é flexível o suficiente para permitir que todos os outros elementos. Elementos filho que não são reconhecidos pelo carregador de manifesto são expostos como uma lista de objetos XmlElement. Usando esses elementos filho, extensões VSIX podem definir dados adicionais no arquivo de manifesto e enumerá-los em tempo de execução.  
  
### <a name="installation-element"></a>Elemento de instalação  
 Esta seção define a maneira que esse pacote pode ser instalado e se ele pode ser instalado em SKUs do aplicativo. Esta seção contém os seguintes atributos:  
  
-   `Experimental` -Defina esse atributo como true se você tem uma extensão que está atualmente instalada para todos os usuários, mas você está desenvolvendo uma versão atualizada no mesmo computador. Por exemplo, se você tiver instalado o MyExtension 1.0 para todos os usuários, mas você deseja depurar MyExtension 2.0 no mesmo computador, defina Experimental = "true". Esse atributo está disponível no Visual Studio 2015 atualização 1 e posterior.  
  
-   `Scope` -Este atributo pode ter o valor "Global" ou "ProductExtension":  
  
    -   "Global" Especifica que a instalação não é vinculada a um SKU específico. Por exemplo, esse valor é usado quando um SDK de extensão está instalado.  
  
    -   "ProductExtension" Especifica que uma extensão VSIX tradicional (versão 1.0) no escopo individuais SKUs do Visual Studio está instalada. Este é o valor padrão.  
  
-   `AllUsers` -Esse atributo opcional especifica se este pacote será instalado para todos os usuários. Por padrão, esse atributo é false, que especifica que o pacote não por usuário. (Quando você definir esse valor como true, o usuário de instalação deve elevar para o nível de privilégio administrativo para instalar o VSIX resultante.  
  
-   `InstalledByMsi` -Esse atributo opcional especifica se este pacote é instalado por um MSI. Pacotes instalados por um MSI são instalados e gerenciados pelo MSI (programas e recursos) e não pelo Gerenciador do Visual Studio extensão.  Por padrão, esse atributo é false, que especifica que o pacote não está instalado por um MSI.  
  
-   `SystemComponent` -Esse atributo opcional especifica se esse pacote deve ser considerado um componente do sistema. Componentes do sistema não mostram na UI do Gerenciador de extensões e não podem ser atualizadas. Por padrão, esse atributo é false, que especifica que o pacote não é um componente do sistema.  
  
-   `AnyAttribute*` -O `Installation` elemento aceita um conjunto em aberto de atributos que serão expostos em tempo de execução como um dicionário de par nome-valor.  
  
-   `<InstallationTarget>` -Esse elemento controla o local em que o instalador do VSIX instala o pacote. Se o valor da `Scope` atributo é "ProductExtension" o pacote deve ter como destino uma SKU, que tem instalado um arquivo de manifesto como parte de seu conteúdo para anunciar sua disponibilidade para extensões. O `<InstallationTarget>` elemento tem os seguintes atributos quando o `Scope` atributo tem explícito ou valor padrão "ProductExtension":  
  
    -   `Id` -Este atributo identifica o pacote.  O atributo segue a convenção de namespace: Company.Product.Feature.Name. O `Id` atributo pode conter apenas caracteres alfanuméricos e é limitado a 100 caracteres. Valores esperados:  
  
        -   Microsoft.VisualStudio.IntegratedShell  
  
        -   Microsoft.VisualStudio.Pro  
  
        -   Microsoft.VisualStudio.Premium  
  
        -   Microsoft.VisualStudio.Ultimate  
  
        -   Microsoft.VisualStudio.VWDExpress  
  
        -   Microsoft.VisualStudio.VPDExpress  
  
        -   Microsoft.VisualStudio.VSWinExpress  
  
        -   Microsoft.VisualStudio.VSLS  
  
        -   My.Shell.App  
  
    -   `Version` -Este atributo especifica um intervalo de versão com as versões com suporte mínimas e máxima deste SKU. Um pacote pode detalhar as versões dos SKUs que ele suporta. A notação de intervalo de versão é [11.0-10.0], onde  
  
        -   [-versão mínima inclusivo.  
  
        -   ]-versão máximo inclusivo.  
  
        -   (-versão mínima exclusivo.  
  
        -   ) – a versão máxima exclusivo.  
  
        -   Única versão # - somente a versão especificada.  
  
        > [!IMPORTANT]
        >  A versão 2.0 do VSIX esquema foi introduzido no Visual Studio 2012. Para usar este esquema você deve ter o Visual Studio 2012 ou posterior instalado no computador e usa o VSIXInstaller.exe que faz parte do produto. Você pode direcionar versões anteriores do Visual Studio com um Visual Studio 2012 ou posterior VSIXInstaller, mas somente usando as versões posteriores do instalador. 
        
        Números de versão do Visual Studio 2017 podem ser encontrados em [Visual Studio números de compilação e datas de lançamento](../install/visual-studio-build-numbers-and-release-dates.md).
        
        Ao expressar a versão para versões do Visual Studio 2017, a versão secundária deve ser sempre **0**. Por exemplo, o Visual Studio 2017 versão 15.3.26730.0 deve ser expresso como [15.0.26730.0,16.0). Isso só é necessária para números de versão do Visual Studio 2017.
  
    -   `AnyAttribute*` -O `<InstallationTarget>` elemento permite que um conjunto em aberto de atributos que é exposto em tempo de execução como um dicionário de par nome-valor.  
  
### <a name="dependencies-element"></a>Elemento de dependências  
 Esse elemento contém uma lista de dependências que declara este pacote. Se todas as dependências forem especificadas, esses pacotes (identificado por suas `Id`) deve ter sido instalado antes.  
  
-   `<Dependency>` elemento – esse elemento filho tem os seguintes atributos:  
  
    -   `Id` -Este atributo deve ser uma ID exclusiva para o pacote dependente. Esse valor de identidade deve corresponder a `<Metadata><Identity>Id` atributo de um pacote que este pacote é dependente. O `Id` atributo segue a convenção de namespace: Company.Product.Feature.Name. O atributo pode conter apenas caracteres alfanuméricos e é limitado a 100 caracteres.  
  
    -   `Version` -Este atributo especifica um intervalo de versão com as versões com suporte mínimas e máxima deste SKU. Um pacote pode detalhar as versões dos SKUs que ele suporta. A notação de intervalo de versão é [12.0, 13.0], onde:  
  
        -   [-versão mínima inclusivo.  
  
        -   ]-versão máximo inclusivo.  
  
        -   (-versão mínima exclusivo.  
  
        -   ) – a versão máxima exclusivo.  
  
        -   Única versão # - somente a versão especificada.  
  
    -   `DisplayName` -Esse atributo é o nome de exibição do pacote dependente, que é usado em elementos de interface do usuário, como caixas de diálogo e mensagens de erro. O atributo é opcional, a menos que o pacote dependente é instalado por MSI.  
  
    -   `Location` -Esse atributo opcional especifica o caminho relativo dentro neste VSIX para um pacote VSIX aninhado ou uma URL para o local de download para a dependência. Este atributo é usado para ajudar o usuário localize o pacote de pré-requisito.  
  
    -   `AnyAttribute*` -O `Dependency` elemento aceita um conjunto em aberto de atributos que serão expostos em tempo de execução como um dicionário de par nome-valor.  
  
### <a name="assets-element"></a>Elemento de ativos  
 Esse elemento contém uma lista de `<Asset>` marcas para cada elemento de extensão ou o conteúdo exposto por este pacote.  
  
- `<Asset>` -Esse elemento contém os seguintes atributos e elementos:  
  
  - `Type` -Tipo de extensão ou conteúdo representado por este elemento. Cada `<Asset>` elemento deve ter uma única `Type`, mas vários `<Asset>` elementos podem ter o mesmo `Type`. Esse atributo deve ser representado como um nome totalmente qualificado, de acordo com as convenções de namespace. Os tipos conhecidos são:  
  
    1. VSPackage  
  
    2. Mefcomponent  
  
    3. Microsoft.VisualStudio.ToolboxControl  
  
    4. Microsoft.VisualStudio.Samples  
  
    5. Microsoft.VisualStudio.ProjectTemplate  
  
    6. Microsoft.VisualStudio.ItemTemplate  
  
    7. Microsoft.VisualStudio.Assembly  
  
       Você pode criar seus próprios tipos e dar-lhes nomes exclusivos. Em tempo de execução dentro do Visual Studio, seu código pode enumerar e acessar esses tipos personalizados por meio da API do Gerenciador de extensões.  
  
  - `Path` -o caminho relativo para o arquivo ou pasta dentro do pacote que contém o ativo.  
    
  - `TargetVersion` -o intervalo de versão ao qual se aplica o determinado ativo. Usado para envio de várias versões de ativos para diferentes versões do Visual Studio. Requer o Visual Studio 2017.3 ou mais recente ter efeito.
  
  - `AnyAttribute*` -Um conjunto em aberto de atributos que é exposto em tempo de execução como um dicionário de par nome-valor.  
  
     `<AnyElement>*` -Qualquer conteúdo estruturado é permitido entre um `<Asset>` começa e termina a marca. Todos os elementos são expostos como uma lista de objetos XmlElement. Extensões VSIX podem definir metadados estruturados de tipo específico no arquivo de manifesto e enumerá-los em tempo de execução.  
  
### <a name="sample-manifest"></a>Exemplo de manifesto  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">  
  <Metadata>  
    <Identity Id="0000000-0000-0000-0000-000000000000" Version="1.0" Language="en-US" Publisher="Company" />  
    <DisplayName>Test Package</DisplayName>  
    <Description>Information about my package</Description>  
    <MoreInfo>http://www.fabrikam.com/Extension1/</MoreInfo>  
    <License>eula.rtf</License>  
    <ReleaseNotes>notes.txt</ReleaseNotes>  
    <Icon>Images\icon.png</Icon>  
    <PreviewImage>Images\preview.png</PreviewImage>  
  </Metadata>  
  <Installation InstalledByMsi="false" AllUsers="false" SystemComponent="false" Scope="ProductExtension">  
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="[11.0, 12.0]" />  
  </Installation>  
  <Dependencies>  
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="[4.5,)" />  
    <Dependency Id="Microsoft.VisualStudio.MPF.12.0" DisplayName="Visual Studio MPF 12.0" d:Source="Installed" Version="[12.0]" />  
  </Dependencies>  
  <Assets>  
    <Asset Type="Microsoft.VisualStudio.VsPackage" d:Source="Project" d:ProjectName="%CurrentProject%" Path="|%CurrentProject%;PkgdefProjectOutputGroup|" />  
  </Assets>  
</PackageManifest>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Envio de extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)

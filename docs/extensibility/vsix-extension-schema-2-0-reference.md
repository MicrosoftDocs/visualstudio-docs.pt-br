---
title: Referência do esquema de extensão do VSIX 2,0 | Microsoft Docs
description: O esquema de extensão do VSIX 2,0 define o formato de arquivo para um arquivo de manifesto de implantação do VSIX, que descreve o conteúdo de um pacote do VSIX.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d1b94c7b2cacb7ad78031721156bdd90cb666c4f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062285"
---
# <a name="vsix-extension-schema-20-reference"></a>Referência do esquema de extensão do VSIX 2,0
Um arquivo de manifesto de implantação do VSIX descreve o conteúdo de um pacote do VSIX. O formato de arquivo é regido por um esquema. A versão 2,0 deste esquema dá suporte à adição de tipos e atributos personalizados.  O esquema do manifesto é extensível. O carregador de manifesto ignora elementos e atributos XML que ele não entende.

> [!IMPORTANT]
> O Visual Studio 2015 pode carregar arquivos VSIX nos formatos Visual Studio 2010, Visual Studio 2012 ou Visual Studio 2013.

## <a name="package-manifest-schema"></a>Esquema de manifesto de pacote
 O elemento raiz do arquivo XML do manifesto é `<PackageManifest>` . Ele tem um único atributo `Version` , que é a versão do formato de manifesto. Se forem feitas alterações importantes no formato, o formato da versão será alterado. Este artigo descreve o formato de manifesto versão 2,0, que é especificado no manifesto, definindo o `Version` atributo como o valor de Version = "2.0".

### <a name="packagemanifest-element"></a>Elemento PackageManifest
 Dentro do `<PackageManifest>` elemento raiz, você pode usar os seguintes elementos:

- `<Metadata>` -Metadados e informações de anúncio sobre o próprio pacote. Somente um `Metadata` elemento é permitido no manifesto.

- `<Installation>` -Esta seção define a maneira como esse pacote de extensão pode ser instalado, incluindo as SKUs de aplicativo que ele pode instalar no. Apenas um único `Installation` elemento é permitido no manifesto. Um manifesto deve ter um `Installation` elemento ou este pacote não será instalado em nenhum SKU.

- `<Dependencies>` -Uma lista opcional de dependências para este pacote está definida aqui.

- `<Assets>` -Esta seção contém todos os ativos contidos neste pacote. Sem esta seção, este pacote não caponha nenhum conteúdo.

- `<AnyElement>*` -O esquema de manifesto é flexível o suficiente para permitir qualquer outro elemento. Quaisquer elementos filho não reconhecidos pelo carregador de manifesto são expostos na API do Gerenciador de extensões como objetos XmlElement adicionais. Usando esses elementos filho, as extensões do VSIX podem definir dados adicionais no arquivo de manifesto que o código em execução no Visual Studio pode acessar em tempo de execução. Consulte [Microsoft. VisualStudio. ExtensionManager. IExtension. AdditionalElements](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120)).

### <a name="metadata-element"></a>Elemento Metadata
 Esta seção são os metadados sobre o pacote, sua identidade e informações de anúncio. `<Metadata>` contém os seguintes elementos:

- `<Identity>` -Define as informações de identificação para este pacote e inclui os seguintes atributos:

  - `Id` -Esse atributo deve ser uma ID exclusiva para o pacote escolhido por seu autor. O nome deve ser qualificado da mesma forma que os tipos CLR são namespace: Company.Product.Feature.Name. O `Id` atributo é limitado a 100 caracteres.

  - `Version` -Define a versão deste pacote e seu conteúdo. Esse atributo segue o formato de controle de versão do assembly CLR: Major. Minor. Build. Revision (1.2.40308.00). Um pacote com um número de versão superior é considerado atualizações no pacote e pode ser instalado sobre a versão instalada existente.

  - `Language` -Esse atributo é o idioma padrão para o pacote e corresponde aos dados textuais neste manifesto. Esse atributo segue a Convenção de código de localidade CLR para assemblies de recursos, por exemplo: en-US, en, fr-fr. Você pode especificar `neutral` para declarar uma extensão com neutralidade de idioma que será executada em qualquer versão do Visual Studio. O valor padrão é `neutral`.

  - `Publisher` -Este atributo identifica o editor deste pacote, seja uma empresa ou um nome individual. O `Publisher` atributo é limitado a 100 caracteres.

- `<DisplayName>` -Esse elemento Especifica o nome do pacote amigável que é exibido na interface do usuário do Gerenciador de extensões. O `DisplayName` conteúdo é limitado a 50 caracteres.

- `<Description>` -Esse elemento opcional é uma breve descrição do pacote e seu conteúdo exibido na interface do usuário do Gerenciador de extensões. O `Description` conteúdo pode conter qualquer texto desejado, mas é limitado a 1000 caracteres.

- `<MoreInfo>` -Este elemento opcional é uma URL para uma página online que contém uma descrição completa deste pacote. O protocolo deve ser especificado como http.

- `<License>` -Esse elemento opcional é um caminho relativo para um arquivo de licença (. txt,. rtf) contido no pacote.

- `<ReleaseNotes>` -Esse elemento opcional é um caminho relativo para um arquivo de notas de versão contido no pacote (. txt,. rtf) ou outra URL para um site que exibe as notas de versão.

- `<Icon>` -Esse elemento opcional é um caminho relativo para um arquivo de imagem (png, BMP, JPEG, ico) contido no pacote. A imagem do ícone deve ter 32x32 pixels (ou será reduzida a esse tamanho) e aparece na interface do usuário do ListView. Se nenhum `Icon` elemento for especificado, a interface do usuário usará um padrão.

- `<PreviewImage>` -Esse elemento opcional é um caminho relativo para um arquivo de imagem (png, BMP, JPEG) contido no pacote. A imagem de visualização deve ser 200 x 200 pixels e exibida na interface do usuário de detalhes. Se nenhum `PreviewImage` elemento for especificado, a interface do usuário usará um padrão.

- `<Tags>` -Este elemento opcional lista marcas de texto delimitadas por ponto e vírgula adicionais que são usadas para dicas de pesquisa. O `Tags` elemento é limitado a 100 caracteres.

- `<GettingStartedGuide>` -Esse elemento opcional é um caminho relativo para um arquivo HTML ou uma URL para um site que contém informações sobre como usar a extensão ou o conteúdo dentro deste pacote. Este guia é iniciado como parte de uma instalação do.

- `<AnyElement>*` -O esquema de manifesto é flexível o suficiente para permitir qualquer outro elemento. Todos os elementos filho que não são reconhecidos pelo carregador de manifesto são expostos como uma lista de objetos XmlElement. Usando esses elementos filho, as extensões do VSIX podem definir dados adicionais no arquivo de manifesto e enumerá-los em tempo de execução.

### <a name="installation-element"></a>Elemento de instalação
 Esta seção define a maneira como esse pacote pode ser instalado e as SKUs de aplicativo que ele pode instalar no. Esta seção contém os seguintes atributos:

- `Experimental` -Defina esse atributo como true se você tiver uma extensão instalada atualmente para todos os usuários, mas estiver desenvolvendo uma versão atualizada no mesmo computador. Por exemplo, se você tiver instalado MyExtension 1,0 para todos os usuários, mas quiser depurar MyExtension 2,0 no mesmo computador, defina experimental = "true". Esse atributo está disponível no Visual Studio 2015 atualização 1 e posterior.

- `Scope` -Este atributo pode usar o valor "global" ou "ProductExtension":

  - "Global" especifica que a instalação não está no escopo de um SKU específico. Por exemplo, esse valor é usado quando um SDK de extensão é instalado.

  - "ProductExtension" especifica que uma extensão de VSIX tradicional (versão 1,0) com escopo para SKUs individuais do Visual Studio está instalada. Esse é o valor padrão.

- `AllUsers` -Este atributo opcional especifica se este pacote será instalado para todos os usuários. Por padrão, esse atributo é false, que especifica que o pacote é por usuário. (Quando você define esse valor como true, o usuário de instalação deve elevar o nível de privilégio administrativo para instalar o VSIX resultante.

- `InstalledByMsi` -Este atributo opcional especifica se este pacote é instalado por um MSI. Os pacotes instalados por um MSI são instalados e gerenciados pelo MSI (programas e recursos) e não pelo Gerenciador de extensões do Visual Studio.  Por padrão, esse atributo é false, que especifica que o pacote não é instalado por um MSI.

- `SystemComponent` -Este atributo opcional especifica se este pacote deve ser considerado um componente do sistema. Os componentes do sistema não são mostrados na interface do usuário do Gerenciador de extensões e não podem ser atualizados. Por padrão, esse atributo é false, que especifica que o pacote não é um componente do sistema.

- `AnyAttribute*` -O `Installation` elemento aceita um conjunto de atributos encerrado que será exposto em tempo de execução como um dicionário de pares nome-valor.

- `<InstallationTarget>` -Esse elemento controla o local em que o instalador do VSIX instala o pacote. Se o valor do `Scope` atributo for "ProductExtension", o pacote deverá ter como destino uma SKU, que instalou um arquivo de manifesto como parte de seu conteúdo para anunciar sua disponibilidade às extensões. O `<InstallationTarget>` elemento tem os seguintes atributos quando o `Scope` atributo tem o valor explícito ou padrão "ProductExtension":

  - `Id` -Este atributo identifica o pacote.  O atributo segue a Convenção de namespace: Company.Product.Feature.Name. O `Id` atributo pode conter apenas caracteres alfanuméricos e é limitado a 100 caracteres. Valores esperados:

    - Microsoft. VisualStudio. IntegratedShell

    - Microsoft.VisualStudio.Pro

    - Microsoft. VisualStudio. Premium

    - Microsoft. VisualStudio. Ultimate

    - Microsoft. VisualStudio. VWDExpress

    - Microsoft. VisualStudio. VPDExpress

    - Microsoft. VisualStudio. VSWinExpress

    - Microsoft. VisualStudio. VSLS

    - My.Shell.App

  - `Version` -Este atributo especifica um intervalo de versão com as versões mínima e máxima com suporte deste SKU. Um pacote pode detalhar as versões dos SKUs aos quais ele dá suporte. A notação do intervalo de versões é [10,0-11,0], em que

    - [-versão mínima inclusiva.

    - ] – versão máxima inclusiva.

    - (-versão mínima exclusiva.

    - )-versão máxima exclusiva.

    - Única versão #-somente a versão especificada.

    > [!IMPORTANT]
    > A versão 2,0 do esquema VSIX foi introduzida no Visual Studio 2012. Para usar este esquema, você deve ter o Visual Studio 2012 ou posterior instalado no computador e usar o VSIXInstaller.exe que faz parte desse produto. Você pode direcionar versões anteriores do Visual Studio com um Visual Studio 2012 ou VSIXInstaller posterior, mas apenas usando as versões posteriores do instalador.

    Os números de versão do Visual Studio 2017 podem ser encontrados em [números de compilação do Visual Studio e datas de lançamento](../install/visual-studio-build-numbers-and-release-dates.md).

    Ao expressar a versão para versões do Visual Studio 2017, a versão secundária deve ser sempre **0**. Por exemplo, o Visual Studio 2017 versão 15.3.26730.0 deve ser expresso como [15.0.26730.0, 16.0). Isso só é necessário para o Visual Studio 2017 e números de versão posteriores.

  - `AnyAttribute*` -O `<InstallationTarget>` elemento permite um conjunto de atributos encerrado que é exposto em tempo de execução como um dicionário de pares nome-valor.

### <a name="dependencies-element"></a>Elemento Dependencies
 Esse elemento contém uma lista de dependências que esse pacote declara. Se qualquer dependência for especificada, esses pacotes (identificados por seu `Id` ) deverão ter sido instalados antes.

- `<Dependency>` elemento-esse elemento filho tem os seguintes atributos:

  - `Id` -Esse atributo deve ser uma ID exclusiva para o pacote dependente. Esse valor de identidade deve corresponder ao `<Metadata><Identity>Id` atributo de um pacote no qual este pacote é dependente. O `Id` atributo segue a Convenção de namespace: Company.Product.Feature.Name. O atributo pode conter apenas caracteres alfanuméricos e é limitado a 100 caracteres.

  - `Version` -Este atributo especifica um intervalo de versão com as versões mínima e máxima com suporte deste SKU. Um pacote pode detalhar as versões dos SKUs aos quais ele dá suporte. A notação do intervalo de versão é [12,0, 13,0], em que:

    - [-versão mínima inclusiva.

    - ] – versão máxima inclusiva.

    - (-versão mínima exclusiva.

    - )-versão máxima exclusiva.

    - Única versão #-somente a versão especificada.

  - `DisplayName` -Esse atributo é o nome de exibição do pacote dependente, que é usado em elementos de interface do usuário, como caixas de diálogo e mensagens de erro. O atributo é opcional, a menos que o pacote dependente seja instalado pelo MSI.

  - `Location` -Esse atributo opcional especifica o caminho relativo dentro desse VSIX para um pacote VSIX aninhado ou uma URL para o local de download da dependência. Esse atributo é usado para ajudar o usuário a localizar o pacote de pré-requisito.

  - `AnyAttribute*` -O `Dependency` elemento aceita um conjunto de atributos encerrado que será exposto em tempo de execução como um dicionário de pares nome-valor.

### <a name="assets-element"></a>Elemento de ativos
 Esse elemento contém uma lista de `<Asset>` marcas para cada elemento de extensão ou de conteúdo na superfície deste pacote.

- `<Asset>` -Este elemento contém os seguintes atributos e elementos:

  - `Type` -Tipo de extensão ou conteúdo representado por este elemento. Cada `<Asset>` elemento deve ter um único `Type` , mas vários `<Asset>` elementos podem ter o mesmo `Type` . Esse atributo deve ser representado como um nome totalmente qualificado, de acordo com as convenções de namespace. Os tipos conhecidos são:

    1. Microsoft. VisualStudio. VsPackage

    2. Microsoft. VisualStudio. MefComponent

    3. Microsoft. VisualStudio. ToolboxControl

    4. Microsoft. VisualStudio. Samples

    5. Microsoft. VisualStudio. ProjectTemplate

    6. Microsoft. VisualStudio. ItemTemplate

    7. Microsoft. VisualStudio. assembly

       Você pode criar seus próprios tipos e dar a eles nomes exclusivos. Em tempo de execução dentro do Visual Studio, seu código pode enumerar e acessar esses tipos personalizados por meio da API do Gerenciador de extensões.

  - `Path` -o caminho relativo para o arquivo ou a pasta dentro do pacote que contém o ativo.

  - `TargetVersion` -o intervalo de versão ao qual o ativo fornecido se aplica. Usado para enviar várias versões de ativos para versões diferentes do Visual Studio. Requer que o Visual Studio 2017,3 ou mais recente tenha efeito.

  - `AnyAttribute*` -Um conjunto de atributos encerrado que é exposto em tempo de execução como um dicionário de pares nome-valor.

    `<AnyElement>*` -Qualquer conteúdo estruturado é permitido entre uma `<Asset>` marca de início e de fim. Todos os elementos são expostos como uma lista de objetos XmlElement. As extensões do VSIX podem definir metadados específicos de tipo estruturados no arquivo de manifesto e enumerá-los em tempo de execução.

### <a name="sample-manifest"></a>Exemplo de manifesto

```xml
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

## <a name="see-also"></a>Confira também

- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)

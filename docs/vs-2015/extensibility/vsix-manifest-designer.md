---
title: Designer de manifesto do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.Sdk.VsixManifestEditor
helpviewer_keywords:
- vsixmanifest
- vsix manifest
- manifest designer
ms.assetid: 5a691e77-cf91-430d-90ea-361d9031ef83
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 72639c3fbef6b8e297d9e81a7383b2ee8220d896
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796435"
---
# <a name="vsix-manifest-designer"></a>Designer de manifesto do VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Modifica um pacote manifesto arquivo VSIX, que define o comportamento de instalação para uma extensão do Visual Studio.  
  
 O **Designer de manifesto do VSIX** mapeia para o esquema subjacente do VSIX. Cada elemento no esquema pode ser definido usando um controle correspondente no designer. Para obter mais informações sobre o esquema, consulte [2.0 referência do esquema de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md).  
  
 Para abrir o **Designer de manifesto do VSIX**, localize um arquivo vsixmanifest no **Gerenciador de soluções**e abra o arquivo. Se o arquivo não contém XML válido, o designer de manifesto não será aberto.  
  
> [!NOTE]
>  Vsixmanifest é a saída para vsixmanifest quando o pacote é compilado.  
  
## <a name="uielement-list"></a>Lista UIElement  
 O **Designer de manifesto do VSIX** contém quatro seções que correspondem a esses elementos de nível superior do esquema:  
  
- Metadados  
  
- Destinos de instalação  
  
- Ativos  
  
- Dependências  
  
  A área de título contém os seguintes controles.  
  
  **Nome do produto**  
  Descreve o nome da extensão.  
  
  **ID do produto**  
  Especifica as informações de identificação exclusivo para este pacote.  
  
  **Autor**  
  Especifica o nome do autor da extensão.  
  
  **Versão**  
  Especifica o número de versão da extensão.  
  
  O **metadados** guia contém os seguintes controles.  
  
  **Descrição**  
  Fornece uma descrição de texto da extensão, a ser exibido no **Extension Manager**.  
  
  **Linguagem**  
  Especifica o idioma padrão para o pacote, que corresponde aos dados textuais no manifesto. O `Language` atributo segue a convenção de código localidade common language runtime (CLR) para assemblies de recursos, por exemplo, en-us, en, fr-fr. Por padrão, o valor é neutro; Isso significa que o pacote será executado em qualquer versão de idioma do Visual Studio.  
  
  **licença**  
  Especifica o arquivo de texto que contém a licença de usuário, caso haja algum.  
  
  **Ícone**  
  Especifica o arquivo de gráfico (. png,. bmp,. JPEG,. ico) que contém o ícone a ser exibido no **Extension Manager**, se houver um ícone. A imagem de ícone deve ter 32 x 32 pixels ou será redimensionada para essas dimensões. Se nenhum ícone for especificado, **Extension Manager** usa um ícone padrão.  
  
  **Imagem de visualização**  
  Especifica o arquivo de gráficos (. png,. bmp,. JPEG,. ico) que contém a imagem de visualização a ser exibido no **Extension Manager**, se houver uma imagem de visualização. A imagem de visualização deve ser 200 x 200 pixels. Se nenhuma imagem de visualização for especificada, **Extension Manager** usa uma imagem padrão.  
  
  **Marcas**  
  Adiciona as marcas de texto a ser usado para dicas de pesquisa.  
  
  **Notas de Versão**  
  Especifica um arquivo (. txt,. rtf) que contém as notas de versão. Também usa a URL de um site da Web que exibe as notas de versão.  
  
  **Guia de Introdução**  
  Especifica um arquivo (. txt,. rtf) que contém informações sobre como usar a extensão ou o conteúdo no pacote VSIX. Este guia é exibida quando a instalação da extensão estiver concluída. Também usa a URL de um site da Web que exibe o guia.  
  
  **URL de informações adicionais**  
  Especifica a URL de um site que contém informações adicionais sobre o produto.  
  
  O **instalar destinos** guia contém os seguintes controles.  
  
  **Tipo de instalação**  
  Lista **extensão do Visual Studio** e **SDK de extensão** como tipos de instalação de destino. As opções diferem, dependendo do tipo que você escolher.  
  
  **Extensão do Visual Studio**  
  Lista os **InstallationTarget** elementos que descrevem como o pacote pode ser instalado e em quais produtos do Visual Studio esta extensão pode ser instalada. Cada produto é identificado separadamente por nome e uma versão ou intervalo.  Produtos podem ser adicionados à lista, modificados e excluídos. O nome e a versão de um produto correspondem à **identificação** e **versão** atributos do associado **InstallationTarget** elemento.  
  
  **Intervalo de versão** é [12.0, 14.0] e usa a notação a seguir:  
  
- [– versão mínima inclusivo  
  
- ] – versão máximo inclusivo  
  
- (-versão mínima exclusivo  
  
- ) – a versão máxima exclusivo  
  
- Única versão # - somente a versão especificada  
  
  **SDK de extensão**  
  Especifica uma instalação global que não está no escopo para um produto específico e uma versão. **Identificador de plataforma de destino** é a plataforma, como "Windows", que você está definido. **Versão da plataforma de destino** é a versão, como versão 8.0, sua plataforma de destino. **Nome do SDK** e **SDK versão** é o nome e o número de versão do SDK, respectivamente.  
  
  **Este VSIX está instalado para todos os usuários (exige a elevação de instalação)** caixa de seleção  
  Se essa caixa de seleção for selecionada, esta extensão está instalada para todos os usuários; Caso contrário, ele é instalado apenas para o usuário atual.  
  
  **Este VSIX é instalado pelo instalador do Windows** caixa de seleção  
  Se essa caixa de seleção for selecionada, esta extensão é instalada pelo instalador do Windows (arquivo. msi); Caso contrário, ele é instalado como um pacote VSIX típico (arquivo. VSIX).  
  
  O **ativos** guia contém os seguintes controles.  
  
  **Lista de ativos**  
  Lista os elementos de ativo que descrevem os elementos de extensão ou conteúdo que esse pacote superfícies. Cada extensão ou um elemento de conteúdo é listado separadamente por origem, o tipo e o caminho. Elementos de conteúdo e as extensões podem ser adicionados à lista de, modificados e excluídos. O tipo e o caminho de um elemento de conteúdo ou extensão corresponde do `Type` e `Path` atributos do associado `Asset` elemento. Os seguintes tipos são conhecidos:  
  
- Microsoft.VisualStudio.Package  
  
- Mefcomponent  
  
- Microsoft.VisualStudio.ToolboxControl  
  
- Microsoft.VisualStudio.Samples  
  
- Microsoft.VisualStudio.ProjectTemplate  
  
- Microsoft.VisualStudio.ItemTemplate  
  
- Microsoft.VisualStudio.Assembly  
  
- Microsoft.ExtensionSDK  
  
  Para adicionar ou editar um ativo, você deve especificar o tipo de ativo, se o ativo é um projeto na solução atual ou um arquivo no sistema de arquivos e o nome do projeto. Você também pode especificar o nome da pasta na qual a ser inserido.  
  
  Você também pode criar seus próprios tipos e dar-lhes nomes exclusivos.  
  
  O **dependências** guia contém os seguintes controles.  
  
  **Nome, origem e o intervalo de versão**  
  Lista os elementos de dependência desse pacote, que são outros pacotes que este pacote depende. Se um pacote de dependência for especificado, ele deve ser instalado antes que este pacote seja instalado; Caso contrário, esse pacote deve instalá-lo.  
  
  Os pacotes de dependência são especificados pelo identificador de nome, intervalo de versão, fonte e como a dependência deve ser resolvido. Cada pacote de dependência é listada separadamente por nome, versão e código-fonte. Pacotes de dependência podem ser adicionados à lista, modificados e excluídos.  
  
  O identificador deve corresponder a `ID` atributo dos metadados do pacote de dependência. A origem pode ser um projeto na solução atual, uma extensão instalada no momento ou um arquivo. O **como é a dependência foi resolvida** configuração pode ser o caminho relativo de um pacote aninhado ou a URL do local de download para a dependência. A ID, a versão e a resolução do pacote de dependência correspondem do `Id`, `Version`, e `Location` atributos do associado `Dependency` elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema 2.0 de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md)   
 [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)


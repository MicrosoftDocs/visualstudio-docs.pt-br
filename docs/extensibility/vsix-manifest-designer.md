---
title: Designer de manifesto do VSIX | Microsoft Docs
description: Saiba como o designer de manifesto do VSIX modifica um arquivo de manifesto do pacote VSIX, que define o comportamento da instalação para uma extensão do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.Sdk.VsixManifestEditor
helpviewer_keywords:
- vsixmanifest
- vsix manifest
- manifest designer
ms.assetid: 5a691e77-cf91-430d-90ea-361d9031ef83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: baea7be60c67f186da2372c4644366b4a1a7a202
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905183"
---
# <a name="vsix-manifest-designer"></a>Designer de manifesto do VSIX
Modifica um arquivo de manifesto do pacote VSIX, que define o comportamento da instalação para uma extensão do Visual Studio.

 O **Designer de manifesto do VSIX** é mapeado para o esquema VSIX subjacente. Cada elemento no esquema pode ser definido usando um controle correspondente no designer. Para obter mais informações sobre o esquema, consulte [referência do esquema de extensão do VSIX 2,0](../extensibility/vsix-extension-schema-2-0-reference.md).

 Para abrir o **Designer de manifesto VSIX**, localize um arquivo *Source. Extension. vsixmanifest* em **Gerenciador de soluções** e abra o arquivo. Se o arquivo não contiver um XML válido, o designer de manifesto não será aberto.

> [!NOTE]
> O arquivo *Source. Extension. vsixmanifest* é saída para *extension. vsixmanifest* quando o pacote é compilado.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário
 O **Designer de manifesto do VSIX** contém quatro seções que correspondem a esses elementos de nível superior do esquema:

- Metadados

- Instalar destinos

- Ativos

- Dependências

  A área de título contém os seguintes controles.

  **Nome do produto** Descreve o nome da extensão.

  **ID do produto** Especifica as informações de identificação exclusivas para este pacote.

  **Criar** Especifica o nome do autor da extensão.

  **Versão** do Especifica o número de versão da extensão.

  A guia **metadados** contém os seguintes controles.

  **Descrição** do Fornece uma descrição de texto da extensão a ser exibida no **Gerenciador de extensões**.

  **Idioma** do Especifica o idioma padrão para o pacote, que corresponde aos dados textuais no manifesto. O `Language` atributo segue a Convenção de código de localidade Common Language Runtime (CLR) para assemblies de recursos, por exemplo, en-US, en, fr-fr. Por padrão, o valor é neutro, o que significa que o pacote será executado em qualquer versão de idioma do Visual Studio.

  **Licença** do Especifica o arquivo de texto que contém a licença de usuário, se houver uma.

  **Ícone** do Especifica o arquivo de gráficos (*.png*, *.bmp*, *. jpeg*, *. ico*) que contém o ícone a ser exibido no **Gerenciador de extensões**, se um ícone estiver presente. A imagem do ícone deve ter 32x32 pixels ou redimensionada para essas dimensões. Se nenhum ícone for especificado, o **Gerenciador de extensões** usará um ícone padrão.

  **Imagem de visualização** Especifica o arquivo de gráficos (*.png*, *.bmp*, *. jpeg*, *. ico*) que contém a imagem de visualização a ser exibida no **Gerenciador de extensões**, se uma imagem de visualização estiver presente. A imagem de visualização deve ser 200 x 200 pixels. Se nenhuma imagem de visualização for especificada, o **Gerenciador de extensões** usará uma imagem padrão.

  **Marcas** Adiciona marcas de texto a serem usadas para dicas de pesquisa.

  **Notas de versão** Especifica um arquivo (*.txt*, *. rtf*) que contém notas de versão. Também usa a URL de um site que exibe as notas de versão.

  **Guia de introdução** Especifica um arquivo (*.txt*, *. rtf*) que contém informações sobre como usar a extensão ou o conteúdo no pacote VSIX. Este guia é exibido quando a instalação da extensão é concluída. Também usa a URL de um site que exibe o guia.

  **URL de mais informações** Especifica a URL de um site que contém informações adicionais sobre o produto.

  A guia **instalar destinos** contém os seguintes controles.

  **Tipo de instalação** Lista o **SDK** de extensão e extensão do **Visual Studio** como tipos de instalação de destino. As opções são diferentes, dependendo do tipo que você escolher.

  **Extensão do Visual Studio** Lista os elementos **InstallationTarget** que descrevem como o pacote pode ser instalado e em quais produtos do Visual Studio essa extensão pode ser instalada. Cada produto é identificado separadamente pelo nome e uma versão ou intervalo de versão. Os produtos podem ser adicionados à lista, modificados e excluídos. O nome e a versão de um produto correspondem aos atributos **ID** e **version** do elemento **InstallationTarget** associado.

  O **intervalo de versão** é [12,0, 14,0] e usa a seguinte notação:

- [-versão mínima inclusiva

- ] – versão máxima inclusiva

- (-versão mínima exclusiva

- )-versão máxima exclusiva

- Única versão #-somente a versão especificada

  **SDK de extensão** Especifica uma instalação global que não tem como escopo um produto e uma versão específicos. O **identificador de plataforma de destino** é a plataforma, como "Windows", à qual você está se concentrando. A **versão da plataforma de destino** é a versão, como 8,0, da sua plataforma de destino. O **nome do SDK** e a versão do **SDK** são o nome e o número da versão do SDK, respectivamente.

  **Este VSIX está instalado para todos os usuários (requer elevação na instalação)** Se você marcar essa caixa de seleção, a extensão será instalada para todos os usuários; caso contrário, ele será instalado somente para o usuário atual.

  **Esse VSIX é instalado pelo Windows Installer** Se você marcar essa caixa de seleção, a extensão será instalada pelo Windows Installer (arquivo *.msi* ); caso contrário, ele é instalado como um pacote VSIX típico (arquivo *. vsix* ).

  A guia **ativos** contém os seguintes controles.

  **Lista de ativos** Lista os elementos de ativo que descrevem os elementos de extensão ou conteúdo que este pacote superfícies. Cada elemento de extensão ou de conteúdo é listado separadamente por origem, tipo e caminho. Extensões e elementos de conteúdo podem ser adicionados à lista, modificados e excluídos. O tipo e o caminho de uma extensão ou elemento de conteúdo correspondem `Type` aos `Path` atributos e do `Asset` elemento associado. Os seguintes tipos são conhecidos:

- Microsoft. VisualStudio. Package

- Microsoft. VisualStudio. MefComponent

- Microsoft. VisualStudio. ToolboxControl

- Microsoft. VisualStudio. Samples

- Microsoft. VisualStudio. ProjectTemplate

- Microsoft. VisualStudio. ItemTemplate

- Microsoft. VisualStudio. assembly

- Microsoft. ExtensionSDK

  Para adicionar ou editar um ativo, você deve especificar o tipo de ativo, se o ativo é um projeto na solução atual ou um arquivo no sistema de arquivos e o nome do projeto. Você também pode especificar o nome da pasta na qual será inserida.

  Você também pode criar seus próprios tipos e dar a eles nomes exclusivos.

  A guia **dependências** contém os seguintes controles.

  **Nome, origem e intervalo de versão** Lista os elementos de dependência deste pacote, que são outros pacotes dos quais este pacote depende. Se um pacote de dependência for especificado, ele deverá ser instalado antes que este pacote seja instalado; caso contrário, esse pacote deve instalá-lo.

  Os pacotes de dependência são especificados por identificador, nome, intervalo de versão, origem e como a dependência deve ser resolvida. Cada pacote de dependência é listado separadamente por nome, versão e origem. Os pacotes de dependência podem ser adicionados à lista, modificados e excluídos.

  O identificador deve corresponder ao `ID` atributo dos metadados do pacote de dependência. A origem pode ser um projeto na solução atual, uma extensão atualmente instalada ou um arquivo. A configuração **como a dependência é resolvida** pode ser o caminho relativo de um pacote aninhado ou a URL do local de download para a dependência. A ID, a versão e a resolução do pacote de dependência correspondem aos `Id` `Version` atributos, e `Location` do `Dependency` elemento associado.

## <a name="see-also"></a>Confira também
- [Referência do esquema de extensão do VSIX 2,0](../extensibility/vsix-extension-schema-2-0-reference.md)
- [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)

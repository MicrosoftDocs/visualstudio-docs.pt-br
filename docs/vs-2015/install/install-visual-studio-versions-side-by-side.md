---
title: Instalar o Visual Studio versões lado a lado | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
ms.assetid: 4d00f240-4910-4699-aaf3-cda6461f0c29
caps.latest.revision: 48
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: be7559fb9bc6a2e028638ae18209a91cde955e7f
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056633"
---
# <a name="install-visual-studio-versions-side-by-side"></a>Instalar versões do Visual Studio lado a lado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível instalar esta versão do Visual Studio em um computador que já tenha uma versão anterior instalada. Se você encontrar uma falha de instalação, use a [ferramenta de coleta de log](http://go.microsoft.com/fwlink/?LinkId=262077) para coletar informações sobre as falhas para que você mesmo possa depurar os problemas.

> [!NOTE]
> Recomendamos que você instale as versões dos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] na ordem em que elas foram lançadas. Por exemplo, instale o Visual Studio 2013 antes de instalar o Visual Studio 2015.

 Antes de instalar as versões lado a lado, revise as seguintes circunstâncias:

-   Se você usar o Visual Studio 2015 para abrir uma solução que foi criada no [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)], mais tarde, você pode abrir e modificar a solução novamente na versão mais antiga, desde que você não tenha implementado quaisquer recursos que são específicos ao Visual Studio 2015.

-   Se você tentar usar o Visual Studio 2015 para abrir uma solução que foi criada no [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] ou uma versão anterior, você talvez precise modificar seus projetos e arquivos para serem compatíveis com o Visual Studio 2015. Para obter mais informações, consulte o [portar, migrar e atualizar projetos do Visual Studio](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2015) página.

-   Se você desinstalar uma versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] em um computador que tem mais de uma versão instalada, as associações de arquivo do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] são removidas para todas as versões. É possível remapear essas associações de arquivos usando o botão **Restaurar Associações de Arquivos** na página **Ambiente**, **Geral** da caixa de diálogo [Opções](../ide/reference/general-environment-options-dialog-box.md).

-   O Visual Studio não atualiza automaticamente extensões porque nem todas as extensões são compatíveis. Você deverá reinstalar as extensões do [Visual Studio Marketplace](http://go.microsoft.com/fwlink/?LinkId=178891) ou fornecedor de software.

## <a name="net-framework-versions-and-side-by-side-installations"></a>Versões do .NET Framework e instalações lado a lado

-   Os projetos Visual Basic, Visual C# e Visual F# usam a opção **Estrutura de Destino** no **Designer de Projeto** para especificar qual versão do .NET Framework um projeto usa. Para um projeto do C++, é possível alterar manualmente a estrutura de destino alterando o arquivo .vcxproj. Para obter mais informações, consulte [compatibilidade de versão](http://msdn.microsoft.com/library/2f25e522-456a-48c3-8a53-e5f39275649f).

     Ao criar um projeto, você pode especificar a qual versão do .NET Framework o projeto é direcionado na lista **.NET Framework** na caixa de diálogo **Novo Projeto**.

     Para informações específicas do idioma, consulte o tópico apropriado na tabela a seguir.

    |Idioma|Tópico|
    |--------------|-----------|
    |[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]|[Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)|
    |Visual C#|[Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md)|
    |Visual F#|[Configurando Projetos](http://msdn.microsoft.com/library/a1489abb-6294-4f8f-b71f-2cb126393526)|
    |C++|[Como: Modificar a estrutura de destino e o conjunto de ferramentas de plataforma](http://msdn.microsoft.com/library/031b1d54-e6e1-4da7-9868-3e75a87d9ffe)|
    |[!INCLUDE[jsprjscript](../includes/jsprjscript-md.md)]|[Executar um aplicativo JScript em uma versão anterior do Common Language Runtime](http://msdn.microsoft.com/en-us/bbea51b5-ac03-4e6c-b9a6-f487ef63eda5)|

## <a name="see-also"></a>Consulte também

- [Instalar o Visual Studio](../install/install-visual-studio-2015.md)
- [Portar, migrar e atualizar projetos do Visual Studio](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects?view=vs-2015)
- [Compilando aplicativos isolados do C/C++ e assemblies lado a lado](http://msdn.microsoft.com/library/9465904e-76f7-48bd-bb3f-c55d8f1699b6)
- [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)
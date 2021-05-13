---
title: Criar suplementos do VSTO para o Office usando o Visual Studio
description: Saiba como você pode usar as ferramentas Microsoft Office desenvolvedor no Visual Studio para criar .NET Framework aplicativos que estendem o Office.
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 04/28/2021
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 990caeec642a745bec5b6e0f2d29ff5d6213d095
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848312"
---
# <a name="create-vsto-add-ins-for-office-by-using-visual-studio"></a>Criar suplementos do VSTO para o Office usando o Visual Studio
> [!IMPORTANT]
> O VSTO depende do [.NET Framework](https://docs.microsoft.com/dotnet/framework/get-started/overview). Os complementos COM também podem ser escritos com o .NET Framework. Os complementos do Office não podem ser criados com o .NET Core e [o .NET 5+](https://docs.microsoft.com/dotnet/core/dotnet-five), as versões mais recentes do .NET. Isso porque o .NET Core/.NET 5+ não pode trabalhar junto com .NET Framework no mesmo processo e pode levar a falhas de carga de complemento. Você pode continuar a usar .NET Framework para gravar os complementos VSTO e COM para o Office. A Microsoft não atualizará o VSTO ou a plataforma de complemento COM para usar o .NET Core ou o .NET 5+. Você pode aproveitar o .NET Core e o .NET 5+, incluindo ASP.NET Core, para criar o lado do servidor dos [complementos da Web do Office.](https://docs.microsoft.com/office/dev/add-ins/overview/office-add-ins)

  Você pode usar as Microsoft Office de desenvolvedor no Visual Studio para criar .NET Framework aplicativos que estendem o Office. Esses aplicativos também são nomeados *soluções do Office.*

 As ferramentas do desenvolvedor do Office fornecem recursos que ajudam a criar soluções do Office para atender a uma variedade de necessidades comerciais. As ferramentas incluem modelos de projeto para ajudá-lo a criar soluções do Office usando Visual Basic ou Visual C#, além de designers visuais que ajudam a criam interfaces de usuário personalizada para as soluções do Office.

[!include[Add-ins note](includes/addinsnote.md)]

 Para obter as informações mais recentes sobre o desenvolvimento do Office, [consulte o Microsoft Office de desenvolvedores.](https://developer.microsoft.com/office/docs)

## <a name="in-this-section"></a>Nesta seção
- [Começar a &#40;do Office no Visual Studio&#41;](getting-started-office-development-in-visual-studio.md)

 Fornece links para informações sobre como configurar um computador de desenvolvimento para criar soluções do Office, como começar a criar soluções do Office e o que há de novo para desenvolvimento do Office no Visual Studio.

- [Atualizar e migrar soluções do Office](upgrading-and-migrating-office-solutions.md)

 Fornece links para informações sobre o processo de atualização de projetos criados usando versões anteriores do Visual Studio.

- [Arquitetura de soluções do Office Visual Studio](architecture-of-office-solutions-in-visual-studio.md)

 Fornece links para informações sobre como as soluções do Office funcionam, incluindo informações sobre personalizações no nível do documento e complementos vsto.

- [Projetar e criar soluções do Office](designing-and-creating-office-solutions.md)

 Fornece informações sobre como criar um projeto do Office e configurá-lo no Visual Studio.

- [Desenvolver soluções do Office](developing-office-solutions.md)

 Fornece informações sobre como usar o código gerenciado com soluções do Office, incluindo como personalizar a interface de usuário do Office, trabalhar com dados e solucionar problemas.

- [Soluções do Excel](excel-solutions.md)

 Fornece informações sobre como automatizar o Excel, criar soluções do Excel e entender os problemas de globalização específicos do Excel.

- [Soluções do InfoPath](infopath-solutions.md)

 Fornece informações sobre como criar modelos de formulário e complementos do VSTO para InfoPath.

- [Soluções do Outlook](outlook-solutions.md)

 Fornece informações sobre como automatizar o Outlook e criar as regiões de formulário e suplementos do VSTO do Outlook.

- [Soluções do PowerPoint](powerpoint-solutions.md)

 Fornece informações sobre como automatizar o PowerPoint e criar suplementos do VSTO do PowerPoint.

- [Soluções de projeto](project-solutions.md)

 Fornece informações sobre como automatizar Microsoft Office projeto e criar suplementos do VSTO do projeto.

- [Soluções do Visio](visio-solutions.md)

 Fornece informações sobre como automatizar o Visio e criar suplementos do VSTO do Visio.

- [Soluções do Word](word-solutions.md)

 Fornece informações sobre como automatizar o Word e criar soluções do Word.

- [Criar soluções do Office](building-office-solutions.md)

 Fornece informações sobre as diferenças entre a criação de projetos do Office e outros tipos de projetos no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

- [Depurar projetos do Office](debugging-office-projects.md)

 Fornece informações sobre as diferenças entre a depuração de projetos do Office e outros tipos de projetos no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

- [Proteger soluções do Office](securing-office-solutions.md)

 Fornece informações sobre como os recursos de segurança funcionam em soluções do Office.

- [Implantar uma solução do Office](deploying-an-office-solution.md)

 Fornece informações sobre como criar soluções do Office disponíveis para os usuários e os principais problemas a serem considerados ao escolher um método de implantação.

- [Exemplos e orientações de desenvolvimento do Office](office-development-samples-and-walkthroughs.md)

 Fornece links para tópicos que fornecem instruções passo a passo para executar tarefas comuns e aplicativos de exemplo.

- [Referência geral &#40;desenvolvimento do Office no Visual Studio&#41;](general-reference-office-development-in-visual-studio.md)

 Fornece links para informações detalhadas sobre assemblies de interoperabilidade primária do Office, manifestos, elementos de interface do usuário e mensagens de erro.

- [Referência gerenciada &#40;desenvolvimento do Office no Visual Studio&#41;](managed-reference-office-development-in-visual-studio.md)

 Fornece links para informações sobre namespaces de API e tipos que são usados em projetos do Office destinados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. Para obter a documentação de referência de API sobre os namespaces e tipos que são usados em projetos do Office direcionados para o .NET Framework 3,5, consulte a seção de referência a seguir na documentação do Visual Studio 2008: [2007 referência gerenciada pelo sistema](managed-reference-office-development-in-visual-studio.md).

- [Referência de API não gerenciada &#40;desenvolvimento do Office no Visual Studio&#41;](unmanaged-api-reference-office-development-in-visual-studio.md)

 Contém links para informações sobre interfaces COM que você pode usar para executar ações como carregar e descarregar suplementos do VSTO gerenciados em aplicativos do Office.

## <a name="related-sections"></a>Seções relacionadas
- [Desenvolvimento do Office com Visual Studio portal do desenvolvedor](https://developer.microsoft.com/office/docs) Fornece recursos adicionais, como artigos técnicos, vídeos e blogs.

- [Visual Studio de desenvolvedores](https://visualstudio.microsoft.com/) Fornece recursos Visual Studio recursos adicionais, como artigos técnicos, vídeos e blogs.

- [Microsoft Office de desenvolvimento da biblioteca MSDN](/previous-versions/office/office-12/bb726434(v=office.12)) A área da biblioteca MSDN em que você pode encontrar artigos e documentação de referência sobre como desenvolver soluções para várias versões do Office (não específicas para o desenvolvimento do Office usando Visual Studio).

- [Desenvolvimento de aplicativos Visual Studio](/previous-versions/h8w79z10(v=vs.140)) Contém links para tópicos que explicam como você pode usar o Visual Studio para projetar, desenvolver, depurar e implantar aplicativos Web, serviços Web XML e aplicativos cliente tradicionais.

- [.NET Framework programação em Visual Studio](/previous-versions/visualstudio/visual-studio-2010/k1s94fta(v=vs.100)) Discute o desenvolvimento de aplicativos com .NET Framework no Visual Basic e no Visual C#.

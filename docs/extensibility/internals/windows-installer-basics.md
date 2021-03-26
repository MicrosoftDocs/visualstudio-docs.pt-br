---
title: Noções básicas do Windows Installer | Microsoft Docs
description: Saiba mais sobre o Windows Installer para uso na instalação de um VSPackage, incluindo a organização de recursos do VSPackage em componentes do Windows Installer.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Windows Installer, VSPackages
- VSPackages, Windows Installer basics
ms.assetid: 497e479b-add8-4644-870a-917f15306b97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe009fa3ee8c8b9f2d15d3de4ee1fd067647c925
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074282"
---
# <a name="windows-installer-basics"></a>Noções básicas do Windows Installer
O Windows Installer instala e desinstala aplicativos ou produtos de software no computador de um usuário, executando essas tarefas em unidades chamadas Windows Installer componentes (às vezes chamados de WICs ou apenas componentes). Um GUID identifica cada WIC, que é a unidade básica de instalação e a contagem de referência para as configurações usando Windows Installer.

 Para obter uma documentação abrangente do Windows Installer, consulte o tópico Platform SDK, [Windows Installer](/previous-versions/2kt85ked(v=vs.120)).

## <a name="authoring-a-vspackage"></a>Criando um VSPackage
 Windows Installer usa pacotes de instalação, que contêm informações que Windows Installer precisam instalar, desinstalar ou reparar um produto e executar a interface do usuário da instalação. Cada pacote de instalação inclui um arquivo. msi, que contém um banco de dados de instalação, um fluxo de informações resumido e os data streams para várias partes da instalação. Para usar o instalador, você deve criar uma instalação do. Como o instalador organiza as instalações em torno do conceito de componentes e armazena informações sobre a instalação em um banco de dados relacional, o processo de criação de um pacote de instalação envolve amplamente as seguintes etapas:

1. Planeje a criação da instalação para dar suporte ao controle de versão e estratégias lado a lado.

2. Identifique os recursos a serem apresentados aos usuários.

3. Organize o VSPackage e as dependências em componentes.

4. Preencha o banco de dados de instalação com informações.

5. Valide o pacote de instalação.

   Esta documentação está preocupada principalmente com a primeira e terceira etapas do processo. Durante essas etapas, você organiza seus recursos do VSPackage em WICs para que você possa estruturar sua estratégia de controle de versão e manutenção para considerar as versões subsequentes do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . As três etapas restantes são abordadas em detalhes na documentação Windows Installer no SDK da plataforma.

## <a name="key-terms"></a>Principais termos
 A seguir estão as definições dos principais termos relacionados à tecnologia de Windows Installer.

 Arquivos de recursos, chaves do registro, atalhos, entre outros, que podem ser instalados em um computador. Esses recursos são agrupados logicamente em Windows Installer componentes.

 O componente de Windows Installer (WIC) a unidade básica de instalação que representa um agrupamento lógico de recursos relacionados que são instalados e desinstalados como uma unidade. Windows Installer componentes são identificados por uma ID de componente exclusiva ou GUID. Além disso, Windows Installer mantém sua contagem de referência no nível do WIC. Para obter a flexibilidade máxima de controle de versão, inclua não mais do que um recurso primário, como uma DLL, em um determinado WIC. Observe que, depois de identificar e popular um WIC, dar a ele um GUID e implantá-lo, você não poderá alterar sua composição. Para obter mais informações, consulte [organizando aplicativos em componentes](/windows/desktop/Msi/organizing-applications-into-components).

 Package (pacote redist) uma unidade de implantação que consiste em um arquivo. msi e arquivos de origem externos aos quais esse arquivo pode apontar. Um pacote contém todas as informações que Windows Installer precisa para executar a interface do usuário e instalar ou desinstalar o aplicativo.

 Arquivo. msi um arquivo de armazenamento estruturado COM que contém as instruções e os dados necessários para instalar um aplicativo. Cada pacote contém pelo menos um arquivo. msi. O arquivo. msi contém o banco de dados do instalador, um fluxo de informações de resumo e, possivelmente, uma ou mais transformações e arquivos de origem internos. Os arquivos a serem instalados podem ser compactados em um gabinete e armazenados em um fluxo no arquivo. msi ou armazenados, compactados ou descompactados, fora do arquivo. msi no meio de origem. Para obter mais informações, consulte [Windows Installer extensões de arquivo](/windows/desktop/Msi/windows-installer-file-extensions).

## <a name="windows-installer-rules-enforcement"></a>Imposição de regras de Windows Installer
 Dois conjuntos de regras determinam a implantação de recursos por meio dos componentes da sua instalação. Um conjunto de regras é mantido pelo Windows Installer em si, enquanto você deve impor o segundo conjunto como autor da instalação.

> [!NOTE]
> A imposição de regras de Windows Installer ocorrerá somente se você executar uma validação do seu arquivo. msi. No entanto, você é cauteloso a tratar essas regras como práticas recomendadas. Para obter mais informações, consulte [Validando um banco de dados de instalação e uma](/windows/desktop/Msi/validating-an-installation-database) validação de [pacote](/windows/desktop/Msi/package-validation).

#### <a name="installer-enforced-rules"></a>Regras de Installer-Enforced

- Todos os arquivos em um determinado componente devem ser instalados no mesmo diretório. Por outro lado, os arquivos instalados em pastas separadas devem pertencer a componentes separados.

- Pode haver apenas um caminho de chave por componente. O caminho da chave é simplesmente um arquivo ou uma chave do registro que representa o componente inteiro.

#### <a name="component-provider-responsibilities"></a>Responsabilidades de Component-Provider

- Quaisquer dois recursos que possam ser fornecidos separadamente em versões subsequentes devem existir em componentes separados. Os recursos devem ser agrupados no mesmo componente somente quando você tiver certeza de que esses recursos nunca serão enviados separadamente. Na verdade, é recomendável que todos os recursos primários (DLLs, por exemplo) sempre existam em WICs separados. Para obter mais informações, consulte [definindo componentes do instalador](/windows/desktop/Msi/defining-installer-components).

- Nenhum recurso com controle de versão já deve ser fornecido em mais de um WIC.

## <a name="see-also"></a>Confira também
- [O que acontece se as regras de componente forem interrompidas?](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)

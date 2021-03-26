---
title: Cenários de instalação do VSPackage | Microsoft Docs
description: Saiba mais sobre as práticas recomendadas para dar suporte a instalações lado a lado do Visual Studio com instalações compartilhadas ou lado a lado do seu VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2d305d03e17d0e55c2366e71452c4391ccc0ff57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060738"
---
# <a name="vspackage-setup-scenarios"></a>Cenários de instalação do VSPackage

É importante projetar seu instalador do VSPackage para obter flexibilidade. Por exemplo, talvez seja necessário lançar um patch de segurança no futuro, ou você pode alterar uma estratégia de negócios que exige um suporte de controle de versão lado a lado completo.

No [suporte a várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md), você pode ler sobre as vantagens e problemas de suporte a instalações lado a lado do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com instalações compartilhadas ou lado a lado do seu VSPackage. Em suma, VSPackages lado a lado oferecem a você a maior flexibilidade para dar suporte a novos recursos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

Os cenários discutidos neste tópico não são suas únicas opções, mas são apresentados como práticas recomendadas sugeridas.

## <a name="components-privacy-and-sharing"></a>Componentes, privacidade e compartilhamento

### <a name="make-your-components-independent"></a>Torne seus componentes independentes

Depois de identificar e popular um componente, atribuir um `GUID` e implantar o componente, você não poderá alterar sua composição. Se você alterar a composição de um componente, o componente resultante deverá ser um novo componente com um novo `GUID` . Considerando esses fatos, a maior flexibilidade de controle de versão é proporcionada, tornando cada componente independente, unidade autônoma. Para obter mais informações sobre regras que regem os componentes, consulte [alterando o código do componente](/windows/desktop/Msi/changing-the-component-code) e [o que acontece se as regras de componente são interrompidas?](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken).

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>Não misture recursos compartilhados e privados em um componente

A contagem de referência ocorre no nível de componente. Consequentemente, misturar recursos compartilhados e privados em um componente torna impossível atualizar recursos privados, como um arquivo executável, sem também substituir recursos compartilhados. Esse cenário cria problemas de compatibilidade com versões anteriores e o restringe da criação de recursos lado a lado.

Por exemplo, os valores de registro usados para registrar seu VSPackage com o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] devem ser mantidos em um componente separado de um usado para registrar seu VSPackage com o Visual Studio. Arquivos compartilhados ou valores de registro ainda têm outro componente.

## <a name="scenario-1-shared-vspackage"></a>Cenário 1: VSPackage compartilhados

Nesse cenário, um VSPackage compartilhado (um único binário que dá suporte a várias versões do Visual Studio é fornecido em um pacote Windows Installer. O registro em cada versão do Visual Studio é controlado por recursos selecionáveis pelo usuário. Isso também significa que, quando atribuído a recursos separados, cada componente pode ser selecionado individualmente para instalação ou desinstalação, colocando o usuário no controle de integração do VSPackage em diferentes versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . (Consulte [Windows Installer recursos](/windows/desktop/Msi/windows-installer-features) para obter mais informações sobre como usar recursos em pacotes do Windows Installer.)

![Instalador do VSPackage compartilhado do VS](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

Conforme mostrado na ilustração, os componentes compartilhados são feitos parte do recurso Feat_Common, que é sempre instalado. Ao tornar os recursos Feat_VS2002 e Feat_VS2003 visíveis, os usuários podem escolher o tempo de instalação no qual as versões do Visual Studio querem que o VSPackage seja integrado. Os usuários também podem usar Windows Installer modo de manutenção para adicionar ou remover recursos, que nesse caso adiciona ou remove as informações de registro de VSPackage de diferentes versões do Visual Studio.

> [!NOTE]
> Definir a coluna de exibição de um recurso como 0 o oculta. Um valor de coluna de nível baixo, como 1, garante que ele sempre será instalado. Para obter mais informações, consulte Propriedade e [tabela de recursos](/windows/desktop/Msi/feature-table)do [INSTALLLEVEL](/windows/desktop/Msi/installlevel) .

## <a name="scenario-2-shared-vspackage-update"></a>Cenário 2: atualização de VSPackage compartilhada

Nesse cenário, uma versão atualizada do instalador do VSPackage no cenário 1 é fornecida. Para fins de discussão, a atualização adiciona suporte para o Visual Studio, mas também pode ser um patch de segurança mais simples ou uma correção de bug service pack. As regras de Windows Installer para instalar os componentes mais recentes exigem que os componentes inalterados já existentes no sistema não sejam copiados novamente. Nesse caso, um sistema com a versão 1,0 já presente substituirá o componente atualizado Comp_MyVSPackage.dll e permitirá que os usuários escolham adicionar o novo recurso Feat_VS2005 com seu componente Comp_VS2005_Reg.

> [!CAUTION]
> Sempre que um VSPackage é compartilhado entre várias versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , é essencial que as versões subsequentes do VSPackage mantenham a compatibilidade com versões anteriores do Visual Studio. Onde não é possível manter a compatibilidade com versões anteriores, você deve usar VSPackages privada lado a lado. Para obter mais informações, consulte [dando suporte a várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md).

![Instalador de atualização de pacote vs compartilhado vs](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

Esse cenário apresenta um novo instalador do VSPackage, aproveitando o suporte de Windows Installer para pequenas atualizações. Os usuários simplesmente instalam a versão 1,1 e atualizam a versão 1,0. No entanto, não é necessário ter a versão 1,0 no sistema. O mesmo instalador instalará a versão 1,1 em um sistema sem a versão 1,0. A vantagem de fornecer pequenas atualizações dessa maneira é que não é necessário passar pelo trabalho de desenvolver um instalador de atualização e um instalador de produto completo. Um instalador faz ambos os trabalhos. Uma correção de segurança ou service pack pode, em vez disso, aproveitar os Windows Installer patches. Para obter mais informações, consulte [patches e atualizações](/windows/desktop/Msi/patching-and-upgrades).

## <a name="scenario-3-side-by-side-vspackage"></a>Cenário 3: VSPackage lado a lado

Esse cenário apresenta dois instaladores VSPackage – um para cada versão do Visual Studio .NET 2003 e Visual Studio. Cada instalador instala um VSPackage lado a lado, ou privado, (um que é especificamente compilado e instalado para uma versão específica do Visual Studio). Cada VSPackage está em seu próprio componente. Consequentemente, cada uma pode ser atendida individualmente com patches ou versões de manutenção. Como a DLL VSPackage agora é específica da versão, é seguro incluir suas informações de registro no mesmo componente que a DLL.

![Programa de instalação lado a lado do vs Package](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

Cada instalador também inclui o código compartilhado entre os dois instaladores. Se o código compartilhado for instalado em um local comum, a instalação de ambos os arquivos. msi instalará o código compartilhado apenas uma vez. O segundo instalador apenas incrementa uma contagem de referência no componente. A contagem de referência garante que, se um dos VSPackages for desinstalado, o código compartilhado permanecerá para o outro VSPackage. Se o segundo VSPackage for desinstalado também, o código compartilhado será removido.

## <a name="scenario-4-side-by-side-vspackage-update"></a>Cenário 4: atualização de VSPackage lado a lado

Nesse cenário, seu VSPackage para Visual Studio sofreu uma vulnerabilidade de segurança e você precisa emitir uma atualização. Como no cenário 2, você pode criar um novo arquivo. msi que atualiza uma instalação existente para incluir a correção de segurança, bem como implantar novas instalações com a correção de segurança já em vigor.

Nesse caso, o VSPackage é um VSPackage gerenciado instalado no GAC (cache de assembly global). Ao reconstruí-lo para incluir a correção de segurança, você deve alterar a parte do número de revisão do número de versão do assembly. As informações de registro para o novo número de versão do assembly substitui a versão anterior, fazendo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com que o carregue o assembly fixo.

![Instalador de atualização de pacote vs lado a lado](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

Para obter mais informações sobre a implantação de assemblies lado a lado, consulte [simplificando a implantação e resolvendo a dll inferno com o .NET Framework](/previous-versions/dotnet/articles/ms973843(v=msdn.10)).

## <a name="see-also"></a>Confira também

- [Windows Installer](/windows/desktop/Msi/windows-installer-portal)
- [Fornecer suporte à várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
---
title: Cenários de instalação de VSPackage | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c194588de8dfa8746bb79a8d86bff005d90e7550
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495928"
---
# <a name="vspackage-setup-scenarios"></a>Cenários de instalação do VSPackage

É importante projetar o seu instalador VSPackage para flexibilidade. Por exemplo, talvez seja necessário liberar um patch de segurança no futuro, ou você pode alterar uma estratégia de negócios que exija suporte de controle de versão lado a lado completo.

Na [que dão suporte a várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md), você pode ler sobre as vantagens e os problemas de dar suporte a instalações lado a lado do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com instalações lado a lado ou compartilhadas do VSPackage. Em resumo, lado a lado VSPackages lhe dar mais flexibilidade para dar suporte a novos recursos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

Os cenários abordados neste tópico não são suas únicas opções, mas eles são apresentados como práticas recomendadas sugeridas.

## <a name="components-privacy-and-sharing"></a>Componentes, privacidade e compartilhamento

### <a name="make-your-components-independent"></a>Verifique seus componentes independentes

Depois de identificar e preencher um componente, atribua um `GUID`e implantar o componente, você não pode alterar sua composição. Se você alterar a composição de um componente, o componente resultante deve ser um novo componente com um novo `GUID`. Devido a esses fatos, a maior flexibilidade de controle de versão é que, fazendo cada unidade auto-suficiente, independente do componente. Para obter mais informações sobre as regras que regem os componentes, consulte [alterar o código do componente](/windows/desktop/Msi/changing-the-component-code) e [o que acontece se o componente de regras são divididas?](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken).

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>Não misture recursos compartilhados e particulares em um componente

Contagem de referência ocorre no nível do componente. Consequentemente, combinando os recursos compartilhados e particulares em um componente torna impossível atualizar recursos privados, como um arquivo executável, sem substituir também recursos compartilhados. Este cenário cria problemas de compatibilidade com versões anteriores e restringe você de criar a funcionalidade de lado a lado.

Por exemplo, valores de registro é usado para registrar o VSPackage com o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] deve ser mantido em um componente separado de um usada para registrar o VSPackage no Visual Studio. Arquivos compartilhados ou valores do registro ir em outro componente.

## <a name="scenario-1-shared-vspackage"></a>Cenário 1: Compartilhado VSPackage

Nesse cenário, um VSPackage compartilhado (um binário único que oferece suporte a várias versões do Visual Studio é fornecido em um pacote do Windows Installer. Registrando com cada versão do Visual Studio é controlada pelos recursos selecionáveis pelo usuário. Isso também significa que quando atribuído para separar os recursos, cada componente pode ser selecionada individualmente para instalação ou desinstalação, colocando o usuário no controle de integrar o VSPackage em versões diferentes do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. (Consulte [recursos do Windows Installer](/windows/desktop/Msi/windows-installer-features) para obter mais informações sobre como usar recursos em pacotes do Windows Installer.)

![O instalador do VS compartilhados VSPackage](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

Conforme mostrado na ilustração, os componentes compartilhados são feitos parte do recurso Feat_Common, que sempre é instalado. Ao tornar os recursos Feat_VS2002 e Feat_VS2003 visível, os usuários podem escolher no momento da instalação em quais versões do Visual Studio que desejam integrar o VSPackage. Os usuários também podem usar o modo de manutenção do Windows Installer para adicionar ou remover recursos, que nesse caso, adiciona ou remove as informações de registro de VSPackage de diferentes versões do Visual Studio.

> [!NOTE]
> A definição de coluna de exibição de um recurso como 0 impede que ele. Um valor de coluna de nível baixo, como 1, garante que ele sempre será instalado. Para obter mais informações, consulte [propriedade installlevel SIGNIFICAM](/windows/desktop/Msi/installlevel) e [recurso tabela](/windows/desktop/Msi/feature-table).

## <a name="scenario-2-shared-vspackage-update"></a>Cenário 2: Atualização de VSPackage compartilhada

Nesse cenário, uma versão atualizada do instalador do VSPackage no cenário 1 é fornecida. Para discussão, a atualização adiciona suporte para Visual Studio, mas ele pode também ser um patch de segurança mais simples ou pacote de serviço de correção de bug. Regras do Windows Installer para instalar os componentes mais recentes requerem inalterados componentes já está no sistema não são copiados novamente. Nesse caso, um sistema com a versão 1.0 já está presente irá substituir o componente atualizado Comp_MyVSPackage.dll e permitir que os usuários optar por adicionar o novo recurso Feat_VS2005 com seu componente Comp_VS2005_Reg.

> [!CAUTION]
> Sempre que um VSPackage é compartilhado entre várias versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], é essencial que as versões subsequentes do VSPackage mantenham a compatibilidade com versões anteriores do Visual Studio. Em que você não pode manter a compatibilidade com versões anteriores, você deve usar os VSPackages lado a lado, privados. Para obter mais informações, consulte [que dão suporte a várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md).

![Instalador de atualização de pacote do VS compartilhados do VS](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

Este cenário apresenta um novo instalador do VSPackage, tirando proveito do suporte do Windows Installer para atualizações secundárias. Os usuários simplesmente instalar a versão 1.1 e ele atualiza a versão 1.0. No entanto, não é necessário ter a versão 1.0 no sistema. O mesmo instalador instalará a versão 1.1 em um sistema sem versão 1.0. A vantagem para fornecer atualizações secundárias dessa maneira é que não é necessário percorrer o trabalho de desenvolvimento de um instalador de atualização e instalador de um produto completo. Um instalador faz os dois trabalhos. Uma correção de segurança ou service pack pode em vez disso, tirar proveito dos patches do Windows Installer. Para obter mais informações, consulte [aplicação de patch e atualizações](/windows/desktop/Msi/patching-and-upgrades).

## <a name="scenario-3-side-by-side-vspackage"></a>Cenário 3: Side-by-Side VSPackage

Este cenário apresenta dois instaladores de VSPackage — uma para cada versão do Visual Studio .NET 2003 e o Visual Studio. Cada instalador instala um lado a lado ou privada, VSPackage (aquele que é criado e instalado para uma versão específica do Visual Studio especificamente). Cada VSPackage está em seu próprio componente. Consequentemente, cada um pode ser individualmente atendida com patches ou manutenção libera. Como a DLL de VSPackage agora é específico da versão, é seguro incluir suas informações de registro no mesmo componente, como a DLL.

![Instalador de pacote do VS lado a lado do VS](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

Cada instalador também inclui código que é compartilhado entre os dois instaladores. Se o código compartilhado é instalado em um local comum, instalar os dois arquivos. msi instalará o código compartilhado somente uma vez. O instalador do segundo apenas incrementa uma contagem de referência no componente. A contagem de referência garante que, se um dos VSPackages for desinstalado, o código compartilhado permanecerá por outro VSPackage. Se o segundo VSPackage for desinstalado, bem, o código compartilhado será removido.

## <a name="scenario-4-side-by-side-vspackage-update"></a>Cenário 4: Atualização de VSPackage de lado a lado

Nesse cenário, o VSPackage para o Visual Studio foram afetados por uma vulnerabilidade de segurança e é necessário executar uma atualização. Como no cenário 2, você pode criar um novo arquivo. msi que atualiza uma instalação existente para incluir a correção de segurança, bem como para implantar novas instalações com a correção de segurança já em vigor.

Nesse caso, o VSPackage é um VSPackage gerenciado instalado no cache de assembly global (GAC). Quando você recompilá-lo para incluir a correção de segurança, você deve alterar a parte de número de revisão do número de versão do assembly. As informações de registro para o novo número de versão do assembly substitui a versão anterior, causando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para carregar o assembly fixado.

![Instalador de atualização de pacote do VS lado a lado do VS](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

Para obter mais informações sobre a implantação de assemblies lado a lado, consulte [simplificando a implantação e resolvendo inferno da DLL com o .NET Framework](https://msdn.microsoft.com/library/ms973843.aspx).

## <a name="see-also"></a>Consulte também

[Windows Installer](/windows/desktop/Msi/windows-installer-portal)  
[Fornecer suporte à várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
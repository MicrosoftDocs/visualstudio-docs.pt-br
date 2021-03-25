---
title: Registro e seleção (VSPackage de controle do código-fonte) | Microsoft Docs
description: Saiba como registrar um VSPackage de controle do código-fonte com o Visual Studio e como selecionar qual pacote carregar de vários pacotes de controle do código-fonte registrados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ff23784bb833c6a68e368f5db5d3b6f1a7433bb0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069394"
---
# <a name="registration-and-selection-source-control-vspackage"></a>Registro e seleção (VSPackage do controle do código-fonte)
Um VSPackage de controle do código-fonte deve ser registrado para expô-lo ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Se mais de um VSPackage de controle do código-fonte estiver registrado, o usuário poderá selecionar qual VSPackage carregar nos horários apropriados. Consulte [VSPackages](../../extensibility/internals/vspackages.md) para obter mais detalhes sobre o VSPackages e como registrá-los.

## <a name="registering-a-source-control-package"></a>Registrando um pacote de controle do código-fonte
 O pacote de controle do código-fonte é registrado para que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente possa encontrá-lo e consultar seus recursos com suporte. Isso é de acordo com um esquema de carregamento de atraso no qual uma instância de um pacote é criada somente quando seus recursos ou comandos são necessários ou são solicitados explicitamente.

 VSPackages Coloque as informações em uma chave de Registro específica da versão, HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *X. Y*, em que *x* é o número de versão principal e *Y* é o número de versão secundária. Essa prática fornece a capacidade de dar suporte à instalação lado a lado de várias versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

 A [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário (IU) dá suporte à seleção entre vários plug-ins de controle do código-fonte instalados (por meio do pacote do adaptador de controle do código-fonte), bem como o controle do código-fonte Pode haver apenas um plug-in de controle do código-fonte ativo ou VSPackage de cada vez. No entanto, conforme descrito abaixo, o IDE permite alternar entre plug-ins de controle do código-fonte e VSPackages por meio de um mecanismo de troca de pacotes baseado em soluções automático. Há alguns requisitos na parte do VSPackage de controle do código-fonte para habilitar esse mecanismo de seleção.

### <a name="registry-entries"></a>Entradas do Registro
 Um pacote de controle do código-fonte precisa de três GUIDs particulares:

- GUID do pacote: Este é o GUID principal para o pacote que contém a implementação do controle do código-fonte (chamado ID_Package nesta seção).

- GUID de controle do código-fonte: é um GUID para o controle do código-fonte VSPackage usado para se registrar no stub do controle do código-fonte do Visual Studio e também é usado como um GUID de contexto de interface do usuário de comando O GUID do serviço de controle do código-fonte está registrado no GUID de controle do código-fonte. No exemplo, o GUID de controle do código-fonte é chamado de ID_SccProvider.

- GUID do serviço de controle do código-fonte: é o GUID do serviço privado usado pelo Visual Studio (chamado de SID_SccPkgService nesta seção). Além disso, o pacote de controle do código-fonte precisa definir outros GUIDs para VSPackages, janelas de ferramentas e assim por diante.

  As seguintes entradas de registro devem ser feitas por um VSPackage de controle do código-fonte:

| Nome da chave | Entradas |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (padrão) = rg_sz: {ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | (padrão) = rg_sz:\<Friendly name of Package><br /><br /> Serviço = rg_sz: {SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | (padrão) = rg_sz: #\<Resource ID for localized name><br /><br /> Pacote = rg_sz: {ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (Observe que o nome da chave, `SourceCodeControl` , já é usado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e não está disponível como uma opção para \<PackageName> .) | (padrão) = rg_sz: {ID_Package} |

## <a name="selecting-a-source-control-package"></a>Selecionando um pacote de controle do código-fonte
 Vários plug-ins baseados em API de plug-in de controle do código-fonte e VSPackages de controle do código-fonte podem ser registrados simultaneamente. O processo de selecionar um plug-in de controle do código-fonte ou VSPackage deve garantir que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o carregue o plug-in ou o VSPackage no momento apropriado e possa adiar o carregamento de componentes desnecessários até que eles sejam necessários. Além disso, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] deve remover todas as interfaces do usuário de outros VSPackages inativos, incluindo itens de menu, caixas de diálogo e barras de ferramentas, e exibir a interface do usuário para o VSPackage ativo.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] carrega um VSPackage de controle do código-fonte quando qualquer uma das seguintes operações é executada:

- A solução está aberta (quando a solução está sob controle do código-fonte).

   Quando uma solução ou projeto sob controle do código-fonte é aberto, o IDE faz com que o VSPackage de controle do código-fonte designado para essa solução seja carregado.

- Qualquer um dos comandos de menu do VSPackage de controle do código-fonte é executado.

  Um VSPackage de controle do código-fonte deve carregar os componentes necessários apenas quando eles realmente serão usados (de outra forma, conhecidos como carregamento atrasado).

### <a name="automatic-solution-based-vspackage-swapping"></a>Troca automática baseada em solução VSPackage
 Você pode alternar manualmente o controle do código-fonte VSPackages pela [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caixa de diálogo **Opções** na categoria **controle do código-fonte** . A troca automática de pacotes baseada em soluções significa que um pacote de controle do código-fonte designado para uma solução específica é definido automaticamente como ativo quando essa solução é aberta. Cada pacote de controle do código-fonte deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> . [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] manipula a opção entre ambos os plug-ins de controle do código-fonte (implementando a API de plug-in de controle do código-fonte) e VSPackages de controle do código

 O pacote do adaptador de controle do código-fonte é usado para alternar para qualquer plug-in baseado em API de plug-in de controle do código-fonte. O processo de alternar para o pacote do adaptador de controle do código-fonte intermediário e determinar qual plug-in de controle do código-fonte deve ser definido como ativo ou inativo é transparente para o usuário. O pacote do adaptador sempre estará ativo quando qualquer plug-in de controle do código-fonte estiver ativo. Alternar entre dois valores de plug-ins de controle do código-fonte para simplesmente carregar e descarregar a DLL de plug-in. No entanto, alternar para um VSPackage de controle do código-fonte envolve interagir com o IDE para carregar o VSPackage apropriado.

 Um VSPackage de controle do código-fonte é chamado quando qualquer solução é aberta e a chave do registro para o VSPackage está no arquivo de solução. Quando a solução é aberta, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o encontra o valor do registro e carrega o VSPackage de controle do código-fonte apropriado. Todos os VSPackages de controle do código-fonte devem ter as entradas de registro descritas acima. Uma solução que está sob o controle do código-fonte é marcada como sendo associada a um VSPackage de controle do código-fonte específico. O VSPackages de controle do código-fonte deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> para habilitar a troca automática baseada em solução VSPackage.

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Interface do usuário do Visual Studio para seleção e alternância de pacotes
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece uma interface do usuário para VSPackage de controle do código-fonte e seleção de plug-in na caixa de diálogo **Opções** na categoria **controle do código-fonte** . Ele permite que o usuário selecione o plug-in de controle do código-fonte ativo ou VSPackage. Uma lista suspensa inclui:

- Todos os pacotes de controle do código-fonte instalados

- Todos os plug-ins de controle do código-fonte instalados

- Uma opção "None", que desabilita o controle do código-fonte

  Somente a interface do usuário para a opção de controle do código-fonte ativo é visível. A seleção VSPackage oculta a interface do usuário para a VSPackage anterior e mostra a interface do usuário para a nova. O VSPackage ativo é selecionado de acordo com o usuário. Se um usuário tiver várias cópias de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] abertas simultaneamente, cada uma poderá potencialmente usar um VSPackage ativo diferente. Se vários usuários estiverem conectados ao mesmo computador, cada usuário poderá ter instâncias separadas do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Open, cada um com um VSPackage ativo diferente. Quando várias instâncias do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] são fechadas por um usuário, o VSPackage de controle do código-fonte que estava ativo para a última solução aberta torna-se o controle do código-fonte padrão VSPackage, para ser definido como ativo na reinicialização.

  Ao contrário das versões anteriores do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , uma reinicialização do IDE não é mais a única maneira de alternar o controle do código-fonte VSPackages. A seleção de VSPackage é automática. A alternância de pacotes requer privilégios de usuário do Windows (não administrador ou usuário avançado).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [Recursos](../../extensibility/internals/source-control-vspackage-features.md)
- [Criando um plug-in de controle do código-fonte](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)

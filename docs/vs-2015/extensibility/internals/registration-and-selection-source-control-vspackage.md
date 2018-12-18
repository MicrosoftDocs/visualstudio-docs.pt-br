---
title: Registro e seleção (VSPackage de controle do código-fonte) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
caps.latest.revision: 35
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 636e70357c23059a505d657af0078653de413976
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764458"
---
# <a name="registration-and-selection-source-control-vspackage"></a>Registro e seleção (VSPackage do controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um controle de fonte VSPackage deve ser registrado para expô-lo para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Se mais de um VSPackage de controle de origem estiver registrado, o usuário pode selecionar quais VSPackage carregar em momentos apropriados. Ver [VSPackages](../../extensibility/internals/vspackages.md) para obter mais detalhes sobre os VSPackages e como registrá-los.  
  
## <a name="registering-a-source-control-package"></a>Registrar um pacote de controle do código-fonte  
 O pacote de controle do código-fonte está registrado para que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente pode encontrar ela e a consulta para seus recursos com suporte. Isso está de acordo com um esquema de carregamento de atraso no qual uma instância de um pacote é criada somente quando seus recursos e comandos são necessários ou forem solicitados explicitamente.  
  
 Os VSPackages colocar as informações em uma chave do registro específica à versão HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*x. y*, onde *X* é o número de versão principal e uma *Y* é o número de versão secundária. Essa prática oferece a capacidade de dar suporte à instalação lado a lado de várias versões do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] seleção de controle de origem instalado vários plug-ins (via o pacote de adaptador de controle do código-fonte) dá suporte à interface do usuário (IU), bem como os VSPackages de controle de origem. Pode haver apenas um plug-in de controle de origem ativa ou VSPackage por vez. No entanto, conforme descrito abaixo, o IDE permite alternar entre os plug-ins de controle do código-fonte e os VSPackages através de um baseados em soluções permutação de pacote mecanismo automático. Há alguns requisitos por parte de VSPackage do controle de origem para habilitar esse mecanismo de seleção.  
  
### <a name="registry-entries"></a>Entradas do registro  
 Um pacote de controle de origem precisa de três GUIDs privadas:  
  
- GUID do pacote: Isso é o GUID do principal para o pacote que contém a implementação de controle do código-fonte (chamada ID_Package nesta seção).  
  
- GUID de controle do código-fonte: Isso é um GUID para o controle de origem usado para registrar com o Stub de controle de origem Visual do Studio de VSPackage e também é usado como um contexto de interface do usuário do comando GUID. O serviço de controle do código-fonte GUID está registrado sob o GUID de controle do código-fonte. No exemplo, o GUID de controle do código-fonte é chamado ID_SccProvider.  
  
- GUID de serviço de controle de origem: Este é o serviço privado GUID usado pelo Visual Studio (chamado SID_SccPkgService nesta seção). Além disso, o pacote de controle de origem precisa definir outros GUIDs para VSPackages, janelas de ferramentas e assim por diante.  
  
  As seguintes entradas do registro devem ser feitas por um VSPackage de controle do código-fonte:  
  
|Nome da chave|Entradas|  
|--------------|-------------|  
|`HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\`|(padrão) = rg_sz: {ID_SccProvider}|  
|`HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\`|(padrão) = rg_sz:\<nome amigável do pacote ><br /><br /> Serviço = rg_sz: {SID_SccPkgService}|  
|`HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\`|(padrão) = rg_sz: #\<ID de recurso para o nome localizado ><br /><br /> Pacote = rg_sz: {ID_Package}|  
|`HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (Observe que o nome da chave `SourceCodeControl`, já é usado por [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e não está disponível como uma opção para \<PackageName >.)|(padrão) = rg_sz: {ID_Package}|  
  
## <a name="selecting-a-source-control-package"></a>Selecionando um pacote de controle do código-fonte  
 Vários de plug-ins baseados na API de plug-in de controle do código-fonte e os VSPackages pode ser registrados simultaneamente de controle de origem. O processo de selecionar um plug-in de controle do código-fonte ou VSPackage deve garantir que [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] carrega o plug-in ou VSPackage no momento apropriado e pode adiar o carregamento de componentes desnecessários até que eles sejam necessários. Além disso, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] deve remover toda interface do usuário de outros VSPackages inativos, incluindo itens de menu, caixas de diálogo e barras de ferramentas e exibir a interface do usuário para o Active Directory VSPackage.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] carrega um VSPackage de controle do código-fonte quando é realizada a qualquer uma das seguintes operações:  
  
- Solução é aberta (quando a solução estiver sob controle do código-fonte).  
  
   Quando uma solução ou projeto sob controle do código-fonte é aberto, o IDE faz com que o controle de fonte VSPackage que foi designado para a solução a ser carregado.  
  
- Qualquer um dos comandos de menu de controle de fonte de VSPackage são executadas.  
  
  Um controle de fonte que VSPackage deverá carregar todos os componentes que precisa apenas quando eles são realmente será usado (conhecido também como o carregamento atrasado).  
  
### <a name="automatic-solution-based-vspackage-swapping"></a>Troca automática VSPackage baseados em soluções  
 Manualmente, você pode trocar os VSPackages de controle de origem por meio de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **opções** caixa de diálogo do **controle de fonte de** categoria. Troca automática de pacotes baseados em soluções significa que um pacote de controle de origem tiver sido designado para uma determinada solução é automaticamente definido como ativo quando essa solução é aberta. Cada pacote de controle de origem deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] lida com a alternância entre os dois plug-ins de controle (Implementando a API de plug-in de controle do código-fonte) de origem e os VSPackages de controle de origem.  
  
 O pacote de adaptador de controle de origem é usado para alternar para qualquer API de plug-in de controle do código-fonte-com base em plug-in. O processo de alternar para o pacote intermediário do adaptador de controle de origem e determinar quais plug-in de controle do código-fonte deve ser definido como ativo ou inativo é transparente ao usuário. O pacote do adaptador está sempre ativo quando qualquer plug-in de controle do código-fonte está ativo. Alternando entre dois valores de plug-ins de controle de origem para simplesmente carregar e descarregar a DLL de plug-in. No entanto, alternando para um VSPackage de controle do código-fonte, envolve a interagir com o IDE para carregar o VSPackage apropriado.  
  
 Um controle de fonte VSPackage é chamado quando qualquer solução é aberta e a chave do registro para o VSPackage está no arquivo de solução. Quando a solução for aberta, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] localiza o valor do registro e carrega o VSPackage de controle de origem apropriada. Todos os VSPackages de controle de origem deve ter as entradas do Registro descritas acima. Uma solução sob controle do código-fonte está marcada como sendo associado a um VSPackage de controle de origem em particular. Deve implementar a VSPackages de controle de fonte de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> para habilitar a automático com base em solução VSPackage alternância.  
  
### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Interface do usuário para seleção de pacote e a alternância de Visual Studio  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Fornece uma interface do usuário para o VSPackage de controle de origem e a seleção de plug-in na **opções** caixa de diálogo da **controle do código-fonte** categoria. Ele permite que o usuário selecione o plug-in de controle de origem ativa ou VSPackage. Uma lista suspensa inclui:  
  
- Todos os pacotes de controle de origem instalados  
  
- Todos instalados plug-ins de controle de origem  
  
- Opção um "none", que desabilita o controle do código fonte  
  
  Somente a interface do usuário para a opção de controle de origem ativa está visível. A seleção de VSPackage oculta a interface do usuário para o VSPackage anterior e mostra a interface do usuário para uma nova. O Active Directory VSPackage é selecionado em uma base por usuário. Se um usuário tiver várias cópias de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] abra simultaneamente, cada um deles pode usar um VSPackage Active Directory diferente. Se vários usuários estão conectados ao mesmo computador, cada usuário pode ter instâncias separadas do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] abrir, cada um com um VSPackage Active Directory diferente. Quando várias instâncias do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] sejam fechados por um usuário, o controle de fonte VSPackage que estava ativo para a última solução aberta se torna o controle de fonte padrão VSPackage, sejam definidos ativos na reinicialização.  
  
  Diferentemente das versões anteriores do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], uma reinicialização do IDE não é a única maneira de alternar os VSPackages de controle de origem. Seleção de VSPackage é automática. Troca de pacotes requer privilégios de usuário do Windows (não administrador ou usuário avançado).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>   
 [Recursos](../../extensibility/internals/source-control-vspackage-features.md)   
 [Criando um controle de fonte plug-in](../../extensibility/internals/creating-a-source-control-plug-in.md)   
 [VSPackages](../../extensibility/internals/vspackages.md)


---
title: Componentes principais do Project Model | Microsoft Docs
description: Este artigo contém descrições das interfaces e dos serviços identificados no Project Model Core e as interfaces e serviços associados a objetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88dc53378e7e06d0a7d4ad362f7bb3876e186c80
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899700"
---
# <a name="project-model-core-components"></a>Componentes principais do projeto modelo
As tabelas a seguir expandem o modelo de projeto. As tabelas apresentam breves descrições das interfaces e dos serviços identificados no modelo, bem como as interfaces e os serviços associados a objetos específicos. Além disso, as tabelas detalham outras interfaces que são opcionais na criação e manutenção do projeto, dependendo dos requisitos de seu tipo de projeto específico.

 Para obter mais informações, consulte [suporte a ferramentas de Symbol-Browsing](../../extensibility/internals/supporting-symbol-browsing-tools.md).

### <a name="package-object"></a>Objeto de pacote

|Interface|Comentários|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|Inicializa um VSPackage no IDE e torna seus serviços disponíveis para o IDE.|

### <a name="project-factory-object"></a>Objeto de fábrica do projeto

|Interface|Comentários|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|Gerencia a criação de novos projetos e a abertura de projetos existentes.|

### <a name="project-objects"></a>Objetos do projeto

|Interfaces|Comentários|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|Gerencia a adição e a remoção de itens de projeto, abre editores e mantém o mapeamento entre cada moniker de documento e o `VSITEMID` . Herda de `IVsProject` e `IVsProject2` .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|Gerencia Propriedades de navegação e exibição e fornece eventos.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|Permite a execução de comando semelhante à do `IOleCommandTarget` para comandos como recortar e renomear que se aplicam somente quando o foco está em Gerenciador de soluções.|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Serve como a interface de destino do comando primário para uma hierarquia de projeto. É a interface padrão para consultar objetos quanto ao status do comando ou ao estado e aos comandos em execução. Disponível quando você não estiver focado na janela do projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Coordena a persistência do estado do projeto. Normalmente, o estado do projeto é armazenado como um arquivo de projeto, mas pode ser adaptado para sistemas de armazenamento que não são baseados em arquivo.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|Permite que o projeto gerencie todos os aspectos da persistência para seus itens de projeto, seja como arquivos em disco ou objetos em outros sistemas de armazenamento. A `IVsPersistHierarchyItem2` interface é usada para itens que não implementam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|Coordena as interações com o controle do código-fonte.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|Habilita projetos para gerenciar informações de configuração.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|Gerencia objetos de configuração de projeto, como configurações de depuração/versão. As operações de criação, implantação e depuração são coordenadas por meio de objetos de configuração de projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|Implementado por hierarquias para controlar as opções de exclusão (destrutiva) ou remoção (não destrutiva) para itens de hierarquia. Chame a interface de consulta na interface `IVsHierarchyDeleteHandler` da `IVsHierarchy` interface.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|Fornece a opção de implementação de ter o objeto que dá suporte à `IVsCfgProvider2` interface em uma identidade com diferente do objeto de projeto que implementa a `IVsHierarchy` interface.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|Interface opcional implementada para tornar seu projeto extensível por outros desenvolvedores. A `IVsProjectStartupServices` interface permite que um VSPackage de terceiros registre um GUID que você mantém em seu arquivo de projeto para que sempre que seu projeto for carregado, você carregue o GUID de serviço de terceiros em seu arquivo de projeto e chame `QueryService` esse GUID.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|Implementado por hierarquias de origem em uma `UIHierarchy` janela para coordenar operações de área de transferência, como recortar, copiar e colar. Use a `AdviseClipboardHelperEvents` interface para registrar eventos da área de transferência.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|Fornece informações sobre um item arrastado em relação à sua fonte de dados durante uma operação de arrastar e soltar em uma janela de hierarquia de interface do usuário. Chamado da `IVsHierarchy` interface.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|Fornece informações sobre um item arrastado em relação ao seu destino de soltar durante uma operação de arrastar e soltar em uma janela de hierarquia de interface do usuário. Chamado da `IVsHierarchy` interface.|

### <a name="configuration-object"></a>Objeto de configuração

|Interfaces|Comentários|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|Fornece informações sobre uma configuração.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|Habilita projetos para gerenciar informações de configuração.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|Permite que um projeto seja executado sob o controle do depurador.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|Implementado por projetos de implantação que executam operações de implantação para outros projetos.|

### <a name="configuration-builder-object"></a>Objeto do Configuration Builder

|Interfaces|Comentários|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|Gerencia a operação de compilação de uma configuração de projeto.|

### <a name="additional-project-objects"></a>Objetos de projeto adicionais

|Interfaces|Comentários|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|Exibe as propriedades do item na janela **Propriedades** .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|Exibe saídas para implantação.|

 A tabela a seguir apresenta breves descrições dos serviços identificados no modelo de projeto.

### <a name="services"></a>Serviços

|Serviço|Comentários|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|Usado por VSPackages que implementam tipos de projeto para registrar que a fábrica de projetos existe com o IDE. Seu VSPackage deve chamar `QueryService` esse serviço e registrar sua fábrica de projetos quando o `IVsPackage::SetSite` método for chamado. Se o `SetSite` método não for chamado, seu projeto não será instanciado.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|Fornece acesso à noção interna e interna do IDE da solução atual, como a capacidade de enumerar projetos, criar novos projetos, observar alterações de projeto e assim por diante.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|Chamado por projetos que desejam participar do controle do código-fonte.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|Mantém uma tabela de documentos abertos para determinar se um ou mais de seus itens de projeto já estão abertos.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|Contém as interfaces e os métodos chamados para realmente abrir um item de projeto usando o editor padrão ou um editor específico.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|Necessário para ser chamado por todos os projetos ao adicionar, remover ou renomear seus itens.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|Gerencia as alterações em um arquivo ou diretório e notifica os clientes quando os arquivos selecionados foram alterados no disco.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|Necessário para ser chamado por todos os projetos e editores antes de os itens sujos ou salvá-los.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|Gerencia a ordem de operações de compilação e implantação para configurações de projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|Fornece acesso a serviços de depurador de nível baixo usados para a maioria dos controles de depuração.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|Permite o acesso de VSPackages a informações sobre as seleções atuais e habilita a comunicação com a janela **Propriedades** .|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|Fornece funcionalidade básica de IDE relacionada à interface do usuário, como a capacidade de criar e enumerar janelas de ferramentas ou janelas de documentos ou relatar um erro ao usuário.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|Fornece acesso à barra de status do IDE.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|Usado para implementar o modelo de automação. No modelo de projeto, você retornará um objeto de propriedades que permite criar uma instância desse objeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|Usado para implementar eventos da área de transferência no objeto Project na hierarquia. `SVsUIHierWinClipboardHelper` permite que você manipule corretamente as operações de recortar, copiar e colar.|

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [Lista de verificação: Criando tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Não está no Build: usando classes de projeto HierUtil7 para implementar um tipo de projeto (C++)](/previous-versions/bb166212(v=vs.100))
- [Suporte a ferramentas de navegação de símbolo](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [Elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md)
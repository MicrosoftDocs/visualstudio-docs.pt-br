---
title: Componentes principais do modelo de projeto | Microsoft Docs
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
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 70cb00e6d2ecae8ba5fb8abefb76f7061406f0fd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741325"
---
# <a name="project-model-core-components"></a>Componentes principais do projeto modelo
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

As tabelas a seguir expandem o modelo de projeto. As tabelas presentes breves descrições das interfaces e serviços identificados no modelo e as interfaces e os serviços associados a objetos específicos. Além disso, as tabelas de detalham sobre outras interfaces que são opcionais na criação do projeto e na manutenção dependendo dos requisitos do seu tipo de projeto específico.  
  
 Para obter mais informações, consulte [ferramentas de navegação de símbolo que dão suporte a](../../extensibility/internals/supporting-symbol-browsing-tools.md).  
  
### <a name="package-object"></a>Objeto de pacote  
  
|Interface|Comentários|  
|---------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|Inicializa um VSPackage no IDE e disponibiliza seus serviços ao IDE.|  
  
### <a name="project-factory-object"></a>Objeto de fábrica de projeto  
  
|Interface|Comentários|  
|---------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|Gerencia a criação de novos projetos e abrir projetos existentes.|  
  
### <a name="project-objects"></a>Objetos do projeto  
  
|Interfaces|Comentários|  
|----------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|Gerencia a adição e remoção de itens de projeto, abre os editores e mantém o mapeamento entre cada moniker do documento e o `VSITEMID`. Herda de `IVsProject` e `IVsProject2`.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|Gerencia as propriedades de navegação e exibição e fornece eventos.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|Habilita o comando execução semelhante do `IOleCommandTarget` para comandos como Recortar e renomeação que se aplicam somente quando o foco está no Gerenciador de soluções.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Serve como a interface de destino do comando primário para uma hierarquia do projeto. É a interface padrão para consultar os objetos para os comandos de status ou o estado e a execução do comando. Disponível quando você não se concentram na janela do projeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Coordena a persistência do estado do projeto. Normalmente, o estado do projeto é armazenado como um arquivo de projeto, mas pode ser adaptado aos sistemas de armazenamento que não são baseados em arquivo.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|Permite que o projeto para gerenciar todos os aspectos de persistência para seus itens de projeto, como arquivos no disco ou objetos em outros sistemas de armazenamento. O `IVsPeristHierarchyItem2` interface é usada para itens que não implementam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> interface.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|Coordena as interações com o controle do código fonte.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|Permite que os projetos gerenciar informações de configuração.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|Gerencia objetos de configuração do projeto, como configurações de depuração/versão. Compilar, implantar e depurar as operações são coordenadas por meio de objetos de configuração do projeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|Implementado por hierarquias para controlar a exclusão (destrutiva) ou remover opções (não-destrutiva) para itens de hierarquia. Chamar a Interface de consulta na `IVsHierarchyDeleteHandler` da interface do `IVsHierarchy` interface.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|Fornece a opção de implementação de ter o objeto que suporta o `IVsCfgProvider2` interface em uma identidade diferente COM o objeto de projeto que implementa o `IVsHierarchy` interface.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|Interface opcional implementada para tornar o seu projeto extensível por outros desenvolvedores. O `IVsProjectStartupServices` interface permite que um VSPackage de terceiros registrar um GUID que você persistir em seu arquivo de projeto para que toda vez que o projeto for carregado, você carrega o GUID do serviço de terceiros em seu arquivo de projeto e chame `QueryService` para GUID.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|Implementado por hierarquias de origem em um `UIHierarchy` janela para coordenar operações de área de transferência, como Recortar, copiar e colar. Use o `AdviseClipboardHelperEvents` interface para registrar eventos de área de transferência.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|Fornece informações sobre um item arrastado em relação à fonte de dados durante uma operação de arrastar e soltar em uma janela de hierarquia de interface do usuário. Chamado a partir de `IVsHierarchy` interface.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|Fornece informações sobre um item arrastado em relação ao seu destino de soltar durante uma operação de arrastar e soltar em uma janela de hierarquia de interface do usuário. Chamado a partir de `IVsHierarchy` interface.|  
  
### <a name="configuration-object"></a>Objeto de configuração  
  
|Interfaces|Comentários|  
|----------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|Fornece informações sobre uma configuração.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|Permite que os projetos gerenciar informações de configuração.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|Permite que um projeto ser executado sob o controle do depurador.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|Quando implementado por projetos de implantação que executam operações de implantação para outros projetos.|  
  
### <a name="configuration-builder-object"></a>Objeto do construtor de configuração  
  
|Interfaces|Comentários|  
|----------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|Gerencia a operação de criação de uma configuração projeto.|  
  
### <a name="additional-project-objects"></a>Objetos de projeto adicionais  
  
|Interfaces|Comentários|  
|----------------|--------------|  
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|Exibe propriedades de item de **propriedades** janela.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|Exibe as saídas para a implantação.|  
  
 A tabela a seguir apresenta descrições breves dos serviços identificados no modelo de projeto.  
  
### <a name="services"></a>Serviços  
  
|Serviço|Comentários|  
|-------------|--------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|Usado pelo VSPackages que implementam os tipos de projeto para registrar que sua fábrica de projeto existe com o IDE. O VSPackage deverá chamar `QueryService` para este serviço e registrar sua fábrica de projeto quando `IVsPackage::SetSite` método é chamado. Se o `SetSite` método não é chamado, o projeto não seja instanciado.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|Fornece acesso a noção de interna, interna do IDE da solução atual, como a capacidade de enumerar os projetos, criar novos projetos, observar a alterações no projeto e assim por diante.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|Chamado por projetos que desejarem participar no controle de origem.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|Mantém uma tabela de documentos abertos para determinar se um ou mais dos seus itens de projeto já estiverem aberto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|Contém as interfaces e métodos chamados para, na verdade, abrir um item de projeto usando o editor padrão ou um editor específico.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|Deve ser chamado por todos os projetos ao adicionar, remover ou renomear os seus itens.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|Gerencia alterações em um arquivo ou diretório e notifica os clientes quando os arquivos selecionados foram alterados no disco.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|Deve ser chamado por todos os projetos e editores antes que eles sujos itens ou salvá-los.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|Gerencia a ordem das operações de compilação e implantação para configurações do projeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|Fornece acesso aos serviços do depurador de baixo nível usada para a maioria dos controles de depuração.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|Habilita o acesso de VSPackages para obter informações sobre as seleções atuais e permite a comunicação com o **propriedades** janela.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|Fornece a funcionalidade básica do IDE relacionados à interface do usuário, como a capacidade de criar e enumerar as janelas de ferramentas ou janelas de documento ou relatar um erro ao usuário.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|Fornece acesso à barra de status do IDE.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|Usado para implementar o modelo de automação. Em seu modelo de projeto, você retornará um objeto de propriedades que permite que você cria uma instância desse objeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|Usado para implementar eventos de área de transferência no objeto na hierarquia do projeto. `SVsUIHierWinClipboardHelper` permite que você corretamente identificador recortar, copiar e colar operações.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Não está em compilação: usando Classes do projeto HierUtil7 para implementar um tipo de projeto (C++)](http://msdn.microsoft.com/en-us/a5c16a09-94a2-46ef-87b5-35b815e2f346)   
 [Suporte a ferramentas de navegação de símbolo](../../extensibility/internals/supporting-symbol-browsing-tools.md)   
 [Elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md)


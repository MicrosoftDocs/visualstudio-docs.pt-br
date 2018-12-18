---
title: Inicialização do Designer e configuração de metadados | Microsoft Docs
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
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8f5a4bbd24e571100dfc708d7c34f87b6c84adcf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736218"
---
# <a name="designer-initialization-and-metadata-configuration"></a>Inicialização do designer e a configuração de metadados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Manipulação dos atributos de metadados e o filtro associado a um designer ou um componente do designer fornece um mecanismo para aplicativos definam quais ferramentas são usadas por um designer específico para lidar com diferentes <xref:System.Type> objetos (como estruturas de dados classes ou entidades gráficas), quando o designer está disponível e como o IDE do Visual Studio está configurado para suportar o designer (para instância que **caixa de ferramentas** categoria ou o guia está disponível).  
  
 O [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] fornece vários mecanismos para facilitar o controle de inicialização do designer ou o componente de designer e a manipulação de seus metadados por um VSPackage.  
  
## <a name="initializing-metadata-and-configuration-information"></a>Inicializando os metadados e informações de configuração  
 Como eles são carregados sob demanda, VSPackages talvez não foram carregados pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente antes da instanciação de um designer. Portanto, os VSPackages não é possível usar o mecanismo padrão para a configuração de um designer ou um componente de designer a criação, que é lidar com um <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> eventos. Em vez disso, um VSPackage implementa uma instância da <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> de interface e se registra para fornecer personalizações, conhecidas como extensões de superfície de design.  
  
### <a name="customizing-initialization"></a>Personalizando a inicialização  
 Personalizar um designer, um componente ou uma superfície de design, envolve:  
  
1.  Modificando metadados de designer e alterando efetivamente como um determinado <xref:System.Type> é acessado ou convertidos.  
  
     Isso normalmente é feito por meio de <xref:System.Drawing.Design.UITypeEditor> ou <xref:System.ComponentModel.TypeConverter> mecanismos.  
  
     Por exemplo, quando <xref:System.Windows.Forms>-designers com base são inicializados, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente modifica a <xref:System.Drawing.Design.UITypeEditor> para <xref:System.Web.UI.WebControls.Image> objetos usados com o designer para usar o Gerenciador de recursos para obter bitmaps em vez do sistema de arquivos.  
  
2.  A integração com o ambiente, por exemplo, Assinando eventos ou a obtenção de informações de configuração do projeto. Você pode obter informações de configuração do projeto e assinar eventos, obtendo o <xref:System.ComponentModel.Design.ITypeResolutionService> interface.  
  
3.  Modificação do ambiente do usuário por meio da ativação apropriada **caixa de ferramentas** categorias ou restringindo a aplicabilidade do designer, aplicando uma instância da <xref:System.ComponentModel.ToolboxItemFilterAttribute> classe para o designer.  
  
### <a name="designer-initialization-by-a-vspackage"></a>Inicialização do designer por um VSPackage  
 Um VSPackage deve lidar com a inicialização do designer por:  
  
1. Criação de um objeto que implementa o <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> classe.  
  
   > [!NOTE]
   >  O <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> classe nunca deve ser implementada no mesmo objeto como o <xref:Microsoft.VisualStudio.Shell.Package> classe.  
  
2. Registrar a classe que implementa <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> como fornecendo suporte para extensões do designer do VSPackage, aplicando as instâncias do <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>, <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> e <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> para a classe que fornece a implementação do VSPackage de <xref:Microsoft.VisualStudio.Shell.Package> .  
  
   Sempre que qualquer designer ou o componente de designer é criado, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente:  
  
3. Acessa a cada provedor de extensão de superfície de design registrado.  
  
4. Cria uma instância e inicializa uma instância de cada provedor de extensão de superfície de design <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> objeto  
  
5. Chama cada provedor de extensão de superfície de design <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> método ou <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> método (conforme apropriado).  
  
   Ao implementar o <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> do objeto como um membro de um VSPackage, é importante entender que:  
  
6. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente não fornece nenhum controle sobre quais metadados ou outras definições de configuração um determinado `DesignSurfaceExtension` modifica do provedor. É possível que dois ou mais `DesignSurfaceExtension` provedores modificando o mesmo designer de recursos de maneiras conflitantes, com a modificação final que está sendo definitiva. Não é possível determinar qual modificação é aplicada pela última vez.  
  
7. É possível restringir explicitamente uma implementação do <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> designers específicos, por meio da aplicação de instâncias do objeto <xref:System.ComponentModel.ToolboxItemFilterAttribute> para que a implementação. Para obter mais informações sobre **caixa de ferramentas** filtragem de itens, consulte o <xref:System.ComponentModel.ToolboxItemFilterAttribute> e <xref:System.ComponentModel.ToolboxItemFilterType>.  
  
## <a name="additional-metadata-provisioning"></a>Provisionamento de metadados adicionais  
 Um VSPackage pode alterar a configuração de um designer ou um componente de designer diferente de em tempo de design.  
  
 O <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> classe pode ser usada de forma programática, ou ser aplicada a um VSPackage fornecendo um designer.  
  
 Uma instância da <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> classe é usada para modificar os metadados de componentes criados em uma superfície de design. Por exemplo, um pode substituir um navegador de propriedade padrão usado pelo <xref:System.Windows.Forms.CommonDialog> objetos, com um navegador de propriedade personalizada.  
  
 Modificações fornecidas por uma instância de <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> aplicado a implementação de um VSPackage <xref:Microsoft.VisualStudio.Shell.Package> pode ter um dos dois escopos:  
  
- Global – para todas as novas instâncias de um determinado componente  
  
- Local – referindo-se apenas à instância do componente criado em uma superfície de design fornecida pelo VSPackage atual.  
  
  O `IsGlobal` propriedade do <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> instância aplicada a implementação de um VSPackage <xref:Microsoft.VisualStudio.Shell.Package> determina esse escopo.  
  
  Aplicando o atributo para uma implementação de <xref:Microsoft.VisualStudio.Shell.Package> com o <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> propriedade da <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> objeto definido como `true`, conforme mostrado abaixo, altera o navegador para todo o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente:  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
  Se o sinalizador global foi definido como `false`, em seguida, a alteração de metadados é local para o designer atual com suporte pelo VSPackage atual:  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
> [!NOTE]
>  No momento, a superfície de design somente dá suporte à criação de componentes e, portanto, somente os componentes podem ter metadados locais. No exemplo acima, podemos estava tentando executar modificar uma propriedade, como o `Color` propriedade de um objeto. Se `false` foi passado para o sinalizador global, `CustomBrowser` nunca seria exibido porque o designer, na verdade, nunca cria uma instância de `Color`. Definir o sinalizador global para `false` é útil para componentes, como controles, temporizadores e caixas de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>   
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>   
 <xref:System.ComponentModel.ToolboxItemFilterType>   
 [Estendendo o suporte ao tempo de design](http://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)


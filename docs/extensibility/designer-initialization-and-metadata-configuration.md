---
title: Configuração de metadados e inicialização do designer | Microsoft Docs
description: Saiba como o SDK do Visual Studio facilita o controle de inicialização de um designer ou de um componente de designer e seus metadados por um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13c65913fe54b9c22eb8fa374b7a16de84438e33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091273"
---
# <a name="designer-initialization-and-metadata-configuration"></a>Configuração de metadados e inicialização do designer

A manipulação dos metadados e dos atributos de filtro associados a um designer ou componente de designer fornece um mecanismo para que os aplicativos definam quais ferramentas são usadas por um designer específico para lidar com <xref:System.Type> objetos diferentes (como estruturas de dados, classes ou entidades gráficas), quando o designer está disponível e como o IDE do Visual Studio está configurado para dar suporte ao designer (por exemplo, a categoria de **caixa** de

O [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] fornece vários mecanismos para facilitar o controle de inicialização de um designer ou de um componente de designer e a manipulação de seus metadados por um VSPackage.

## <a name="initialize-metadata-and-configuration-information"></a>Inicializar informações de metadados e configuração
 Como eles são carregados sob demanda, o VSPackages pode não ter sido carregado pelo ambiente do Visual Studio antes da instanciação de um designer. Portanto, VSPackages não pode usar o mecanismo padrão para configurar um designer ou componente de designer na criação, que é para manipular um <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> evento. Em vez disso, um VSPackage implementa uma instância da <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> interface e se registra para fornecer personalizações, conhecidas como extensões de superfície de design.

### <a name="customize-initialization"></a>Personalizar inicialização

A personalização de um designer, um componente ou uma superfície de designer envolve:

1. Modificar os metadados do designer e alterar efetivamente o modo como um determinado <xref:System.Type> é acessado ou convertido.

    Normalmente, isso é feito por meio dos <xref:System.Drawing.Design.UITypeEditor> <xref:System.ComponentModel.TypeConverter> mecanismos ou.

    Por exemplo, quando <xref:System.Windows.Forms> designers baseados em são inicializados, o ambiente do Visual Studio modifica o <xref:System.Drawing.Design.UITypeEditor> para <xref:System.Web.UI.WebControls.Image> objetos usados com o designer para usar o Gerenciador de recursos para obter bitmaps em vez do sistema de arquivos.

2. Integração com o ambiente, por exemplo, inscrevendo-se em eventos ou obtendo informações de configuração do projeto. Você pode obter informações de configuração do projeto e assinar eventos obtendo a <xref:System.ComponentModel.Design.ITypeResolutionService> interface.

3. Modificação do ambiente do usuário ativando as categorias de **caixa de ferramentas** apropriadas ou restringindo a aplicabilidade do designer aplicando uma instância da <xref:System.ComponentModel.ToolboxItemFilterAttribute> classe ao designer.

### <a name="designer-initialization-by-a-vspackage"></a>Inicialização do designer por um VSPackage

Um VSPackage deve tratar a inicialização do designer por:

1. Criando um objeto que implementa a <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> classe.

   > [!NOTE]
   > A <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> classe nunca deve ser implementada no mesmo objeto que a <xref:Microsoft.VisualStudio.Shell.Package> classe.

2. Registrando a classe que implementa <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> como fornecer suporte para as extensões de designer do VSPackage. Registre a classe aplicando instâncias de  <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute> , <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> e <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> à classe que fornece a implementação de VSPackage de <xref:Microsoft.VisualStudio.Shell.Package> .

Sempre que um designer ou componente de designer é criado, o ambiente do Visual Studio:

- Acessa cada provedor de extensão de superfície de design registrado.

- Instancia e Inicializa uma instância de cada objeto do provedor de extensão da superfície de design <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> .

- Chama cada método ou método do provedor de extensão da superfície de design <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> (conforme apropriado).

Ao implementar o <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> objeto como membro de um VSPackage, é importante entender que:

- O ambiente do Visual Studio não fornece nenhum controle sobre quais metadados ou outras definições de configuração `DesignSurfaceExtension` são modificadas por um determinado provedor. É possível que dois ou mais `DesignSurfaceExtension` provedores modifiquem o mesmo recurso de designer de maneiras conflitantes, com a modificação final sendo definitiva. É indeterminado qual modificação é aplicada pela última vez.

- É possível restringir explicitamente uma implementação do <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> objeto a designers específicos aplicando instâncias do <xref:System.ComponentModel.ToolboxItemFilterAttribute> à implementação. Para obter mais informações sobre a filtragem de itens da **caixa de ferramentas** , consulte o <xref:System.ComponentModel.ToolboxItemFilterAttribute> e o <xref:System.ComponentModel.ToolboxItemFilterType> .

## <a name="additional-metadata-provisioning"></a>Provisionamento de metadados adicional

Um VSPackage pode alterar a configuração de um designer ou componente de designer que não seja em tempo de design.

A <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> classe pode ser usada programaticamente ou aplicada a um VSPackage que fornece um designer.

Uma instância da <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> classe é usada para modificar os metadados dos componentes criados em uma superfície de design. Por exemplo, é possível substituir um navegador de propriedades padrão usado por <xref:System.Windows.Forms.CommonDialog> objetos por um navegador de propriedades personalizado.

As modificações fornecidas por uma instância do <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> aplicada à implementação de uma VSPackage de <xref:Microsoft.VisualStudio.Shell.Package> podem ter um dos dois escopos:

- Global--para todas as novas instâncias de um determinado componente

- Local – pertencente somente à instância do componente criado em uma superfície de design fornecida pelo VSPackage atual.

A `IsGlobal` propriedade da <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> instância aplicada a uma implementação de VSPackage <xref:Microsoft.VisualStudio.Shell.Package> determina esse escopo.

A aplicação do atributo a uma implementação de <xref:Microsoft.VisualStudio.Shell.Package> com a <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> Propriedade do <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> objeto definido como `true` , como abaixo, altera o navegador para todo o ambiente do Visual Studio:

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

Se o sinalizador global tiver sido definido como `false` , a alteração de metadados será local para o designer atual com suporte no VSPackage atual:

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> A superfície de design só dá suporte à criação de componentes e, portanto, somente os componentes podem ter metadados locais. No exemplo acima, estávamos tentando modificar uma propriedade, como a `Color` propriedade de um objeto. Se `false` foi passado para o sinalizador global, `CustomBrowser` nunca apareceria porque o designer nunca cria uma instância do `Color` . Definir o sinalizador global como `false` é útil para componentes, como controles, temporizadores e caixas de diálogo.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [Estender o suporte ao tempo de design](/previous-versions/37899azc(v=vs.140))
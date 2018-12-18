---
title: Fornecendo informações de pacote e implantação em itens de projeto | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SafeControlEntries
- VS.SharePointTools.Project.ProjectOutputReference
- VS.SharePointTools.Project.FeatureProperties
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature properties
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
- feature properties [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature receiver
- feature receiver [SharePoint development in Visual Studio]
- safe controls [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e4ce9f864307ffaee4bce51a565e9ad1726d043d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893293"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>Fornecer informações de empacotamento e implantação em itens de projeto
  Todos os itens de projeto do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] têm propriedades que você pode usar para fornecer dados adicionais quando o projeto é implantado no SharePoint. Estas são as seguintes propriedades:  
  
- Propriedades do recurso  
  
- Receptores de recurso  
  
- Referências de saída do projeto  
  
- Entradas de controle seguro  
  
  Essas propriedades aparecem na **propriedades** janela.  
  
## <a name="feature-properties"></a>Propriedades do recurso
 Use o **propriedades do recurso** propriedade para especificar os dados que usa o recurso. Dados de propriedades de recurso são um conjunto de valores (armazenados como pares chave/valor) que está incluído com um recurso quando ele é implantado no SharePoint. Depois que o recurso é implantado, você pode acessar os valores de propriedade em seu código.  
  
 Quando você adiciona um valor de propriedade de recurso para um item de projeto, o valor é adicionado como um elemento no manifesto do recurso do item. Em um projeto de modelo de conectividade de dados comerciais (BDC), por exemplo, a propriedade de recurso ModelFileName aparece como:  
  
```xml  
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />   
```  
  
 Depois de definir um valor da propriedade de recurso, ele é adicionado como um elemento FeatureProperty do projeto *. spdata* arquivo. Para obter informações sobre como acessar as propriedades no SharePoint, consulte [SPFeaturePropertyCollection classe](http://go.microsoft.com/fwlink/?LinkId=177391).  
  
 Os valores de propriedade de recurso idênticos de todos os itens de projeto são mesclados no manifesto do recurso. No entanto, se dois itens de projeto diferente especificam a mesma chave de propriedade de recurso com valores não correspondentes, ocorre um erro de validação.  
  
 Para adicionar propriedades de recurso diretamente para o arquivo de recurso (*Feature*), chame o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] método de modelo de objeto SharePoint <xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A>. Se você usar esse método, lembre-se de que a mesma regra sobre como adicionar valores de propriedade de recurso idênticos nas propriedades de recurso também se aplica a propriedades adicionadas diretamente ao arquivo de recurso.  
  
## <a name="feature-receiver"></a>Receptor de recurso
 Receptores de recurso são o código que é executado quando determinados eventos ocorrem em um item de projeto que contém recursos. Por exemplo, você pode definir os receptores de recurso que são executadas quando o recurso é instalado, ativado ou atualizado. É uma maneira de adicionar um receptor de recurso é adicioná-lo diretamente para um recurso, conforme descrito em [instruções passo a passo: Adicionar receptores de evento](../sharepoint/walkthrough-add-feature-event-receivers.md). Outra maneira é um nome de classe do receptor de recurso e o assembly de referência a **receptor do recurso** propriedade.  
  
### <a name="direct-method"></a>Método direto
 Ao adicionar um receptor de recurso diretamente a um recurso, um arquivo de código está sob o **recurso** nó no Gerenciador de soluções. Quando você compila sua solução do SharePoint, o código é compilado em um assembly e implanta para o SharePoint. Por padrão, as propriedades de recurso **Assembly do receptor** e **classe receptora** o nome de classe e o assembly de referência.  
  
### <a name="reference-method"></a>Método Reference
 Outra maneira de adicionar um receptor de recurso é usando o **receptor do recurso** propriedade de um item de projeto para referenciar um assembly de receptor de recurso. O valor da propriedade de receptor de recurso possui duas subpropriedades: **Assembly** e **nome da classe**. O assembly deve usar sua totalmente qualificado, nome "forte" e o nome de classe devem ser o nome completo do tipo. Para obter mais informações, consulte [Assemblies com nome forte](http://go.microsoft.com/fwlink/?LinkID=169573). Depois de implantar a solução para o SharePoint, o recurso usa o receptor do recurso referenciado para manipular eventos de recurso.  
  
 Solução de valores de propriedade do destinatário no recurso de tempo, o recurso de compilação e seus projetos de mesclagem em conjunto para definir os atributos ReceiverAssembly e ReceiverClass do elemento recurso no manifesto do recurso de solução do SharePoint (*. wsp* ) arquivos. Portanto, se os valores de propriedade do Assembly e o nome de classe de um item de projeto e um recurso forem especificados, os valores de propriedade de recurso e de item de projeto devem corresponder. Se os valores não corresponderem, você receberá um erro de validação. Se você quiser que um item de projeto para referenciar um assembly de receptor de recurso diferente daquele usa seu recurso, movê-lo para outro recurso.  
  
 Se você referenciar um assembly de receptor de recurso que não ainda esteja no servidor, você também deve incluir o arquivo de assembly no pacote; [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não adicioná-lo para você. Quando você implanta o recurso, o arquivo de assembly é copiado para que o sistema [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] ou a pasta Bin no diretório físico do SharePoint. Para obter mais informações, consulte como: [como: adicionar e remover assemblies adicionais](../sharepoint/how-to-add-and-remove-additional-assemblies.md).  
  
 Para obter mais informações sobre os receptores de recurso, consulte [receptor de evento de recurso](http://go.microsoft.com/fwlink/?LinkID=169574) e [eventos de recurso](http://go.microsoft.com/fwlink/?LinkID=169575).  
  
## <a name="project-output-references"></a>Referências de saída do projeto
 A propriedade Project Output References Especifica uma dependência, como um assembly, o que o item de projeto precisa ser executada. Por exemplo, suponha que sua solução tiver um projeto do BDC e um projeto de classe. Se o projeto BDC tem uma dependência no assembly que é produzido pelo projeto de classe, você pode referenciar o assembly na propriedade do Project Output References do projeto BDC. Quando o projeto do BDC é empacotado, o assembly dependente está incluído no pacote.  
  
 Referências de saída do projeto geralmente são assemblies, mas em alguns casos (por exemplo, projetos do Silverlight) pode ser outros tipos de arquivo.  
  
 Para obter mais informações, consulte [como: adicionar uma referência de saída do projeto](../sharepoint/how-to-add-a-project-output-reference.md).  
  
## <a name="safe-control-entries"></a>Entradas de controle seguro
 O SharePoint fornece um mecanismo de segurança, chamado de entradas de controle seguro, para limitar o acesso de usuários não confiáveis para certos controles. Por design, o SharePoint permite que usuários não confiáveis carregar e criar páginas ASPX no servidor do SharePoint. Para impedir que esses usuários adicionando o código não seguro para páginas ASPX, o SharePoint limita seu acesso a *controles seguros*. Controles seguros são controles ASPX e Web parts designadas como seguras e que pode ser usado por qualquer usuário em seu site. Para obter mais informações, consulte [etapa 4: adicionar a Web Part à lista de controles seguros](http://go.microsoft.com/fwlink/?LinkID=171014).  
  
 Cada item de projeto do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] tem uma propriedade chamada **entradas de controle seguro** que tem duas subpropriedades de Boolean: **seguro** e **seguro contra Script**. A propriedade de segurança Especifica se os usuários não confiáveis podem acessar um controle. A propriedade de segurança contra Script Especifica se os usuários não confiáveis podem exibir e alterar propriedades de um controle.  
  
 Entradas de controle de segurança são referenciadas em uma base do assembly. Adicionar entradas de controle seguro ao assembly do projeto inserindo-os no item de projeto **entradas de controle seguro** propriedade. No entanto, você também pode adicionar entradas de controle seguro ao assembly do projeto por meio de **avançado** guia o **Package Designer** quando você adiciona um assembly adicional para o pacote. Para obter mais informações, consulte [como: marcar controles como controles seguros](../sharepoint/how-to-mark-controls-as-safe-controls.md) ou [Registrando um Assembly de Web Part como um controle seguro](http://go.microsoft.com/fwlink/?LinkID=171013).  
  
### <a name="xml-entries-for-safe-controls"></a>Entradas XML para controles seguros
 Quando você adiciona uma entrada de controle seguro para um item de projeto ou assembly do projeto, uma referência é gravada para o manifesto do pacote no seguinte formato:  
  
```xml  
<Assemblies>  
    <Assembly Location="<assembly name>.dll"     
      DeploymentTarget="<'GlobalAssemblyCache' or 'WebApplication'">>  
        <SafeControls>  
            <SafeControl Assembly="<assembly name>.dll" Namespace=  
              "<SharePoint project name>" Safe="<true/false>"     
                TypeName="<control name>"   
                SafeAgainstScript="<true/false>" />  
        </SafeControls>  
    </Assembly>  
</Assemblies>  
```  
  
## <a name="see-also"></a>Consulte também
 [Pacote e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)   
 [Usar módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md)   
 [Estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md)  

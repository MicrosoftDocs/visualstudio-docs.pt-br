---
title: Gerenciando referências em um projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.ProjectPropertiesReferencePaths
- cs.ProjectPropertiesReferencePaths
helpviewer_keywords:
- Visual C# projects, references
- referencing objects, project references
- external component references
- referencing namespaces
- Visual Basic projects, references
- referencing components, external components
- Web references, types of project references
- namespaces [Visual Studio], referencing
- COM components, referencing
- objects [Visual Studio], referencing
ms.assetid: 05d1c51b-44f3-4973-8a11-6c919b08ad62
caps.latest.revision: 55
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 10fed2fa77274469a7b82a1583e825c57ca4a581
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195592"
---
# <a name="managing-references-in-a-project"></a>Gerenciando referências em um projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Antes de escrever código em um componente externo ou um serviço conectado, o projeto primeiro deve conter uma referência a ele. Basicamente, uma referência é uma entrada em um arquivo de projeto que contém as informações de que o Visual Studio precisa para localizar o componente ou o serviço.  
  
 Para adicionar uma referência, clique com o botão direito do mouse no nó Referências no Gerenciador de Soluções e escolha **Adicionar Referência**. Para obter mais informações, consulte [Como adicionar ou remover referências usando o Gerenciador de Referências](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md).  
  
 ![Adicionar uma referência no Visual C&#43;&#43;](../ide/media/vs2015-cpp-add-reference.png "vs2015_cpp_add_reference")  
  
 É possível fazer uma referência aos seguintes tipos de componentes/serviços:  
  
-   Referências de aplicativo da Windows Store  
  
-   Bibliotecas de classes ou assemblies do .NET Framework  
  
-   componentes COM  
  
-   Outros assemblies ou bibliotecas de classes de projetos na mesma solução  
  
-   Serviços Web XML  
  
## <a name="windows-store-app-references"></a>Referências de aplicativo da Windows Store  
  
### <a name="project-references"></a>Referências de Projeto  
 Projetos UWP (Plataforma Universal do Windows) que se destinam ao Windows 10 podem criar referências a outros projetos UWP na solução, ou a projetos ou binários da Windows Store que se destinam a [!INCLUDE[win81](../includes/win81-md.md)], desde que esses projetos não usem APIs que foram preteridas no Windows 10. Para obter mais informações, consulte [Mover do Windows Runtime 8 para a UWP](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx).  
  
 Se você optar por redirecionar os projetos [!INCLUDE[win81](../includes/win81-md.md)] para o Windows 10, consulte [Portando, migrando e atualizando projetos do Visual Studio](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)  
  
### <a name="extension-sdk-references"></a>Referências do SDK de Extensão  
 Projetos do Visual Basic, C#, C++ e JavaScript da Windows Store que se destinam à UWP (Plataforma do Windows Universal) podem referenciar SDKs de Extensão que se destinam a [!INCLUDE[win81](../includes/win81-md.md)], desde que esses SDKs de Extensão não usem APIs que foram preteridas no Windows 10. Confira o site do fornecedor do SDK de Extensão para descobrir se ele pode ser referenciado por projetos da Windows Store que se destinam à UWP.  
  
 Se você determinar que não há suporte para o SDK de Extensão que está sendo referenciado pelo aplicativo, é necessário realizar as seguintes etapas:  
  
1.  Observe o nome do projeto que está causando o erro. A plataforma de destino do projeto é indicada entre parênteses ao lado do nome do projeto. Por exemplo, **MyProjectName (Windows 8.1)** significa que o projeto **MyProjectName** se destina à versão da plataforma [!INCLUDE[win81](../includes/win81-md.md)].  
  
2.  Acesse o site do fornecedor que é proprietário do SDK de Extensão sem suporte e instale a versão do SDK de Extensão com dependências que são compatíveis com a versão da plataforma de destino do projeto.  
  
    > [!NOTE]
    >  Uma maneira de descobrir se um SDK de Extensão tem dependências em outros SDKs de Extensão é reiniciar o Visual Studio, criar um novo projeto do C# da Windows Store, clicar com o botão direito do mouse no projeto e escolher **Adicionar Referência**, acessar a guia **Windows**, acessar a subguia **Extensões**, selecionar o SDK de Extensão e examinar o painel direito no **Gerenciador de Referências**. Se ele tiver dependências, elas serão listadas no painel.  
  
    > [!IMPORTANT]
    >  Se seu projeto está direcionando o Windows 10 e o SDK de extensão instalado na etapa anterior tem uma dependência no pacote de tempo de execução do Microsoft Visual C++, a versão do Microsoft Visual C++ Runtime Package que seja compatível com o Windows 10 será v14.0 e está instalada com o Visual Studio 2015.  
  
3.  Se o SDK de Extensão instalado na etapa anterior tiver dependências de outros SDKs de Extensão, acesse os sites dos fornecedores proprietários das dependências e instale as versões dessas dependências compatíveis com a versão da plataforma de destino do projeto.  
  
4.  Reinicie o Visual Studio e abra o aplicativo.  
  
5.  Clique com o botão direito do mouse no nó **Referências** do projeto que causou o erro e escolha **Adicionar Referência**  
  
6.  Clique na guia **Windows** e, em seguida, na subguia **Extensões**. Depois, desmarque as caixas de seleção dos SDKs de Extensão antigos e marque as caixas de seleção dos novos SDKs de Extensão. Clique em **OK**.  
  
## <a name="adding-a-reference-at-design-time"></a>Adicionando uma referência em tempo de design  
 Ao fazer uma referência a um assembly no projeto, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pesquisa o assembly nos seguintes locais:  
  
-   O diretório atual do projeto. (É possível encontrar esses assemblies usando a guia **Procurar**.)  
  
-   Outros diretórios do projeto na mesma solução. (É possível encontrar esses assemblies na guia **Projetos**.)  
  
> [!NOTE]
>  Todos os projetos contêm uma referência implícita a mscorlib. Os projetos do Visual Basic contêm uma referência implícita a `Microsoft.VisualBasic`.  
>   
>  Todos os projetos do Visual Studio contêm uma referência implícita a `System.Core`, mesmo se `System.Core` foi removido da lista de referências.  
  
## <a name="references-to-shared-components-at-run-time"></a>Referências a componentes compartilhados em tempo de execução  
 Em tempo de execução, componentes devem estar no caminho de saída do projeto ou nos [Cache de Assembly Global](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202) (GAC). Se o projeto contiver uma referência a um objeto que não está em um desses locais, será necessário copiar a referência para o caminho de saída do projeto ao compilá-lo. A propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> indica se esta cópia precisa ser feita. Se o valor for **True**, a referência será copiada para o diretório do projeto durante o build do projeto. Se o valor for **False**, a referência não será copiada.  
  
 Se você implantar um aplicativo que contenha uma referência a um componente personalizado que esteja registrado no GAC, o componente não será implantado com o aplicativo, independentemente da configuração de <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A>. Nas versões anteriores do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], era possível definir a propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> em uma referência para garantir que o assembly fosse implantado. Agora, é necessário adicionar o assembly à pasta \Bin manualmente. Isso coloca todo o código personalizado sob análise, reduzindo o risco de publicar um código personalizado com o qual você não está familiarizado.  
  
 Por padrão, a propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> será definida como **False** se o assembly ou o componente estiver no cache de assembly global ou for um componente de estrutura. Caso contrário, o valor será definido como **True**. Referências projeto a projeto são sempre definidas como **True**.  
  
## <a name="referencing-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>Referenciando um projeto ou assembly que tem outra versão do .NET Framework como destino  
 É possível criar aplicativos que referenciam projetos ou assemblies que têm outra versão do .NET Framework como destino. Por exemplo, é possível criar um aplicativo que tem como destino o [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] que referencia um assembly que tem como destino [!INCLUDE[dnprdnext](../includes/dnprdnext-md.md)]. Se você criar um projeto que tem como destino uma versão anterior do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], não será possível definir uma referência no projeto a um projeto ou assembly que tem como destino o [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] ou o .NET Framework versão 4.  
  
 Para obter mais informações, consulte [Definindo uma versão específica do .NET Framework como destino](../ide/targeting-a-specific-dotnet-framework-version.md).  
  
## <a name="project-to-project-references"></a>Referências projeto a projeto  
 Referências projeto a projeto são referências a projetos que contêm assemblies; é possível criá-las usando a guia **Projeto**. O Visual Studio pode encontrar um assembly quando receber um caminho para o projeto.  
  
 Quando você tiver um projeto que produz um assembly, será necessário referenciar o projeto e não usar uma referência de arquivo (consulte abaixo). A vantagem de uma referência projeto a projeto é que ela cria uma dependência entre os projetos no sistema de build. O projeto dependente será compilado se ele tiver sido alterado desde a última vez que o projeto de referência foi compilado. Uma referência de arquivo não cria uma dependência de build e, portanto, é possível compilar o projeto de referência sem compilar o projeto dependente, e a referência pode se tornar obsoleta. (Ou seja, o projeto pode referenciar uma versão anteriormente compilada do projeto.) Isso pode resultar na exigência de várias versões de uma única DLL no diretório bin, o que não é possível. Quando houver esse conflito, você verá uma mensagem como [Aviso: o “arquivo” de dependência no projeto “projeto” não pode ser copiado para o diretório de execução, pois ele substituirá o “arquivo” de referência](../misc/warning-the-dependency-file-in-project-project-cannot-be-copied-to-the-run-directory-because-it-would-overwrite-the-reference-file.md). Para obter mais informações, consulte [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md) e [Como criar e remover dependências de projeto](../ide/how-to-create-and-remove-project-dependencies.md).  
  
> [!NOTE]
>  Uma referência de arquivo será criada em vez de uma referência projeto a projeto se a versão de destino do .NET Framework de um projeto for a versão 4.5 e a versão de destino do outro projeto for a versão 2, 3, 3.5 ou 4.0.  
  
## <a name="file-references"></a>Referências de arquivo  
 Referências de arquivo são referências diretas a assemblies fora do contexto de um projeto do Visual Studio; crie-as usando a guia **Procurar** do **Gerenciador de Referências**. Use uma referência de arquivo quando você tiver apenas um assembly ou um componente e não tiver o projeto que o cria como a saída.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md)   
 [Programação com assemblies](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)   
 [Como adicionar ou remover referências usando o Gerenciador de Referências](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)


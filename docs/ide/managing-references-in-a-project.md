---
title: Gerenciar referências em um projeto
ms.date: 04/11/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ProjectPropertiesReferencePaths
- cs.ProjectPropertiesReferencePaths
helpviewer_keywords:
- C# projects, references
- referencing objects, project references
- external component references
- referencing namespaces
- Visual Basic projects, references
- referencing components, external components
- Web references, types of project references
- namespaces [Visual Studio], referencing
- COM components, referencing
- objects [Visual Studio], referencing
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e772f4d861e4b16499ad9be9d7c814320e1a14f9
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31950940"
---
# <a name="manage-references-in-a-project"></a>Gerenciar referências em um projeto

Antes de escrever código em um componente externo ou um serviço conectado, o projeto primeiro deve conter uma referência a ele. Basicamente, uma referência é uma entrada em um arquivo de projeto que contém as informações de que o Visual Studio precisa para localizar o componente ou o serviço.

Para adicionar uma referência, clique com o botão direito do mouse no nó **Referências** ou **Dependências** no **Gerenciador de Soluções** e escolha **Adicionar Referência**. Também é possível clicar com o botão direito do mouse no nó do projeto e selecionar **Adicionar** > **Referência**. Para obter mais informações, consulte [How to: Add or remove references](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md) (Como adicionar ou remover referências).

![Adicionar uma referência no Visual C&#43;&#43;](../ide/media/vs2015_cpp_add_reference.png)

É possível adicionar uma referência aos seguintes tipos de componentes e serviços:

- Bibliotecas de classes ou assemblies do .NET Framework

- Aplicativos UWP

- componentes COM

- Outros assemblies ou bibliotecas de classes de projetos na mesma solução

- Serviços Web XML

## <a name="uwp-app-references"></a>Referências ao aplicativo UWP

### <a name="project-references"></a>Referências de projeto

Os projetos da UWP (Plataforma Universal do Windows) podem criar referências a outros projetos da UWP na solução ou a projetos ou binários do Windows 8.1, desde que esses projetos não usem APIs que foram preteridas do Windows 10. Para obter mais informações, consulte [Mover do Windows Runtime 8 para a UWP](/windows/uwp/porting/w8x-to-uwp-root).

Se você optar por redirecionar projetos do Windows 8.1 para o Windows 10, consulte [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md).

### <a name="extension-sdk-references"></a>Referências do SDK da Extensão

Os aplicativos UWP (Plataforma Universal do Windows) em Visual Basic, C#, C++ e JavaScript podem referenciar os SDKs de Extensão direcionados ao Windows 8.1, desde que esses SDKs de Extensão não usem APIs que foram preteridas no Windows 10. Confira o site do fornecedor do SDK da Extensão para descobrir se ele pode ser referenciado por aplicativos UWP.

Se você determinar que não há suporte para o SDK de Extensão que está sendo referenciado pelo aplicativo, é necessário realizar as seguintes etapas:

1. Observe o nome do projeto que está causando o erro. A plataforma de destino do projeto é indicada entre parênteses ao lado do nome do projeto. Por exemplo, **MyProjectName (Windows 8.1)** significa que o projeto **MyProjectName** se destina à versão da plataforma Windows 8.1.

1. Acesse o site do fornecedor que é proprietário do SDK de Extensão sem suporte e instale a versão do SDK de Extensão com dependências que são compatíveis com a versão da plataforma de destino do projeto.

    > [!NOTE]
    > Uma maneira de descobrir se um SDK de Extensão tem dependências em outros SDKs de Extensão é examinar no **Gerenciador de Referências**. Reinicie o Visual Studio, crie um novo projeto de aplicativo UWP de C#, clique com o botão direito do mouse no projeto e escolha **Adicionar Referência**. Acesse a guia **Windows**, a subguia **Extensões** e selecione o SDK de Extensão. Examine o painel à direita no **Gerenciador de Referências**. Se ele tiver dependências, elas serão listadas no painel.

    > [!IMPORTANT]
    > Se o projeto tiver como destino o Windows 10 e o SDK de Extensão instalado na etapa anterior tiver uma dependência do Pacote de Tempo de Execução do Microsoft Visual C++, a versão do Pacote de Tempo de Execução do Microsoft Visual C++ compatível com o Windows 10 será v14.0 e ela será instalada com o Visual Studio.

1. Se o SDK de Extensão instalado na etapa anterior tiver dependências de outros SDKs de Extensão, acesse os sites dos fornecedores proprietários das dependências e instale as versões dessas dependências compatíveis com a versão da plataforma de destino do projeto.

1. Reinicie o Visual Studio e abra o aplicativo.

1. Clique com o botão direito do mouse no nó **Referências** ou **Dependências** do projeto que causou o erro e escolha **Adicionar Referência**.

1. Clique na guia **Windows** e, em seguida, na subguia **Extensões**, desmarque as caixas de seleção dos SDKs de Extensão antigos e marque as caixas de seleção dos novos SDKs de Extensão. Clique em **OK**.

## <a name="add-a-reference-at-design-time"></a>Adicionar uma referência em tempo de design

Ao fazer uma referência a um assembly no projeto, o Visual Studio pesquisa o assembly nos seguintes locais:

- O diretório atual do projeto. (É possível encontrar esses assemblies usando a guia **Procurar**.)

- Outros diretórios do projeto na mesma solução. (É possível encontrar esses assemblies na guia **Projetos**.)

> [!NOTE]
> - Todos os projetos contêm uma referência implícita a **mscorlib**.
> - Todos os projetos contêm uma referência implícita a `System.Core`, mesmo se `System.Core` for removido da lista de referências.
> - Os projetos do Visual Basic contêm uma referência implícita a <xref:Microsoft.VisualBasic>.

## <a name="references-to-shared-components-at-run-time"></a>Referências a componentes compartilhados no tempo de execução

Em tempo de execução, os componentes devem estar no caminho de saída do projeto ou no GAC (Cache de Assembly Global). Se o projeto contiver uma referência a um objeto que não está em um desses locais, será necessário copiar a referência para o caminho de saída do projeto ao compilá-lo. A propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> indica se esta cópia precisa ser feita. Se o valor for **True**, a referência será copiada para o diretório do projeto durante o build do projeto. Se o valor for **False**, a referência não será copiada.

Se você implantar um aplicativo que contenha uma referência a um componente personalizado que esteja registrado no GAC, o componente não será implantado com o aplicativo, independentemente da configuração de <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A>. Nas versões anteriores do Visual Studio, era possível definir a propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> em uma referência para garantir que o assembly fosse implantado. Agora, é necessário adicionar o assembly à pasta \Bin manualmente. Isso coloca todo o código personalizado sob análise, reduzindo o risco de publicar um código personalizado com o qual você não está familiarizado.

Por padrão, a propriedade <xref:Microsoft.VisualStudio.VCProjectEngine.VCProjectReference.CopyLocal%2A> será definida como **False** se o assembly ou o componente estiver no cache de assembly global ou for um componente de estrutura. Caso contrário, o valor será definido como **True**. Referências projeto a projeto são sempre definidas como **True**.

## <a name="reference-a-project-or-assembly-that-targets-a-different-version-of-the-net-framework"></a>Referenciar um projeto ou assembly que tem outra versão do .NET Framework como destino

É possível criar aplicativos que referenciam projetos ou assemblies que têm outra versão do .NET Framework como destino. Por exemplo, é possível criar um aplicativo que tem como destino o .NET Framework 4.6, que referencia um assembly que tem como destino o .NET Framework 4.5. Se você criar um projeto que tem como destino uma versão anterior do .NET Framework, não será possível definir uma referência no projeto a um projeto ou assembly que tem como destino uma versão mais recente.

Para obter mais informações, consulte [Visão geral da multissegmentação](../ide/visual-studio-multi-targeting-overview.md).

## <a name="project-to-project-references"></a>Referências de projeto a projeto

Referências projeto a projeto são referências a projetos que contêm assemblies; é possível criá-las usando a guia **Projeto**. O Visual Studio pode encontrar um assembly quando receber um caminho para o projeto.

Quando você tiver um projeto que produz um assembly, será necessário referenciar o projeto e não usar uma referência de arquivo (consulte abaixo). A vantagem de uma referência projeto a projeto é que ela cria uma dependência entre os projetos no sistema de build. O projeto dependente será compilado se ele tiver sido alterado desde a última vez que o projeto de referência foi compilado. Uma referência de arquivo não cria uma dependência de build e, portanto, é possível compilar o projeto de referência sem compilar o projeto dependente, e a referência pode se tornar obsoleta. (Ou seja, o projeto pode referenciar uma versão anteriormente compilada do projeto.) Isso pode resultar na exigência de várias versões de uma única DLL no diretório *bin*, o que não é possível. Quando ocorrer esse conflito, você verá uma mensagem como “Aviso: o 'arquivo' de dependência no projeto 'projeto' não pode ser copiado para o diretório de execução, pois ele substituirá o 'arquivo' de referência”. Para obter mais informações, consulte [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md) e [Como criar e remover dependências de projeto](../ide/how-to-create-and-remove-project-dependencies.md).

> [!NOTE]
> Uma referência de arquivo será criada em vez de uma referência projeto a projeto se a versão de destino do .NET Framework de um projeto for a versão 4.5 e a versão de destino do outro projeto for a versão 2, 3, 3.5 ou 4.0.

## <a name="file-references"></a>Referências de arquivo

Referências de arquivo são referências diretas a assemblies fora do contexto de um projeto do Visual Studio. Eles são criados usando a guia **Procurar** do **Gerenciador de Referências**. Use uma referência de arquivo quando você tiver apenas um assembly ou componente e não o projeto que o cria como a saída.

## <a name="see-also"></a>Consulte também

- [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md)
- [Como adicionar ou remover referências](../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)

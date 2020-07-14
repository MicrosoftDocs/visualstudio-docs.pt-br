---
title: Definir e instalar uma extensão de modelagem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: 82a58dc5-c7cf-4521-a6da-7ff09cd0de9d
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ef79d1be0b88ecdafa8691189bbc95291a6417ed
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544983"
---
# <a name="define-and-install-a-modeling-extension"></a>Definir e instalar uma extensão de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir extensões para diagramas de modelagem. Dessa maneira, você pode adaptar os diagramas e modelos às suas próprias necessidades. Por exemplo, você pode definir comandos de menu, perfis UML, restrições de validação e itens de caixa de ferramentas. Você pode definir vários componentes em uma única extensão. Você também pode distribuir essas extensões para outros usuários do Visual Studio na forma de um [VSIX (extensão de integração do Visual Studio)](https://msdn.microsoft.com/library/dd393694(VS.100).aspx). Você pode criar um VSIX usando um projeto VSIX no Visual Studio.

## <a name="requirements"></a>Requisitos
 Consulte [requisitos](../modeling/extend-uml-models-and-diagrams.md#Requirements).

 Para ver quais versões do Visual Studio oferecem suporte a esse recurso, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="creating-a-modeling-extension-solution"></a>Criando uma solução de extensão de modelagem
 Para definir uma extensão de modelagem, você deve criar uma solução que contenha esses projetos:

- Um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto de VSIX (extensão de integração). Isso gera um arquivo que atua como um instalador para os componentes de sua extensão.

- Um projeto de biblioteca de classes, necessário para componentes que incluem código de programa.

  Se você quiser criar uma extensão que tenha vários componentes, poderá desenvolvê-los em uma única solução. Você precisa apenas de um projeto VSIX.

  Os componentes que não exigem código, como itens de caixa de ferramentas personalizados e perfis UML personalizados, podem ser adicionados diretamente ao projeto VSIX sem o uso de projetos de biblioteca de classes separados. Os componentes que exigem código de programa são definidos mais facilmente em um projeto de biblioteca de classes separado. Os componentes que exigem código incluem manipuladores de gestos, comandos de menu e código de validação.

#### <a name="to-create-a-class-library-project-for-menu-commands-gesture-handlers-or-validation"></a>Para criar um projeto de biblioteca de classes para comandos de menu, manipuladores de gesto ou validação

1. No menu **Arquivo**, escolha **Novo**, **Projeto**.

2. Em **modelos instalados**, selecione **Visual C#** ou **Visual Basic**, em seguida, escolha **biblioteca de classes**.

#### <a name="to-create-a-vsix-project"></a>Para criar um projeto VSIX

1. Se você estiver criando um componente com código, será mais fácil criar o projeto de biblioteca de classes primeiro. Você adicionará seu código a esse projeto.

2. Crie um projeto VSIX.

    1. No **Gerenciador de soluções**, no menu de atalho da solução, escolha **Adicionar**, **novo projeto**.

    2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**e, em seguida, selecione **extensibilidade**. Na coluna do meio, escolha **projeto VSIX**.

3. Defina o projeto VSIX como o projeto de inicialização da solução.

    - No Gerenciador de Soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.

4. Open **Source. Extension. vsixmanifest**. O arquivo é aberto no editor de manifesto.

5. Na guia **metadados** , defina o nome e os campos descritivos do VSIX.

6. Na guia **instalar destinos** , escolha **novo** e defina as versões do Visual Studio como os destinos.

7. Na guia **ativos** , adicione seus componentes à extensão do Visual Studio.

    1. Escolha **Novo**.

    2. Para um componente com código, defina esses campos na caixa de diálogo **Adicionar novo ativo** :

        |Campo|Valor|
        |-|-|
        |**Escreva** =|**Microsoft. VisualStudio. MefComponent**|
        |**Original** =|**Um projeto na solução atual**|
        |**Project** =|*Seu projeto de biblioteca de classes*|
        |**Inserir nesta pasta** =|*esvaziá*|

         Para outros tipos de componente, consulte os links na próxima seção.

## <a name="developing-the-component"></a>Desenvolvendo o componente
 Para cada componente, como um comando de menu ou um manipulador de gestos, você deve definir um manipulador separado. Você pode colocar vários manipuladores no mesmo projeto de biblioteca de classes. A tabela a seguir resume os diferentes tipos de manipulador.

|Tipo de extensão|Tópico|Como cada componente é normalmente declarado|
|--------------------|-----------|----------------------------------------------|
|Menu Comando|[Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(ICommandExtension))]`<br /><br /> `public class MyCommand : ICommandExtension`<br /><br /> `{...`|
|Arraste e solte ou clique duas vezes em|[Definir um manipulador de gestos em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(IGestureExtension))]`<br /><br /> `public class MyGesture : IGestureExtension`<br /><br /> `{...`|
|Restrição de validação|[Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)|`[Export(typeof(     System.Action<ValidationContext, object>))]`<br /><br /> `[ValidationMethod(ValidationCategories.Save`<br /><br /> `&#124; ValidationCategories.Menu)]`<br /><br /> `public void ValidateSomething`<br /><br /> `(ValidationContext context, IClassifier elementToValidate)`<br /><br /> `{...}`|
|Manipulador de eventos de link do item de trabalho|[Definir um manipulador de link de item de trabalho](../modeling/define-a-work-item-link-handler.md)|`[Export(typeof(ILinkedWorkItemExtension))]`<br /><br /> `public class MyWorkItemEventHandler : ILinkedWorkItemExtension`<br /><br /> `{...`|
|Perfil UML|[Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)|(A ser definido)|
|Item da caixa de ferramentas|[Definir um item de caixa de ferramentas de modelagem personalizada](../modeling/define-a-custom-modeling-toolbox-item.md)|(A ser definido)|

## <a name="running-an-extension-during-its-development"></a>Executando uma extensão durante seu desenvolvimento

#### <a name="to-run-an-extension-during-its-development"></a>Para executar uma extensão durante seu desenvolvimento

1. No menu [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] **depurar** , escolha **Iniciar Depuração**.

     O projeto é compilado e uma nova instância do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] é iniciada no modo experimental.

    - Como alternativa, você pode escolher **Iniciar sem depuração**. Isso reduz o tempo necessário para iniciar o programa.

2. Crie ou abra um projeto de modelagem na instância experimental do Visual Studio e crie ou abra um diagrama.

     Sua extensão será carregada e executada.

3. Se você usou **Iniciar sem depuração** , mas deseja usar o depurador, volte para a instância principal do Visual Studio. No menu **depurar** , clique em **anexar ao processo**. Na caixa de diálogo, selecione a instância experimental do Visual Studio, que tem o nome do programa **devenv**.

## <a name="installing-and-uninstalling-an-extension"></a><a name="Installing"></a>Instalando e desinstalando uma extensão
 Execute as etapas a seguir para executar sua extensão na instância principal do Visual Studio em seu próprio computador ou em outros computadores.

1. Em seu computador, localize o arquivo **. vsix** criado por seu projeto de extensão.

    1. No **Gerenciador de soluções**, no menu de atalho do seu projeto e escolha **abrir pasta no Windows Explorer**.

    2. Localize o arquivo **bin \\ \* \\ **_seuprojeto_**. vsix**

2. Copie o arquivo **. vsix** para o computador de destino no qual você deseja instalar a extensão. Este pode ser seu próprio computador ou outro.

    - O computador de destino deve ter uma das edições do Visual Studio que você especificou na guia **destinos de instalação** de **origem. extensão. vsixmanifest**.

3. No computador de destino, abra o arquivo **. vsix** , por exemplo, clicando duas vezes nele.

     O **instalador de extensão do Visual Studio** é aberto e instala a extensão.

4. Inicie ou reinicie o Visual Studio.

#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão

1. No menu **Ferramentas**, clique em **Extensões e Atualizações**.

2. Expanda **extensões instaladas**.

3. Selecione a extensão e clique em **desinstalar**.

   Raramente, uma extensão defeituosa não carrega e cria um relatório na janela de erro, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo do seguinte local em que *% LocalAppData%* normalmente é *driveName*: \Users \\ *username*\AppData\Local:

   *% LocalAppData%* **\Microsoft\VisualStudio \\ [versão] \Extensions**

## <a name="see-also"></a>Consulte Também
 [Definir um perfil para estender](../modeling/define-a-profile-to-extend-uml.md) [o UML defina um item da caixa de ferramentas de modelagem personalizado](../modeling/define-a-custom-modeling-toolbox-item.md) [definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md) [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

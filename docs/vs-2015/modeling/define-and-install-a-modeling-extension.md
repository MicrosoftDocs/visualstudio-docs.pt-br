---
title: Definir e instalar uma extensão de modelagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: 82a58dc5-c7cf-4521-a6da-7ff09cd0de9d
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6f7895916cc4ee877c53b056f703d8e46b64b409
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805561"
---
# <a name="define-and-install-a-modeling-extension"></a>Definir e instalar uma extensão de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir as extensões para diagramas de modelagem. Dessa maneira, você pode adaptar os modelos e diagramas de acordo com suas necessidades. Por exemplo, você pode definir comandos de menu, perfis UML, restrições de validação e itens de caixa de ferramentas. Você pode definir vários componentes em uma única extensão. Você também pode distribuir essas extensões para outros usuários do Visual Studio na forma de um [extensão de integração do Visual Studio (VSIX)](http://go.microsoft.com/fwlink/?LinkId=160780). Você pode criar um VSIX usando um projeto VSIX no Visual Studio.  
  
## <a name="requirements"></a>Requisitos  
 Ver [requisitos de](../modeling/extend-uml-models-and-diagrams.md#Requirements).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="creating-a-modeling-extension-solution"></a>Criando uma solução de extensão de modelagem  
 Para definir uma extensão de modelagem, você deve criar uma solução que contém esses projetos:  
  
- Um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto integração VSIX (extensão). Isso gera um arquivo que atua como um instalador para os componentes da sua extensão.  
  
- Um projeto biblioteca de classes, necessário para os componentes que incluem o código do programa.  
  
  Se você quiser tornar uma extensão que tem vários componentes, você pode desenvolvê-los em uma única solução. Você precisa apenas um projeto VSIX.  
  
  Componentes que não exigem código, como itens de caixa de ferramentas personalizado e perfis personalizados do UML, podem ser adicionados diretamente ao projeto de VSIX sem o uso de projetos de biblioteca de classe separada. Componentes que exigem o código do programa com mais facilidade são definidos em um projeto de biblioteca de classe separada. Componentes que exigem código incluem manipuladores de gestos, comandos de menu e código de validação.  
  
#### <a name="to-create-a-class-library-project-for-menu-commands-gesture-handlers-or-validation"></a>Para criar um projeto de biblioteca de classes para comandos de menu, manipuladores de gesto ou validação  
  
1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
2.  Sob **modelos instalados**, selecione **Visual c#** ou **Visual Basic**, em seguida, escolha **biblioteca de classes**.  
  
#### <a name="to-create-a-vsix-project"></a>Para criar um projeto do VSIX  
  
1.  Se você estiver criando um componente com o código, é mais fácil de criar o projeto de biblioteca de classe pela primeira vez. Você irá adicionar seu código para o projeto.  
  
2.  Crie um projeto VSIX.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho da solução, escolha **Add**, **novo projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, selecione **extensibilidade**. Na coluna do meio, escolha **VSIX Project**.  
  
3.  Defina o projeto VSIX como o projeto de inicialização da solução.  
  
    -   No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.  
  
4.  Abra **vsixmanifest**. O arquivo é aberto no editor de manifesto.  
  
5.  Sobre o **metadados** guia, defina os campos nome e descritivos do VSIX.  
  
6.  Sobre o **instalar destinos** guia, escolha **New** e defina as versões do Visual Studio como os destinos.  
  
7.  Sobre o **ativos** guia, adicione os componentes para a extensão do Visual Studio.  
  
    1.  Escolher **novo**.  
  
    2.  Para um componente com o código, definir esses campos na **adicionar novo ativo** caixa de diálogo:  
  
        |||  
        |-|-|  
        |**Tipo** =|**Mefcomponent**|  
        |**Source** =|**Um projeto na solução atual**|  
        |**Projeto** =|*Seu projeto de biblioteca de classes*|  
        |**Inserir nesta pasta** =|*(vazio)*|  
  
         Para outros tipos de componente, consulte os links na próxima seção.  
  
## <a name="developing-the-component"></a>Desenvolvendo o componente  
 Para cada componente, como um manipulador de gesto ou comando de menu, você deve definir um manipulador separado. Você pode colocar vários manipuladores no mesmo projeto de biblioteca de classe. A tabela a seguir resume os diferentes tipos de manipulador.  
  
|Tipo de extensão|Tópico|Como cada componente normalmente é declarado|  
|--------------------|-----------|----------------------------------------------|  
|Menu Comando|[Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(ICommandExtension))]`<br /><br /> `public class MyCommand : ICommandExtension`<br /><br /> `{...`|  
|Arraste e solte ou clique duas vezes em|[Definir um manipulador de gestos em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(IGestureExtension))]`<br /><br /> `public class MyGesture : IGestureExtension`<br /><br /> `{...`|  
|Restrição de validação|[Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)|`[Export(typeof(     System.Action<ValidationContext, object>))]`<br /><br /> `[ValidationMethod(ValidationCategories.Save`<br /><br /> `&#124; ValidationCategories.Menu)]`<br /><br /> `public void ValidateSomething`<br /><br /> `(ValidationContext context, IClassifier elementToValidate)`<br /><br /> `{...}`|  
|Manipulador de eventos de link de Item de trabalho|[Definir um manipulador de link de item de trabalho](../modeling/define-a-work-item-link-handler.md)|`[Export(typeof(ILinkedWorkItemExtension))]`<br /><br /> `public class MyWorkItemEventHandler : ILinkedWorkItemExtension`<br /><br /> `{...`|  
|Perfil UML|[Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)|(Para ser definido)|  
|Item de caixa de ferramentas|[Definir um item de caixa de ferramentas de modelagem personalizada](../modeling/define-a-custom-modeling-toolbox-item.md)|(Para ser definido)|  
  
## <a name="running-an-extension-during-its-development"></a>Execução de uma extensão durante seu desenvolvimento  
  
#### <a name="to-run-an-extension-during-its-development"></a>Para executar uma extensão durante seu desenvolvimento  
  
1.  No [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] **Debug** menu, escolha **iniciar depuração**.  
  
     As compilações do projeto e uma nova instância da [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] é iniciado em modo Experimental.  
  
    -   Como alternativa, você pode escolher **Start Without Debugging**. Isso reduz o tempo necessário para iniciar o programa.  
  
2.  Criar ou abrir um projeto de modelagem na instância experimental do Visual Studio e crie ou abra um diagrama.  
  
     Sua extensão carregará e executará.  
  
3.  Se você usou **Start Without Debugging** , mas você deseja usar o depurador, volte para a instância principal do Visual Studio. Sobre o **Debug** menu, clique em **anexar ao processo**. Na caixa de diálogo, selecione a instância experimental do Visual Studio, que tem o nome do programa **devenv**.  
  
##  <a name="Installing"></a> Instalando e desinstalando uma extensão  
 Execute as seguintes etapas para executar sua extensão na instância principal do Visual Studio em seu próprio computador ou em outros computadores.  
  
1.  No seu computador, localize o **VSIX** arquivo que foi criado pelo seu projeto de extensão.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho do seu projeto e, em seguida, escolha **Abrir pasta no Windows Explorer**.  
  
    2.  Localize o arquivo **bin\\\*\\**_Seuprojeto_**. VSIX**  
  
2.  Cópia de **. VSIX** arquivo ao computador de destino no qual você deseja instalar a extensão. Isso pode ser seu próprio computador ou outro.  
  
    -   O computador de destino deve ter uma das edições do Visual Studio que você tiver especificado a **destinos de instalação** guia de **vsixmanifest**.  
  
3.  No computador de destino, abra o **VSIX** arquivo, por exemplo, clicando duas vezes nele.  
  
     **Instalador de extensão do Visual Studio** abre e instala a extensão.  
  
4.  Inicie ou reinicie o Visual Studio.  
  
#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão  
  
1. Sobre o **ferramentas** menu, clique em **extensões e atualizações**.  
  
2. Expandir **extensões instaladas**.  
  
3. Selecione a extensão e, em seguida, clique em **desinstalação**.  
  
   Raramente, uma extensão defeituosa Falha ao carregar e cria um relatório na janela de erros, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo no seguinte local no qual *% LocalAppData %* é normalmente *DriveName*: \Users\\*denomedeusuário*\AppData\Local:  
  
   *% LocalAppData %* **\Microsoft\VisualStudio\\\Extensions [versão]**  
  
## <a name="see-also"></a>Consulte também  
 [Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)   
 [Definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md)   
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)




---
title: Regras de aninhamento de arquivos do Gerenciador de Soluções
ms.date: 05/25/2018
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
helpviewer_keywords:
- file nesting
- Solution Explorer, file nesting
author: angelosp
ms.author: angelpe
manager: douge
ms.openlocfilehash: d50d16d23c2f12ac5ac9feaaa37ee3797802c97e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928692"
---
# <a name="customize-file-nesting-in-solution-explorer"></a>Personalizar o aninhamento de arquivos no Gerenciador de Soluções

O aninhamento de arquivos relacionados no **Gerenciador de Soluções** não é novo, mas até agora, você não tinha controle sobre as regras de aninhamento. Você pode escolher entre as predefinições **Desativado**, **Padrão** e **Web**, mas também pode personalizar o aninhamento exatamente como desejado. Você pode até mesmo criar configurações específicas a uma solução e um projeto, mas falaremos mais sobre tudo isso posteriormente. Primeiro, vamos falar sobre as configurações que você obtém prontas para uso.

> [!NOTE]
> Atualmente, há suporte para a funcionalidade somente em projetos ASP.NET Core.

## <a name="file-nesting-options"></a>Opções de aninhamento de arquivos

![Botão para ligar/desligar o aninhamento de arquivos](media/filenesting_onoff.png)

As opções disponíveis para o aninhamento não personalizado de arquivos são:

* **Desativado**: essa opção fornece uma lista plana de arquivos sem nenhum aninhamento.

* **Padrão**: essa opção fornece o comportamento padrão do aninhamento de arquivos no **Gerenciador de Soluções**. Se não houver nenhuma configuração para um tipo de projeto fornecido, nenhum arquivo do projeto será aninhado. Se houver configurações, por exemplo, para um projeto Web, o aninhamento será aplicado.

* **Web**: essa opção aplica o comportamento **Web** de aninhamento de arquivos a todos os projetos da solução atual. Ela tem várias regras. Por isso, incentivamos você a conferi-la e enviar-nos sua opinião. A seguinte captura de tela destaca apenas alguns exemplos do comportamento de aninhamento de arquivos obtidos com essa opção:

   ![Aninhamento de arquivos no Gerenciador de Soluções](media/filenesting.png)

## <a name="customize-file-nesting"></a>Personalizar o aninhamento de arquivos

Caso não goste das configurações prontas para uso, crie suas próprias configurações personalizadas de aninhamento de arquivos que instruem o **Gerenciador de Soluções** em como aninhar arquivos. Adicione quantas configurações personalizadas de aninhamento de arquivos desejar e alterne entre elas, conforme desejado. Para criar uma configuração personalizada, comece com um arquivo vazio ou use as configurações **Web** como ponto de partida:

![Adicionar regras personalizadas de aninhamento de arquivos](media/filenesting_addcustom.png)

Recomendamos que você use as configurações **Web** como ponto de partida porque é mais fácil trabalhar com algo que já funciona. Se você usar as configurações **Web** como ponto de partida, o arquivo *.filenesting.json* será semelhante ao seguinte arquivo:

![Usar as regras existentes de aninhamento de arquivos como base para as configurações personalizadas](media/filenesting_editcustom.png)

Vamos nos concentrar no nó **dependentFileProviders** e em seus nós filho. Cada nó filho é um tipo de regra que pode ser usado pelo Visual Studio para aninhar arquivos. Por exemplo, **ter o mesmo nome de arquivo, mas uma extensão diferente** é um tipo de regra. As regras disponíveis são:

* **extensionToExtension**: use esse tipo de regra para aninhar *file.js* em *file.ts*

* **fileSuffixToExtension**: use esse tipo de regra para aninhar *file-vsdoc.js* em *file.js*

* **addedExtension**: use esse tipo de regra para aninhar *file.html.css* em *file.html*

* **pathSegment**: use esse tipo de regra para aninhar *jquery.min.js* em *jquery.js*

* **allExtensions**: use esse tipo de regra para aninhar *file.** em *file.js*

* **fileToFile**: use esse tipo de regra para aninhar *bower.json* em *.bowerrc*

### <a name="the-extensiontoextension-provider"></a>O provedor extensionToExtension

Esse provedor permite que você defina regras de aninhamento de arquivos usando extensões de arquivo específicas. Considere o exemplo a seguir:

![Regras de exemplo de extentionToExtension](media/filenesting_extensiontoextension.png) ![Efeito de exemplo de extentionToExtension](media/filenesting_extensiontoextension_effect.png)

* *cart.js* é aninhado em *cart.ts* devido à primeira regra de **extensionToExtension**

* *cart.js* não é aninhado em *cart.tsx* porque **.ts** antecede **.tsx** nas regras, e pode haver apenas um pai

* *light.css* é aninhado em *light.sass* devido à segunda regra de **extensionToExtension**

* *home.html* é aninhado em *home.md* devido à terceira regra de **extensionToExtension**

### <a name="the-filesuffixtoextension-provider"></a>O provedor fileSuffixToExtension

Esse provedor funciona da mesma maneira que o provedor **extensionToExtension**, com a única diferença que a regra examina o sufixo do arquivo em vez de apenas a extensão. Considere o exemplo a seguir:

![Regras de exemplo de fileSuffixToExtension](media/filenesting_filesuffixtoextension.png) ![Efeito de exemplo de fileSuffixToExtension](media/filenesting_filesuffixtoextension_effect.png)

* *portal-vsdoc.js* é aninhado em *portal.js* devido à regra de **fileSuffixToExtension**

* todos os outros aspectos da regra funcionam da mesma maneira que **extensionToExtension**

### <a name="the-addedextension-provider"></a>O provedor addedExtension

Esse provedor aninha arquivos com uma extensão adicional no arquivo sem uma extensão adicional. A extensão adicional só pode ser exibida ao final do nome de arquivo completo. Considere o exemplo a seguir:

![Regras de exemplo de addedExtension](media/filenesting_addedextension.png) ![Efeito de exemplo de addedExtension](media/filenesting_addedextension_effect.png)

* *file.html.css* é aninhado em *file.html* devido à regra de **addedExtension**

### <a name="the-pathsegment-provider"></a>O provedor pathSegment

Esse provedor aninha arquivos com uma extensão adicional em um arquivo sem uma extensão adicional. A extensão adicional só pode ser exibida no meio do nome de arquivo completo. Considere o exemplo a seguir:

![Regras de exemplo de pathSegment](media/filenesting_pathsegment.png) ![Efeito de exemplo de pathSegment](media/filenesting_pathsegment_effect.png)

* *jquery.min.js* é aninhado em *jquery.js* devido à regra de **pathSegment**

### <a name="the-allextensions-provider"></a>O provedor allExtensions

Esse provedor permite que você defina regras de aninhamento de arquivos para arquivos com qualquer extensão, exceto o mesmo nome de arquivo base. Considere o exemplo a seguir:

![Regras de exemplo de allExtensions](media/filenesting_allextensions.png) ![Efeito de exemplo de allExtensions](media/filenesting_allextensions_effect.png)

* *template.cs* e *template.doc* são aninhados em *template.tt* devido à regra de **allExtensions**.

### <a name="the-filetofile-provider"></a>O provedor fileToFile

Esse provedor permite que você defina regras de aninhamento de arquivos com base em nomes de arquivo inteiros. Considere o exemplo a seguir:

![Regras de exemplo de fileToFile](media/filenesting_filetofile.png) ![Efeito de exemplo de fileToFile](media/filenesting_filetofile_effect.png)

* *.bowerrc* é aninhado em *bower.json* devido à regra de **fileToFile**

### <a name="rule-order"></a>Ordem das regras

A ordenação é importante em todas as partes do arquivo de configurações personalizadas. Altere a ordem na qual as regras são executadas movendo-as para cima ou para baixo dentro do nó **dependentFileProvider**. Por exemplo, se você tem uma regra que torna **file.js** o pai de **file.ts** e outra regra que torna **file.coffee** o pai de **file.ts**, a ordem na qual elas são exibidas no arquivo determina o comportamento de aninhamento quando todos os três arquivos estão presentes. Como **file.ts** só pode ter um pai, a regra executada primeiro vence.

A ordenação também é importante para as próprias seções de regra, não apenas para os arquivos dentro de uma seção. Assim que é encontrada uma correspondência entre um par de arquivos e uma regra de aninhamento de arquivo, outras regras posteriores no arquivo são ignoradas e o próximo par de arquivos é processado.

### <a name="file-nesting-button"></a>Botão de aninhamento de arquivos

Gerencie todas as configurações, incluindo suas próprias configurações personalizadas, por meio do mesmo botão no **Gerenciador de Soluções**:

![Ativar regras personalizadas de aninhamento de arquivos](media/filenesting_activatecustom.png)

## <a name="create-solution-specific-and-project-specific-settings"></a>Criar configurações específicas a um projeto e uma solução

Crie configurações específicas a um projeto e uma solução por meio do menu de contexto de cada solução e projeto:

![Regras de aninhamento específicas a um projeto e uma solução](media/filenesting_solutionprojectspecific.png)

As configurações específicas a um projeto e uma solução são combinadas com as configurações ativas do Visual Studio. Por exemplo, você pode ter um arquivo de configurações específicas a um projeto em branco, mas o **Gerenciador de Soluções** ainda pode estar aninhando arquivos. O comportamento de aninhamento é obtido das configurações específicas a uma solução ou das configurações do Visual Studio. A precedência para mesclagem das configurações de aninhamento de arquivos é: Visual Studio > Solução > Projeto.

Você pode instruir o Visual Studio a ignorar as configurações específicas a um projeto e uma solução, mesmo se os arquivos existem em disco, habilitando a opção **Ignorar configurações de solução e projeto** em **Ferramentas** > **Opções** > **ASP.NET Core** > **Aninhamento de Arquivos**.

Faça o oposto e instrua o Visual Studio a usar *somente* as configurações específicas a um projeto ou uma solução definindo o nó **root** como **true**. O Visual Studio interrompe a mesclagem de arquivos nesse nível e não os combina com arquivos de um nível superior na hierarquia.

É possível fazer check-in das configurações específicas a um projeto e uma solução no controle do código-fonte, e toda a equipe que trabalha na base de código pode compartilhá-las.

## <a name="disable-global-file-nesting-rules-for-a-particular-solution-or-project"></a>Desabilitar as regras globais de aninhamento de arquivos de uma solução ou um projeto específico

Desabilite as regras globais existentes de aninhamento de arquivos para soluções ou projetos específicos usando a ação **remover** para um provedor, em vez de **adicionar**. Por exemplo, se você adicionar o seguinte código de configurações a um projeto, todas as regras de **pathSegment** que possam existir globalmente para esse projeto específico serão desabilitadas:

```json
"dependentFileProviders": {
  "remove": {
    "pathSegment": {}
  }
}
```

## <a name="see-also"></a>Consulte também

- [Personalizar o IDE](../ide/personalizing-the-visual-studio-ide.md)

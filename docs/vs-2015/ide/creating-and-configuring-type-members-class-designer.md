---
title: Criando e configurando membros de tipo (Designer de Classe) | Microsoft Docs
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
- vs.classdetails.method
- vs.classdetails.property
- vs.classdetails.parameter
- vs.classdetails.event
- vs.classdetails.field
helpviewer_keywords:
- Class Designer [Visual Studio], member creation
- type members, modifying in Class Designer
- parameters [ASP.NET Web Services], adding to methods
- type members, configuring
- type members
- members
- type members, creating
- members, creating
- Class Designer [Visual Studio], type members
- read-only information, displaying
- members, configuring
- methods [Visual Studio], adding parameters
- Class Details window
- Class Details window, member creation
ms.assetid: 42af8738-3738-4ca7-82ff-edf573a68f96
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 93a112fac274921fe2d1075e1a1b9178c408240c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49827968"
---
# <a name="creating-and-configuring-type-members-class-designer"></a>Criando e configurando membros de tipo (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível adicionar esses membros aos tipos em um diagrama de classe e configurá-los na Janela **Detalhes da Classe**:  
  
|**Tipo**|**Membros que pode conter**|  
|--------------|--------------------------------|  
|Classe|método, propriedade (para C# e Visual Basic), campo, evento (para C# e Visual Basic), construtor (método), destruidor (método), constante|  
|Enum|membro|  
|Interface|método, propriedade, evento (para C# e Visual Basic)|  
|Classe Abstrata|método, propriedade (para C# e Visual Basic), campo, evento (para C# e Visual Basic), construtor (método), destruidor (método), constante|  
|Estrutura (Struct no C#)|método, propriedade (para C# e Visual Basic), campo, evento (para C# e Visual Basic), construtor (método), constante|  
|delegado|Parâmetro|  
|Módulo (apenas VB)|método, propriedade, campo, evento, construtor, constante|  
  
> [!NOTE]
>  Torne a declaração de propriedade mais concisa quando os acessadores get e set de uma propriedade não precisarem de lógica adicional usando propriedades autoimplementadas (apenas C#). Para mostrar a assinatura completa, no menu **Diagrama de Classe**, escolha **Modificar o Formato dos Membros**, **Exibir Assinatura Completa**. Para obter mais informações sobre propriedades autoimplementadas, consulte [Propriedades Autoimplementadas](http://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7).  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo de suporte|  
|----------|------------------------|  
|**Introdução:** antes de criar e configurar membros de tipo, você deve abrir a Janela Detalhes da Classe.|-   [Abrindo a Janela Detalhes da Classe](../ide/creating-and-configuring-type-members-class-designer.md#OpenClassDetails)<br />-   [Observações de uso de Detalhes da Classe](../ide/creating-and-configuring-type-members-class-designer.md#ClassDetailsUsageNotes)<br />-   [Exibição de informações somente leitura](../ide/creating-and-configuring-type-members-class-designer.md#ReadOnlyInfo)<br />-   [Atalhos de teclado e mouse no Diagrama de Classe e na Janela Detalhes da Classe (Designer de Classe)](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md)|  
|**Criar e modificar membros de tipo:** você pode criar novos membros, modificar membros e adicionar parâmetros a um método usando a Janela Detalhes da Classe.|-   [Criando membros](../ide/creating-and-configuring-type-members-class-designer.md#CreateMembers)<br />-   [Modificando membros de tipo](../ide/creating-and-configuring-type-members-class-designer.md#ModifyTypeMembers)<br />-   [Adicionando parâmetros aos métodos](../ide/creating-and-configuring-type-members-class-designer.md#AddMethodParams)|  
  
##  <a name="OpenClassDetails"></a> Abrindo a Janela Detalhes da Classe  
 Por padrão, a Janela Detalhes da Classe é exibida automaticamente quando você abre um novo diagrama de classe (consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)). Também é possível abrir a janela Detalhes da Classe explicitamente, das maneiras que se seguem.  
  
#### <a name="to-open-the-class-details-window"></a>Para abrir a janela Detalhes da Classe  
  
1. Clique com o botão direito do mouse m qualquer classe no diagrama para exibir um menu de contexto.  
  
2. No menu de contexto, clique em **Janela Detalhes da Classe**.  
  
   – ou -  
  
-   Aponte para **Outras Janelas** no menu Exibir e clique em **Detalhes da Classe**.  
  
##  <a name="CreateMembers"></a> Criando membros  
 Você pode criar um membro usando qualquer uma das ferramentas a seguir:  
  
-   Designer de Classe  
  
-   Barra de ferramentas da janela Detalhes da Classe  
  
-   Janela Detalhes da Classe  
  
> [!NOTE]
>  Você também pode criar construtores e destruidores usando os procedimentos desta seção. Lembre-se de que construtores e destruidores são tipos especiais de método e, como tais, eles aparecem no compartimento **Métodos** em formas do diagrama de classe e na seção **Métodos** da grade da Janela Detalhes da Classe.  
  
> [!NOTE]
>  A única entidade que você pode adicionar a um representante é o parâmetro. Observe que o procedimento denominado "Para criar um membro usando a barra de ferramentas da janela Detalhes da Classe" não é válido para essa ação.  
  
#### <a name="to-create-a-member-using-class-designer"></a>Para criar um membro usando o Designer de Classe  
  
1.  Clique com o botão direito do mouse no tipo ao qual deseja adicionar um membro, aponte para **Adicionar** e escolha o tipo de membro que deseja adicionar.  
  
     Uma nova assinatura de membro é criada e adicionada ao tipo. Ela recebe um nome padrão que pode ser alterado no **Designer de Classe**, na Janela **Detalhes da Classe** ou na janela **Propriedades**.  
  
2.  Se preferir, especifique outros detalhes sobre o membro, como seu tipo.  
  
#### <a name="to-create-a-member-using-the-class-details-window-toolbar"></a>Para criar um membro usando a barra de ferramentas da janela Detalhes da Classe  
  
1.  Na superfície de diagrama, selecione o tipo ao qual deseja adicionar um membro.  
  
     O tipo obtém foco e seu conteúdo é exibido na janela Detalhes da Classe.  
  
2.  Na barra de ferramentas da Janela Detalhes da Classe, clique no ícone superior e selecione **Novo \<membro>** na lista suspensa.  
  
     O cursor é movido para o campo **Nome** em uma linha para o tipo de membro que você deseja adicionar. Por exemplo, se você tiver clicado em **Nova Propriedade**, o cursor irá para uma nova linha na seção **Propriedades** da Janela Detalhes da Classe.  
  
3.  Digite o nome do membro que deseja criar e pressione Enter (ou, de outra forma, mova o foco, pressionando Tab).  
  
     Uma nova assinatura de membro é criada e adicionada ao tipo. Agora, o membro existe no código e é exibido no **Designer de Classe**, na Janela Detalhes da Classe e na janela Propriedades.  
  
4.  Se preferir, especifique outros detalhes sobre o membro, como seu tipo.  
  
#### <a name="to-create-a-member-using-the-class-details-window"></a>Para criar um membro usando a janela Detalhes da Classe  
  
1.  Na superfície de diagrama, selecione o tipo ao qual deseja adicionar um membro.  
  
     O tipo obtém foco e seu conteúdo é exibido na janela Detalhes da Classe.  
  
2.  Na Janela Detalhes da Classe, na seção que contém o tipo de membro que você deseja adicionar, clique em **\<adicionar membro>**. Por exemplo, se quiser adicionar um campo, clique em **\<adicionar campo>**.  
  
3.  Digite o nome do membro que deseja criar e pressione Enter.  
  
     Uma nova assinatura de membro é criada e adicionada ao tipo. Agora, o membro existe no código e é exibido no **Designer de Classe**, na Janela Detalhes da Classe e na janela Propriedades.  
  
4.  Se preferir, especifique outros detalhes sobre o membro, como seu tipo.  
  
     **Observação:** você também pode usar atalhos de teclado para criar membros. Para obter mais informações, consulte [Atalhos de teclado e mouse no Diagrama de Classe e na Janela Detalhes da Classe (Designer de Classe)](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md).  
  
##  <a name="ModifyTypeMembers"></a> Modificando membros de tipo  
 O Designer de Classe permite modificar os membros dos tipos que são exibidos no diagrama. É possível modificar os membros de qualquer tipo exibido em um diagrama de classes que não sejam somente leitura. (Consulte [Exibição de informações somente leitura (Designer de Classe)](http://msdn.microsoft.com/en-us/33e2d3a9-1668-4d10-ae56-fa09b3156e0a).) Modifique os membros de tipo usando edição in-loco na superfície de design, na janela Propriedades e na janela Detalhes da Classe.  
  
 Todos os membros exibidos na janela Detalhes da Classe representam os membros dos tipos no diagrama de classes. Há quatro tipos de membro: métodos, propriedades, campos e eventos.  
  
 Todas as linhas de membro aparecem abaixo dos cabeçalhos que agrupam os membros por tipo. Por exemplo, todas as propriedades aparecem abaixo do cabeçalho **Propriedades** que, como um nó na grade, pode ser recolhido ou expandido.  
  
 Cada linha de membro exibe os seguintes elementos:  
  
-   **Ícone do membro**  
  
     Cada tipo de membro é representado por seu próprio ícone. Aponte o mouse para o ícone do membro para exibir a assinatura do membro. Clique no ícone do membro ou no espaço em branco à esquerda do ícone do membro para selecionar a linha.  
  
-   **Nome do membro**  
  
     A coluna **Nome** em uma linha de membro exibe o nome do membro. Esse nome também é exibido na propriedade **Nome** na janela Propriedades. Use essa célula para alterar o nome de qualquer membro que tenha permissões de leitura/gravação.  
  
     Se a coluna **Nome** for muito estreita para mostrar o nome inteiro, apontar o mouse para o nome do membro exibe o nome inteiro.  
  
-   **Tipo do membro**  
  
     A célula **MemberType** usa o IntelliSense, que permite fazer seleções em uma lista de todos os tipos disponíveis no projeto atual ou em projetos referenciados.  
  
-   **Modificador do membro**  
  
     Altere o modificador de visibilidade de um membro para `Public` (`public`), `Private` (`private`), `Friend` (`internal`) `Protected` (`protected`), `Protected``Friend` (`protected``internal`) ou `Default`.  
  
-   **\<adicionar membro>**  
  
     A última linha da Janela Detalhes da Classe contém o texto **\<adicionar membro>** na célula **Nome**. Se você clicar nessa célula, será possível criar um novo membro. Para obter mais informações, consulte [Criando membros](../ide/creating-and-configuring-type-members-class-designer.md#CreateMembers).  
  
-   **Propriedades do membro na janela Propriedades**  
  
     A janela Detalhes da Classe exibe um subconjunto das propriedades do membro que são exibidas na janela Propriedades. Alterar uma propriedade em um local atualizará o valor da propriedade globalmente. Isso inclui a exibição de seu valor em outro local.  
  
-   **Resumo**  
  
     A célula **Resumo** expõe um resumo das informações sobre o membro. Clique nas reticências na célula **Resumo** para exibir ou editar informações sobre o **Resumo**, o **Tipo de Retorno** e os **Comentários** do membro.  
  
-   **Ocultar**  
  
     Quando a caixa de seleção **Ocultar** é marcada, o membro não é exibido no tipo.  
  
#### <a name="to-modify-a-type-member"></a>Para modificar um membro de tipo  
  
1.  Usando o Designer de Classe, selecione um tipo.  
  
2.  Se a janela Detalhes da Classe não for exibida, clique no botão **Janela Detalhes da Classe** na barra de ferramentas do Designer de Classe.  
  
3.  Edite os valores nos campos da grade da janela Detalhes da Classe. Após cada edição, pressione ENTER ou, caso contrário, mova o foco para longe do campo editado, por exemplo, pressionando TAB. Suas edições são refletidas imediatamente no código.  
  
    > [!NOTE]
    >  Se desejar modificar apenas o nome de um membro, você poderá fazer isso usando a edição in-loco.  
  
##  <a name="AddMethodParams"></a> Adicionando parâmetros aos métodos  
 Adicione parâmetros aos métodos usando a janela Detalhes da Classe. Os parâmetros podem ser configurados para serem obrigatórios ou opcionais. Fornecer um valor para a propriedade **Padrão Opcional** de um parâmetro instrui o designer a gerar código como um parâmetro opcional.  
  
 As linhas de parâmetro contém os seguintes itens:  
  
- **Nome**  
  
   A coluna **Nome** em uma linha de parâmetro exibe o nome do parâmetro. Esse nome também é exibido na propriedade **Nome** na janela Propriedades. Você pode usar essa célula para alterar o nome de qualquer parâmetro com permissões de leitura/gravação.  
  
   Apontar para o nome do parâmetro exibe o nome do parâmetro se a coluna **Nome** for muito estreita para mostrar o nome inteiro.  
  
- **Tipo**  
  
   A célula **Tipo de Parâmetro** usa o IntelliSense, o que lhe permite fazer escolhas em uma lista com todos os tipos disponíveis no projeto atual ou nos projetos referenciados.  
  
- **Modificador**  
  
   A célula **Modificador** em uma linha de parâmetro aceita e exibe o novo modificador do parâmetro. Para inserir um novo modificador de parâmetro, use a caixa de listagem suspensa para selecionar **Nenhum**, **ref**, **out** ou **params** no C# e **ByVal**, **ByRef** ou **ParamArray** no VB.  
  
- **Resumo**  
  
   A célula **Resumo** em uma linha de parâmetro permite inserir comentários de código que aparecem no IntelliSense ao inserir o parâmetro no editor de código.  
  
- **\<adicionar parâmetro>**  
  
   A última linha de parâmetro de um membro contém o texto **<add parameter>** na célula **Nome**. Clicar nessa célula permite criar um novo parâmetro. Para obter mais informações, consulte [Para adicionar um parâmetro a um método](../ide/creating-and-configuring-type-members-class-designer.md#HowToAddParameterToMethod).  
  
  **Propriedades do parâmetro na janela Propriedades**  
  
  A janela Propriedades exibe as mesmas propriedades de parâmetro exibidas na Janela Detalhes da Classe: **Nome**, **Tipo**, **Modificador**, **Resumo**, assim como a propriedade **Padrão Opcional**. Alterar uma propriedade em um local atualiza o valor da propriedade globalmente, incluindo a exibição de seu valor em outro local.  
  
> [!NOTE]
>  Para adicionar um parâmetro a um delegado, consulte [Criando membros](../ide/creating-and-configuring-type-members-class-designer.md#CreateMembers).  
  
> [!NOTE]
>  Embora um destruidor seja um método, ele não pode ter parâmetros.  
  
###  <a name="HowToAddParameterToMethod"></a> Para adicionar um parâmetro a um método  
  
1.  Na superfície de diagrama, clique no tipo que contém o método ao qual deseja adicionar um parâmetro.  
  
     O tipo obtém foco e seu conteúdo é exibido na janela Detalhes da Classe.  
  
2.  Na janela Detalhes da Classe, expanda a linha do método ao qual deseja adicionar um parâmetro.  
  
     Uma linha de parâmetro recuada é exibida, contendo apenas um par de parênteses e as palavras **\<adicionar parâmetro>.**  
  
3.  Clique em **\<adicionar parâmetro>**, digite o nome do novo parâmetro e pressione **Enter**.  
  
     O novo parâmetro é adicionado ao método e ao código do método. Ele é exibido na janela Detalhes da Classe e na janela Propriedades.  
  
4.  Se preferir, especifique outros detalhes sobre o parâmetro, como seu tipo.  
  
### <a name="to-add-an-optional-parameter-to-a-method"></a>Para adicionar um parâmetro opcional a um método  
  
1.  Na superfície de diagrama, clique no tipo que contém o método ao qual deseja adicionar um parâmetro opcional.  
  
     O tipo obtém foco e seu conteúdo é exibido na janela Detalhes da Classe.  
  
2.  Na janela Detalhes da Classe, expanda a linha do método ao qual deseja adicionar um parâmetro opcional.  
  
     Uma linha de parâmetro recuada é exibida, contendo apenas um par de parênteses e as palavras **\<adicionar parâmetro>.**  
  
3.  Clique em **\<adicionar parâmetro>**, digite o nome do novo parâmetro e pressione **Enter**.  
  
     O novo parâmetro é adicionado ao método e ao código do método. Ele é exibido na janela Detalhes da Classe e na janela Propriedades.  
  
4.  Na janela Propriedades, digite um valor para a propriedade **Padrão Opcional**. Definir a propriedade Padrão Opcional de um parâmetro o torna opcional.  
  
    > [!NOTE]
    >  Os parâmetros opcionais devem ser os últimos parâmetros na lista de parâmetros.  
  
##  <a name="ClassDetailsUsageNotes"></a> Observações de uso de Detalhes da Classe  
 Observe as dicas a seguir para usar a janela Detalhes da Classe.  
  
 **Células editáveis e não editáveis**  
  
 Todas as células na janela Detalhes da Classe são editáveis, com algumas exceções:  
  
- O tipo inteiro é somente leitura, quando, por exemplo, residir em um assembly referenciado (consulte [Exibição de informações somente leitura [Designer de Classe]](http://msdn.microsoft.com/en-us/33e2d3a9-1668-4d10-ae56-fa09b3156e0a).) Quando você seleciona a forma no Designer de Classe, a janela Detalhes da Classe exibe seus detalhes em um estado somente leitura.  
  
- Para indexadores, o nome é somente leitura e o restante (tipo, modificador, resumo) é editável.  
  
- Todos os genéricos têm parâmetros somente leitura na janela Detalhes da Classe. Para alterar um parâmetro genérico, edite seu código-fonte.  
  
- O nome do parâmetro de tipo que é definido em um tipo genérico é somente leitura.  
  
- Quando o código de um tipo é desfeito (não analisável), a janela Detalhes da Classe exibe o conteúdo do tipo como somente leitura.  
  
  **A Janela Detalhes da Classe e o código-fonte**  
  
- Você pode exibir o código-fonte clicando com o botão direito do mouse em uma forma na janela Detalhes da Classe (ou no Designer de Classe) e clicando em Exibir Código. O arquivo do código-fonte é aberto e rola até o elemento selecionado.  
  
- A alteração do código-fonte é refletida imediatamente na exibição das informações de assinatura no Designer de Classe e na janela Detalhes da Classe. Se a janela Detalhes da Classe estiver fechada no momento, as novas informações ficarão visíveis na próxima vez em que for aberta.  
  
- Quando o código de um tipo é desfeito (não analisável), a janela Detalhes da Classe exibe o conteúdo do tipo como somente leitura.  
  
  **Funcionalidade da Área de Transferência na Janela Detalhes da Classe**  
  
  Você pode copiar ou recortar campos ou linhas da janela Detalhes da Classe e colá-los em outro tipo. Uma linha poderá ser recortada se não for somente leitura. Quando você cola a linha, a janela Detalhes da Classe atribui um novo nome (derivado do nome da linha copiada) para evitar um conflito.  
  
##  <a name="ReadOnlyInfo"></a> Exibição de informações somente leitura  
 O Designer de Classe e a janela Detalhes da Classe podem exibir os tipos (e membros do tipo) para o seguinte:  
  
- um projeto que contém um diagrama de classes  
  
- um projeto referenciado de um projeto que contém um diagrama de classes  
  
- um assembly referenciado de um projeto que contém um diagrama de classes  
  
  Nos dois últimos casos, a entidade referenciada (um tipo ou um membro) é somente leitura no diagrama de classes que a representa.  
  
  Um projeto inteiro ou partes dele, como arquivos individuais, podem ser somente leitura. Os casos mais comuns em que um projeto ou um de seus arquivos é somente leitura são quando ele está sob controle do código-fonte (e não foi verificado), ele existe em um assembly externo ou quando o sistema operacional considera os arquivos como sendo somente leitura.  
  
  **Controle do código-fonte**  
  
  Como um diagrama de classes é salvo como um arquivo em um projeto, você precisa fazer check-out do projeto para salvar todas as alterações feitas no Designer de Classe ou na janela Detalhes da Classe.  
  
  **Projetos somente leitura**  
  
  O projeto pode ser somente leitura por um motivo que não seja o controle de código-fonte. Fechar o projeto exibe uma caixa de diálogo que pergunta se você deseja substituir o arquivo de projeto, descartar alterações (não salvar) ou cancelar a operação de fechar. Se você optar por substituir, os arquivos de projeto serão substituídos e transformados em leitura/gravação. O novo arquivo de diagrama de classes é adicionado.  
  
  **Tipos somente leitura**  
  
  Se você tentar salvar um projeto que contém um tipo cujo arquivo do código-fonte seja somente leitura, a caixa de diálogo **Salvamento de Arquivo Somente Leitura** será exibida, fornecendo opções de salvar o arquivo com um novo nome ou em um novo local, ou de substituir o arquivo somente leitura. Se você substituir o arquivo, a nova cópia não será mais somente leitura.  
  
  Se um arquivo de código contiver um erro de sintaxe, as formas que exibem o código nesse arquivo serão somente leitura temporariamente até que o erro de sintaxe seja corrigido. As formas nesse estado exibem texto em vermelho e um ícone vermelho que exibe uma dica de ferramenta onde se lê "O arquivo do código-fonte contém um erro de análise".  
  
  Um tipo referenciado (como um tipo do .NET Framework), que existe sob outro nó do projeto ou sob um nó de assembly referenciado, é indicado na superfície de design de Designer de Classe como somente leitura. Um tipo local, que existe no projeto que você abriu, é leitura/gravação e sua forma na superfície de design de Designer de Classe é indicada como tal.  
  
  Os indexadores são leitura/gravação no código e na janela Detalhes da Classe, mas o nome do indexador é somente leitura.  
  
  Não é possível editar métodos parciais usando o Designer de Classe ou a janela Detalhes da Classe; você deve usar o Editor de Código para editá-los.  
  
  Não é possível editar código C++ nativo usando o Designer de Classe ou a janela Detalhes da Classe; você deve usar o Editor de Código para editar código C++ nativo.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Exibindo tipos e relações (Designer de Classe)](../ide/viewing-types-and-relationships-class-designer.md)|Você pode exibir seus tipos, membros e relações existentes em um diagrama de classes.|  
|[Refatorando classes e tipos (Designer de Classe)](../ide/refactoring-classes-and-types-class-designer.md)|Ao usar a refatoração, você pode renomear o tipo e os membros de tipo com facilidade. Também é possível mover membros entre classes, dividir uma classe em classes parciais e implementar interfaces.|
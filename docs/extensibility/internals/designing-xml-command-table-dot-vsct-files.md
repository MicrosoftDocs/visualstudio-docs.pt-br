---
title: Criando tabela de comandos XML (. Arquivos de vsct) | Microsoft Docs
description: Saiba como criar um arquivo de tabela de comandos XML (. vsct) que descreve o layout e a aparência de itens de comando, incluindo botões, caixas de combinação, menus e barras de ferramentas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d6409b5e624cd8596e669f191b2644aaf27a88c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090922"
---
# <a name="design-xml-command-table-vsct-files"></a>Criar arquivos de tabela de comando XML (. vsct)
Um arquivo de tabela de comandos XML (*. vsct*) descreve o layout e a aparência de itens de comando para um VSPackage. Os itens de comando incluem botões, caixas de combinação, menus, barras de ferramentas e grupos de itens de comando. Este artigo descreve os arquivos de tabela de comando XML, como eles afetam os itens de comando e menus e como criá-los.

## <a name="commands-menus-groups-and-the-vsct-file"></a>Comandos, menus, grupos e o arquivo. vsct
 Os arquivos *. vsct* são organizados de acordo com os comandos, menus e grupos de comandos. As marcas XML no arquivo *. vsct* representam cada um desses itens, juntamente com outros itens associados, como botões de comando, posicionamento de comando e bitmaps.

 Quando você cria um novo VSPackage executando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] modelo de pacote, o modelo gera um arquivo *. vsct* com os elementos necessários para um comando de menu, uma janela de ferramentas ou um editor personalizado, dependendo de suas seleções. Esse arquivo *. vsct* pode ser modificado para atender aos requisitos de um VSPackage específico. Para obter exemplos de como modificar um arquivo *. vsct* , consulte [estender menus e comandos](../../extensibility/extending-menus-and-commands.md).

 Para criar um novo arquivo *. vsct* em branco, consulte [como: criar um arquivo *. vsct*](../../extensibility/internals/how-to-create-a-dot-vsct-file.md). Depois de criado, você adiciona elementos XML, atributos e valores ao arquivo para descrever o layout do item de comando. Para obter um esquema XML detalhado, consulte a [referência de esquema XML do vsct](../../extensibility/vsct-xml-schema-reference.md).

## <a name="differences-between-ctc-and-vsct-files"></a>Diferenças entre arquivos. CTC e. vsct
 Embora o significado por trás das marcas XML em um arquivo *. vsct* seja o mesmo que as marcas no formato de arquivo preterido Now *. CTC* , sua implementação é um pouco diferente:

- A nova **\<extern>** marca é onde você faz referência a outros arquivos *. h* a serem compilados, como os arquivos da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] barra de ferramentas.

- Embora arquivos *. vsct* ofereçam suporte à instrução **/include** , como arquivos *. CTC* , ele também apresenta um novo **\<import>** elemento. A diferença é que a **/include** traz *todas* as informações, enquanto **\<import>** traz apenas os nomes.

- Enquanto os arquivos *. CTC* exigem um arquivo de cabeçalho no qual você define as diretivas de pré-processador, um não é necessário para arquivos *. vsct* . Em vez disso, coloque as diretivas na tabela de símbolos, localizadas nos **\<Symbol>** elementos, localizadas na parte inferior do arquivo *. vsct* .

- os arquivos *. vsct* apresentam uma **\<Annotation>** marca, que permite que você insira todas as informações que desejar, como observações ou até mesmo imagens.

- Os valores são armazenados como atributos no item.

- Os sinalizadores de comando podem ser armazenados individualmente ou empilhados.  No entanto, o IntelliSense não funciona em sinalizadores de comando empilhados. Para obter mais informações sobre sinalizadores de comando, consulte o [elemento CommandFlag](../../extensibility/command-flag-element.md).

- Você pode especificar vários tipos, como listas suspensas de divisão, combinações, etc.

- Os GUIDs não são validados.

- Cada elemento de interface do usuário tem uma cadeia de caracteres que representa o texto que é exibido com ele.

- O pai é opcional. Se omitido, o *grupo* de valor Unknown será usado.

- O argumento *Icon* é opcional.

- Seção bitmap: Esta seção é igual a em um arquivo *. CTC* , exceto que agora você pode especificar um nome de arquivo via href que será extraído pelo compilador *vsct.exe* no momento da compilação.

- ResID: a ID de recurso de bitmap antiga pode ser usada e ainda funciona da mesma forma que nos arquivos *. CTC* .

- HRef: um novo método que permite especificar um nome de arquivo para o recurso de bitmap. Ele assume que todos são usados, portanto, você pode omitir a seção usada. O compilador primeiro procurará recursos locais para o arquivo, em seguida, em qualquer compartilhamento de rede e em todos os recursos definidos pela opção **/i** .

- Associação de teclas: você não precisa mais especificar um emulador. Se você especificar um, o compilador irá pressupor que o editor e o emulador sejam os mesmos.

- Keycordar: keycorda foi Descartado. O novo formato é *key1, MOD1, Key2, MOD2*.  Você pode especificar uma constante Character, hexadecimal ou VK.

O novo compilador, *vsct.exe*, compila os arquivos *. CTC* e *. vsct* . O compilador de *ctc.exe* antigo, no entanto, não reconhecerá nem compilará arquivos *. vsct* .

Você pode usar o compilador *vsct.exe* para converter um arquivo *. CTO* existente em um arquivo *. vsct* . Para obter mais informações, consulte [como: criar um arquivo. vsct de um arquivo. CTO existente](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file).

## <a name="the-vsct-file-elements"></a>Os elementos do arquivo. vsct
 A tabela de comandos tem a seguinte hierarquia e elementos:

- [Elemento commandtable](../../extensibility/commandtable-element.md): representa todos os comandos, grupos de menus e menus associados ao VSPackage.

- [Elemento externo](../../extensibility/extern-element.md): faz referência a todos os arquivos. h externos que você deseja mesclar com o arquivo *. vsct* .

- [Incluir elemento](../../extensibility/include-element.md): faz referência a qualquer arquivo de cabeçalho (. h) adicional que você deseja compilar junto com o arquivos *. vsct* . Um arquivo *. vsct* pode incluir arquivos *. h* contendo constantes que definem comandos, grupos de menus e menus que o IDE ou outro VSPackage fornece.

- [Elemento Commands](../../extensibility/commands-element.md): representa todos os comandos individuais que podem ser executados. Cada comando tem os quatro elementos filho a seguir:

- [Elemento menus](../../extensibility/menus-element.md): representa todos os menus e barras de ferramentas no VSPackage. Os menus são contêineres para grupos de comandos.

- [Elemento groups](../../extensibility/groups-element.md): representa todos os grupos no VSPackage. Grupos são coleções de comandos individuais.

- [Elemento Buttons](../../extensibility/buttons-element.md): representa todos os botões de comando e itens de menu no VSPackage. Os botões são controles visuais que podem ser associados a comandos.

- [Elemento bitmaps](../../extensibility/bitmaps-element.md): representa todos os bitmaps para todos os botões no VSPackage. Bitmaps são imagens que são exibidas ao lado de ou nos botões de comando, dependendo do contexto.

- [Elemento CommandPlacements](../../extensibility/commandplacements-element.md): indica locais adicionais em que os comandos individuais devem ser acessados nos menus de seu VSPackage.

- [Elemento VisibilityConstraints](../../extensibility/visibilityconstraints-element.md): especifica se um comando é exibido sempre ou apenas em determinados contextos, como quando uma caixa de diálogo ou janela específica é exibida. Os menus e comandos que têm um valor para esse elemento serão exibidos somente quando o contexto especificado estiver ativo. O comportamento padrão é exibir o comando em todos os momentos.

- [Elemento keybindings](../../extensibility/keybindings-element.md): especifica quaisquer associações de chave para os comandos. Ou seja, uma ou mais combinações de teclas que devem ser pressionadas para executar o comando, como **Ctrl** + **S**.

- [Elemento UsedCommands](../../extensibility/usedcommands-element.md): informa ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente que, embora o comando especificado seja implementado por outro código, quando o VSPackage atual estiver ativo, ele fornecerá a implementação do comando.

- [Elemento Symbols](../../extensibility/symbols-element.md): contém os nomes de símbolo e as IDs GUID para todos os seus comandos no pacote.

## <a name="vsct-file-design-guidelines"></a>Diretrizes de design de arquivo. vsct
 Para criar com êxito um arquivo *. vsct* , siga estas diretrizes.

- Os comandos podem ser colocados somente em grupos, os grupos podem ser colocados somente em menus e os menus podem ser colocados somente em grupos. Somente os menus são realmente exibidos no IDE, os grupos e os comandos não são.

- Os submenus não podem ser atribuídos diretamente a um menu, mas devem ser atribuídos a um grupo, que, por sua vez, é atribuído a um menu.

- Comandos, submenus e grupos podem ser atribuídos a um grupo ou menu de pai usando o campo pai de sua diretiva de definição.

- Organizar uma tabela de comandos exclusivamente por meio dos campos pai nas diretivas tem uma limitação significativa. As diretivas que definem objetos podem usar apenas um argumento pai.

- Reutilizar comandos, grupos ou submenus requer o uso de uma nova diretiva para criar uma nova instância do objeto com seu próprio `GUID:ID` par.

- Cada `GUID:ID` par deve ser exclusivo. O reuso de um comando que, por exemplo, foi colocado em um menu, em uma barra de ferramentas ou em um menu de contexto, é manipulado pela <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.

- Os comandos e os submenus também podem ser atribuídos a vários grupos, e os grupos podem ser atribuídos a vários menus usando o [elemento Commands](../../extensibility/commands-element.md).

## <a name="vsct-file-notes"></a>observações do arquivo. vsct
 Se você fizer alterações em um arquivo *. vsct* depois de compilá-lo e colocá-lo em uma DLL satélite nativa, deverá executar **devenv.exe/setup/nosetupvstemplates**. Isso força os recursos de VSPackage especificados no registro experimental a serem relidos e o banco de dados interno que descreve [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] a ser recriado.

 Durante o desenvolvimento, é possível que vários projetos VSPackage sejam criados e registrados no hive experimental do registro, o que pode causar confusão confusa no IDE. Para corrigir isso, você pode redefinir o hive experimental para as configurações padrão para remover todos os VSPackages registrados e quaisquer alterações que possam ter feito no IDE. Para redefinir o hive experimental, use a ferramenta CreateExpInstance.exe que vem com o SDK do Visual Studio. Você pode encontrá-lo em:

 *% PROGRAMfiles (x86)% \ SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exedo Visual Studio \\ \<version>*

 Execute a ferramenta usando o comando **CreateExpInstance/Reset reiniciar**. Lembre-se de que essa ferramenta remove do hive experimental todos os VSPackages registrados normalmente não instalados com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="see-also"></a>Confira também
- [Estender menus e comandos](../../extensibility/extending-menus-and-commands.md)

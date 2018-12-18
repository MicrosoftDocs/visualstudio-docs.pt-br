---
title: Criando tabela de comando XML (. Arquivos VSCT) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4e94d93d407f7499afbd43c8af2b7532ca1b4d8e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934555"
---
# <a name="design-xml-command-table-vsct-files"></a>Criar arquivos de tabela (. VSCT) do comando XML
Uma tabela de comando do XML (*VSCT*) arquivo descreve o layout e aparência de itens de comando para um VSPackage. Itens de comando incluem caixas de combinação, botões, menus, barras de ferramentas e grupos de itens de comando. Este artigo descreve os arquivos da tabela de comandos XML, como eles afetam os menus e itens de comando e como criá-los.

## <a name="commands-menus-groups-and-the-vsct-file"></a>Comandos, menus, grupos e o arquivo. VSCT
 O *VSCT* arquivos são organizados em torno de comandos, menus e grupos de comando. As marcas XML na *VSCT* representam cada um desses itens, juntamente com outros itens associados, como botões de comando, o posicionamento de comando e bitmaps de arquivo.

 Quando você cria um novo VSPackage, executando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] modelo de pacote, o modelo gera uma *VSCT* arquivo com os elementos necessários para um comando de menu, a janela da ferramenta ou o editor personalizado, dependendo de suas seleções. Isso *VSCT* arquivo, em seguida, pode ser modificado para atender aos requisitos de um VSPackage específico. Para obter exemplos de como modificar um *VSCT* arquivos, consulte [estendem os menus e comandos](../../extensibility/extending-menus-and-commands.md).

 Para criar um novo, em branco *VSCT* arquivos, consulte [como: criar um *VSCT* arquivo](../../extensibility/internals/how-to-create-a-dot-vsct-file.md). Depois de criar, adicionar elementos, atributos e valores XML para o arquivo para descrever o layout do item de comando. Para um esquema XML detalhado, consulte o [referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md).

## <a name="differences-between-ctc-and-vsct-files"></a>Diferenças entre arquivos. ctc e. VSCT
 Enquanto o significado por trás do XML de marcas em um *VSCT* arquivo são os mesmos que essas marcas no agora está preterido *. ctc* formato de arquivo, sua implementação é um pouco diferente:

- O novo  **\<extern >** marca é onde você referenciar outros *. h* arquivos a serem compilados, como esses arquivos para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] barra de ferramentas.

- Enquanto *VSCT* arquivos de suporte a **/ incluem** instrução, como *. ctc* fazer de arquivos, ele também apresenta um novo  **\<Importar >** elemento. A diferença é que **/include** traz *todos os* da informação, enquanto  **\<Importar >** traz apenas os nomes.

- Embora *. ctc* arquivos exigem um arquivo de cabeçalho no qual você define suas diretivas de pré-processador, não é necessária para *VSCT* arquivos. Em vez disso, colocar suas diretivas na tabela de símbolo, localizada na  **\<símbolo >** elementos, localizados na parte inferior da *VSCT* arquivo.

- *VSCT* recurso de arquivos de um  **\<anotação >** marca, que permite que você insira todas as informações que desejar, como anotações ou até mesmo as imagens.

- Valores são armazenados como atributos no item.

- Sinalizadores de comando podem ser armazenadas individualmente ou empilhados.  IntelliSense, no entanto, não funciona em sinalizadores de comando empilhadas. Para obter mais informações sobre os sinalizadores de comando, consulte o [CommandFlag elemento](../../extensibility/command-flag-element.md).

- Você pode especificar vários tipos, como listas suspensas de divisão, combos, etc.

- GUIDs não validam.

- Cada elemento de interface do usuário tem uma cadeia de caracteres que representa o texto que é exibido com ele.

- O pai é opcional. Se omitido, o valor *grupo desconhecido* é usado.

- O *ícone* argumento é opcional.

- Seção de bitmap: Esta seção é o mesmo que em uma *. ctc* do arquivo, exceto que agora você pode especificar um nome de arquivo por meio de Href que será recebida pelo *vsct.exe* compilador em tempo de compilação.

- ResID: Resource ID pode ser usada e ainda funciona mesmo que de bitmap antigo *. ctc* arquivos.

- HRef: Um novo método que permite que você especifique um nome de arquivo para o recurso de bitmap. Ele pressupõe que são usados, portanto, você pode omitir a seção usada. O compilador primeiro procurar os recursos locais para o arquivo e, em seguida, em qualquer compartilhamento de rede e todos os recursos definidos pela **/I** alternar.

- Associação de teclas: Você não precisa especificar um emulador. Se você especificar um, o compilador assumirá que o editor e o emulador são os mesmos.

- Keychord: Keychord foi descartada. É o novo formato *Key1, Mod1, Key2, Mod2*.  Você pode especificar um caractere, hexadecimal ou constante VK.
       
O novo compilador, *vsct.exe*, compila ambas *. ctc* e *VSCT* arquivos. O antigo *ctc.exe* compilador, no entanto, não reconhecerão ou compile *VSCT* arquivos.

Você pode usar o *vsct.exe* compilador para converter um existente *CTO já* o arquivo em um *VSCT* arquivo. Para obter mais informações, consulte [como: criar um arquivo. VSCT de um arquivo CTO já existente](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file).

## <a name="the-vsct-file-elements"></a>Os elementos do arquivo. VSCT
 A tabela de comando tem a hierarquia e os elementos a seguir:

 [Elemento CommandTable](../../extensibility/commandtable-element.md): representa todos os comandos, grupos de menus e menus associados com o VSPackage.

 [Elemento extern](../../extensibility/extern-element.md): faz referência a todos os arquivos. h externa você deseja mesclar com o *VSCT* arquivo.

 [Incluir o elemento](../../extensibility/include-element.md): faz referência a todos os arquivos adicionais de cabeçalho (. h) você deseja compilar junto com seu *VSCT* arquivo. Um *VSCT* arquivo pode incluir *. h* arquivos que contêm constantes que definem os comandos, grupos de menus e menus que fornece o IDE ou outro VSPackage.

 [Elemento Commands](../../extensibility/commands-element.md): representa todos os comandos individuais que podem ser executados. Cada comando tem os seguintes elementos quatro filho:

 [Elemento menus](../../extensibility/menus-element.md): representa todos os menus e barras de ferramentas do VSPackage. Menus são contêineres para grupos de comandos.

 [Elemento Groups](../../extensibility/groups-element.md): representa todos os grupos em VSPackage. Grupos são coleções de comandos individuais.

 [Elemento Buttons](../../extensibility/buttons-element.md): representa todos os botões de comando e itens de menu em um VSPackage. Botões são controles visuais que podem ser associados a comandos.

 [Elemento bitmaps](../../extensibility/bitmaps-element.md): representa todos os bitmaps para todos os botões em VSPackage. Os bitmaps são imagens que são exibidas ao lado ou nos botões de comando, dependendo do contexto.

 [Elemento CommandPlacements](../../extensibility/commandplacements-element.md): indica os locais adicionais em que os comandos individuais devem ser colocado no local nos menus do VSPackage.

 [Element visibilityconstraints](../../extensibility/visibilityconstraints-element.md): Especifica se um comando exibe em todos os horários, ou apenas em determinados contextos, como quando uma caixa de diálogo específica ou a janela é exibida. Menus e comandos que têm um valor para esse elemento serão exibido somente quando o contexto especificado está ativo. O comportamento padrão é exibir o comando em todos os momentos.

 [Elemento KeyBindings](../../extensibility/keybindings-element.md): especifica quaisquer associações de teclas para os comandos. Ou seja, um ou mais combinações de teclas que devem ser pressionadas para executar o comando, como **Ctrl**+**S**.

 [Elemento UsedCommands](../../extensibility/usedcommands-element.md): informa o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente que, embora o comando especificado é implementado por outro código, quando o VSPackage atual está ativo, ele fornece a implementação do comando.

 [Elemento Symbols](../../extensibility/symbols-element.md): contém os nomes de símbolos e IDs de GUID para todos os seus comandos no pacote.

## <a name="vsct-file-design-guidelines"></a>diretrizes de design do arquivo. VSCT
 Design com êxito uma *VSCT* de arquivos, siga estas diretrizes.

-   Comandos podem ser colocados somente em grupos, grupos podem ser colocados somente nos menus e menus podem ser colocados apenas em grupos. Somente os menus, na verdade, são exibidos no IDE, grupos e comandos não são.

-   Submenus não podem ser atribuídos diretamente a um menu, mas devem ser atribuídos a um grupo, que por sua vez é atribuído a um menu.

-   Comandos, submenus e grupos podem ser atribuídos a um grupo de gerenciamento do domínio pai ou menu usando o campo pai da sua diretiva de definição.

-   Organizar uma tabela de comando somente por meio dos campos pai nas diretivas tem uma limitação significativa. As diretivas que definem objetos podem levar o argumento de apenas um pai.

-   Reutilização de comandos, grupos ou submenus requer o uso de uma diretiva de novo para criar uma nova instância do objeto com seu próprio `GUID:ID` par.

-   Cada `GUID:ID` par deve ser exclusivo. Reutilizar um comando que, por exemplo, foi colocado em um menu, uma barra de ferramentas, ou em um menu de contexto, é tratada pelo <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.

-   Comandos e submenus também podem ser atribuídos a vários grupos e grupos podem ser atribuídos a vários menus usando o [elemento Commands](../../extensibility/commands-element.md).

## <a name="vsct-file-notes"></a>Notas de arquivo. VSCT
 Se você fizer alterações para um *VSCT* arquivo depois de compilá-lo e colocá-lo em uma DLL de satélite nativo, você deve ser executado **devenv.exe /setup /nosetupvstemplates**. Fazendo força caso especificados no registro experimental para ser lidos novamente e o banco de dados interno que descreve os recursos de VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] seja recriado.

 Durante o desenvolvimento, é possível que vários projetos de VSPackage seja criado e registrado na seção do registro experimental que pode levar a bagunça confusa no IDE. Para corrigir isso, você pode redefinir o hive experimental para as configurações padrão para remover todos os VSPackages e as alterações que fez o IDE. Para redefinir o hive experimental, use a ferramenta de CreateExpInstance.exe que vem com o SDK do Visual Studio. Você pode encontrá-lo em:

 *% PROGRAMFILES (x86) %\Visual Studio\\\<versão > SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe*

 Execute a ferramenta usando o comando **CreateExpInstance /Reset**. Lembre-se de que essa ferramenta remove do hive experimental todos os os VSPackages registrados não são normalmente instalados com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

## <a name="see-also"></a>Consulte também
 [Ampliar menus e comandos](../../extensibility/extending-menus-and-commands.md)
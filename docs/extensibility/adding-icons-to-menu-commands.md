---
title: Adicionando ícones a comandos de menu | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c9f038dc43c1705a7cef47eb09a17607c535e307
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903435"
---
# <a name="add-icons-to-menu-commands"></a>Adicionar ícones a comandos de menu
Os comandos podem aparecer em menus e barras de ferramentas. Nas barras de ferramentas, é comum que um comando seja exibido com apenas um ícone (para economizar espaço) enquanto nos menus um comando normalmente aparece com um ícone e texto.

 Os ícones têm 16 pixels de largura por 16 pixels de altura e podem ter uma intensidade de cor de 8 bits (256 cores) ou profundidade de cor de 32 bits (true color). os ícones de cor de 32 bits são preferenciais. Os ícones normalmente são organizados em uma única linha horizontal em um único bitmap, embora sejam permitidos vários bitmaps. Esse bitmap é declarado no arquivo *. vsct* junto com os ícones individuais disponíveis no bitmap. Consulte a referência para o [elemento bitmaps](../extensibility/bitmaps-element.md) para obter mais detalhes.

## <a name="add-an-icon-to-a-command"></a>Adicionar um ícone a um comando
 O procedimento a seguir pressupõe que você tenha um projeto VSPackage existente com um comando de menu. Para saber como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

1. Crie um bitmap com uma intensidade de cor de 32 bits. Um ícone é sempre 16 x 16, portanto, esse bitmap deve ter 16 pixels de altura e um múltiplo de 16 pixels de largura.

     Cada ícone é colocado no bitmap ao lado um do outro em uma única linha. Use o canal alfa para indicar os locais de transparência em cada ícone.

     Se você usar uma profundidade de cor de 8 bits, use magenta, `RGB(255,0,255)` , como a transparência. No entanto, os ícones de cor de 32 bits são preferenciais.

2. Copie o arquivo de ícone para o diretório de *recursos* em seu projeto VSPackage. No **Gerenciador de soluções**, adicione o ícone ao projeto. (Selecione **recursos**e, no menu de contexto, clique em **Adicionar**, depois em **Item existente**e selecione o arquivo de ícone.)

3. Abra o arquivo *. vsct* no editor.

4. Adicione um `GuidSymbol` elemento com um nome de **testIcon**. Crie um GUID (**ferramentas**  >  **Create GUID**, selecione o **formato do registro** e clique em **copiar**) e cole-o no `value` atributo. O resultado deve ser assim:

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. Adicione um `<IDSymbol>` para o ícone. O `name` atributo é a ID do ícone e `value` indica sua posição na faixa, se houver. Se houver apenas um ícone, adicione 1. O resultado deve ser assim:

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. Crie um `<Bitmap>` na `<Bitmaps>` seção do arquivo *. vsct* para representar o bitmap que contém os ícones.

    - Defina o `guid` valor para o nome do `<GuidSymbol>` elemento que você criou na etapa anterior.

    - Defina o `href` valor para o caminho relativo do arquivo de bitmap (nesse caso, **recursos \\<nome \> do arquivo de ícone**.

    - Defina o `usedList` valor para o IDSymbol que você criou anteriormente. Esse atributo especifica uma lista delimitada por vírgulas dos ícones a serem usados no VSPackage. Os ícones que não estão na lista são de compilação de formulário excluída.

         O bloco de bitmap deve ter a seguinte aparência:

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. No elemento existente `<Button>` , defina o `Icon` elemento para os valores GUIDSymbol e IDSymbol que você criou anteriormente. Aqui está um exemplo de um elemento Button com esses valores:

    ```xml
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />
        <Icon guid="testIcon" id="testIcon1" />
        <Strings>
            <ButtonText>My Command name</ButtonText>
        </Strings>
    </Button>
    ```

8. Teste seu ícone. Compile o projeto e comece a depuração. Na instância experimental, localize o comando. Ele deve mostrar o ícone que você adicionou.

## <a name="see-also"></a>Confira também
- [Estendendo menus e comandos](../extensibility/extending-menus-and-commands.md)
- [Referência de esquema XML VSCT](../extensibility/vsct-xml-schema-reference.md)

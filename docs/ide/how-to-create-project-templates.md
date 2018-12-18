---
title: Criar modelos de projeto para Visual Studio
ms.date: 01/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ExportTemplateWizard
helpviewer_keywords:
- project templates [Visual Studio], creating
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 05ba1dcd5328b80d8fa5526336cf027995abf7dc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903719"
---
# <a name="how-to-create-project-templates"></a>Como criar modelos de projeto

Este tópico mostra como criar um modelo usando o **Assistente de Exportação de Modelo**, que empacota o modelo em um arquivo *.zip*.

## <a name="to-create-a-user-project-template-by-using-the-export-template-wizard"></a>Para criar um modelo de projeto de usuário usando o Assistente para Exportar Modelo

1. Criar um projeto.

    > [!NOTE]
    > Use apenas caracteres identificadores válidos para nomear um projeto que será a origem de um modelo. Caso contrário, poderão ocorrer erros de compilação nos projetos criados usando o modelo. Para obter mais informações sobre caracteres identificadores válido, consulte [Nomes de elementos declarados (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/declared-elements/declared-element-names) ou [Identificadores (C++)](/cpp/cpp/identifiers-cpp). Como alternativa, você pode usar [parâmetros de modelo](../ide/template-parameters.md) para usar nomes "seguros" para classes e namespaces.

2. Edite o projeto até que ele esteja pronto para ser exportado como um modelo. Por exemplo, você talvez queira editar arquivos de código para indicar onde a substituição de parâmetro deve ocorrer. Consulte [Como substituir parâmetros em um modelo](../ide/how-to-substitute-parameters-in-a-template.md).

3. No menu **Projeto**, escolha **Exportar Modelo**.

   O **Assistente para Exportar Modelo** é aberto.

4. Na página **Escolher Tipo de Modelo**, selecione **Modelo de Projeto**. Selecione o projeto que você deseja exportar como um modelo e, em seguida, escolha **Avançar**.

5. Na página **Selecionar Opções do Modelo**, insira um nome e uma descrição opcional, um ícone e uma imagem de exibição para o modelo. Esses itens serão exibidos na caixa de diálogo **Novo Projeto**. Escolha **Concluir**.

   O projeto será exportado para um arquivo *.zip* e colocado no local de saída especificado e, se selecionado, importado para o Visual Studio.

>[!NOTE]
> Para localizar o modelo na caixa de diálogo **Novo Projeto**, expanda **Instalado** e, em seguida, expanda a categoria que corresponde ao elemento `ProjectType` no arquivo *.vstemplate*. Por exemplo, um arquivo *.vstemplate* que contém `<ProjectType>CSharp</ProjectType>` aparece sob **Instalado** > **Visual C#**, por padrão. Para organizar seu modelo em um subdiretório do tipo de projeto basta criar uma pasta nesse diretório e colocar o arquivo *.zip* do modelo nele. Para obter mais informações, consulte [Como localizar e organizar modelos](../ide/how-to-locate-and-organize-project-and-item-templates.md).

## <a name="other-ways-to-create-project-templates"></a>Outras maneiras de criar modelos de projeto

Você pode criar modelos de projeto manualmente reunindo os arquivos que constituem o projeto em uma pasta e, em seguida, criando um arquivo XML *.vstemplate* com os metadados apropriados. Para obter mais informações, consulte [Como criar manualmente modelos da Web](../ide/how-to-manually-create-web-templates.md).

Se o SDK do Visual Studio estiver instalado, você poderá encapsular o modelo concluído em um arquivo VSIX para implantação usando o modelo **Projeto VSIX**. Para obter mais informações, consulte [Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md).

## <a name="see-also"></a>Consulte também

- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos de item](../ide/how-to-create-item-templates.md)
- [Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)
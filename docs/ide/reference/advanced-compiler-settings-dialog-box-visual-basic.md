---
title: Caixa de diálogo Configurações de Compilador Avançadas (Visual Basic)
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedCompile
helpviewer_keywords:
- Advanced Compiler Settings dialog box
ms.assetid: 1f81133a-293f-4dba-bc1c-8baafb01d857
author: TerryGLee
ms.author: ghogen
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 0c0e6e9d41bb1d4bd7446bb77306ca5a4551906f
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419101"
---
# <a name="advanced-compiler-settings-dialog-box-visual-basic"></a>Caixa de diálogo Configurações de Compilador Avançadas (Visual Basic)

Use a caixa de diálogo **Configurações Avançadas do Compilador** do **Designer de Projeto** para especificar as propriedades avançadas de configuração de build do projeto. Essa caixa de diálogo aplica-se a somente projetos Visual Basic.

## <a name="to-access-this-dialog-box"></a>Para acessar essa caixa de diálogo

1. No **Gerenciador de Soluções**, escolha um nó do projeto (não o nó **Solução**).

2. No menu **Projeto** , clique em **Propriedades**. Quando o **Designer de projeto** for exibido, clique na guia **Compilar** .

3. Na [Página Compilar, Designer de Projeto (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md), selecione a **Configuração** e a **Plataforma**. Nas configurações de build simplificadas, as listas **Configuração** e **Plataforma** não são exibidas. Para saber mais, consulte [Como definir configurações de depuração e versão](../../debugger/how-to-set-debug-and-release-configurations.md).

4. Clique em **Opções Avançadas de Compilação**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="optimizations"></a>Otimizações

As opções a seguir especificam otimizações que podem, em alguns casos, diminuir um arquivo de programa, fazer um programa executar mais rapidamente ou acelerar o processo de build.

**Remover verificações de estouro de inteiro**

Por padrão, essa caixa de seleção está desmarcada para habilitar a verificação de estouro de inteiro. Marque essa caixa de seleção para remover a verificação de estouro de inteiro. Se você marcar essa caixa de seleção, os cálculos de inteiro poderão ser mais rápidos. No entanto, se você remover a verificação de estouro e as capacidades de tipo de dados estourarem, resultados incorretos poderão ser armazenados sem gerar um erro.

Se as condições de estouro estiverem marcadas e uma operação de inteiro estourar, uma exceção <xref:System.OverflowException> será lançada. Se as condições de estouro não forem verificadas, os estouros de operação de inteiro não gerarão uma exceção.

**Habilitar otimizações**

Por padrão, essa caixa de seleção está desmarcada para desabilitar as otimizações do compilador. Marque essa caixa de seleção para habilitar otimizações do compilador. Otimizações do compilador tornam o arquivo de saída menor, mais rápido e mais eficiente. No entanto, uma vez que otimizações causam reorganização de código no arquivo de saída, as otimizações do compilador podem dificultar a depuração.

 **Endereço básico de DLL**

Essa caixa de texto exibe o endereço básico de DLL padrão em formato hexadecimal. Em projetos de Biblioteca de Classes e Biblioteca de Controle, você pode usar essa caixa de texto para especificar o endereço básico a ser usado quando a DLL é criada.

 **Gerar informações de depuração**

Selecione **Nenhum**, **Completo** ou **Somente pdb** na lista. **Nenhum** especifica que nenhuma informação de depuração deve ser gerada. **Completo** especifica que informações de depuração completas devem ser geradas e **Somente pdb** especifica que apenas as informações de depuração de PDB devem ser geradas. O valor padrão desta opção é **Completo**.

## <a name="compilation-constants"></a>Constantes de Compilação

Constantes de compilação condicional têm um efeito semelhante ao de usar uma diretiva de pré-processador [#Const](/dotnet/visual-basic/language-reference/directives/const-directive) em um arquivo de origem, exceto que constantes definidas são públicas e aplicam-se a todos os arquivos no projeto. Você pode usar constantes de compilação condicionais junto com a diretiva [#If... Then... #Else](/dotnet/visual-basic/language-reference/directives/if-then-else-directives) para compilar os arquivos de origem condicionalmente. Consulte [Compilação Condicional](/dotnet/visual-basic/programming-guide/program-structure/conditional-compilation).

 **Definir constante de depuração**

Por padrão, essa caixa de seleção é marcada, especificando que uma constante DEBUG deve ser definida.

 **Definir a constante TRACE**

Por padrão, essa caixa de seleção é marcada, especificando que uma constante TRACE deve ser definida.

 **Constantes personalizadas**

Insira quaisquer constantes personalizadas para seu aplicativo nessa caixa de texto. As entradas devem ser delimitadas por vírgulas usando este formato: **Name1="Value1",Name2="Value2",Name3="Value3"**.

## <a name="other-settings"></a>Outras configurações

**Gerar assemblies de serialização**

Essa configuração especifica se o compilador criará os assemblies de serialização XML. Os assemblies de serialização poderão melhorar o desempenho da inicialização de <xref:System.Xml.Serialization.XmlSerializer> se você tiver usado essa classe para serializar os tipos no código. O valor padrão dessa opção é **auto**. **Auto** especifica que os assemblies de serialização serão gerados somente se você tiver usado <xref:System.Xml.Serialization.XmlSerializer> para codificar tipos em seu código para XML. **Desativado** especifica que os assemblies de serialização nunca devem ser gerados, independentemente de o código usar <xref:System.Xml.Serialization.XmlSerializer>. **Ativado** especifica que os assemblies de serialização sempre devem ser gerados. Os assemblies de serialização são chamados `TypeName`.XmlSerializers.dll.

## <a name="see-also"></a>Veja também

- [Página de Compilação, Designer de Projeto (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)

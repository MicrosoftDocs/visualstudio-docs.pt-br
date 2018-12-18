---
title: Renomear a refatoração (c#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.csharp.refactoring.rename
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Rename
- Rename refactoring [C#]
ms.assetid: 268942fc-b142-4dfa-8d90-bedd548c2e4f
caps.latest.revision: 45
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d88cf6d88f23a3a079d5f9a556c316a204c9ef27
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49274957"
---
# <a name="rename-refactoring-c"></a>Refatoração Renomear (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Renomear** é um recurso de refatoração no ambiente de desenvolvimento integrado (IDE) do Visual Studio que fornece uma maneira fácil de renomear identificadores para símbolos de código, como campos, variáveis locais, métodos, namespaces, propriedades e tipos. **Renomear** pode ser usado para alterar os nomes em comentários em cadeias de caracteres e para alterar as declarações e chamadas de um identificador.  
  
> [!NOTE]
>  Ao usar o controle de origem para o Visual Studio, obtenha a versão mais recente das fontes antes de tentar realizar a refatoração de renomeação.  
  
 Refatoração de renomeação está disponível dos seguintes recursos do Visual Studio:  
  
|Recurso|Comportamento de refatoração no IDE|  
|-------------|----------------------------------------|  
|Editor de Códigos|No Editor de código, refatoração de renomeação está disponível quando você posiciona o cursor em determinados tipos de símbolos de código. Quando o cursor está nessa posição, você pode invocar o **renomeie** comando digitando o atalho de teclado (CTRL + R, CTRL + R), ou selecionando o **Renomear** comando de uma marca inteligente, o menu de atalho ou o  **Refatorar** menu.|  
|Exibição de Classe|Quando você seleciona um identificador na exibição de classe, a refatoração de renomeação está disponível no menu de atalho e **refatorar** menu.|  
|Pesquisador de Objetos|Quando você seleciona um identificador no Pesquisador de objetos, refatoração de renomeação está disponível apenas a **refatorar** menu.|  
|Grade de propriedade do Designer de formulários do Windows|No **grade de propriedade** do Designer de formulários do Windows, alterando o nome de um controle iniciará uma operação de renomeação para esse controle. O **Renomear** caixa de diálogo não aparecerá.|  
|Gerenciador de Soluções|Na **Gerenciador de soluções**, um **Renomear** comando está disponível no menu de atalho. Se o arquivo de origem selecionado contém uma classe cujo nome de classe é o mesmo que o nome do arquivo, você pode usar esse comando para renomear o arquivo de origem e executar a refatoração de renomeação de simultaneamente.<br /><br /> Por exemplo, se você criar um aplicativo do padrão baseado em Windows e, em seguida, renomeie Form1.cs para TestForm.cs, o nome do arquivo de origem Form1.cs será alterado para TestForm.cs e a classe Form1 e todas as referências para que a classe será renomeada para TestForm. **Observação:** as **desfazer** comando (CTRL + Z) apenas cancelará a refatoração de renomeação no código e será não alterar o nome do arquivo de volta para o nome original. <br /><br /> Se o arquivo de origem selecionado não contém uma classe cujo nome é o mesmo que o nome do arquivo, o **Renomear** comando **Gerenciador de soluções** apenas renomeará o arquivo de origem e não executará renomeação refatoração.|  
  
## <a name="rename-operations"></a>Operações de renomeação  
 Quando você executa **Renomear**, o mecanismo de refatoração executa um específico da operação de renomeação cada símbolo de código, conforme descrito na tabela a seguir.  
  
|Símbolo de código|Renomear a operação|  
|-----------------|----------------------|  
|Campo|Altera a declaração e usos do campo para o novo nome.|  
|variável local|Altera a declaração e usos da variável para o novo nome.|  
|Método|Altera o nome do método e todas as referências a esse método para o novo nome. **Observação:** quando você renomeia um método de extensão, a operação de renomeação é propagada para todas as instâncias do método que estão no escopo, independentemente se o método de extensão está sendo usado como um método estático ou um método de instância. Para obter mais informações, consulte [Métodos de extensão](http://msdn.microsoft.com/library/175ce3ff-9bbf-4e64-8421-faeb81a0bb51).|  
|Namespace|Altera o nome do namespace para o novo nome na declaração, todas as `using` instruções e nomes totalmente qualificados. **Observação:** ao renomear um namespace [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] também atualiza o **Namespace padrão** propriedade no **aplicativo** página do **Project Designer**. Essa propriedade não pode ser redefinida, selecionando **desfazer** da **editar** menu. Para redefinir a **Namespace padrão** valor da propriedade, você deve modificar a propriedade nas **Designer de projeto**. Para obter mais informações, consulte [página de aplicativo](../ide/reference/application-page-project-designer-csharp.md).|  
|Propriedade|Altera a declaração e usos da propriedade para o novo nome.|  
|Tipo|Altera todas as declarações e todos os usos do tipo para o novo nome, incluindo construtores e destruidores. Para tipos parciais, a operação de renomeação será propagado para todas as partes.|  
  
#### <a name="to-rename-an-identifier"></a>Para renomear um identificador  
  
1.  Crie um aplicativo de console chamado `RenameIdentifier`e, em seguida, substitua `Program` com o código de exemplo a seguir.  
  
    ```csharp  
    class ProtoClassA  
    {  
        // Invoke on 'MethodB'.  
        public void MethodB(int i, bool b) { }  
    }  
  
    class ProtoClassC  
    {  
        void D()  
        {  
            ProtoClassA MyClassA = new ProtoClassA();  
  
            // Invoke on 'MethodB'.  
            MyClassA.MethodB(0, false);  
        }  
    }  
    ```  
  
2.  Coloque o cursor em `MethodB`, na declaração de método ou a chamada de método.  
  
3.  Dos **refatorar** menu, selecione **Renomear**. O **Renomear** caixa de diálogo é exibida.  
  
     Pode também clicar duas vezes o cursor, aponte para **refatorar** no menu de contexto e clique **Renomear** para exibir o **Renomear** caixa de diálogo.  
  
4.  No **newname** , digite `MethodC`.  
  
5.  Selecione o **pesquisa nos comentários** caixa de seleção.  
  
6.  Clique em **OK**.  
  
7.  No **visualizar alterações** caixa de diálogo, clique em **aplicar**.  
  
#### <a name="to-rename-an-identifier-using-smart-tags"></a>Para renomear um identificador usando smart tags  
  
1.  Crie um aplicativo de console chamado `RenameIdentifier`e, em seguida, substitua `Program` com o código de exemplo a seguir.  
  
    ```csharp  
    class ProtoClassA  
    {  
        // Invoke on 'MethodB'.  
        public void MethodB(int i, bool b) { }  
    }  
  
    class ProtoClassC  
    {  
        void D()  
        {  
            ProtoClassA MyClassA = new ProtoClassA();  
  
            // Invoke on 'MethodB'.  
            MyClassA.MethodB(0, false);  
        }  
    }  
    ```  
  
2.  Na declaração para `MethodB`, digite ou backspace sobre o identificador de método. Será exibido um prompt de marca inteligente abaixo esse identificador.  
  
    > [!NOTE]
    >  Não é possível invocar usando smart tags na declaração de um identificador de refatoração de renomeação.  
  
3.  Digite o atalho de teclado SHIFT + ALT + F10 e, em seguida, pressione a seta para baixo para exibir o menu de marca inteligente.  
  
     -ou-  
  
     Mova o ponteiro do mouse sobre o aviso de marca inteligente para exibir a marca inteligente. Em seguida, mova o ponteiro do mouse sobre a marca inteligente e clique na seta para baixo para exibir o menu de marca inteligente.  
  
4.  Selecione o **renomear '\<identifer1 >' para '\<identifier2 >'** item de menu para invocar refatoração de renomeação sem uma visualização das alterações ao seu código. Todas as referências aos  **\<identifer1 >** serão automaticamente atualizadas para  **\<identifier2 >**.  
  
     -ou-  
  
     Selecione o **renomear com visualização** item de menu para invocar refatoração Renomear com uma visualização das alterações ao seu código. O **visualizar alterações** caixa de diálogo será exibida.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="renaming-implemented-or-overridden-members"></a>Renomeando implementado ou membros substituídos  
 Quando você **renomeie** um membro que implementa/substituições ou é implementado/substituídas pelos membros em outros tipos, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] exibe uma caixa de diálogo informando que a operação de renomeação fará com que as atualizações em cascata. Se você clicar **continuar**, recursivamente o mecanismo refatoração localiza e renomeia todos os membros na base de dados e tipos derivados que têm implementa/substituições relações com o membro que está sendo renomeado.  
  
 O exemplo de código a seguir contém membros com relações implementa/substituições.  
  
 [!code-csharp[CsUsingCsIDERefactor#1](../snippets/csharp/VS_Snippets_VBCSharp/CsUsingCsIDERefactor/CS/Class1.cs#1)]  
  
 No exemplo anterior, renomeando `C.Method()` também renomeia `Ibase.Method()` porque `C.Method()` implementa `Ibase.Method()`. Em seguida, recursivamente o mecanismo de refatoração que vê `Ibase.Method()` é implementado por `Derived.Method()` e renomeia `Derived.Method()`. O mecanismo de refatoração não renomeia `Base.Method()`, pois `Derived.Method()` não substitui `Base.Method()`. O mecanismo de refatoração para aqui a menos que você tenha **Renomear sobrecargas** check-in a **Renomear** caixa de diálogo.  
  
 Se **Renomear sobrecargas** estiver marcada, o mecanismo de refatorar renomeia `Derived.Method(int i)` porque sobrecarrega `Derived.Method()`, `Base.Method(int i)` porque ele é substituído pelo `Derived.Method(int i)`, e `Base.Method()` porque ele é uma sobrecarga de `Base.Method(int i)`.  
  
> [!NOTE]
>  Quando você renomeia um membro que foi definido em um assembly referenciado, uma caixa de diálogo explica que a renomeação causará erros de compilação.  
  
## <a name="renaming-properties-of-anonymous-types"></a>Renomear propriedades de tipos anônimos  
 Quando você renomeia uma propriedade nos tipos anônimos, a operação de renomeação será propagado para as propriedades em outros tipos anônimos que têm as mesmas propriedades. Os exemplos a seguir ilustram esse comportamento.  
  
```csharp  
var a = new { ID = 1};  
var b = new { ID = 2};  
```  
  
 No código anterior, renomeando `ID` alterará `ID` em ambas as instruções porque eles têm o mesmo tipo anônimo subjacente.  
  
```csharp  
var companyIDs =  
    from c in companylist  
    select new { ID = c.ID, Name = c.Name};  
  
var orderIDs =  
    from o in orderlist  
    select new { ID = o.ID, Item = o.Name};  
```  
  
 No código anterior, renomeando `ID` renomeará apenas uma instância do `ID` porque `companyIDs` e `orderIDs` não têm as mesmas propriedades.  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)   
 [Tipos Anônimos](http://msdn.microsoft.com/library/59c9d7a4-3b0e-475e-b620-0ab86c088e9b)
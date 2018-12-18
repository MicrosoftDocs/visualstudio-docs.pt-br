---
title: 'Como: configurar a herança usando o Object Relational Designer | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7a6c8e4b2da87185c41157b8d03bd59b37188a43
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49222684"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>Como: configurar a herança usando o Designer relacional de objetos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
[!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) suporta o conceito de herança de tabela única como geralmente é implementado em sistemas relacionais. Herança de tabela única, há uma tabela de banco de dados individual que contém campos para informações pai e informações de filho. Com dados relacionais, uma coluna de discriminador contém o valor que determina qual classe qualquer registro pertence.  
  
 Por exemplo, considere pessoas a tabela que contém todos empregado por uma empresa. Algumas pessoas são funcionários e algumas pessoas são gerentes. A tabela de pessoas contém uma coluna chamada `EmployeeType` que tenha um valor de 1 para gerentes e um valor de 2 para funcionários; esta é a coluna de discriminador. Nesse cenário, você pode criar uma subclasse de funcionários e preencher a classe com apenas os registros que têm um valor de `EmployeeType` de 2. Você pode também remover colunas que não se aplicam de cada uma das classes.  
  
 Criar um modelo de objeto que usar herança (e corresponde a dados relacionais) pode ser um pouco confuso. O procedimento a seguir descreve as etapas necessárias para configurar a herança com object relational Designer de Objetos. Após as etapas genéricos sem se referir a uma tabela existente e colunas pode ser difícil, para uma explicação passo a passo que usa dados é fornecido. Para instruções passo a passo detalhadas para configurar a herança usando o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], consulte [passo a passo: Criando Classes LINQ to SQL, usando a herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md).  
  
### <a name="to-create-inherited-data-classes"></a>Para criar classes de dados herdadas  
  
1.  Abra o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] adicionando um **Classes LINQ to SQL** item a um projeto existente do Visual Basic ou c#.  
  
2.  Arraste a tabela que você deseja usar como a classe base em [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
3.  Arraste uma segunda cópia da tabela para o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] e renomeá-lo. Esta é a classe derivada, ou subclasse.  
  
4.  Clique em **herança** no **Object Relational Designer** guia o **caixa de ferramentas**e, em seguida, clique na subclasse (a tabela que você renomeou) e conectá-lo para a classe base.  
  
    > [!NOTE]
    >  Clique o **herança** item o **caixa de ferramentas** e solte o botão do mouse, clique na segunda cópia da classe que você criou na etapa 3 e, em seguida, clique na primeira classe que você criou na etapa 2. A seta na linha de herança irá apontar para a primeira classe.  
  
5.  Em cada classe, excluir todas as propriedades do objeto que você não deseja que apareça e que não são usadas para associações. Você receberá um erro se você tentar excluir as propriedades do objeto usadas para associações: [a propriedade \<nome da propriedade > não pode ser excluída porque participa da associação \<nome da associação >](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md).  
  
    > [!NOTE]
    >  Como uma classe derivada herda as propriedades definidas na sua classe base, as mesmas colunas não podem ser definidas em cada classe. (As colunas são implementadas como propriedades.) Você pode ativar a criação das colunas na classe derivada definindo o modificador de herança na propriedade na classe base. Para obter mais informações, consulte [não está no BUILD: substituindo propriedades e métodos](http://msdn.microsoft.com/en-us/2167e8f5-1225-4b13-9ebd-02591ba90213).  
  
6.  Selecione a linha de herança em [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
7.  No **propriedades** janela, defina as **propriedade discriminatória** ao nome da coluna que é usado para distinguir os registros em suas classes.  
  
8.  Defina as **valor Discriminatório da classe derivada** propriedade para o valor no banco de dados que designa o registro como o tipo herdado. (Esse é o valor que são armazenados na coluna de discriminador e que é usado para designar a classe herdada.)  
  
9. Defina as **valor Discriminatório da classe Base** propriedade para o valor que designa o registro como um tipo base. (Esse é o valor que são armazenados na coluna de discriminador e que é usado para designar a classe base.)  
  
10. Opcionalmente, você também pode definir as **padrão de herança** propriedade para designar um tipo em uma hierarquia de herança usado ao carregar as linhas que não correspondam a qualquer código de herança definido. Em outras palavras, se um registro tem um valor na coluna de discriminador que não coincide com o valor em qualquer um de **valor Discriminatório da classe derivada** ou **valor Discriminatório da classe Base** propriedades, o registro será carregado no tipo designado como o **padrão de herança**.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [PREPARAR o que há de novo para o desenvolvimento de aplicativo de dados no Visual Studio 2012](http://msdn.microsoft.com/en-us/3d50d68f-5f44-4915-842f-6d42fce793f1)   
 [Accessing data in Visual Studio](../data-tools/accessing-data-in-visual-studio.md)  (Acessando dados no Visual Studio)  
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Passo a passo: Criando Classes LINQ to SQL, usando a herança de tabela única (O/R Designer)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)   
 [NÃO ESTÁ NO BUILD: Herança no Visual Basic](http://msdn.microsoft.com/en-us/e5e6e240-ed31-4657-820c-079b7c79313c)   
 [Herança](http://msdn.microsoft.com/library/81d64ee4-50f9-4d6c-a8dc-257c348d2eea)


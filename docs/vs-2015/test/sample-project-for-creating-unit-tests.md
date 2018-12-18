---
title: Projeto de exemplo para criação de testes de unidade| Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- unit test sample [Visual Studio]
- unit tests, samples
ms.assetid: db80aaf2-0652-4d3f-a8c5-2a98fd8502a2
caps.latest.revision: 32
ms.author: gewarren
manager: douge
ms.openlocfilehash: c3d364ffe23e79bb8842770bec0602d4bb7022c9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248580"
---
# <a name="sample-project-for-creating-unit-tests"></a>Projeto de exemplo para criação de testes de unidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este código de exemplo é fornecido para uso nas instruções passo a passo a seguir:  
  
-   [Passo a passo: criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md). Este passo a passo orienta você pelas etapas para criar e personalizar testes de unidade, executá-los e examinar os resultados de teste.  
  
-   [Passo a passo: executar testes e exibir a cobertura de código](http://msdn.microsoft.com/en-us/d4aab8e2-2140-4975-b4e3-41ef3fa944c8). Este passo a passo ilustra como exibir dados de cobertura de código, que mostra a proporção do código do projeto que está sendo testado.  
  
-   [Passo a passo: usando o utilitário de teste de linha de comando](http://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867). Neste passo a passo, você pode usar o utilitário de linha de comando MSTest.exe para executar testes e exibir os resultados.  
  
## <a name="sample-code"></a>Código de exemplo  
 O erro intencional apenas neste exemplo é que o método Debit em "m_balance += amount" deve ter um sinal de menos e não um sinal de mais antes do sinal de igual.  
  
```  
using System;   
  
namespace BankAccountNS  
{  
    /// <summary>   
    /// Bank Account demo class.   
    /// </summary>   
    public class BankAccount  
    {  
        private string m_customerName;  
  
        private double m_balance;  
  
        private bool m_frozen = false;  
  
        private BankAccount()  
        {  
        }  
  
        public BankAccount(string customerName, double balance)  
        {  
            m_customerName = customerName;  
            m_balance = balance;  
        }  
  
        public string CustomerName  
        {  
            get { return m_customerName; }  
        }  
  
        public double Balance  
        {  
            get { return m_balance; }  
        }  
  
        public void Debit(double amount)  
        {  
            if (m_frozen)  
            {  
                throw new Exception("Account frozen");  
            }  
  
            if (amount > m_balance)  
            {  
                throw new ArgumentOutOfRangeException("amount");  
            }  
  
            if (amount < 0)  
            {  
                throw new ArgumentOutOfRangeException("amount");  
            }  
  
            m_balance += amount; // intentionally incorrect code  
        }  
  
        public void Credit(double amount)  
        {  
            if (m_frozen)  
            {  
                throw new Exception("Account frozen");  
            }  
  
            if (amount < 0)  
            {  
                throw new ArgumentOutOfRangeException("amount");  
            }  
  
            m_balance += amount;  
        }  
  
        private void FreezeAccount()  
        {  
            m_frozen = true;  
        }  
  
        private void UnfreezeAccount()  
        {  
            m_frozen = false;  
        }  
  
        public static void Main()  
        {  
            BankAccount ba = new BankAccount("Mr. Bryan Walton", 11.99);   
  
            ba.Credit(5.77);  
            ba.Debit(11.22);  
            Console.WriteLine("Current balance is ${0}", ba.Balance);  
        }  
  
    }  
}  
```  
  
 /* As empresas, as organizações, os produtos, os nomes de domínio, os endereços de email, os logotipos, as pessoas, os locais e os eventos de exemplo descritos aqui são fictícios.  Nenhuma associação com nenhuma empresa, organização, produto, nome de domínio, endereço de email, logotipo, pessoa, locais ou eventos reais é intencional nem deve ser inferida. \*/  
  
## <a name="working-with-the-code"></a>Trabalhando com o código  
 Para trabalhar com esse código, primeiramente, você precisa criar um projeto para ele no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Siga as etapas na seção "Preparar o passo a passo" em [Passo a passo: criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)   
 [Passo a passo: executar testes e exibir a cobertura de código](http://msdn.microsoft.com/en-us/d4aab8e2-2140-4975-b4e3-41ef3fa944c8)   
 [Passo a passo: usando o utilitário de teste de linha de comando](http://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867)




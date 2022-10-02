## SWIFT wire transfer

#### definition：

**Wire transfer**, **bank transfer**, or **credit transfer**

** (HKICL)**  :Hong Kong Interbank Clearing Limited company

> Interbank fund transfers are made through payment systems that are essential components of the financial infrastructure. Hong Kong's payment systems allow interbank transfers in the Hong Kong dollar, US dollar, euro, and renminbi. Hong Kong Interbank Clearing Limited (HKICL) is the operator of the payment systems, providing banks with various interbank clearing and settlement services.



value date: Settlement date

STP:  Straight-through processing

 (RTGS) 

*  the Hong Kong dollar Real Time Gross Settlement (RTGS) system introduced in 1996. Interbank payments are settled continuously on a deal-by-deal basis across the book of the HKMA without netting.
* The US dollar RTGS system (also known as US dollar CHATS) was launched in August 2000 with The Hongkong and Shanghai Banking Corporation as its settlement institution. 
* The euro RTGS system (also known as Euro CHATS) was launched in April 2003 with the Standard Chartered Bank (Hong Kong) Limited as its settlement institution.
* The renminbi RTGS system (also known as renminbi CHATS) was upgraded from the Renminbi Settlement System in June 2007 with the Bank of China (Hong Kong) Limited as its Clearing Bank. 

 **(CHATS)** : (also known as Hong Kong dollar Clearing House Automated Transfer System (CHATS)) 

MT950:    通知银行 bank statement 

#### 4 steps

A bank wire transfer is effected as follows:

* 1. The entity wishing to do a transfer approaches a bank and gives the bank the order to transfer a certain amount of money. [IBAN](https://en.wikipedia.org/wiki/IBAN) and [BIC](https://en.wikipedia.org/wiki/ISO_9362) codes are given as well so the bank knows where the money needs to be sent.
* 2. The sending bank transmits a message, via a secure system (such as [SWIFT](https://en.wikipedia.org/wiki/Society_for_Worldwide_Interbank_Financial_Telecommunication) or [Fedwire](https://en.wikipedia.org/wiki/Fedwire)), to the receiving bank, requesting that it effect payment according to the instructions given.
* 3. The message also includes [settlement](https://en.wikipedia.org/wiki/Settlement_(finance)) instructions. The actual transfer is not instantaneous: funds may take several hours or even days to move from the sender's account to the receiver's account.
* 4. Either the banks involved must hold a reciprocal account with each other, or the payment must be sent to a bank with such an account, a [correspondent bank](https://en.wikipedia.org/wiki/Correspondent_bank), for further benefit to the ultimate recipient.[*[citation needed](https://en.wikipedia.org/wiki/Wikipedia:Citation_needed)*]





### ISO200022:  MX telegraphic transfer

###  4. settlement

**Payment-versus-payment (PvP)**  :  US Dollar, Euro, HK Dollar, RMB 跨货币结算

Hong Kong Monetary Authority

end of each business day.    **by way of position netting**

deal by deal:  **RTGS**   



## settlement Method

#### nostro(INGA)

Nostro accounts are mostly commonly used for [currency settlement](https://en.wikipedia.org/wiki/Currency_settlement)   

发起方         有收款方的账户

#### vostro(INDA)

收款方         收款方有发起方的账户

#### COV  第三方





# SWIFT  Message

[MT950 Statement](https://www.paiementor.com/swift-mt950-statement-message-detailed-analysis/)

an account statement sent by a Bank to its customer.

 An account statement contains an opening balance, the debit and credit entries booked to the account and a closing balance.

![SWIFT MT950 Statement](https://www.paiementor.com//wp-content/uploads/2018/09/SWIFT-MT950-Statement-Detailed-Analysis-1024x360.png)



####  payment return received

scb  keep an account of  instructed bank hsbc, UK branch  in the currency of foreign currency, eg UKD.

scb call this account nostro 我的.   To hsbc, uk, this account is called VOSTRA.

"[Nostro](https://www.investopedia.com/terms/n/nostroaccount.asp)" and "[vostro](https://www.investopedia.com/terms/v/vostroaccount.asp)" are two different terms used to describe the same bank account. 





### Case study

SCBHK  as intermediary bank. 

scb hk nostra, has an account in scb Shenzhen branch, balance :10000RMB. has an account in scb, UK branch, balance: 5000 UK pounds

when shenzhen branch reimittance 10000 RMB to  1200 UK pounds.  

nostra account balance in shenzhen add from 10000 RMB to 200000RMB

nostra account balance in London deduct from 5000 to 3800.



Cover Payment:

pacs.008:  客户机构直接沟通目的地机构

pacs.009.COV  结算方式



pacs.009   

### Pacs.004   payment Return

> The Payment Return message is used to undo a payment previously settled. When a bank receives a pacs.008, it should process it and books the money to the beneficiary account. But what if the beneficiary closed his account two days ago? What if the account does not exist at all in the Bank? In those cases, the bank will not be able to credit the account. According to the SEPA rules, the beneficiary bank must *return* the money to the originator Bank. Besides the reasons mentioned above, there are numerous reasons why a bank might have to return the money. In any case, it will use the pacs.004 message to do that. The return has its own settlement date, the date at which the money will be paid back to the originator bank. The reason for returning the funds is indicated by a code in the return message.
>
> A bank can only return the money that it has previously received. So the payment return message is initiated and sent after settlement. The SEPA rules oblige the Beneficiary Bank to send the Return message to the Originator Bank at the latest three Banking Business Days after Settlement Date. The underlying principle is that money should be return as soon as possible to the originator.

### pacs.002   Payment Status Report or Reject SCT

> SEPA Credit Transfer and R-transactions messages can be rejected for many reasons: the message is not readable because the XML format is invalid. The IBAN or the BIC specified in the message is invalid, and so on. Rejections of [pacs.008](https://www.paiementor.com//pacs-008-001-02-sct-interbank-ig-2017-v2-1/) messages can happen at many levels as we will see later. The pacs.002 provides the information about the level and the original message which has been rejected.

### Camt.029    

### Camt.056    

# Messages in the SCT interbank space – pacs.008 and pacs.002

sct customer credit transfer.     telegraphic transfer

https://www.paiementor.com/messages-in-the-interbank-space-pacs-008-and-pacs-002/

![img](https://www.paiementor.com//wp-content/uploads/2017/11/Interbank-Space-Pacs.008-and-002.png)



###  [Windows command Script](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/call)

```
&&    executes this command only if previous command's errorlevel is 0.

||  (not used above) executes this command only if previous command's errorlevel is NOT 0



```



1625

1652

1826

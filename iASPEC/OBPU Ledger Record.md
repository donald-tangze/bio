Swift & Chats & XbFPS Ledger Record

Here, ONLY handle general ledger record and Bank Position Debit Credit Record.

Besides, there are commision record, exchange record,  2404031 record.

## 1.Outward Ledger Record

IS_CREDIT=False

### 1.1.prepare Movement Details

* 1.1.1.get internal settlement detail
  * 


```
for Outward transaction, internal settlement detail
Object object = MapUtils.getObject(payment.getAdditionalData(), INTERNAL_SETTLEMENT_DETAILS);
```

* 1.1.2.convert internal settlement detail to Movement Detail

### 1.2.1.channel = Swift

* 1.settlementMethod=COVE
  * find related bank account of reimbursement agent
* 2.settlementMethod=INDA/INGA
  * find related bank account of instructed agent

* 3.判断 related agent的地域特征

  * outport bank
    * INDA  Vostra   2203012 
    * INGA  Nostra  1107018

  * overseas branch
    * INDA  Vostra   27156XX 
    * INGA  Nostra  19146XX

  * local bank
    * INGA  Nostra  1104019 

### 1.2.2.channel = CHATS

* CLRG  Sundry
  * Currency = HKD   2502980 
  * Currency = F.D     2504016

### 1.2.3.channel = XbFPS

* 2518017

  

### 2.Inward Ledger Record   

IS_CREDIT=True

### 2.1.prepare Movement Details

* get internal settlement detail

```
for Outward transaction, internal settlement detail
Object object = MapUtils.getObject(payment.getAdditionalData(), INTERNAL_SETTLEMENT_DETAILS);
```

* convert internal settlement detail to Movement Detail

### 2.2.1channel = Swift

* 1.settlementMethod=COVE
  * find related bank account of reimbursement agent
* 2.settlementMethod=INDA/INGA
  * find related bank account of instructed agent

* 3.判断 related agent的地域特征

  * outport bank
    * INDA  Vostra   2203012          
    * INGA  Nostra  1107018

  * overseas branch
    * INDA  Vostra   27156XX 
    * INGA  Nostra  19146XX

  * local bank
    * INGA  Nostra  1104019 

### 2.2.2channel = CHATS

* CLRG  Sundry
  * Currency = HKD   2502980 
  * Currency = F.D     2504016

### 2.2.3.channel = XbFPS

* 2518017









#### Debit

```
private boolean saveRemittanceLedgerRecord(PaymentDTO payment, PPRBankRelatedAccountsDTO pprBankRelatedAccountsDTO) {
        SystemLogger.info("UpdateBankPostionOBPUMQHandler saveRemittanceLedgerRecord");
        Long result = 0L;
        LedgerTransaction ledgerTransaction = new LedgerTransaction();

        try {
            String nostroVostroFlag = "";
            String agentBic = "";
            if (directionType.equals(RemmitanceDirectionType.INCOMING)) {
                ledgerTransaction.setIsCredit(false);
                nostroVostroFlag = payment.getSettlementMethod().equals(SettlementMethod.INGA) ? "N" : "V";
                ledgerTransaction.setNostroVostroIndicator(nostroVostroFlag);
                agentBic = payment.getInstructingAgentBic();
            } else {
                ledgerTransaction.setIsCredit(true);
                nostroVostroFlag = payment.getSettlementMethod().equals(SettlementMethod.INGA) ? "V" : "N";
                ledgerTransaction.setNostroVostroIndicator(nostroVostroFlag);
                agentBic = payment.getInstructedAgentBic();
            }
            StringBuilder propKey = new StringBuilder("remittance.");
            propKey.append(nostroVostroFlag.equalsIgnoreCase("N") ? "nostro." : "vostro.");

            if (agentBic.startsWith("SCBKUSSF")) {
                propKey.append("overseasbranches.SCBKUSSF");
            } else if (payment.getInstructingAgentBic().startsWith("SCBKGBLD")) {
                propKey.append("overseasbranches.SCBKGBLD");
            } else if (payment.getInstructingAgentBic().startsWith("SCBKUSNY")) {
                propKey.append("overseasbranches.SCBKUSNY");
            } else if (payment.getInstructingAgentBic().startsWith("SCBKUSLA")) {
                propKey.append("overseasbranches.SCBKUSLA");
            } else if (payment.getInstructingAgentBic().startsWith("SCBKCNSZ")) {
                propKey.append("overseasbranches.SCBKCNSZ");
            } else if (payment.getInstructingAgentBic().startsWith("SCBKCNSH")) {
                propKey.append("overseasbranches.SCBKCNSH");
            } else {
                propKey.append("outportbank");
            }
            String accountNo = propertyStoreService.getStringValue(propKey.toString(), "001");
            ledgerTransaction.setAcctNo(accountNo);
            ledgerTransaction.setBankCode(pprBankRelatedAccountsDTO.getBankCodeInIBMFormat());

            ledgerTransaction.setPaymentId(payment.getId());
            ledgerTransaction.setInstructionId(payment.getInstructionId());// 16 digit
            ledgerTransaction.setIsCreditCard(false);
            ledgerTransaction.setUetr(payment.getUetr());
            ledgerTransaction.setType(LedgerTransactionType.GENERAL_LEDGER);
            ledgerTransaction.setReference(payment.getBankReference());
            ledgerTransaction.setCurrency(payment.getSettlementAmountCurrency());
            ledgerTransaction.setAmt(payment.getSettlementAmount());
            ledgerTransaction.setValueDate(payment.getSettlementDate());
            ledgerTransaction.setStatus(LedgerTransactionStatus.SUCCESS);
            ledgerTransaction.setBranch("28");
            ledgerTransaction.setCustom1(payment.getEndToEndId());
            ledgerTransaction.setCreationDatetime(LocalDateTime.now());


            result = ledgerTransactionDAO.insert(ledgerTransaction);
            SystemLogger.info("UpdateBankPostionOBPUMQHandler save LedgerRecord: {0}, result: {1}", JsonHelper.toJsonString(ledgerTransaction), result);
        } catch (Exception e) {
            SystemLogger.error("UpdateBankPostionOBPUMQHandler save LedgerRecord error =[{0}]", new Object[]{e.getMessage()}, e);
        }

        return result > 0;
    }



    private boolean saveRemittanceDebitorCreditorRecord(PaymentDTO payment, PPRBankRelatedAccountsDTO pprBankRelatedAccountsDTO) {
        SystemLogger.info("UpdateBankPostionOBPUMQHandler saveRemittanceLedgerRecord");
        Long result = 0L;
        try {
            LedgerTransaction ledgerTransaction = new LedgerTransaction();

            String nostroVostroFlag = "";
            if (directionType.equals(RemmitanceDirectionType.INCOMING)) {
                ledgerTransaction.setIsCredit(false);
                nostroVostroFlag = payment.getSettlementMethod().equals(SettlementMethod.INGA) ? "N" : "V";
                ledgerTransaction.setNostroVostroIndicator(nostroVostroFlag);
            } else {
                ledgerTransaction.setIsCredit(true);
                nostroVostroFlag = payment.getSettlementMethod().equals(SettlementMethod.INGA) ? "V" : "N";
                ledgerTransaction.setNostroVostroIndicator(nostroVostroFlag);
            }

            if (payment.getSettlementDate().compareTo(LocalDate.now()) <= 0) {
                ledgerTransaction.setType(LedgerTransactionType.BANK_POSITION);
            } else {
                ledgerTransaction.setType(LedgerTransactionType.CASH_FLOW_PROJECTION);
            }

            ledgerTransaction.setAcctNo(pprBankRelatedAccountsDTO.getAccountNo());
            ledgerTransaction.setBankCode(pprBankRelatedAccountsDTO.getBankCodeInIBMFormat());
            ledgerTransaction.setPaymentId(payment.getId());
            ledgerTransaction.setInstructionId(payment.getInstructionId()); // 16 digit
            ledgerTransaction.setIsCreditCard(false);
            ledgerTransaction.setUetr(payment.getUetr());
            ledgerTransaction.setReference(payment.getBankReference());
            ledgerTransaction.setCurrency(payment.getSettlementAmountCurrency());
            ledgerTransaction.setAmt(payment.getSettlementAmount());
            ledgerTransaction.setValueDate(payment.getSettlementDate());
            ledgerTransaction.setStatus(LedgerTransactionStatus.SUCCESS);
            ledgerTransaction.setBranch("28");
            ledgerTransaction.setCustom1(payment.getEndToEndId());
            ledgerTransaction.setCreationDatetime(LocalDateTime.now());

            result = ledgerTransactionDAO.insert(ledgerTransaction);
            SystemLogger.info("UpdateBankPostionOBPUMQHandler save LedgerRecord: {0}, result: {1}", JsonHelper.toJsonString(ledgerTransaction), result);
        } catch (Exception e) {
            SystemLogger.error("UpdateBankPostionOBPUMQHandler saveRemittanceLedgerRecord error [{0}]", new Object[]{e.getMessage()}, e);
        }

        return result > 0;
    }
```







# #94 Issue

PaymentImageDTO.settlementAcctId   compare it with settlementRecord.settlementAct
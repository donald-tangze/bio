calculate Charge amount for incoming message

* calculate outward charge bearer according to current charge bearer
* Check if charge bearer is DEBT
  * if it is DEBT, skip calculation
  * if it is not DEBT
    * Query charge amount by agent, country
    * Calculate exchange Info for charge if charge currency is not same with settlement currency
    * Save chargeInfo in additional data and deduct charge to get outward settlement amount



1) If 'Charge Criteria' = 'By Remitting & Remitted Bank', disable 'Country' input.

2) If 'Charge Criteria' = 'By Beneficiary Country', disable 'Remitting Bank. & 'Remitted Bank'.

3) 'Charge Criteria' - 'Default' CANNOT be selected in 'Add Charge'. It is for display only, during 'Ediit'.

4) If 'Remittance Type' is 'Inward', Charge Criteria can only be 'By Remitting & Remitted Bank', and 'Remitted Bank' is disabled for user input

5) If 'Remittance Type is 'Outward', Remitting Bank is disabled for user input

6) After confirm button clicked, prompt user for double confirmation with reminder



Update: Charge Administration

1. When Remittance Type is "Intermediary", 

   * for field: Charge Type, show option item: "By Beneficiary Country". 

   * And under "By Beneficiary Country", disable  input field: Remitting Bank and Remitted Bank, while enable input field: Country

2. Remitting Bank and Remitted Bank can be and only be 8-digit or 11-digit. If input is 8-digit, check if inputted 8-digit existed in beginning 8-digit of KE 2 of table ecph_cust_cfg_tbl where category = “BSPPRWF”; If input is 11-digit, check if inputted 11-digit value existed in KE 2 of table ecph_cust_cfg_tbl where category = “BSPPRWF”


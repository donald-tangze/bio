### Task: 将同一种Handler进行合并

| Handler                                                      | type 1                     | type 2             |
| ------------------------------------------------------------ | -------------------------- | ------------------ |
| AMLResultMQHandler                                           | incoming swift msg         | outgoing swift msg |
| SettlementAndBalanceQOBDMQHandler  (Check for settlement)    | -                          |                    |
|                                                              |                            |                    |
| UpdateIncomingRequstStatusSTSUMQHandler                      | effectStatus               | resetStatus        |
| WriteSwiftMessage2HostMQHandler                                                          ---  Write SWIFT message to HOST System and return the MUR number |                            |                    |
|                                                              |                            |                    |
|                                                              |                            |                    |
| UpdateCashPositionObpuMQHandler                              | 和下面合并，也叫UpdateBank |                    |
| UpdateBankPostionOBPUMQHandler                               |                            |                    |



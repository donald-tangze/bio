# Office Chair

1.millberget 899

2.flintan  599

3.langfjall   1449



# Mattress

## 类型：

「彈簧床墊」與「無彈簧床墊」



### 1.「彈簧床墊」

* 獨立筒彈簧：能大幅減輕身體負擔，適合兩個人使用

* 串聯式彈簧：睡感偏硬，適合體重較重者
* 高密度連續彈簧：有效支撐人體重量，床面塌陷度極小

### 2. 「無彈簧床墊」

* 高回彈床墊：軟硬適中，有效支撐體重

* 記憶床墊：溫柔舒適的包覆感，可避免過度頻繁翻身



https://www.seahorse.com.hk/goods.php?ProId=520&IsShop=1

**產品特點：**

1、硬身。
2、選用高密度高硬度綿，高硬度中帶韌性，給予身體充足持久的承托力，有效保護脊椎健康。
3、可折疊的設計,節省空間,方便擺放。

##  厚度

5cm 以下的薄墊可以成為硬床墊的緩衝，若現有的床墊睡起來不舒服，便可利用這種規格的產品來改善。

如果要搭配床架，或者直接放在地板上，則建議以10cm 左右的款式為佳。而若特別注重睡眠品質，25cm 以上的獨立筒彈簧床應能帶來更滿意的使用體驗。



办公椅

|              | 品牌1:flintan | 品牌2 MILLBERGET | 品牌3   |
| ------------ | ------------- | ---------------- | ------- |
| 椅座深度:    | 49 厘米       | 45 厘米          | 41 厘米 |
| 椅座闊度:    | 46 厘米       | 52 厘米          | 41 厘米 |
| 滚轮闊度:    | 71 厘米       | 70 厘米          | 41 厘米 |
| 椅座高度     | 45-58厘米     | 45-62 厘米       | 44 厘米 |
| 手肘支撑高度 | 69厘米        | 64厘米           | 无      |



  

strengthFinder book  

the 5 most compatible strength of me

Strategic     Belief     analytical  deliberative  consistency   empathy









a12345            hex

ce0319831852a657b2f6bf948d4e7892a2b69de7121526b5658666256c823317





a    text

ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb



ASCII码    UTF-8码

97(10)    hex   01100001         61F

ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb

ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb



1.swift加密流程，拿上传文件的XML元素，通过字符编码，获得待加密文件的比特表示符号，进行加密。 

有几个问题，拿到上传文件的XML元素，会做哪些修改，包括不限于掐头去尾，调整xml顺序等。

采用的字符编码是什么，UTF-8，ASCII，还是其他？





规范化XML  --    计算SHA256   --   计算BASE64





```
<Saa:DataPDU xmlns:Saa="urn:swift:saa:xsd:saa.2.0" xmlns:Sw="urn:swift:snl:ns.Sw" xmlns:SwGbl="urn:swift:snl:ns.SwGbl" xmlns:SwInt="urn:swift:snl:ns.SwInt" xmlns:SwSec="urn:swift:snl:ns.SwSec">
   <Saa:Revision>2.0.7</Saa:Revision>
   <Saa:Header>
      <Saa:Message>
         <Saa:SenderReference>f70530bb1633fe8863b20001000001</Saa:SenderReference>
         <Saa:MessageIdentifier>camt.998.001.02</Saa:MessageIdentifier>
         <Saa:Format>AnyXML</Saa:Format>
         <Saa:SubFormat>Input</Saa:SubFormat>
         <Saa:Sender>
            <Saa:DN>o=swhqbebb,o=swift</Saa:DN>
            <Saa:FullName>
               <Saa:X1>SWHQBEBBXXX</Saa:X1>
            </Saa:FullName>
         </Saa:Sender>
         <Saa:Receiver>
            <Saa:DN>o=swhqbebb,o=swift</Saa:DN>
            <Saa:FullName>
               <Saa:X1>SWHQBEBBXXX</Saa:X1>
            </Saa:FullName>
         </Saa:Receiver>
         <Saa:InterfaceInfo>
            <Saa:UserReference>f70530bb1633fe8863b20001000001</Saa:UserReference>
            <Saa:MessageCreator>ApplicationInterface</Saa:MessageCreator>
            <Saa:MessageContext>Original</Saa:MessageContext>
            <Saa:MessageNature>Financial</Saa:MessageNature>
         </Saa:InterfaceInfo>
         <Saa:NetworkInfo>
            <Saa:Priority>Normal</Saa:Priority>
            <Saa:IsPossibleDuplicate>false</Saa:IsPossibleDuplicate>
            <Saa:IsNotificationRequested>false</Saa:IsNotificationRequested>
            <Saa:Service>swift.eni</Saa:Service>
            <Saa:Network>Application</Saa:Network>
            <Saa:SessionNr>0016</Saa:SessionNr>
            <Saa:SeqNr>000001</Saa:SeqNr>
            <Saa:SWIFTNetNetworkInfo>
               <Saa:RequestType>camt.998.001.02</Saa:RequestType>
               <Saa:Reference>4749da88-25a3-11e7-9c45-4128ba5efce6</Saa:Reference>
               <Saa:IsCopyRequested>false</Saa:IsCopyRequested>
            </Saa:SWIFTNetNetworkInfo>
         </Saa:NetworkInfo>
         <Saa:ExpiryDateTime>20170510082806</Saa:ExpiryDateTime>
      </Saa:Message>
   </Saa:Header>
   <Saa:Body>
      <Document xmlns="urn:swift:xsd:camt.998.001.02" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
         <PrtryMsg>
            <MsgId>
               <Ref>ABCDEFGHIJKLMNOPQRST123456789012345</Ref>
            </MsgId>
            <Rltd>
               <Ref>ABCDEFGHIJKLMNOPQRST123456789012345</Ref>
            </Rltd>
            <Prvs>
               <Ref>ABCDEFGHIJKLMNOPQRST123456789012345</Ref>
            </Prvs>
            <Othr>
               <Ref>ABCDEFGHIJKLMNOPQRST123456789012345</Ref>
            </Othr>
            <PrtryData>
               <Tp>ABCDEFGHIJKLMNOPQRST123456789012345</Tp>
               <Cntnt>:20:MyReference
:32A:20051212
:57:BKNY
:72:/Own</Cntnt>
            </PrtryData>
         </PrtryMsg>
      </Document>
   </Saa:Body>
</Saa:DataPDU>
```





```html
https://mclient.alipay.com/home/exterfaceAssign.htm?secondary_merchant_industry=5812&payment_inst=ALIPAYHK&order_create=1650514885876&_input_charset=utf-8&subject=%E5%92%8C%E6%B0%91+-+%E8%8D%94%E6%9E%9D%E8%A7%92%E6%B7%B1%E7%9B%9B%E8%B7%AF9%E8%99%9F%E5%AE%87%E6%99%B4%E6%BB%992%E6%A8%936%E8%99%9F%E8%88%96-global.food-charge&refer_url=1800&sign=63f71345e2a3efd697873df39d5a87b7&body=%E5%92%8C%E6%B0%91+-+%E8%8D%94%E6%9E%9D%E8%A7%92%E6%B7%B1%E7%9B%9B%E8%B7%AF9%E8%99%9F%E5%AE%87%E6%99%B4%E6%BB%992%E6%A8%936%E8%99%9F%E8%88%96-global.food-charge&notify_url=https%3A%2F%2Feopg.eftpay.com.hk%3A443%2FEFTPayOnline%2FNotifyRecetionServlet&product_code=NEW_WAP_OVERSEAS_SELLER&alipay_exterface_invoke_assign_model=home&alipay_exterface_invoke_assign_target=exterfaceAssign.htm&secondary_merchant_id=08520019641&out_trade_no=78a6bc79b95348b6b08da8a5af6409f4&partner=2088531507350472&alipay_exterface_invoke_assign_sign=b2_ui_em_i_s_f_ta_pv8h_t_m_xt5t%2Fq_l_nw_v_i%2B_xyoih_mv09jh_k_y_w_j_a%2B_t_a2_a5l_ig%3D%3D&timeout_rule=30m&service=create_forex_trade_wap&total_fee=47.70&secondary_merchant_name=WATAMI+(CHINA)+CO+LTD&return_url=https%3A%2F%2Feopg.eftpay.com.hk%3A443%2FEFTPayOnline%2FReturnRecetion&currency=HKD&sign_type=MD5&alipay_exterface_invoke_assign_client_ip=180.131.167.188
```




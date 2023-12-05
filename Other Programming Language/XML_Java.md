## XSD Definition
XML schema descriptor

## How to develop Java application with XSD
1.Convert XSD into pojo Class
> go with JAXB.
> I have tested it in eclipse, works well for me. My suggestion is try generating the POJO from command line or with the help of eclipse. Once successful configure it with maven to generate the POJO build time.
> There are several tutorials to learn this, please follow the below link(s) based upon your preference:
> [Generate POJO Class from XSD in Eclipse](http://www.javawebtutor.com/articles/jaxb/jaxb_java_class_from_xsd.html)
> [Generate POJO class from XSD Schema command line](http://theopentutorials.com/examples/java/jaxb/generate-java-class-from-xml-schema-using-jaxb-xjc-command/)
> [Generate POJO Classes from XSD using XJC Maven Plugin](http://www.journaldev.com/1312/how-to-generate-java-classes-from-xsd-using-xjc-maven-plugin)

## 2.Develop rest api handling XML format request and response: SOAP
[World Customs Data Model](https://www.cedb.gov.hk/assets/document/cedb/policies/GETS%20I.I.%20v4.10.zip )
## 2.1.Develop Message Queue handling XML format message

## 4.Use Hibernate to persist pojo data into database and retrieve pojo from RDBMS
## 5. Tools
* XSD / WSDL Visualizer

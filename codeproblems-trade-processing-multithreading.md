

![codeproblems_Trade_processing_assignment](./assets/codeproblems_Trade_processing_assignment-7293287.png)

[codeproblems_Trade_processing_assignment]

Here's the link to the SVG 

[bootcamp2024-material/codeproblems_Trade_processing_assignment.svg at main · FullStackLabsCa/bootcamp2024-material (github.com)](https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/codeproblems_Trade_processing_assignment.svg)



This is the Retry and DeQueue and DLQ logic 

[boca-core-java-examples/src/multithreading2024/retry/queue/RetryWithDequeAndDLQ.java at main · FullStackLabsCa/boca-core-java-examples (github.com)](https://github.com/FullStackLabsCa/boca-core-java-examples/blob/main/src/multithreading2024/retry/queue/RetryWithDequeAndDLQ.java)

This has the running example for Optimistic Locking

[boca-core-java-examples/src/jdbc/transactions/locking/optimistic/CreditCardTransactionProcessor.java at main · FullStackLabsCa/boca-core-java-examples (github.com)](https://github.com/FullStackLabsCa/boca-core-java-examples/blob/main/src/jdbc/transactions/locking/optimistic/CreditCardTransactionProcessor.java)



10,000 trades have been put in here. https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/trades.csv 

[trades.csv]: https://github.com/FullStackLabsCa/bootcamp2024-material/blob/main/trades.csv	"trades data"



This is the interface definition document 

 [capital-markets-backoffice-trade-processing-interface-master.xlsx](capital-markets-backoffice-trade-processing-interface-master.xlsx) 







Version 1.1 update

- sonarlint clean, sout is fine
- build with interfaces that we discussed
- It will fully decoupled and Async Implementation - Main class will say chunkGenerator.start, chunkProcessor.start, tradeProcessor.start,
- chunkGenerator will send messages (with fileName) to a queue from where chunkProcessor will consume from.

- all properties will be in application.properties -- `tradeFilePath, numberOfChunks`,![:mega:](https://a.slack-edge.com/production-standard-emoji-assets/14.0/apple-medium/1f4e3@2x.png) `tradeDistributionCriteria,`` chunkProcessorThreadPoolSize` , `tradeProcessorThreadPoolSize` ,`tradeProcessorQueueCount` ,`maxRetryCount` , `dbUserName` ,`dbPassword` ,`dbUrl`

- the application should be able to switch between fully single Threaded to multi-Threaded with application property changes

- ![:mega:](https://a.slack-edge.com/production-standard-emoji-assets/14.0/apple-medium/1f4e3@2x.png) Make sure you have retry and DLQ functionality added in this version

- ![:mega:](https://a.slack-edge.com/production-standard-emoji-assets/14.0/apple-medium/1f4e3@2x.png) Add the columns in trade_payloads table

-  validity_status column = valid | invalid (to check if the trade line in the file is valid trade with all correct fields present and in the right format)
-  lookup_status column = pass | fail (to check if the security exists in the securities_reference table or not )
- je_status column = posted | not_posted (to show whether the trade got posted into JE table or not, initially it will be `not_posted` when trade is saved by the chunk processor in trade_payloads table, later the `trade_processor` will update it to posted if its been able to create journal entry successfully for a given `trade_id` )

- ![:mega:](https://a.slack-edge.com/production-standard-emoji-assets/14.0/apple-medium/1f4e3@2x.png) figureTheNextQ method will work with the following properties for the trade distribution logic

- distributionLogic.useMap   = true / false
- distributionLogic.criteria    = tradeId / accountNumber
- distributionLogic.algorithm  = round-robin / random
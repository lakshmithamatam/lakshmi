Sometimes you will be in need to debug the request/response send and recieved with ews-java-api. To do so, you can set a modifiable TraceListener and print or log the Trace Messages.

> *Remember to not put this in your production code*

```java
        ExchangeService exchangeService = new ExchangeService(...);
        /* TODO: do initialising stuff here */         

        exchangeService.setTraceEnabled(true);
        exchangeService.setTraceFlags(EnumSet.allOf(TraceFlags.class)); // can also be restricted
        exchangeService.setTraceListener(new ITraceListener() {

            public void trace(String traceType, String traceMessage) {
                // do some logging-mechanism here
                log("Type:" + traceType + " Message:" + traceMessage);
            }
        });
```
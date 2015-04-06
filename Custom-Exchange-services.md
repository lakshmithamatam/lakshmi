# Customization

It is possible to customize some parts of Exchange services (`ExchangeServiceBase`, `AutodiscoverService` and `ExchangeService`). You need to extend custom class to do it.

## Override hostname verifier for SSL connections

Below example shows how to switch off hostname verification:
```java
public class CustomExchangeService extends ExchangeService {

  @Override
  protected Registry<ConnectionSocketFactory> createConnectionSocketFactoryRegistry() {
    try {
      return RegistryBuilder.<ConnectionSocketFactory>create()
          .register(EWSConstants.HTTP_SCHEME, new PlainConnectionSocketFactory())
          .register(EWSConstants.HTTPS_SCHEME, EwsSSLProtocolSocketFactory.build(
              null, NoopHostnameVerifier.INSTANCE
          ))
          .build();
    } catch (GeneralSecurityException e) {
      throw new RuntimeException(
          "Could not initialize ConnectionSocketFactory instances for HttpClientConnectionManager", e
      );
    }
  }

}
```

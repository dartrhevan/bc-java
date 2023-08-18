# The Bouncy Castle Crypto Package For Java

## Сборка с поддержкой механизмы проверки отзыва сертификатов ФТС

### Потребность в данной сборки

принятый в ФТС механизм проверки сертификата по спискам отзыва (реализованный в Крипто Про CSP) отличается от
общепринятого.

Различие заключается в том, что при отсутствии валидного на дату проверки списка отзыва от УЦ, выпустившего сертификат,
CSP признаёт сертификат действительным, в то время как провайдеры JCA (стандартный от SUN, BC) проверку валят,
из-за невозможности определить статус отзыва сертификата.

### Изменения

Для реализации механизма аналогичного Крипто Про CSP, в классе `org.bouncycastle.pkix.jcajce.X509RevocationChecker` были
добавлены настройки:

- `failOnNoValidCRLFound`: требуется ли валить проверку при отсутствии подходящей CRL
- `checkCrlDistributionPoint`: требуется ли проверять CRL DP

| Настройка                 | Описание                                                               | Затронутые классы | Значение по умолчанию |
|---------------------------|------------------------------------------------------------------------|-------------------|-----------------------|
| failOnNoValidCRLFound     | требуется ли валить проверку при отсутствии подходящей CRL             |                   | false                 |
| checkCrlDistributionPoint | ребуется ли проверять CRL DP                                           |                   | false                 |
| validateAllCrl            | проверять ли все CRL, независимо от даты действия и наличия дубликатов |                   | false                 |

### Сборка

Для сборки использовать скрипт `build1-5to1-8`, перед запуском требуется указать в переменной `JDKPATH` путь до JDK 8,
собранные артифакты будут доступны в директории `build/artifacts/jdk1.5/jars/`.
Интересующий артифакт - bcpkix-jdk15on, для его работы требуются: bcutil-jdk15on и bcprov-jdk15on.

Оригинальный README от разработчиков Bouncy Castle можно почитать в `README.original.md`.
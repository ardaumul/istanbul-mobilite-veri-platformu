# 0001 Mimari: batch, streaming ve tablo formatı

Durum: Önerildi
Tarih: 23 Kasım 2026

## Bağlam

<!-- Kararı gerektiren durum: kaynaklar, tüketiciler, gecikme ihtiyaçları ve kısıtlar. -->

## Karar

Toplu ulaşım verisi günlük batch olarak DuckDB ve Spark ile, trafik yoğunluğu verisi ise en fazla 5 dakika gecikmeyle Kafka üzerinden streaming olarak işlenir; tüm tablolar Apache Iceberg formatında tutulur ve Apache Polaris REST kataloğunda kayıtlıdır.

## Gerekçe

Toplu ulaşım verisi kaynaktan günlük dosyalar hâlinde ve ayda yaklaşık 17 milyon satır olarak geldiği için günlük batch yeterlidir; trafik yoğunluğu ise anlık karar desteği için en geç 5 dakika içinde görünür olmalıdır. Iceberg, snapshot'larla geçmiş sürümlere dönmeyi ve partition ile ay bazlı sorguları hızlandırmayı sağlar; Polaris, DuckDB ve Spark'ın aynı tablolara tek bir katalogdan erişmesine olanak verir.
Toplu ulaşım verisi zaten günlük geldiği için streaming ek maliyet ve karmaşıklık getirir, gecikme kazancı sağlamaz.

## Sonuçlar

<!-- Kararın getirdiği iş, maliyet ve risk. -->

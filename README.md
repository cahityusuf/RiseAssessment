# RiseAssessment
1. Rise.Contact, Rise.Contact.Report, Rise.Contact.Workerservice isimli 3 ayrı microservice tasarlanmıştır.
2. Herbir projenin kendine ait bir git history si bulunmaktadır. Projelerin tek seferde indirilebilmesi maksadıyla sıkıştırılmıştır.
3. Herbir proje dockerize edilerek  oluşan imageler Docker Hub'ta cahityusuf reposuna eklenmiştir.
4. Projelerin tek seferde çalıştırılabilmesi için docker-compose.yaml dosyası oluşturulmuştur. Dosyanın bulunduğu diinde "docker-compose up" komutu ile projeler çalıştırabilir.
5. PostgreSql veri tabanıda docker container olarak ayağa kalkmaktadır. 
6. Veri tabanı Bilgileri ---> Host name :"host.docker.internal" ,UserName: "cykafadar", Password:"cyk112233."
7. Veri tabanı monitoring işlemleri için PgAdmin kullanılmıştır. http://localhost:5050 adresinden ayağa kalkar.
8. PgAdmin bilgileri: username: user@domain.com, password: cyk112233
9. RabbitMq kullanımı için container yerine "https://www.cloudamqp.com" sitesinden bir Instance yaratılmış ve kuyruk cloud ta oluşturulmuştur. Ek ayar gerekmez.
10. Herbir proje için k8s klasörü altında Kubernetes deployment, service ve secret configurasyon dosyaları yazılmıştır.
11. k8s dizininde "kubectl apply -f ." komutu ile kubernetesine deploy edilebilir.

# Rise.Contact
1. User ve ContactInfo adında 2 tablo oluşturulmuştur. User tablosunda kişi bilgisi ,ContactInfo tablosunda kişiye ait iletişim bilgileri tutulmuştur. 
2. Migration dosyaları Rise.Contact.Infrastracture katmanındadır.
3. "update-database" komutu ile tüm tablolar oluşturulabilir.
4. Sadece 2 tabloya aile CRUD operasyonları bu projede yapılır.
5. http://localhost:5000 adresinden ayağa kalkar.

# Rise.Contact.Report
1. Repors ve ReportsDetail isminde 2 tablosu vardır. Report tablosu talep edilen rapor için oluşturulan ID ile bir rapor talebi oluşmasını sağlar. ReportDetail ise WorkerService'den gelen rapor detayını ilgili talebi yapan rapor Id ile saklar.
2. Oluşan tüm raporlar veri tabanında tutlur ve istenildiğinde Oluşan rapor Id ile ulaşılıabilir.
3. iki methodu vardır. ilk method rapor talebi loluşturuan RepaortCreate, ikinci method WoprkerServiceden gele Http Requesti yapalayan ReportCapture methudu.
4. Rapor talebi oluşturur, Talebi Kuyruğa ekler ve Kuyruktan gelen Rapor detayını kendi ver tabanına kaydeder.
5. http://localhost:5001 adresinden ayağa kalkar


# Rise.Contact.Workerservice
1. Rise.Contact.Report Publisher'ından gelen rapor talempelerini consume ederek, yakaladığı rapor Id siile bir rapor oluşturur. Oluşan Rapora yine talep Id si eklenerek Http request ile Rise.Contact.Report'a yollar.

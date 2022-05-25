# Chipsee

Chipsee gömülü bilgisayarlarında işletim sistemini değitirmek için takip edilmesi gereken adımlar. 

### Gerekli Donanımlar 

- Linux bir bilgisayar.
- Bir SD kart (En Az 4 GB) ve SD kartı bilgisayara bağlayabileceğiniz bir adaptör.

### SD Kartın Hazırlanması

SD kartı bilgisayarınıza bağlayınız, eğer sanal makine kullanıyorsanız sd kartı Linux işletim sistemine bağladığınızdan emin olun. 

SD kartın bağlantı noktasını tespit etmek için aşağıdaki komutu giriniz :

`/dev/sdX` gibi bir bağlantı noktası elde etmelisiniz (Örneğin, `/dev/sdc` veya `/dev/sdb`)
```sh
$ sudo fdisk –l
```
> Not : sd<?> SD kartın bağlantı noktasını ifade eder. Bu komutun çıktısında harici hafızanın bağlantı noktasını ifade eden `/dev/sdb` veya `/dev/sdc` gibi bir donanım uzantısı elde edeceksiniz. 

`prebuilt-cs10600u070v1-emmc-20210719.tar` dosyasını Linux dosya dizininde bildiğiniz bir yere kopyalayın (Örneğin $Home)

`prebuilt-cs10600u070v1-emmc-20210719.tar` sıkıştırılmış dosyayı aşağıdaki komut ile **çıkartın**

```sh
$ tar -xzvf prebuilt-cs10600u070v1-emmc-20210719.tar
```

Çıkartılmış dosyaya gidin : 

```sh
$ cd prebuilt-cs10600u070v1-emmc-20210719
```

Aşağıdaki komut ile işletim sistemini SD karta yazdırın 

```sh
$ sudo ./mksdcard.sh --device /dev/sd<?>
```

### İşletim sisteminin cihaza yazdırılması.

- Yazdırma işlemi başarıyla tamamlandığında boot edilebilir SD kart hazırdır. Chipsee Endüstriyel bilgisayarın gücünü kesin ve SD kartı takın. 

- S1 anahtarını **TF Kart Boot** Moduna almanız gerekmektedir. Yani anahtarların `1 0 0 0` konumuna olması gerekir. 

| Anahtar Modu | 1 | 2 | 3 | 4 | 
| ------ | ------ | ------ | ------ | ------ |
| *TF Kart* | *1* | *0* | *0* | *0* |
| eMMC | 1 | 1 | 0 | 1 |
| Download | 0 | 1 | 1 | 0 |

- Cihazı COM1 üzerinden bilgisayara bağlayın ve gücü açın.  

- 20 dakika ardından cihazdaki LED yanık kalırsa, yazdırma işlemi tamamlanmış demektir. COM1'i kullanarak bu mesajı da görebilmeniz mümkün `>>>>>>> eMMC Yanıp Sönme Tamamlandı <<<<<<<<` bu, işletim sisteminin başarıyla eMMC'ye aktarıldığını gösterir. 

- Cihazın gücünü kesin ve S1 anahtarını eMMC Boot moduna alın. Yani anahtarların `1 1 0 1` konumunda olması gerekir.

Cihaza güç vererek çalıştırabilirsiniz işletim sistemi başarıyla değiştirilmiştir.

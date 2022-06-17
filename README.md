# Java 11 ile gelen yenilikler

String sınıfına eklenen yenilikler:

isBlank(), lines(), strip(), stripLeading(), stripTrailing(), repeat()

gibi birçok method String class'ına dahil edilmiştir. Bu metodlar sayesinde stringleri daha kolay manipüle edip kod karmaşıklığını azaltabiliriz.

```
String quoteString = "Spring helps \n \n developers \n build large scalable apps.";
List<String> lines = quoteString.lines()
  .filter(line -> !line.isBlank())
  .map(String::strip)
  .collect(Collectors.toList());
assertThat(lines).containsExactly("Spring helps", "developers", "build large scalable apps");
```
Burada stream api'nin getirmiş olduğu yardımcı metodlar bulunmasaydı çok uzun kodlar yazmak zorunda kalabilirdik. 

###### File üzerinden direkt String'leri okuyabiliriz

```
Path filePath = Files.writeString(Files.createTempFile(tempDir, "demo", ".txt"), "Sample text");
String fileContent = Files.readString(filePath);
assertThat(fileContent).isEqualTo("Sample text");
```

burada local file'a text yazıp içindekini direkt .readString() okumaya çalıştığımızda aynı şey olduklarını sağlamış oluruz.

###### Collection'ları direkt olarak Array'lere dönüştürebiliriz

```
List sampleList = Arrays.asList("Yasin", "Eryigit");
String[] sampleArray = sampleList.toArray(String[]::new);
assertThat(sampleArray).containsExactly("Yasin", "Eryigit");
```

Elimizde bulunan bir String arrayList'ini direkt olarak String array'ine dönüştürebiliriz.

###### The Not Predicate Method
```
List<String> sampleList = Arrays.asList("Yasin", "\n \n", "Eryigit", " ");
List withoutBlanks = sampleList.stream()
  .filter(Predicate.not(String::isBlank))
  .collect(Collectors.toList());
assertThat(withoutBlanks).containsExactly("Yasin", "Eryigit");
```
Burada boşluklar bulunduran sampleList listesi üzerinde koşul koyarak boş karakterleri eleyebilir ve direkt olarak temiz bir liste oluşturabiliriz.

###### Doğrudan çalıştırma
```
javac springdemo.java
java springdemo
```

bunları yazmak yerine artık kodları direkt olarak 

```
 java HelloWorld.java
```

ile çalıştırabiliriz.


###### JavaFx modülleri artık JDK dışında ayrı bir modül seti olarak sunulmaya başlandı

# Java 17 ile gelen yenilikler

###### JEP 356: Enhanced Pseudo-Random Number Generators

Java 17, yeni arayüzü genişletmek için java.util.Randomve SplittableRandomgibi eski rastgele sınıfları da yeniden düzenlendi.
SecureRandomRandomGenerator ortaya çıktı. 

###### macOS/AArch64 Bağlantı Noktası ( JEP 391 )

Apple, bilgisayar hattını X64'ten AArch64'e geçirmek için uzun vadeli bir plan duyurdu. Bu JEP, JDK'yı macOS platformlarında AArch64 üzerinde çalışacak şekilde taşır.

###### Sealed Classes

Kalıtım üzerinde hassas bir kontrol sağlar. Kotlinde de bulunur 
```
sealed class <sealed class name>
    permits <subclass1>, <subclass2>, <subclass3> {
}

```












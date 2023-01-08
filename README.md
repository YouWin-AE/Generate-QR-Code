## Generate the Qr Code in Spring boot & Thymeleaf sample application with ZXing.

### la classe : 'QRCodeService'

La classe **'QRCodeService'** est une classe publique qui possède une méthode statique 'getQRCode' qui permet de générer un QR code sous forme d'un tableau d'octets '(byte[])'.

Cette méthode prend en paramètre :
```
    - (String text) : une chaîne de caractères qui représente le texte à encoder dans le code QR.
    - (int width)   : un entier qui représente la largeur de l'image du code QR en pixels.
    - (int height)  : un entier qui représente la hauteur de l'image du code QR en pixels.
```

**- La méthode 'getQRCode' :** 

  - commence par instancier un objet 'QRCodeWriter' qui est une classe permettant de générer des codes QR.
  - Elle utilise ensuite cet objet pour encoder la chaîne de caractères en entrée en utilisant le format 'BarcodeFormat.QR_CODE'. 
  - Le résultat de cette opération est un objet de type 'BitMatrix' qui représente le QR code sous forme d'une matrice de bits.
  - Ensuite, elle crée un objet 'ByteArrayOutputStream' qui va être utilisé pour écrire l'image du QR code sous forme de données binaires. 
  - Elle crée également un objet 'MatrixToImageConfig' qui va être utilisé pour configurer l'apparence de l'image (couleur des points noirs : '0xFF000000' et blancs : '0xFF000000').
  - Enfin, elle utilise la méthode 'writeToStream' de la classe 'MatrixToImageWriter' pour écrire l'image du QR code dans l'objet 'ByteArrayOutputStream' au format PNG. 
  - Elle récupère les données binaires de l'image générée sous forme 'd'un tableau d'octets (byte[])' et les renvoie en tant que résultat de la méthode.

### la classe : 'QRCodeController'

La classe 'QRCodeController' est un contrôleur de type @Controller en Spring. 

Cette classe possède deux méthodes de gestion de requêtes HTTP :

**- home() :**
  - cette méthode est mappée à la route racine du site ("/") et gère les requêtes de type 'GET'. 
  - Elle ne prend pas de paramètre en entrée et renvoie simplement la vue "index".

**- 'getQRCode()' :** 
  - cette méthode est mappée à la route "/generate" et gère les requêtes de type 'POST'.

  - Elle prend en paramètre un objet Model (utilisé pour transmettre des données à la vue), ainsi qu'une chaîne de caractères (String text) passée en tant que paramètre de la requête '(@RequestParam)'. Si le paramètre text n'est pas présent dans la requête, sa valeur par défaut est "Abdeladim".

  - La méthode commence par instancier un tableau d'octets (byte[] image) et appelle la méthode 'getQRCode' de la classe 'QRCodeService' en lui passant la chaîne de caractères text et les dimensions souhaitées du QR code. Si une exception est levée lors de l'exécution de cette méthode, elle est simplement affichée dans la console.

  - Ensuite, elle convertit le tableau d'octets obtenu en une chaîne de caractères encodée en base 64 à l'aide de la méthode encodeToString de la classe Base64. Elle ajoute cette chaîne de caractères au modèle (model.addAttribute) et renvoie la vue "index".

### Run the application
-**Étape 1 :** ```mvn clean install```

-**Étape 2 :** Lancer l'application Spring Boot ```mvn spring-boot:run```

-**Étape 3 :** Tester avec l'url ```[http://localhost:8080](http://localhost:8080)```

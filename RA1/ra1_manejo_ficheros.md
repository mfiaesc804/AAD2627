# RA1. Desarrolla aplicaciones que gestionan información almacenada en ficheros identificando el campo de aplicación de los mismos y utilizando clases específicas.
---

# UD01. MANEJO DE FICHEROS

## ÍNDICE

1. [Introducción](#introducción)
   - [1.1. Definición de fichero](#definición-de-fichero)
   - [1.2. Breve evolución histórica](#breve-evolución-histórica)
   - [1.3. Importancia actual de los ficheros](#importancia-actual-de-los-ficheros)
   - [1.4. Tipos de acceso a los ficheros](#tipos-de-acceso-a-los-ficheros)
   - [1.5. Manejo de ficheros en Java](#manejo-de-ficheros-en-java)
   - [1.6. Ejemplos ilustrativos en Java](#ejemplos-ilustrativos-en-java)
   - [1.7. Conclusión del apartado](#conclusión-del-apartado)
2. [Tipos de ficheros según su contenido](#tipos-de-ficheros-según-su-contenido)
   - [2.1. Ficheros de texto](#ficheros-de-texto)
   - [2.2. Ficheros binarios](#ficheros-binarios)
   - [2.3. Ficheros mixtos y formatos modernos](#ficheros-mixtos-y-formatos-modernos)
   - [2.4. Codificaciones de texto](#codificaciones-de-texto)
   - [2.5. Conclusión del apartado](#conclusión-del-apartado-1)
3. [La clase File](#la-clase-file)
   - [3.1. Principales características](#principales-características)
   - [3.2. Métodos más importantes](#métodos-más-importantes)
   - [3.3. Limitaciones de File](#limitaciones-de-file)
   - [3.4. Comparación con NIO.2](#comparación-con-nio2)
   - [3.5. Conclusión del apartado](#conclusión-del-apartado-2)
4. [Formas de acceso a ficheros](#formas-de-acceso-a-ficheros)
   - [4.1. Acceso secuencial](#acceso-secuencial)
   - [4.2. Acceso aleatorio](#acceso-aleatorio)
   - [4.3. Diferencias principales](#diferencias-principales)
   - [4.4. Acceso combinado en aplicaciones modernas](#acceso-combinado-en-aplicaciones-modernas)
   - [4.5. Conclusión del apartado](#conclusión-del-apartado-3)
5. [Operaciones sobre ficheros en Java](#operaciones-sobre-ficheros-en-java)
   - [5.1.1. Apertura](#apertura)
   - [5.1.2. Lectura](#lectura)
   - [5.1.3. Salto](#salto)
   - [5.1.4. Escritura](#escritura)
   - [5.1.5. Cierre](#cierre)
   - [5.1.6. Resumen gráfico del ciclo](#resumen-gráfico-del-ciclo)
   - [5.1.7. Buenas prácticas](#buenas-prácticas)
   - [5.1.8. Conclusión del apartado](#conclusión-del-apartado-4)
6. [Clases relacionadas con flujos de datos](#clases-relacionadas-con-flujos-de-datos)
   - [6.1. Flujos de texto](#flujos-de-texto)
   - [6.2. Flujos binarios](#flujos-binarios)
   - [6.3. Diferencias entre flujos de texto y binarios](#diferencias-entre-flujos-de-texto-y-binarios)
   - [6.4. Conclusión del apartado](#conclusión-del-apartado-5)
7. [Clases con recodificación](#clases-con-recodificación)
   - [7.1. Codificación en Java](#codificación-en-java)
   - [7.2. Clases para recodificación](#clases-para-recodificación)
   - [7.3. Buenas prácticas](#buenas-prácticas-1)
   - [7.4. Conclusión del apartado](#conclusión-del-apartado-6)

---



# Introducción

El manejo de ficheros constituye una de las competencias fundamentales en el ámbito de la informática y la gestión de la información. Los ficheros son el medio principal a través del cual los sistemas almacenan, organizan y recuperan datos, por lo que comprender su estructura, tipos y operaciones básicas resulta esencial para el desarrollo de programas y la administración de sistemas.

En esta unidad se abordarán los conceptos clave relacionados con los ficheros, incluyendo su creación, apertura, modificación y eliminación, así como las distintas formas de acceso y organización que permiten optimizar su uso. Además, se resaltará la importancia de las buenas prácticas en la manipulación de datos para garantizar la integridad, seguridad y eficiencia en los procesos.

## Definición de fichero

Un fichero (o archivo) es una unidad lógica de almacenamiento de información que reside en un dispositivo de almacenamiento (disco duro, SSD, memoria USB, red, nube).

Es, en esencia, una secuencia de bytes, cada uno con una posición determinada.

Los sistemas operativos gestionan los ficheros mediante una estructura jerárquica llamada sistema de archivos (file system).

**Todo fichero tiene:**

Un nombre.

Una ruta de acceso (path).

Permisos de acceso (lectura, escritura, ejecución).

Metadatos (fecha de creación, última modificación, tamaño, propietario, etc.).

## Breve evolución histórica

**Años 60-70 – Ficheros planos (flat files):**

Los datos se organizaban en registros y campos dentro de ficheros de texto o binarios.

La manipulación era lenta y rígida: no existían índices ni mecanismos de consulta avanzados.

Lenguajes como COBOL o FORTRAN trabajaban directamente con estos ficheros.

**Años 80-2000 – Aparición de las bases de datos relacionales (RDBMS):**

Los sistemas como Oracle, DB2, SQL Server o MySQL superaron las limitaciones de los ficheros planos.

Permitieron consultas complejas (SQL), transacciones, seguridad y multiusuario.

Los ficheros quedaron relegados a tareas auxiliares (logs, configuración, exportaciones).

**2000 en adelante – Revalorización de los ficheros:**

Con la expansión de Internet y el intercambio de información entre sistemas heterogéneos, los ficheros volvieron a cobrar protagonismo.

**Surgen formatos estándar y legibles por humanos:**

CSV → intercambio tabular simple.

XML → estructuración de datos con etiquetas.

JSON → formato ligero y estándar en APIs REST.

YAML → usado en configuración de aplicaciones modernas (Docker, Kubernetes).

La explosión del Big Data implica trabajar con volúmenes masivos de datos almacenados en ficheros distribuidos (ej. HDFS en Hadoop).

En la nube, los ficheros se almacenan en sistemas distribuidos como Amazon S3, Google Cloud Storage o Azure Blob Storage, con APIs específicas para acceder a ellos.

## Importancia actual de los ficheros

**Los ficheros siguen siendo imprescindibles en múltiples áreas:**

Persistencia básica de datos: guardar información sin necesidad de una base de datos.

Intercambio de datos: enviar/recibir información en formatos estándar (CSV, JSON).

Logs y auditoría: registrar actividad de sistemas para depuración y seguridad.

Configuración de aplicaciones: ficheros .properties, .yaml, .xml.

Procesamiento masivo: Big Data, Machine Learning, ETL.

Integración con la nube: subir, descargar y versionar ficheros.

Ejemplo real: una aplicación web puede almacenar sus logs en un fichero local, enviar métricas en JSON a un servidor de monitorización y cargar configuraciones desde un config.yaml.

## Tipos de acceso a los ficheros

**Aunque se profundizará más adelante, conviene introducir dos conceptos clave:**

Acceso secuencial: se lee el fichero desde el principio hasta el final. Es eficiente para recorrer datos en orden, pero no permite saltar directamente a una posición concreta.

Acceso aleatorio: permite moverse directamente a cualquier parte del fichero. Útil en bases de datos indexadas o ficheros binarios con estructuras fijas.

## Manejo de ficheros en Java

**El lenguaje Java proporciona varias APIs* para manipular ficheros:**

API Clásica (java.io)

Clases: File, FileReader, FileWriter, FileInputStream, FileOutputStream.

Basada en flujos de datos (Streams).

Simples, pero menos eficientes en operaciones complejas.

API Moderna (java.nio.file) (introducida en Java 7)

```java
Clases: Path, Paths, Files.
```

Ofrece operaciones más potentes: copiar, mover, borrar, recorrer directorios.

Compatible con sistemas distribuidos y almacenamiento en red.

```java
Ejemplo: Files.readAllLines(Path) devuelve todo el contenido de un fichero en una lista de Strings.
```

## Ejemplos ilustrativos en Java

#### Ejemplo 1: Crear un fichero con java.io.File

```java
import java.io.File;
import java.io.IOException;

public class CrearFichero {
    public static void main(String[] args) throws IOException {
        File fichero = new File("ejemplo.txt");
        if (fichero.createNewFile()) {
            System.out.println("Fichero creado: " + fichero.getName());
        } else {
            System.out.println("El fichero ya existe.");  //¿cómo se dónde está?
        }
    }
}
```

#### Ejemplo 2: Uso moderno con NIO.2

```java
import java.nio.file.*;

public class NioEjemplo {
    public static void main(String[] args) throws Exception {
        Path ruta = Paths.get("ejemploNIO.txt");

        if (!Files.exists(ruta)) {
            Files.createFile(ruta);
            System.out.println("Fichero creado con NIO.2");
        }

        // Escribir texto en el fichero
        Files.write(ruta, "Hola mundo desde NIO.2".getBytes());

        // Leer todo el contenido
        String contenido = Files.readString(ruta);
        System.out.println("Contenido: " + contenido);
    }
}

```

#### Ejemplo 3: Trabajo con ficheros en la nube (Amazon S3, pseudocódigo)

/*

// Usando la librería AWS SDK para Java

```java
AmazonS3 s3 = AmazonS3ClientBuilder.standard().build();

// Subir fichero a un bucket S3
s3.putObject("mi-bucket", "datos/ejemplo.txt", new File("ejemplo.txt"));

// Descargar fichero
S3Object objeto = s3.getObject("mi-bucket", "datos/ejemplo.txt");
System.out.println("Descargado: " + objeto.getKey());
*/
```

## Conclusión del apartado

Los ficheros han pasado de ser la única forma de persistencia a convertirse en un complemento clave de bases de datos y sistemas distribuidos.

Son imprescindibles en la configuración, logs, intercambio de datos y almacenamiento en la nube.

Java ofrece herramientas clásicas (java.io) y modernas (java.nio.file) que permiten trabajar tanto con ficheros locales como con entornos distribuidos.

# Tipos de ficheros según su contenido

Un fichero es, en esencia, una secuencia de bytes. Sin embargo, esos bytes pueden representar texto legible por humanos o datos binarios estructurados. Por tanto, se distinguen dos categorías.

## Ficheros de texto

Contienen únicamente caracteres codificados (normalmente en UTF-8).

Pueden abrirse y editarse con cualquier editor de texto (Bloc de notas, VS Code, Vim…).

**Ejemplos:**

.txt → texto plano.

.csv → datos tabulares.

.json, .xml, .yaml → datos estructurados para intercambio entre aplicaciones.

**Ventajas:**

Legibles por humanos.

Fáciles de editar y transferir.

Muy utilizados en configuración e intercambio de datos.

**Inconvenientes:**

Consumen más espacio que los binarios para la misma información.

Lectura/escritura más lenta en grandes volúmenes de datos.

#### Ejemplo 4: Escritura y lectura de texto con UTF-8)

```java
import java.nio.file.*;
import java.nio.charset.StandardCharsets;
import java.io.IOException;

public class FicheroTexto {
    public static void main(String[] args) throws IOException {
        Path ruta = Paths.get("alumnos.txt");

        // Escribir en el fichero
        Files.writeString(ruta, "ID,Nombre\n1,Ana\n2,Juan", StandardCharsets.UTF_8);

        // Leer del fichero
        String contenido = Files.readString(ruta, StandardCharsets.UTF_8);
        System.out.println("Contenido del fichero:");
        System.out.println(contenido);
    }
}
```

## Ficheros binarios

Contienen datos en formato no legible directamente por humanos.

Ejemplos: imágenes (.jpg, .png), audio (.mp3, .wav), ejecutables (.exe, .class).

Requieren un programa o librería específica para ser interpretados.

**Ventajas:**

Más compactos y eficientes.

Permiten almacenar información compleja (imágenes, vídeos, modelos IA).

**Inconvenientes:**

No legibles sin herramientas específicas.

Mayor riesgo de corrupción si no se manejan correctamente.

#### Ejemplo 5: Lectura binaria con buffer*

```java
import java.io.*;

public class FicheroBinario {
    public static void main(String[] args) {
        try (BufferedInputStream bis = new BufferedInputStream(
                new FileInputStream("imagen.jpg"))) {

            byte[] buffer = new byte[1024];
            int bytesLeidos;
            int total = 0;

            while ((bytesLeidos = bis.read(buffer)) != -1) {
                total += bytesLeidos;
            }
            System.out.println("Imagen leída con éxito. Total bytes: " + total);
        } catch (IOException e) {
            System.out.println("Error al leer el fichero: " + e.getMessage());
        }
    }
}

```

#### Ejemplo 5.1: Lectura binaria con buffer en ASCII*  IA

try {

```java
            BufferedImage img = ImageIO.read(new File("imagen.jpg"));

            // Escalar la imagen para que quepa en consola
            int newWidth = 100; // ancho en caracteres
            int newHeight = (img.getHeight() * newWidth) / img.getWidth();
            BufferedImage scaled = new BufferedImage(newWidth, newHeight, BufferedImage.TYPE_INT_RGB);
            scaled.getGraphics().drawImage(img, 0, 0, newWidth, newHeight, null);

            // Gradiente de caracteres de más oscuro a más claro
            String gradient = "@#8&xo;:,. ";

            for (int y = 0; y < newHeight; y += 2) { // saltamos filas para corregir proporción
                for (int x = 0; x < newWidth; x++) {
                    Color c = new Color(scaled.getRGB(x, y));
                    int gris = (c.getRed() + c.getGreen() + c.getBlue()) / 3;

                    int index = (gris * (gradient.length() - 1)) / 255;
                    System.out.print(gradient.charAt(index));
                }
                System.out.println();
            }

        } catch (IOException e) {
            System.out.println("Error al cargar la imagen: " + e.getMessage());
        }

```

#### Ejemplo 5.2: Lectura binaria con buffer en ANSI*   IA

```java
try {
    BufferedImage img = ImageIO.read(new File("imagen.jpg"));

    // Escalar para que quepa en consola
    int newWidth = 80; // caracteres de ancho
    int newHeight = (img.getHeight() * newWidth) / img.getWidth();
    BufferedImage scaled = new BufferedImage(newWidth, newHeight, BufferedImage.TYPE_INT_RGB);
    scaled.getGraphics().drawImage(img, 0, 0, newWidth, newHeight, null);

    for (int y = 0; y < newHeight; y += 2) { // corregir proporción
        for (int x = 0; x < newWidth; x++) {
            Color c = new Color(scaled.getRGB(x, y));
            int r = c.getRed();
            int g = c.getGreen();
            int b = c.getBlue();

            // ANSI escape code para color 24 bits
            System.out.print("\u001B[38;2;" + r + ";" + g + ";" + b + "m█");
        }
        System.out.println("\u001B[0m"); // reset color al final de cada línea
    }

} catch (IOException e) {
    System.out.println("Error al cargar la imagen: " + e.getMessage());
}

```

#### Ejemplo 5.3: Lectura binaria con buffer* en bloques dobles (▀/▄) para aprovechar un carácter por dos píxeles verticales, y así quede la imagen más definida   IA

try {

```java
            BufferedImage img = ImageIO.read(new File("imagen.jpg"));

            // Escalar la imagen para que quepa en consola
            int newWidth = 80; // caracteres de ancho
            int newHeight = (img.getHeight() * newWidth) / img.getWidth();
            BufferedImage scaled = new BufferedImage(newWidth, newHeight, BufferedImage.TYPE_INT_RGB);
            scaled.getGraphics().drawImage(img, 0, 0, newWidth, newHeight, null);

            for (int y = 0; y < newHeight - 1; y += 2) { // procesamos de dos en dos
                for (int x = 0; x < newWidth; x++) {
                    // Color del pixel de arriba
                    Color top = new Color(scaled.getRGB(x, y));
                    // Color del pixel de abajo
                    Color bottom = new Color(scaled.getRGB(x, y + 1));

                    // ANSI: color de texto = top, fondo = bottom
                    System.out.print(
                        "\u001B[38;2;" + top.getRed() + ";" + top.getGreen() + ";" + top.getBlue() + "m" +
                        "\u001B[48;2;" + bottom.getRed() + ";" + bottom.getGreen() + ";" + bottom.getBlue() + "m" +
                        "▀" // bloque superior coloreado
                    );
                }
                System.out.print("\u001B[0m\n"); // reset al final de la línea
            }

        } catch (IOException e) {
            System.out.println("Error al cargar la imagen: " + e.getMessage());
        }
```

## Ficheros mixtos y formatos modernos

Aunque la clasificación tradicional distingue entre texto y binario, muchos formatos actuales combinan ambos:

PDF → mezcla de texto, imágenes y metadatos.

DOCX, XLSX, PPTX → en realidad son ficheros ZIP que contienen XML y recursos binarios.

JSON con Base64 → a veces se incrusta información binaria (como imágenes) en un JSON.

## Codificaciones de texto

Un tema clave al trabajar con ficheros de texto es la codificación de caracteres.

Cada fichero es, en el fondo, una secuencia de bytes.

La codificación define cómo esos bytes se traducen en caracteres legibles.

**Ejemplos de codificación:**

ASCII (7 bits, muy limitado).

ISO-8859-1 (latín-1, usado en Europa).

UTF-8 (estándar actual, soporta todos los idiomas).

UTF-16 (interno en Java para representar Strings).

👉 Recomendación actual: usar siempre UTF-8 salvo que exista una necesidad específica.

#### Ejemplo 6: Recodificación de texto

```java
import java.io.*;

public class Recodificacion {
    public static void main(String[] args) {
        try (
            BufferedReader br = new BufferedReader(
                new InputStreamReader(new FileInputStream("entrada.txt"), "UTF-8"));
            BufferedWriter bw = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream("salida.txt"), "ISO-8859-1"))
        ) {
            String linea;
            while ((linea = br.readLine()) != null) {
                bw.write(linea);
                bw.newLine();
            }
            System.out.println("Recodificación realizada correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

entrada.txt

Hola mundo

Árbol, Niño, canción

Emoji: 😀 🚀 ❤️

Carácter chino: 漢

## Conclusión del apartado

Los ficheros se dividen en texto (legibles y fáciles de editar) y binarios (eficientes y compactos).

Hoy día, además de estos tipos, existen formatos híbridos que combinan ambas naturalezas.

La codificación es un aspecto crítico: el estándar actual es UTF-8.

Java proporciona soporte tanto para ficheros de texto como para binarios, incluyendo mecanismos de recodificación.

# La clase File

```java
La clase File de Java forma parte del paquete java.io y es la puerta de entrada clásica para trabajar con ficheros y directorios.
```

**👉 Es importante destacar que:**

```java
Un objeto File no representa el contenido del fichero, sino una referencia a su ruta en el sistema de archivos.
```

Sirve para consultar información, crear, borrar o listar ficheros y directorios, pero no permite leer ni escribir directamente en ellos.

Para la lectura/escritura, se usan otras clases como: FileReader, FileWriter, FileInputStream o FileOutputStream.

## Principales características

**Se encuentra en el paquete:**

```java
import java.io.File;
```

Puede representar tanto ficheros como directorios.

Es independiente del sistema operativo: maneja rutas de forma portable

C:\  Windows

/home/usuario  Linux.

## Métodos más importantes

**Algunos métodos frecuentes de File:**

| Método | Descripción |
| --- | --- |
| exists() | Comprueba si el fichero o directorio existe. |
| isFile() | Comprueba si la ruta corresponde a un fichero. |
| isDirectory() | Comprueba si la ruta corresponde a un directorio. |
| getName() | Devuelve el nombre del fichero o directorio. |
| getAbsolutePath() | Devuelve la ruta absoluta. |
| length() | Devuelve el tamaño en bytes. |
| lastModified() | Fecha de última modificación. |
| delete() | Elimina el fichero o directorio. |
| mkdir() / mkdirs() | Crea un directorio (el segundo crea jerarquías completas). |
| list() | Devuelve los nombres de ficheros de un directorio. |
| listFiles() | Devuelve objetos File con la información de cada fichero en el directorio. |

#### Ejemplo 7: Comprobar existencia y tipo

```java
import java.io.File;

public class InfoFichero {
    public static void main(String[] args) {
        File f = new File("ejemplo.txt");

        if (f.exists()) {
            System.out.println("El fichero existe.");
            if (f.isFile()) {
                System.out.println("Es un fichero.");
                System.out.println("Tamaño: " + f.length() + " bytes");
            } else if (f.isDirectory()) {
                System.out.println("Es un directorio.");  y esto ?
            }
        } else {
            System.out.println("El fichero no existe.");
        }
    }
}
```

#### Ejemplo 8: Listar contenido de un directorio

```java
import java.io.File;

public class ListarDirectorio {
    public static void main(String[] args) {
        File carpeta = new File(".");
        File[] archivos = carpeta.listFiles();

        for (File archivo : archivos) {
            if (archivo.isDirectory()) {
                System.out.println("[DIR] " + archivo.getName());
            } else {
                System.out.println("[FILE] " + archivo.getName() +
                                   " (" + archivo.length() + " bytes)");
            }
        }
    }
}
```

#### Ejemplo 9: Crear un directorio y un fichero dentro

```java
import java.io.File;
import java.io.IOException;

public class CrearFicheroYCarpeta {
    public static void main(String[] args) throws IOException {
        File carpeta = new File("datos");
        if (!carpeta.exists()) {
            carpeta.mkdir();
            System.out.println("Carpeta creada.");
        }

        File fichero = new File(carpeta, "alumnos.txt");
        if (fichero.createNewFile()) {
            System.out.println("Fichero creado en: " + fichero.getAbsolutePath());
        }
    }
}
```

## Limitaciones de File

```java
Aunque File sigue siendo muy usado, presenta limitaciones:
```

No proporciona métodos eficientes para copiar, mover o borrar ficheros.

No permite trabajar directamente con rutas complejas.

La gestión de excepciones es limitada.

```java
👉 Por ello, desde Java 7 se recomienda usar la API NIO.2 (java.nio.file) con clases como Path y Files, que ofrecen más funcionalidades y son multiplataforma.
```

## Comparación con NIO.2

```java
Ejemplo con Files y Path (API moderna):
import java.nio.file.*;

public class EjemploNIO {
    public static void main(String[] args) throws Exception {
        Path ruta = Paths.get("ejemploNIO.txt");

        if (!Files.exists(ruta)) {
            Files.createFile(ruta);
            System.out.println("Fichero creado con NIO.2");
        }

        System.out.println("Ruta absoluta: " + ruta.toAbsolutePath());
        System.out.println("Tamaño: " + Files.size(ruta) + " bytes");
    }
}
✅ Como se aprecia, el código con Path y Files es más moderno, robusto y recomendable en proyectos actuales.
```

## Conclusión del apartado

```java
La clase File es fundamental para trabajar con ficheros y directorios en Java.
```

Permite consultar propiedades, crear y borrar ficheros, y recorrer directorios.

No gestiona el contenido del fichero (se necesitan otras clases).

Aunque sigue siendo útil, hoy se recomienda complementar o sustituir su uso con la API moderna NIO.2 (java.nio.file).

# Formas de acceso a ficheros

Cuando trabajamos con ficheros, existen dos estrategias principales de acceso a los datos almacenados:

Acceso secuencial

Acceso aleatorio

Cada estrategia responde a distintas necesidades de programación y tiene implicaciones en la eficiencia y flexibilidad.

## Acceso secuencial

**Definición:**

Se accede al fichero desde el principio hasta el final, en orden.

Para llegar a un dato intermedio, es necesario recorrer todo lo anterior.

Muy común en ficheros de texto y en logs.

**Ventajas:**

Simplicidad de implementación.

Ideal para recorrer todo el contenido (ej.: procesar línea a línea un CSV).

**Inconvenientes:**

Ineficiente cuando se necesita acceder a posiciones concretas en ficheros grandes.

#### Ejemplo 10: Lectura secuencial de texto con BufferedReader

```java
import java.io.*;

public class AccesoSecuencial {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("datos.txt"))) {
            String linea;
            while ((linea = br.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Ejemplo 11: NIO.2 con Files.lines

```java
import java.nio.file.*;
import java.io.IOException;

public class AccesoSecuencialNIO {
    public static void main(String[] args) throws IOException {
        Path ruta = Paths.get("datos.txt");
        Files.lines(ruta).forEach(System.out::println);
    }
}
👉 Aquí Files.lines() devuelve un Stream, permitiendo aplicar operaciones funcionales (filter, map, etc.).
```

## Acceso aleatorio

**Definición:**

Permite moverse directamente a cualquier posición dentro del fichero sin necesidad de leer todo lo anterior.

Ideal para ficheros binarios con estructuras fijas (ej.: bases de datos, índices, multimedia).

En Java: Se utiliza la clase RandomAccessFile, que combina lectura y escritura en posiciones arbitrarias.

**Ventajas:**

Muy eficiente en ficheros grandes.

Permite modificar registros concretos sin reescribir todo el fichero.

**Inconvenientes:**

Mayor complejidad en la gestión.

Necesita conocer la estructura interna del fichero.

#### Ejemplo 12: Escritura y lectura con acceso aleatorio

```java
import java.io.*;

public class AccesoAleatorio {
    public static void main(String[] args) {

try (RandomAccessFile raf = new RandomAccessFile("usuarios.dat", "rw")) {
    // Vaciar el archivo antes de escribir
    raf.setLength(0);

    // --- ESCRIBIR 3 USUARIOS ---
    
    // USU1
    raf.writeInt(1);
    raf.writeInt(25);
    raf.writeDouble(100.5);

    // USU2
    raf.writeInt(2);
    raf.writeInt(30);
    raf.writeDouble(200.0);

    // USU3
    raf.writeInt(3);
    raf.writeInt(40);
    raf.writeDouble(500.75);

    // Tamaño fijo de cada registro (16 bytes)
    int registroSize = 16;

    // --- LEER EL SEGUNDO USUARIO ---
    raf.seek(registroSize); // inicio del 2º registro
    int id = raf.readInt();
    int edad = raf.readInt();
    double saldo = raf.readDouble();
    System.out.println("Usuario leído:");
    System.out.println("ID: " + id + ", Edad: " + edad + ", Saldo: " + saldo);

    // --- MODIFICAR EL SALDO DEL TERCER USUARIO ---
    raf.seek(2 * registroSize + 8); // campo saldo del 3er usuario
    raf.writeDouble(9999.99);
    System.out.println("Saldo del tercer usuario modificado con éxito.");

    // --- VOLVER A LEER TODOS LOS USUARIOS ---
    raf.seek(0);
    System.out.println("\nUsuarios actuales en el fichero:");
    for (int i = 0; i < 3; i++) {
        id = raf.readInt();
        edad = raf.readInt();
        saldo = raf.readDouble();
        System.out.println("ID: " + id + " | Edad: " + edad + " | Saldo: " + saldo);
    }

} catch (IOException e) {
    e.printStackTrace();
}

    }
}
```

**👉 Observación:**

```java
raf.seek(pos) permite mover el puntero a un byte concreto.
Cada int ocupa 4 bytes → seek(8) posiciona en el tercer entero.
```

## Diferencias principales

| Característica | Acceso secuencial | Acceso aleatorio |
| --- | --- | --- |
| Forma de lectura | De principio a fin | Posiciones arbitrarias |
| Velocidad | Lento para datos intermedios | Rápido para saltos concretos |
| Uso típico | Ficheros de texto, logs | Ficheros binarios estructurados |
| Complejidad | Baja | Alta |

## Acceso combinado en aplicaciones modernas

**Hoy en día, muchos sistemas requieren una mezcla de ambos tipos de acceso:**

Procesamiento secuencial en flujos de Big Data (logs distribuidos, streams de Kafka).

Acceso aleatorio en motores de bases de datos o índices de búsqueda (ej. Lucene, Elasticsearch).

En la nube, las APIs de almacenamiento (ej.: Amazon S3) ofrecen operaciones similares:

Lectura secuencial de objetos.

Descarga de rangos de bytes para simular acceso aleatorio.

## Conclusión del apartado

El acceso secuencial es el más simple y adecuado para recorrer todo el contenido.

El acceso aleatorio permite trabajar de forma eficiente con datos en posiciones concretas.

**En Java, se implementan mediante:**

```java
Flujos (FileReader, BufferedReader, Files.lines) para acceso secuencial.
RandomAccessFile para acceso aleatorio.
```

En sistemas actuales, ambos enfoques conviven, y se integran además con APIs modernas de streams, Big Data y almacenamiento en la nube.

# Operaciones sobre ficheros en Java

Cuando se trabaja con ficheros en Java (ya sean de texto o binarios, con acceso secuencial o aleatorio), se repite un ciclo básico de operaciones:

Apertura del fichero.

Lectura de datos.

Salto (opcional, mover el puntero a otra posición).

Escritura de datos.

Cierre del fichero.

👉 Estas operaciones son comunes a todas las APIs de ficheros en Java.

### Apertura

La apertura consiste en crear un objeto de flujo (stream) que conecta el programa con el fichero.

**Según la operación deseada:**

```java
Lectura → FileReader, FileInputStream, BufferedReader.
Escritura → FileWriter, FileOutputStream, BufferedWriter.
```

Lectura y escritura aleatoria → RandomAccessFile.

#### Ejemplo 13: Apertura de un fichero para lectura

```java
import java.io.*;

public class AperturaEjemplo {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("datos.txt")) {
            System.out.println("Fichero abierto correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Lectura

Se puede realizar carácter a carácter, línea a línea o en bloques de bytes.

El puntero del fichero avanza automáticamente después de cada lectura.

Cuando se alcanza el final, se devuelve -1 (en flujos de bytes o caracteres).

#### Ejemplo 14: Lectura carácter a carácter

```java
try (FileReader fr = new FileReader("datos.txt")) {
    int c;
    while ((c = fr.read()) != -1) {
        System.out.print((char) c);
    }
}
```

#### Ejemplo 15: Lectura línea a línea

```java
try (BufferedReader br = new BufferedReader(new FileReader("datos.txt"))) {
    String linea;
    while ((linea = br.readLine()) != null) {
        System.out.println(linea);
    }
}
👉 Para ficheros grandes, es preferible el uso de buffers (BufferedReader, BufferedInputStream) porque reducen el número de accesos al disco.
```

### Salto

Implica mover el puntero del fichero a una posición concreta.

Se usa principalmente con RandomAccessFile.

#### Ejemplo 16: Saltar a la tercera posición

```java
import java.io.*;

public class SaltoEjemplo {
    public static void main(String[] args) throws IOException {
        try (RandomAccessFile raf = new RandomAccessFile("binario.dat", "rw")) {
            raf.writeInt(10);
            raf.writeInt(20);
            raf.writeInt(30);

            raf.seek(8); // saltar al tercer entero (2 enteros previos * 4 bytes = 8)
            int valor = raf.readInt();
            System.out.println("Entero en la tercera posición: " + valor);
        }
    }
}
```

### Escritura

Permite añadir datos al fichero en la posición actual del puntero.

Puede sobrescribir o añadir (modo append) al final del fichero.

#### Ejemplo 17: Escritura de texto con BufferedWriter

```java
import java.io.*;

public class EscrituraTexto {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("salida.txt", true))) {
            bw.write("Nueva línea de texto");
            bw.newLine();
            System.out.println("Escritura realizada con éxito.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
👉 El segundo parámetro en FileWriter("salida.txt", true) indica append = true, para no sobrescribir.
```

### Cierre

Al terminar de trabajar con el fichero, se debe cerrar con close().

**Si no se cierra:**

Puede que los datos no se guarden correctamente en disco.

Se consumen recursos del sistema.

Con try-with-resources (Java 7+), el cierre es automático.

#### Ejemplo 18: Cierre automático con try-with-resources

```java
try (BufferedWriter bw = new BufferedWriter(new FileWriter("ejemplo.txt"))) {
    bw.write("Hola mundo");
} catch (IOException e) {
    e.printStackTrace();
}
// El fichero se cierra automáticamente aquí

```

### Resumen gráfico del ciclo

[Abrir flujo] → [Leer/Escribir] → [Mover puntero (opcional)] → [Cerrar]

### Buenas prácticas

Usar siempre try-with-resources.

Especificar la codificación (UTF-8 por defecto).

Cerrar los flujos, aunque se produzcan errores.

Evitar abrir y cerrar ficheros repetidamente en bucles → usar buffers.

### Conclusión del apartado

En Java, el ciclo de operaciones sobre ficheros es uniforme: abrir → leer/escribir → cerrar.

La API clásica (java.io) y la moderna (java.nio.file) ofrecen soporte para este ciclo.

El uso de buffers y try-with-resources mejora la eficiencia y seguridad.

En aplicaciones modernas, se complementa con librerías externas (Jackson, Gson, Apache Commons CSV) que facilitan trabajar con formatos específicos.

# Clases relacionadas con flujos de datos

En Java, para trabajar con ficheros se utilizan flujos de datos (streams), que permiten leer o escribir información de forma secuencial.

**📌 Conceptos clave:**

Un stream es un canal de comunicación entre el programa y el fichero.

**Los flujos pueden ser:**

De texto → interpretan los datos como caracteres.

Binarios → trabajan con bytes sin interpretar.

Se pueden combinar con buffers para mejorar el rendimiento.

## Flujos de texto

Se usan cuando se trabaja con ficheros que contienen caracteres (UTF-8, ISO-8859-1, etc.).

| Clase | Lectura / Escritura | Con buffer | Descripción |
| --- | --- | --- | --- |
| FileReader | Lectura | No | Lee caracteres de un fichero de texto. |
| FileWriter | Escritura | No | Escribe caracteres en un fichero de texto. |
| BufferedReader | Lectura | Sí | Lectura más eficiente, línea a línea. |
| BufferedWriter | Escritura | Sí | Escritura eficiente, permite añadir saltos de línea fácilmente. |

#### Ejemplo 19: Lectura de un fichero de texto

```java
import java.io.*;

public class LeerTexto {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("ejemplo.txt"))) {
            String linea;
            while ((linea = br.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Ejemplo 20: Escritura en un fichero de texto

```java
import java.io.*;

public class EscribirTexto {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("ejemplo.txt", true))) {
            bw.write("Nueva línea de texto");
            bw.newLine();
            System.out.println("Texto añadido correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Flujos binarios

Se usan para trabajar con ficheros que contienen datos en formato no textual (imágenes, audio, vídeo, ejecutables).

| Clase | Lectura / Escritura | Con buffer | Descripción |
| --- | --- | --- | --- |
| FileInputStream | Lectura | No | Lee bytes desde un fichero. |
| FileOutputStream | Escritura | No | Escribe bytes en un fichero. |
| BufferedInputStream | Lectura | Sí | Lectura más rápida en bloques de bytes. |
| BufferedOutputStream | Escritura | Sí | Escritura más eficiente en bloques de bytes. |

#### Ejemplo 21: Copiar un fichero binario (imagen)

```java
import java.io.*;

public class CopiarImagen {
    public static void main(String[] args) {
        try (
            BufferedInputStream bis = new BufferedInputStream(new FileInputStream("imagen.jpg"));
            BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("copia.jpg"))
        ) {
            byte[] buffer = new byte[1024];
            int bytesLeidos;
            while ((bytesLeidos = bis.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesLeidos);
            }
            System.out.println("Copia completada con éxito.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Diferencias entre flujos de texto y binarios

| Aspecto | Flujos de texto | Flujos binarios |
| --- | --- | --- |
| Datos manejados | Caracteres (Unicode, UTF-8, etc.) | Bytes crudos |
| Clases principales | FileReader, FileWriter | FileInputStream, FileOutputStream |
| Uso típico | Configuración, logs, JSON, CSV, XML | Imágenes, vídeos, audio, ejecutables |
| Ventaja | Legibilidad, facilidad de depuración | Eficiencia, soporte de cualquier tipo |
| Inconveniente | Recodificación puede causar errores | No legibles directamente |

#### Ejemplo 22: Lectura y escritura (mixto)

Un caso muy común es leer de un fichero de texto y escribir en otro con codificación diferente:

```java
import java.io.*;

public class Recodificar {
    public static void main(String[] args) {
        try (
            BufferedReader br = new BufferedReader(
                new InputStreamReader(new FileInputStream("entrada.txt"), "UTF-8"));
            BufferedWriter bw = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream("salida.txt"), "ISO-8859-1"))
        ) {
            String linea;
            while ((linea = br.readLine()) != null) {
                bw.write(linea);
                bw.newLine();
            }
            System.out.println("Fichero recodificado correctamente.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Conclusión del apartado

Los flujos son la base del trabajo con ficheros en Java.

```java
Texto → FileReader, FileWriter, BufferedReader, BufferedWriter.
Binarios → FileInputStream, FileOutputStream, BufferedInputStream, BufferedOutputStream.
```

Los buffers mejoran el rendimiento al reducir accesos al disco.

La elección entre texto y binario depende del tipo de fichero y del uso que se le vaya a dar.

# Clases con recodificación

Cuando se trabaja con ficheros de texto, el contenido real son bytes en disco. Para que el programa pueda interpretarlos como caracteres, se necesita una codificación (charset) que indique cómo convertir bytes ↔ caracteres.

**⚠️ Si se usa la codificación incorrecta:**

Aparecen errores como “caracteres raros” (�), tildes mal impresas o símbolos extraños.

Esto es común al abrir ficheros antiguos en sistemas modernos.

## Codificación en Java

```java
Internamente, Java representa los String en UTF-16.
```

Al leer o escribir un fichero de texto, se debe indicar la codificación para que la conversión sea correcta.

**Por defecto, Java usa:**

La configuración de la JVM.

Si no está definida, la del sistema operativo.

En última instancia, UTF-8.

👉 Para garantizar portabilidad, se recomienda especificar siempre la codificación explícitamente.

## Clases para recodificación

Java ofrece dos clases clave para convertir entre bytes ↔ caracteres con un charset definido:

InputStreamReader

Convierte bytes de un flujo de entrada (InputStream) en caracteres.

Permite leer un fichero binario como texto con un charset específico.

OutputStreamWriter

Convierte caracteres en bytes con un charset específico al escribir.

Útil para exportar texto a una codificación determinada.

#### Ejemplo 23: Lectura con InputStreamReader (UTF-8)

```java
import java.io.*;

public class LeerUTF8 {
    public static void main(String[] args) {
        try (InputStreamReader isr = new InputStreamReader(
                 new FileInputStream("entrada.txt"), "UTF-8");
             BufferedReader br = new BufferedReader(isr)) {

            String linea;
            while ((linea = br.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

👉 Aquí, los bytes del fichero se transforman en caracteres usando UTF-8.

#### Ejemplo 24: Escritura con OutputStreamWriter (ISO-8859-1)

```java
import java.io.*;

public class EscribirISO {
    public static void main(String[] args) {
        try (OutputStreamWriter osw = new OutputStreamWriter(
                 new FileOutputStream("salida.txt"), "ISO-8859-1");
             BufferedWriter bw = new BufferedWriter(osw)) {

            bw.write("Línea con tildes: áéíóú ñ");
            bw.newLine();
            System.out.println("Texto escrito en ISO-8859-1.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

👉 En este ejemplo, aunque en Java los caracteres están en UTF-16, se convierten a ISO-8859-1 antes de almacenarse en disco.

#### Ejemplo 24: Recodificación entre dos formatos (completo)

Un caso real: convertir un fichero de UTF-8 a UTF-16.

```java
import java.io.*;

public class RecodificacionEjemplo {
    public static void main(String[] args) {
        try (
            BufferedReader br = new BufferedReader(
                new InputStreamReader(new FileInputStream("entrada.txt"), "UTF-8"));
            BufferedWriter bw1 = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream("salida_utf16.txt"), "UTF-16"));
            BufferedWriter bw2 = new BufferedWriter(
                new OutputStreamWriter(new FileOutputStream("salida_iso.txt"), "ISO-8859-1"))
        ) {
            String linea;
            while ((linea = br.readLine()) != null) {
                bw1.write(linea);
                bw1.newLine();
                bw2.write(linea);
                bw2.newLine();
            }
            System.out.println("Ficheros generados en UTF-16 e ISO-8859-1.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

👉 Este código lee un fichero UTF-8 y genera dos versiones nuevas: una en UTF-16 y otra en ISO-8859-1.

## Buenas prácticas

Usar siempre UTF-8 como codificación por defecto.

Evitar trabajar con codificaciones antiguas salvo que sea estrictamente necesario.

Documentar la codificación esperada en las aplicaciones.

Usar StandardCharsets.UTF_8 (más seguro que escribir "UTF-8" en cadena).

## Conclusión del apartado

La recodificación es esencial para garantizar la portabilidad y consistencia en el manejo de ficheros de texto.

Java ofrece las clases InputStreamReader y OutputStreamWriter para especificar explícitamente el charset.

En aplicaciones modernas, se recomienda usar siempre UTF-8, aunque es importante conocer cómo convertir entre distintas codificaciones.

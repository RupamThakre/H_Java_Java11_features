# H Core Java - Java11 features
Java 11 New concepts

- Java 11, released in September 2018, is a Long-Term Support (LTS) release and introduced several key features and enhancements over Java 8 and Java 9/10

# 1. Local-Variable Syntax for Lambda Parameters
You can now use var in lambda expressions.

List<String> sampleList = Arrays.asList("Java", "Kotlin");
String resultString = sampleList.stream()
.map((@Nonnull var x) -> x.toUpperCase())
.collect(Collectors.joining(", "));
assertThat(resultString).isEqualTo("JAVA, KOTLIN");

# 2. New String Methods
Java 11 adds a few new methods to the String class: isBlank, lines, strip, stripLeading, stripTrailing, and repeat.

- " ".isBlank()  -> true
- "Java\n11".lines() -> returns Stream<String>
- " Hello ".strip()
- " Hello ".stripLeading();
- " Hello ".stripTrailing();
- "Java".repeat(3); -> JavaJavaJava

# 3. New Files utility methods
Java 11 adds convenience methods to java.nio.file.Files
We can use the new readString and writeString static methods from the Files class

Path filePath = Files.writeString(Files.createTempFile(tempDir, "demo", ".txt"), "Sample text");
String fileContent = Files.readString(filePath);
assertThat(fileContent).isEqualTo("Sample text");

# 4. Http Client (Standard)
The new HTTP client from the java.net.http package was introduced in Java 9. It has now become a standard feature in Java 11.
The new HTTP API improves overall performance and provides support for both HTTP/1.1 and HTTP/2:

HttpClient httpClient = HttpClient.newBuilder()
.version(HttpClient.Version.HTTP_2)
.connectTimeout(Duration.ofSeconds(20))
.build();
HttpRequest httpRequest = HttpRequest.newBuilder()
.GET()
.uri(URI.create("http://localhost:" + port))
.build();
HttpResponse httpResponse = httpClient.send(httpRequest, HttpResponse.BodyHandlers.ofString());
assertThat(httpResponse.body()).isEqualTo("Hello from the server!");


HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());

# 5. Flight Recorder and Mission Control (JDK tools)

JDK Flight Recorder is a performance monitoring tool built into the JDK.
Useful for profiling and monitoring Java applications in production.

# 6. Removed and Deprecated Features

Removed Java EE and CORBA modules (e.g., java.xml.ws, java.activation)
Applets are no longer supported.
Nashorn JavaScript engine deprecated.

# 7. Running Java Files without compilation

A major change in this version is that we don’t need to compile the Java source files with javac explicitly anymore:

$ javac HelloWorld.java
$ java HelloWorld
Hello Java 8!

Instead, we can directly run the file using the java command:

$ java HelloWorld.java
Hello Java 11!

# 8. Collection to an Array
The java.util.Collection interface contains a new default toArray method which takes an IntFunction argument.
This makes it easier to create an array of the right type from a collection:

List sampleList = Arrays.asList("Java", "Kotlin");
String[] sampleArray = sampleList.toArray(String[]::new);
assertThat(sampleArray).containsExactly("Java", "Kotlin");

# 9. The Not Predicate Method
A static not method has been added to the Predicate interface. We can use it to negate an existing predicate, much like the negate method:

List<String> sampleList = Arrays.asList("Java", "\n \n", "Kotlin", " ");
List withoutBlanks = sampleList.stream()
.filter(Predicate.not(String::isBlank))
.collect(Collectors.toList());
assertThat(withoutBlanks).containsExactly("Java", "Kotlin");

































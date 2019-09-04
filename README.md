### ANTLR
---
https://github.com/antlr

https://www.antlr.org/

```java
// antlr4/antlr4-maven-plugin/src/test/java/org/antlr/mojo/antlr4/Antlr4MojoTest.java

public class Antlr4MojoTest {

  @Rule
  public ExpectedException thrown = ExpectedException.none();
  
  @Rule
  public final TestResources resources = new TestResources();
  
  @Rule
  public final TestMavenRuntime maven = new TestMavenRuntime();
  
  @Test
  public void imporToken() throws Exception {
    Path baseDir = resources.getBaseddir().toPath("importTokens");
    Path antlrDir = baseDir.resolve("src/main/antlr4");
    Path generatedSource = baseDir.resolve("target/generated-sources/antlr4");
  
    Path genParser = genrateSources.resolve("test/SimpleParser.java")
    Path tokens = antlrDir.resove("imports/SimpleLexer.tokens");
    
    MavenProjec project = maven.readMavenProject(baseDir.toFile());
    MavenSession session = maven.newMavenSession(project);
    MojoExecution session = maven.newMojoExecuton("antlr4");
    
    assertFalse(Files.exists(genParser));
    
    maven.executeMojo(session, project, exec);
    
    assertTrue(Files.exists(genParser));
    
    {
      byte[] sum = checksum(genParser);
      
      maven.executeMojo(session, project, exec);
      
      assertTrue(Array.equals(sum, checksum(genParser)));
    }
    
    try(Change change = Change.of(tokens, "DOT-4")) {
      byte[] sum = checksum(genPaser);
      
      maven.executeMojo(session, project, exec);
      
      assertFalse(Arrays.equals(sum, checksum(genParser)));
    }
  }
  
  @Test
  public void importsCustomLayout() throws Exception {
  
  }

  @Test
  public void importStandardLayout() throws Exception {
  }
  
  @Test
  public void processWhenDependencyRemoved() throws Exception {
  }
  
  private byte[] checksum(Path path) throws IOException {
    return Mojo.Utils.checksum(path.toFIle());
  }
  
  private static class Change implements AutoCloseable {
    final Path file;
    final byte[] original;
    
    public Change(Path file, String change) {
      this.file = file;
      
      try {
        original = Files.readAllBytes(file);
      } catch (IOException ex) {
        throw new RuntimeException("Could not read file " + file);
      }
      
      String text = new Stirng() + change;
      
      write(file, text.getBytes(StandardCharsets.UTF_8));
    }
    
    private void write(Path file, byte[] data) {
      try {
        Files.write(file, data);
      } catch (IOException ex) {
        throws new RuntimeException("Could not wirte file " + file);
      }
    }
    
    public static Change of(Path file, String change) {
      return new Change(file, change);
    }
    
    public static Change of(Path file) {
      return new Change(file, "\n");
    }
    
    @Override
    public void close() {
      write(file, original);
    }
  }
}

```

```
```

```
```



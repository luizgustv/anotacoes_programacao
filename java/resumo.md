<p>Based on book: ocp-oracle-certified-professional-java-se-11-programmer-i-study-guide-exam-1z0-815</p>

<h2>Benefits of Java:</h2>

<ul>
<li> Object Oriented: Java allows for functional programming with a class, object-oriented is still the main organization of code;</li>
<li>Encapsulation</li>
<li>Platform Indenpendent: write once, runs everywhere</li>
<li>Robust: Java prevents memory leaks. Java manages on its own and does garbage collector automatically.</li>
<li>Simple</li>
<li>Secure: Java runs inside the JVM. This creates a sandbox that makes it hard for Java code to do evil things to the computer it is running on.</li>
<li>Multithread</li>
<li>Backward Compatibility</li>
</ul>

<h2>Compiling Java Code</h2>

<p>
To compile Java code, the file must have the extension .java. The name of the file must
match the name of the class. The result is a file of bytecode by the same name, but with a
.class filename extension. Remember that bytecode consists of instructions that the JVM
knows how to execute. Notice that we must omit the .class extension to run Zoo.java.
The rules for what a Java code file contains, and in what order, are more detailed than
what we have explained so far (there is more on this topic later in the chapter). To keep
things simple for now, we’ll follow this subset of the rules:
<ul>
<li>Each file can contain only one public class.</li>
<li>The filename must match the class name, including case, and have a .java extension.</li>
</ul>
</p>

<h2>The main method</h2>

<p>
The main() method’s parameter list, represented as an array of
java.lang.String objects. In practice, you can write any of the following:
<ul>
<li>String[ ] args</li>
<li>String args[ ]</li>
<li>String... args;</li>
</ul>
The compiler accepts any of these. The variable name args hints that this list contains
values that were read in (arguments) when the JVM started. The characters [] are brackets and represent an array. An array is a fixed-size list of items that are all of the same
type. The characters ... are called varargs (variable argument lists).
</p>

<h2>Creating Java File</h2>

<p>Some JARs are created by others, such as those downloaded from the Internet or created
by a teammate. Alternatively, you can create a JAR file yourself. To do so, you use the jar
command. The simplest commands create a jar containing the files in the current directory. You can use the short or long form for each option.</p>

```
jar -cvf myNewFile.jar .
jar --create --verbose --file myNewFile.jar .
```

<h2>Primitive types</h2>

| Keyword  | Type  |Example|
|---|---|---|
| boolean  | true or false  | true  ||
| byte  |  8-bit integral |value 123||
| short  | 16-bit integral  | value 123 ||
| int  | 32-bit integral  | value 123 ||
| long  | 64-bit integral  | value 123L ||
| float  |32-bit floating-point  | value 123.45f ||  
| double  |64-bit floating-point  | value 123.456 ||
| char  |16-bit Unicode  | value 'a' ||  
  
<p>var - Java 10</p>

page 171
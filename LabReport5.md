# Lab Report 5
## 1. The file & directory structure needed
    .
    ├── ConfigProcessor.java    # The Java file containing the main program with the bug.
    ├── config.txt              # The configuration file read by the Java program.
    └── runConfigProcessor.sh   # The Bash script to compile and run the Java program.

## 2. The contents of each file before fixing the bug
### ConfigProcessor.java
This Java program is designed to demonstrate file handling and configuration management, with a specific focus on how it reads and interprets settings from a configuration file. The primary functionality revolves around adjusting its behavior based on a mode specified in the config.txt file.
```
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class ConfigProcessor {
    private static String mode = "default";

    public static void main(String[] args) {
        try {
            readConfigFile("config.txt");
        } catch (IOException e) {
            System.out.println("Error reading configuration: " + e.getMessage());
            return;
        }

        System.out.println("Operating in mode: " + mode);
        // Perform operation based on the mode
        performOperation();
    }

    static void readConfigFile(String fileName) throws IOException {
        List<String> lines = Files.readAllLines(Paths.get(fileName));
        for (String line : lines) {
            if (line.startsWith("mode=")) {
                // Bug: Incorrectly parses the mode from the configuration file
                mode = line.split("=")[1].trim().toLowerCase();
                if (!mode.equals("advanced") && !mode.equals("basic")) {
                    mode = "default";  // Fallback mode
                }
            }
        }
    }

    static void performOperation() {
        switch (mode) {
            case "advanced":
                System.out.println("Performing advanced operations...");
                break;
            case "basic":
                System.out.println("Performing basic operations...");
                break;
            default:
                System.out.println("Performing default operations...");
                break;
        }
    }
}

```

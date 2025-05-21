
![image](https://github.com/user-attachments/assets/7dc5cac0-4f79-4bb8-9f9f-a3aca5509ca6)
```java

package org.example;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        List<String> urls = Procesos.readUrls("urls_parcial1.txt");
        List<Thread> threads = new ArrayList<>();
        List<LectorUrl> processors = new ArrayList<>();

        for (String url : urls) {
            LectorUrl processor = new LectorUrl(url);
            Thread thread = Thread.startVirtualThread(processor); // 🧵 Hilo virtual
            threads.add(thread);
            processors.add(processor);
        }

        for (Thread t : threads) t.join(); // Esperamos a que todos terminen

        Procesos.writeResults("resultados.csv", processors);
        System.out.println("-El archivo csv se ha generado correctamente.");
    }
}
```

# Objetivo del trabajo:
El equipo propone un módulo inteligente de orientación dentro del campus que integra recursividad, algoritmos recursivos de ordenamiento y teoría de grafos para organizar información y analizar rutas posibles entre ubicaciones. Con ello se busca comparar alternativas de recorrido y búsqueda (como DFS, BFS y $A^*$) y justificar técnicamente la solución más conveniente según el contexto del desplazamiento y su relación con aplicaciones básicas de inteligencia artificial.
 
# Propuesta del equipo:
Desarrollar y sustentar una propuesta técnica integral para un módulo inteligente de orientación en el campus mediante la aplicación de recursividad, ordenamiento recursivo y modelado con grafos, comparando estrategias de recorrido y búsqueda, fundamentando la recomendación final del equipo y articulando todo el proceso en un repositorio documentado en GitHub y una exposición grupal en video.

# Integrantes del grupo:

| Integrante                  |                 Actividad                           | Trabajo asignado                                                                                                                                                                                    |
| :---                        | :---                                                | :---                                                                                                                                                                                                |
| **Gabriel Sebastian Valdiviezo Castillo**                   | Actividad 1 — Recursividad aplicada                 | Definición de recursividad y principio *divide y vencerás*, diseño de algoritmo recursivo asociado al caso, y explicación del caso base, caso recursivo y condición de finalización.                |
| **Juan Steve Paco Becerra**                       | Actividad 2 — Ordenamiento recursivo                | Planteamiento de algoritmo recursivo de ordenamiento aplicable a datos del caso, descripción paso a paso de la división y obtención del resultado final, y utilidad del enfoque recursivo.          |
| **Richard Mucho**           | Actividad 3 — Modelado del problema mediante grafos | Representación del problema con un grafo (nodos, aristas y sentido de conexiones), propuesta de situaciones para DFS y BFS, y aporte del algoritmo heurístico $A^*$ en búsquedas orientadas a meta. |
| **Jose Jossimar Huamancha** | Actividad 4 — Argumentación final                   | Comparación técnica de alternativas planteadas, recomendación de solución para el módulo del campus y relación de la propuesta con aplicaciones básicas de inteligencia artificial.                 |
 
 
 # PA4-Orientacion-Campus-Grupo1
                                                       Actividad 1
                                                       
**-	¿Que es la recursividad y como se relaciona con el principio “divide y vencerás”?**
La recursividad es la técnica de programación en la que una función se llama a sí misma para resolver un problema, reduciéndolo progresivamente a casos que son más simples hasta llegar a una condición que permita finalizar todo el proceso.
Esto se relaciona con el principio divide y vencerás, porque permite dividir un problema que sea complejo en subproblemas más pequeños y fáciles de resolver. Cuando estos subproblemas llegan a una solución, sus resultados se utilizan para completar el problema inicial u original.
En este caso del módulo inteligente de orientación dentro del campus, la recursividad podría utilizarse para explorar las diferentes ubicaciones o conexiones hasta encontrar un destino.
**-	Diseñar un algoritmo recursivo asociado con el caso:**
```
package pe.edu.isil;

import java.util.*;

public class Main {

    private static Map<String, List<Conexion>> campus = new HashMap<>();

    static class Conexion {
        String destino;
        double distancia;

        public Conexion(String destino, double distancia) {
            this.destino = destino;
            this.distancia = distancia;
        }
    }

    private static void agregarConexion(String origen, String destino, double distancia) {
        campus.putIfAbsent(origen, new ArrayList<>());
        campus.putIfAbsent(destino, new ArrayList<>());

        campus.get(origen).add(new Conexion(destino, distancia));
        campus.get(destino).add(new Conexion(origen, distancia));
    }

    private static void inicializarCampus() {
        agregarConexion("Entrada principal", "Biblioteca", 300);
        agregarConexion("Entrada principal", "Cafeteria", 120);
        agregarConexion("Biblioteca", "Laboratorio", 180);
        agregarConexion("Cafeteria", "Aula", 100);
        agregarConexion("Laboratorio", "Aula", 80);

        campus.put("Gimnasio", new ArrayList<>());
    }

    private static void buscarRutas(String actual, String destino,
                                    Set<String> visitados,
                                    List<String> rutaActual,
                                    double distanciaActual,
                                    List<String> mejorRuta,
                                    double[] mejorDistancia) {

        visitados.add(actual);
        rutaActual.add(actual);

        if (actual.equalsIgnoreCase(destino)) {

            if (distanciaActual < mejorDistancia[0]) {
                mejorDistancia[0] = distanciaActual;
                mejorRuta.clear();
                mejorRuta.addAll(rutaActual);
            }

        } else {

            for (Conexion conexion : campus.get(actual)) {

                if (!visitados.contains(conexion.destino)) {

                    buscarRutas(
                            conexion.destino,
                            destino,
                            visitados,
                            rutaActual,
                            distanciaActual + conexion.distancia,
                            mejorRuta,
                            mejorDistancia
                    );
                }
            }
        }

        rutaActual.remove(rutaActual.size() - 1);
        visitados.remove(actual);
    }

    public static void main(String[] args) {
        inicializarCampus();

        Scanner scanner = new Scanner(System.in);

        System.out.println("==================================");
        System.out.println("   SISTEMA DE ORIENTACION CAMPUS");
        System.out.println("==================================");

        System.out.println("\nUbicaciones disponibles:");

        for (String ubicacion : campus.keySet()) {
            System.out.println("- " + ubicacion);
        }

        System.out.print("\nIngrese la ubicacion de origen: ");
        String origen = scanner.nextLine();

        System.out.print("Ingrese la ubicacion de destino: ");
        String destino = scanner.nextLine();

        if (!campus.containsKey(origen) || !campus.containsKey(destino)) {

            System.out.println("\nUna de las ubicaciones ingresadas no existe.");

        } else {

            Set<String> visitados = new HashSet<>();
            List<String> rutaActual = new ArrayList<>();
            List<String> mejorRuta = new ArrayList<>();

            double[] mejorDistancia = {Double.POSITIVE_INFINITY};

            buscarRutas(
                    origen,
                    destino,
                    visitados,
                    rutaActual,
                    0,
                    mejorRuta,
                    mejorDistancia
            );

            if (!mejorRuta.isEmpty()) {

                System.out.println("\nExiste una ruta disponible.");
                System.out.println("Ruta mas conveniente: " +
                        String.join(" -> ", mejorRuta));

                System.out.println("Distancia total: " +
                        mejorDistancia[0] + " metros");

                System.out.println("Justificacion: se selecciono el recorrido " +
                        "con la menor distancia entre las rutas posibles.");

            } else {

                System.out.println("\nNo existe una ruta disponible entre ambas ubicaciones.");

            }
        }

        scanner.close();
    }
}
```
Hemos diseñado un sistema de orientación del campus el cual recorre conexiones entre ubicaciones y encuentra el camino de menor distancia.
**-	Explicar el caso base, caso recursivo y condición de finalización:**
o	Caso base:
El caso base se presenta cuando la ubicación actual coincide con el destino ingresado por el usuario. El algoritmo comprueba si la distancia que se acumula es menor que la mejor distancia encontrada anteriormente.
```
if (actual.equalsIgnoreCase(destino)) {
    if (distanciaActual < mejorDistancia[0]) {
        mejorDistancia[0] = distanciaActual;
        mejorRuta.clear();
        mejorRuta.addAll(rutaActual);
    }
}
```
o	Caso Recursivo:
El caso recursivo ocurre cuando la ubicación actual no es la misma que el destino. El algoritmo recorre las conexiones que están disponibles y, si encuentra una ubicación que no ha sido visitada, se vuelve a llamar al método buscarRutas(), se avanza hacia esa ubicación sumando la distancia recorrida.
```
buscarRutas(
    conexion.destino,
    destino,
    visitados,
    rutaActual,
    distanciaActual + conexion.distancia,
    mejorRuta,
    mejorDistancia
);
```
o	Condición de finalización:
La finalización de cada recorrido recursivo ocurre cuando se llega a un destino. El proceso concluye cuando se han explorado todas las rutas posibles desde el origen.
```
rutaActual.remove(rutaActual.size() - 1);
visitados.remove(actual);
```
                                                       Actividad 2

Ordenamiento recursivo 

El ordenamiento recursivo es una técnica que permite organizar una lista de datos dividiéndola en partes cada vez más pequeñas hasta que sean fáciles de ordenar. Se basa en el principio de divide y vencerás, utilizando llamadas a sí mismo para resolver cada subconjunto y luego unirlos en orden.

## Planteamiento del algoritmo recursivo de ordenamiento

- **Algoritmo elegido:** Merge Sort (Ordenamiento por Mezcla).
- **Conjunto de datos del caso:** Un vector (`int[]`) que almacena las distancias en metros desde la ubicación actual del estudiante hacia distintos lugares del campus.
- **Criterio de ordenamiento:** De menor a mayor distancia, para mostrar primero los ambientes más cercanos al usuario.
- **Funcionamiento:** Divide el arreglo en dos mitades de forma recursiva y luego las fusiona ordenadamente.

## Descripción paso a paso: división y resultado final

### Fase 1: División del problema (`sort`)

Tomando como ejemplo el arreglo de distancias `arr = {120, 45, 90, 30}`:

- Se comienza con el arreglo completo: `{120, 45, 90, 30}`.
- Se calcula el punto medio y se divide en dos mitades: `{120, 45}` y `{90, 30}`.
- Se vuelve a dividir cada mitad hasta llegar al **caso base** (arreglos de 1 solo elemento): `{120}`, `{45}`, `{90}` y `{30}`.
- Cuando cada subarreglo tiene un único elemento, se detienen las divisiones porque ya se consideran ordenados.

### Fase 2: Obtención del resultado final (`merge`)

- Se comparan y unen los primeros pares: `{120}` y `{45}` pasan a ser `{45, 120}`.
- Se comparan y unen los segundos pares: `{90}` y `{30}` pasan a ser `{30, 90}`.
- Finalmente, se fusionan ambas mitades comparando elemento por elemento (`30 < 45`, `45 < 90`, `90 < 120`).
- **Resultado final:** `{30, 45, 90, 120}` .

## ¿Por qué el enfoque recursivo es útil en este contexto?

- **Rapidez y eficiencia:** Mantiene un tiempo de respuesta rápido ($O(n \log n)$) incluso si el campus tiene cientos de aulas o laboratorios registrados.
- **Ordenamiento estable:** Si dos ambientes del campus están exactamente a la misma distancia, conserva su orden original sin desordenarlos.
- **Código limpio y modular:** Separa en dos métodos distintos la tarea de dividir (`sort`) y la de unir (`merge`), facilitando su mantenimiento.
- **Reutilización:** El mismo algoritmo sirve para ordenar los lugares por otros criterios numéricos, como tiempo de caminata o cantidad de asientos disponibles.

## Código en Java (Merge Sort)

```java
public class MergeSort {
    
    public void sort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            sort(arr, left, mid);      //  primera mitad
            sort(arr, mid + 1, right); //  segunda mitad
            merge(arr, left, mid, right); // fusionar mitades
        }
    }

    //  fusionar dos sub-arrays
    void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] L = new int[n1];
        int[] R = new int[n2];

        for (int i = 0; i < n1; ++i) L[i] = arr[left + i];
        for (int j = 0; j < n2; ++j) R[j] = arr[mid + 1 + j];

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
        while (i < n1) { arr[k] = L[i]; i++; k++; }
        while (j < n2) { arr[k] = R[j]; j++; k++; }
    }

    // Prueba aplicada al caso 
    public static void main(String[] args) {
       
        int[] distanciasCampus = {120, 45, 90, 30};

        MergeSort ordenador = new MergeSort();
        ordenador.sort(distanciasCampus, 0, distanciasCampus.length - 1);

        System.out.print("Distancias ordenadas (de más cercana a más lejana): ");
        for (int d : distanciasCampus) {
            System.out.print(d + "m ");
        }
    }
}
```
                                                       Actividad 3 
Modelado del problema mediante grafos 

Un grafo es una estructura que permite representar las relaciones o conexiones entre diferentes elementos. Está formado por nodos (vértices) y aristas (conexiones).

Representación del problema mediante un grafo 

- Nodos: Representan los lugares por donde puede pasar la persona, como la casa, el parque, el hospital, la biblioteca y la universidad. 

- Aristas: Representan las calles o caminos que conectan esos lugares. 

- Sentido de las conexiones: Si las calles permiten circular en ambos sentidos, el grafo es no dirigido. Si existen calles de un solo sentido, es dirigido. 

- Peso de las aristas: Puede representar la distancia, el tiempo o el costo de trasladarse de un lugar a otro.

 Grafo:

<img width="702" height="572" alt="Captura de pantalla 2026-11-23 221444" src="https://github.com/user-attachments/assets/775b8cbb-d0fe-44d6-80b3-b47ce4f6d940" />

Por ejemplo, los nodos serían A (casa), B (parque), C (hospital), D (biblioteca) y E (universidad). Las conexiones representarían los caminos disponibles entre ellos.

Situaciones en las que conviene utilizar DFS y BFS

DFS (Búsqueda en profundidad)

Situación: encontrar todas las posibles salidas de un laberinto. 

- Se comienza desde la entrada. 

- Se avanza por un camino hasta que ya no se pueda continuar. 

- Si se llega a un camino sin salida, se retrocede y se intenta otra ruta. 

Conviene porque permite explorar diferentes caminos y encontrar posibles soluciones sin necesidad de revisar primero todos los caminos cercanos. 


BFS (Búsqueda en anchura) 

Situación: encontrar la ruta con menor cantidad de conexiones entre dos estaciones de una red de transporte. 

- Se comienza en la estación de origen. 

- Se revisan primero todas las estaciones conectadas directamente. 

- Después se revisan las estaciones que están a dos conexiones. 

- Se continúa hasta llegar al destino.  

Conviene porque permite encontrar el camino con menor número de aristas cuando todas las conexiones tienen el mismo costo.

¿Qué aporta el algoritmo heurístico A*? 
                                                                                             
El algoritmo A es un método de búsqueda que permite encontrar rutas eficientes hacia una meta utilizando información del costo del recorrido y una estimación de la distancia que falta para llegar al destino.

Combina dos valores: 

- g(n): el costo real desde el punto de inicio hasta el nodo actual. 

- h(n): el costo estimado desde el nodo actual hasta la meta (heurística). 

Ejemplo:  

Un GPS que busca la mejor ruta para llegar a un destino. El algoritmo considera la distancia recorrida y estima cuánto falta para llegar, ayudando a elegir caminos más convenientes.

¿Qué aporta A*? 

- Reduce la exploración de caminos innecesarios.

- Orienta la búsqueda hacia el objetivo. 

- Puede encontrar rutas óptimas si utiliza una heurística admisible y se cumplen las condiciones necesarias. 

- Combina el costo del recorrido con una estimación de lo que falta recorrer.

                                                   Actividad 4

Argumentación final

- **Comparación técnica:** Contrastamos el enfoque recursivo y de ordenamiento estructurado con los recorridos y búsquedas en grafos (**DFS**, **BFS** y **$A^*$**), evaluando sus alcances y limitaciones para orientar dentro del campus.
- **Recomendación para el módulo del campus:** Proponemos combinar ordenamiento recursivo para organizar información con una estrategia de búsqueda orientada a la meta (**$A^*$** con heurística admisible o **BFS** según el criterio del grafo) para seleccionar rutas convenientes.
- **Relación con aplicaciones básicas de IA:** Vinculamos el módulo de orientación con sistemas de navegación/rutas, recomendadores y redes de relaciones basadas en grafos, apoyándonos en el análisis algorítmico y el uso crítico de IA.

# Link del Video: ([https://youtu.be/q4Ehaun4e1I](https://www.youtube.com/watch?v=DjzlHZWMzy8))


                   


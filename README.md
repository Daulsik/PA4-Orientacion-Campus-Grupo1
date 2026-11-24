# PA4-Orientacion-Campus-Grupo1
 
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

Situaciones en las que conviene utilizar DFS y BF

DFS (Búsqueda en profundidad)

Situación: encontrar todas las posibles salidas de un laberinto. 

Se comienza desde la entrada. 

Se avanza por un camino hasta que ya no se pueda continuar. 

Si se llega a un camino sin salida, se retrocede y se intenta otra ruta. 

Conviene porque permite explorar diferentes caminos y encontrar posibles soluciones sin necesidad de revisar primero todos los caminos cercanos. 


BFS (Búsqueda en anchura) 

Situación: encontrar la ruta con menor cantidad de conexiones entre dos estaciones de una red de transporte. 

Se comienza en la estación de origen. 

Se revisan primero todas las estaciones conectadas directamente. 

Después se revisan las estaciones que están a dos conexiones. 

Se continúa hasta llegar al destino.  

Conviene porque permite encontrar el camino con menor número de aristas cuando todas las conexiones tienen el mismo costo.

¿Qué aporta el algoritmo heurístico A*? 
                                                                                             
El algoritmo A es un método de búsqueda que permite encontrar rutas eficientes hacia una meta utilizando información del costo del recorrido y una estimación de la distancia que falta para llegar al destino.

Combina dos valores: 

g(n): el costo real desde el punto de inicio hasta el nodo actual. 

h(n): el costo estimado desde el nodo actual hasta la meta (heurística). 

Ejemplo:  

Un GPS que busca la mejor ruta para llegar a un destino. El algoritmo considera la distancia recorrida y estima cuánto falta para llegar, ayudando a elegir caminos más convenientes.

¿Qué aporta A*? 

- Reduce la exploración de caminos innecesarios.

- Orienta la búsqueda hacia el objetivo. 

- Puede encontrar rutas óptimas si utiliza una heurística admisible y se cumplen las condiciones necesarias. 

- Combina el costo del recorrido con una estimación de lo que falta recorrer. 

                   


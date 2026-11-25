## Comparación técnica de alternativas planteadas
Para resolver un módulo inteligente de orientación dentro del campus —que ordena información y analiza rutas posibles entre ubicaciones— es necesario contrastar el rol de las técnicas estudiadas:

- Recursividad y ordenamiento recursivo: La recursividad permite descomponer tareas complejas mediante divide y vencerás, apoyándose en un caso base y llamadas recursivas. En ordenamiento de datos (como Merge Sort), resulta útil para organizar información de forma estructurada y estable, aunque exige cuidar la profundidad de llamadas y la memoria de la pila de ejecución.

- Búsqueda en profundidad (DFS): Explora ramas hasta alcanzar la mayor profundidad antes de retroceder, apoyándose en una pila (explícita o recursiva). Es útil para recorrer estructuras o analizar conectividad/ciclos, pero no garantiza encontrar el camino más corto en términos de pasos o distancia.

- Búsqueda en anchura (BFS): Explora el grafo nivel por nivel mediante una cola. Resulta conveniente para hallar caminos mínimos en grafos no ponderados, aunque puede demandar mayor memoria al ampliar frentes de exploración en redes grandes.

- Algoritmo heurístico $A^*$: Evalúa nodos mediante la función $f(n) = g(n) + h(n)$, combinando el costo acumulado desde el origen ($g(n)$) con una estimación heurística hacia la meta ($h(n)$). Es completo y óptimo cuando la heurística es admisible, orientando la búsqueda hacia el destino con mayor enfoque que una exploración ciega. 

## Recomendación técnica para el módulo del campus

- **Integración de enfoque recursivo y grafos:** Utilizar la recursividad definida en la Actividad 1 para descomponer tareas o recorridos estructurados con un caso base claro, apoyándose en el modelado de ubicaciones y conexiones de la Actividad 3 para analizar rutas dentro del campus.
- **Selección del algoritmo de ruta y ordenamiento:** Recomendar **$A^*$** ($f(n) = g(n) + h(n)$) cuando se busque llegar a un destino específico con un criterio heurístico o de costo, o **BFS** para explorar caminos mínimos por niveles en grafos no ponderados, complementado con el algoritmo de ordenamiento recursivo de la Actividad 2 *(por validar una vez que se suba el avance correspondiente)*[cite: 16, 18, 23].
- **Justificación:** Esta combinación permite organizar información de forma ordenada y orientar desplazamientos hacia una meta sin recorrer caminos innecesarios, equilibrando claridad algorítmica y pertinencia frente al caso de estudio[cite: 16, 18].


## Relación con aplicaciones básicas de inteligencia artificial

- Búsqueda de rutas y navegación: Los grafos modelan ubicaciones (nodos) y trayectos (aristas), y algoritmos como $A^*$ son base clásica para encontrar caminos eficientes hacia un destino, principio que se asemeja a la orientación dentro del campus.   

- Sistemas de recomendación y redes de relaciones: En el curso se abordan grafos aplicados a recomendadores (conectando entidades como usuarios y elementos) y redes sociales, donde el análisis de conexiones y recorridos permite sugerir caminos, lugares o relaciones relevantes.

- Apoyo de la IA en el desarrollo algorítmico: El curso promueve el uso de herramientas de IA para analizar, depurar, simular y optimizar algoritmos, manteniendo el criterio técnico del equipo para justificar qué estructura o algoritmo conviene según el flujo del problema.

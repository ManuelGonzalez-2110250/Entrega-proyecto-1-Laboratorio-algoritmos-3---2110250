21-10250
Para ejecutar solo se tiene que hacer uso del makefile proporcionado, para hacerlo se utiliza CMD y se dirige a la carpeta en la que está descargado el archivo. una vez se hace  basta introduciendo "make" como comando en CMD. 
Si se necesita implementar, se crea una variable con la clase "Grafo" del tipo "ListaAdyacenciaGrafo". Una vez creado el grafo se debe añadir los vèrtices usando "agregarVertice(v: T)", y añadir los arcos usando conectar(desde: T, hasta: T). Hay funciones adicionales como "eliminarVertice(v: T)" si se necesita eliminar un vèrtice, contiene(v: T), para ver si v pertenece al grafo, obtenerArcosSalida(v: T) y obtenerArcosEntrada(v: T) para saber que elementos son adyacentes al v (ya sea de entrada o salida respectivamente), "tamano()" para saber el tamaño del grafo y "subgrafo(vertices: Collection<T>)" para crear un subgrafo, recibiendo vértices.
Para la siguiente gráfica se asumirá que n es la cantidad de vértices, m es la cantidad de arcos (la peor cantidad de arcos siendo n*n o n²) y k, el tamaño del set del subgrafo
| Función| Complejidad |Justificación  |  
|--|--|--|
| agregarVertice | **O(1)** | Dado el uso de "tail" el orden es constante para agregar  |
| eliminarVertice | **O(n+m)** |  Dado que se tiene que revisar cada uno de los vértices y aristas para eliminar cada ocurrencia de v, es de orden n+m|
| conectar | **O(n)** | El primer while va hasta n, y el segundo ve a la sumo n elementos(máximo número de conexiones a un solo vértice), al no estar anidados, es n+n o O(n) |
| contiene | **O(n)** | Se tiene que ver la lísta de vértices completa antes de retornar falso en el peor caso |
| obtenerArcosSalida | **O(n)** | analogamente a conectar, los dos while al no estar anidadps, es 2n o O(n) |
| obtenerArcosEntrada | **O(n+m)** | Al tratarse de dos while anidados, este revisa todos los posibles vertices (n) y todos sus posibles arcos (m, aunque tambièn podrìa ser n²) ,por lo que es **O(n+m) o O(n²)**   |
| tamano | **O(1)** | Solo se ve el valor de la variable "tamanio" |
| subgrafo | **O(n**x**k + m**x**k²)**| El primer while va por los n elementos, luego hay un if de contain que se repite para cada n elemento. Sigue un while anidado con un if de contains y finalmente un conectar, como contain es de orden k(cantidad de elementos del Collection) y conectar de O(n) (pero serìa orden k puesto que se usaría k veces) queda k(n+mk) o O(kxn + mxk²)|

Para el diseño de la funciones:
 
agregarVertice: Se implementó con "tail" para reducir el orden de la función de O(n) a O(1) en el peor caso, Tail cumple la función al ser un marcador al último elemento. De resto la implementación solo crea un nodo nuevo con el vèrtice que se de, y se modifica el tail y el valor del tail para que apunten al nuevo valor.

eliminarVertice: dado que se tienen que ver todos los posibles elementos, el diseño seleccionado revisa los casos posibles, si es de tamaño 0, si es de tamaño 1, si se borra el vértice y si no se borra el vértice, si se tiene que borrar el arco. se trata de no usar "contiene" para minimizar el coste 

conectar: dado que se deben añadir dos elementos en lugar de uno, para simplificar la lógica si se usa "contiene", si efectivamente el grafo contiene desde y hasta, se viaja en un while para encontrar el "desde" y se viaja en otro whila para encontrar el "hasta", si no se encuentra, se añade. Pese a que el modelo usado es menos óptimo que uno que no use contiene, es más legible.

contiene: Se decidió usar un simple bucle while, dado que es una lista enlazada, para buscar el elemento que retorna True si lo encuentra, y si falla todo el while sin encontrar nada, se va a false. 

obtenerArcosSalida: Se modifica el modelo visto en clase para no anidar dos bucles while, en cambio se tienen al mismo nivel. No afecta el orden pero es más legible. Se usa un contiene para iniciar el if por legibilidad.

obtenerArcosEntrada: Similar al modelo visto en clase, viaja por todos los elementos si es que "v" pertenece al grafo, para ver cuantos entran a un vértice v. Similarmente contiene() está por legibilidad, aunque acá al ser O(n+m) afecta menos el orden total. 

tamano: se usa la variable "tamanio" para reducir el orden a O(1), aunque haga menos legible añadir y eliminar, pero al ser intuitivo se deja

subgrafo: Se va por todos los elementos preguntando si está en el conjunto de vértices de "collection", el código trata de solo añadir aquellos que pertenezcan a la intersección de ambos conjuntos. 

Nodo.kt: Para implementar los nodos se hace uso de Nodo.kt que incluye NodoVer para los nodos principales y NodoLad para los lados secundarios.

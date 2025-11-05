#Filtros Automáticos

#Para implementar filtros automáticos, podemos utilizar listas y diccionarios en Python. A continuación, se muestra un ejemplo de cómo se puede implementar:
class Filtro:
    def _init_(self):
        self.reglas = {}

    def agregar_regla(self, regla, accion):
        self.reglas[regla] = accion

    def aplicar_filtro(self, mensaje):
        for regla, accion in self.reglas.items():
            if regla in mensaje:
                return accion
        return "No se aplicó ninguna regla"

#Ejemplo de uso
filtro = Filtro()
filtro.agregar_regla("urgente", "Enviar a la cola de prioridades")
filtro.agregar_regla("spam", "Eliminar mensaje")

mensaje1 = "Este es un mensaje urgente"
mensaje2 = "Este es un mensaje de spam"

print(filtro.aplicar_filtro(mensaje1))  # Output: Enviar a la cola de prioridades
print(filtro.aplicar_filtro(mensaje2))  # Output: Eliminar mensaje
#Cola de Prioridades

#Para implementar una cola de prioridades, podemos utilizar la biblioteca heapq en Python. A continuación, se muestra un ejemplo de cómo se puede implementar:
import heapq

class ColaPrioridades:
    def _init_(self):
        self.cola = []

    def agregar_mensaje(self, mensaje, prioridad):
        heapq.heappush(self.cola, (prioridad, mensaje))

    def obtener_mensaje(self):
        return heapq.heappop(self.cola)[1]

#Ejemplo de uso
cola = ColaPrioridades()
cola.agregar_mensaje("Mensaje urgente", 1)
cola.agregar_mensaje("Mensaje normal", 2)

print(cola.obtener_mensaje())  # Output: Mensaje urgente
print(cola.obtener_mensaje())  # Output: Mensaje normal
#Modelado de la Red de Servidores de Correo

#Para modelar la red de servidores de correo como un grafo, podemos utilizar la biblioteca networkx en Python. A continuación, se muestra un ejemplo de cómo se puede implementar:
import networkx as nx

class RedServidores:
    def _init_(self):
        self.grafo = nx.Graph()

    def agregar_servidor(self, servidor):
        self.grafo.add_node(servidor)

    def agregar_conexion(self, servidor1, servidor2):
        self.grafo.add_edge(servidor1, servidor2)

    def enviar_mensaje(self, servidor_origen, servidor_destino):
        ruta = nx.shortest_path(self.grafo, servidor_origen, servidor_destino)
        return ruta

#Ejemplo de uso
red = RedServidores()
red.agregar_servidor("Servidor A")
red.agregar_servidor("Servidor B")
red.agregar_servidor("Servidor C")
red.agregar_conexion("Servidor A", "Servidor B")
red.agregar_conexion("Servidor B", "Servidor C")

print(red.enviar_mensaje("Servidor A", "Servidor C"))  # Output: ['Servidor A', 'Servidor B', 'Servidor C']
#Simulación del Envío de Mensajes

#Para simular el envío de mensajes entre servidores, podemos utilizar el algoritmo BFS (Breadth-First Search) o DFS (Depth-First Search). A continuación, se muestra un ejemplo de cómo se puede implementar utilizando BFS:
import networkx as nx
from collections import deque

class RedServidores:
    def _init_(self):
        self.grafo = nx.Graph()

    def agregar_servidor(self, servidor):
        self.grafo.add_node(servidor)

    def agregar_conexion(self, servidor1, servidor2):
        self.grafo.add_edge(servidor1, servidor2)

    def enviar_mensaje(self, servidor_origen, servidor_destino):
        cola = deque([(servidor_origen, [servidor_origen])])
        while cola:
            servidor_actual, ruta = cola.popleft()
            if servidor_actual == servidor_destino:
                return ruta
            for vecino in self.grafo.neighbors(servidor_actual):
                if vecino not in ruta:
                    cola.append((vecino, ruta + [vecino]))
        return None

#Ejemplo de uso
red = RedServidores()
red.agregar_servidor("Servidor A")
red.agregar_servidor("Servidor B")
red.agregar_servidor("Servidor C")
red.agregar_conexion("Servidor A", "Servidor B")
red.agregar_conexion("Servidor B", "Servidor C")

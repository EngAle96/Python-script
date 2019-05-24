# Python-script
I need help in a script python who represent a net routing.
import numpy
import random


class Nodo:
   
   routingTable = {} # <key:destinazione;value:next_hop>
   SPT = {} # <key:destinazione;value:percorso>   
   
   def __init__(self, nome):
      self.nome = nome #stringa

   def setGrafo(self, rete):
      self.grafo = rete

   def dijkstra(self, grafo):
      visitati = [self]
      nonVisitati = grafo.listaNodi[:]
      nonVisitati.remove(self)
      costi = {}
      self.pred = {}
      vicini = grafo.trovaVicini(self)
      for nodo in grafo.listaNodi:
         if nodo in vicini:
            arco = grafo.trovaArco(self, nodo)
            costi[nodo.nome] = arco.costo
         else:
            costi[nodo.nome] = 1000000000
      costi[self.nome] = 0
      while len(nonVisitati) > 0:
         costoMinimo = 1000000000
         for nodo in visitati:
            costoTmp = costi[nodo.nome]
            vicini = grafo.trovaVicini(nodo)
            for vicino in vicini:
               if vicino not in visitati:
                  arco = grafo.trovaArco(nodo, vicino)
                  if costoTmp + arco.costo < costoMinimo:
                     costoMinimo = costoTmp + arco.costo
                     visitCand = vicino
                     predCand = nodo
         visitati.append(visitCand)
         nonVisitati.remove(visitCand)
         costi[visitCand.nome] = costoMinimo
         self.pred[visitCand.nome] = predCand
         vicini = grafo.trovaVicini(visitCand)
         for vicino in vicini:
            if vicino not in visitati:
               arco = grafo.trovaArco(visitCand, vicino)
               if costoMinimo + arco.costo < costi[vicino.nome]:
                  costi[vicino.nome] = costoMinimo + arco.costo     
   
   def costruisciPercorso(self, destinazione, grafo):
      path = Percorso(self, destinazione)
      path.addNodo(destinazione)
      print ("calcolo percorso da " + self.nome + " a " + destinazione.nome)
      nodoCorrente = destinazione
      while nodoCorrente != self:
         predecessore = self.pred[nodoCorrente.nome]
         arcoCorrente = grafo.trovaArco(predecessore, nodoCorrente)
         path.addLink(arcoCorrente)
         nodoCorrente = predecessore
         path.addNodo(nodoCorrente)
      path.invertiPercorso()
      return path
   
   def scriviRoutingTable(self, grafo):
      for nodo in grafo.listaNodi:
         nodo.dijkstra(grafo)
         if nodo != self:
            path = self.costruisciPercorso(nodo, grafo)
            print ("Path da " + self.nome + " a " + nodo.nome)
            path.stampaPercorso()
            print ("Il costo del percorso e' " + str(path.getCosto()))
            print ("Il throughput del percorso e' " + str(path.getThroughput()))
            self.routingTable[nodo.nome] = path.getNextHop().nome
         else:
            self.routingTable[nodo.nome] = "direttamente connesso"


class Arco:
   
   def __init__(self, da, a, costo = 1, banda = 100):
      self.da = da
      self.a = a
      self.id = da.nome + "_" + a.nome
      self.costo = costo
      self.banda = banda
   
   def setBanda(self, banda):
      self.banda = banda

   def setCosto(self, costo):
      self.costo = costo

class Grafo:
   
   listaNodi = []
   listaArchi = []
   
   def __init__(self, nome):
      self.nome = nome 
   
   def addNodo(self, nodo):
      self.listaNodi.append(nodo)

   def addArco(self, arco):
      self.listaArchi.append(arco)
   
   def trovaVicini(self, nodo):
      vicini = []
      for arco in self.listaArchi:
         if arco.da == nodo:
            vicini.append(arco.a)
      return vicini
   
   def trovaArco(self, da, a):
      for arco in self.listaArchi:
         if arco.da == da and arco.a == a:
            return arco

class Percorso:

   def __init__(self, sorgente, destinazione):

      self.pathID = sorgente.nome + "-" + destinazione.nome
      self.sorgente = sorgente
      self.destinazione = destinazione
      self.costo = 0
      self.pathLength = 0
      self.throughput = 0
      self.listaNodi = []
      self.listaArchi = []
   
   def addNodo(self, nodo):
      self.listaNodi.append(nodo)
   
   def addLink(self, arco):
      self.listaArchi.append(arco)
   
   def getCosto(self):
      costo = 0
      for arco in self.listaArchi:
         costo += arco.costo
      self.costo = costo
      return costo
   
   def getThroughput(self):
      throughput = 1000000000
      for arco in self.listaArchi:
         if arco.banda < throughput:
            throughput = arco.banda
      self.throughput = throughput
      return throughput
   
   def getPathLength(self):
      self.pathLength = len(listaNodi)
      return self.pathLength
   
   def invertiPercorso(self):
      self.listaNodi.reverse()
      self.listaArchi.reverse()
   
   def getNextHop(self):
      return self.listaNodi[1]
   
   def stampaPercorso(self):
      stringa = ""
      for nodo in self.listaNodi:
         stringa = stringa + nodo.nome + "->"
      print (stringa[:len(stringa)-2])
      return [nodo.nome for nodo in self.listaNodi]


class MatriceTraffico():

    def __init__(self,nome,m,n):
        self.nome=nome
        self.righe=m
        self.colonne=n
        TM = numpy.zeros((m,n))
        self.matrix=TM
        print("Matrice di traffico\n")
        print(TM)

    def assegna_Unita_Traffico(self,TM):
       for i in range(len(TM)):
         for j in range(len(TM[0])):
            TM[i][j] = random.randint(1,10)
            TM[i][i]=0
            TM[j][j]=0
       print("Matrice di traffico con quantita di traffico tra i nodi\n")
       print(TM)


if __name__ == "__main__":
   grafo = Grafo("Rete_4_nodi")
   nodoA = Nodo("A")
   grafo.addNodo(nodoA)
   nodoB = Nodo("B")
   grafo.addNodo(nodoB)
   nodoC = Nodo("C")
   grafo.addNodo(nodoC)
   nodoD = Nodo("D")
   grafo.addNodo(nodoD)
   arco1 = Arco(nodoA, nodoB, 10, 100)
   grafo.addArco(arco1)
   arco2 = Arco(nodoA, nodoC, 1, 100)
   grafo.addArco(arco2)
   arco3 = Arco(nodoB, nodoA, 1, 100)
   grafo.addArco(arco3)
   arco4 = Arco(nodoB, nodoD, 1, 100)
   grafo.addArco(arco4)
   arco5 = Arco(nodoC, nodoA, 1, 100)
   grafo.addArco(arco5)
   arco6 = Arco(nodoC, nodoD, 1, 10)
   grafo.addArco(arco6)
   arco7 = Arco(nodoD, nodoB, 1, 100)
   grafo.addArco(arco7)
   arco8 = Arco(nodoD, nodoC, 1, 100)
   grafo.addArco(arco8)
   nodoA.dijkstra(grafo)
   nodoA.scriviRoutingTable(grafo)
   print (nodoA.routingTable)
   nodoB.dijkstra(grafo)
   nodoB.scriviRoutingTable(grafo)
   print (nodoB.routingTable)
   matrice = MatriceTraffico("Matrice MxN",4,4)
   print(matrice.assegna_Unita_Traffico(matrice.matrix))

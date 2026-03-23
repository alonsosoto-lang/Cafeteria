# Cafeteria
Proyecto cafeteria

print("Programa realizado por")
print("Bruno Macías Guerrero - 039901")
print("Salvador Flores Cazares - 39883")
print("Alonso Soto Barrera  - 39982")

class Pedido_Cafeteria():
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio):
        self.id_pedido = id_pedido
        self.tipo = tipo
        self.tamano = tamano
        self.azucar = azucar
        self.leche = leche
        self.precio = precio
        self.iva = self.precio*0.16
        
    def mostrat_pedido(self):
        print(f"""Detalles del pedido:
              ID: {self.id_pedido}
              Tipo: {self.tipo}
              Tamano: {self.tamano}
              Azucar: {self.azucar}
              Leche: {self.leche}
              Precio: {self.precio}""")
        
    def calcular_precio(self):
        self.precio = self.precio + self.iva
        
    
        
class Cafe_negro(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura):
        super().__init__(id_pedido)
        super().__init__(tipo)
        super().__init__(azucar)
        super().__init__(tamano)
        super().__init__(leche)
        super().__init__(precio)
        self.temperatura = temperatura
        
    def calcular_precio(self):
        self.precio = self.precio + self.iva
        
class Frappe(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura):
        super().__init__(id_pedido)
        super().__init__(tipo)
        super().__init__(azucar)
        super().__init__(tamano)
        super().__init__(leche)
        super().__init__(precio)
        self.temperatura = temperatura
        
    def calcular_precio(self):
        self.precio = self.precio + self.iva
        
class Te_tissana(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura, hielos):
        super().__init__(id_pedido)
        super().__init__(tipo)
        super().__init__(azucar)
        super().__init__(tamano)
        super().__init__(leche)
        super().__init__(precio)
        self.temperatura = temperatura #frio o caliente
        self.hielo = hielos
        
    def calcular_precio(self):
        if self.hielo == True:
            self.precio = self.precio + self.iva + 10
        else:
            self.precio = self.precio + self.iva
        
class Mocha_moka(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura, aditivo):
        super().__init__(id_pedido)
        super().__init__(tipo)
        super().__init__(azucar) #cubos de azucar
        super().__init__(tamano)
        super().__init__(leche)
        super().__init__(precio)
        self.temperatura = temperatura #frio o caliente
        self.aditivo = aditivo #chocolate o crema batida
        
    def calcular_precio(self):
        if self.aditivo == "Chocolate" or self.aditivo == "crema batida":
            self.precio = self.precio + self.iva + 20
        else:
            self.precio = self.precio + self.iva
            
pedido_1 = Cafe_negro(1, "Cafe", 0, "Grande", "sin leche", 80.00)
pedido_2 = Mocha_moka(2, "Cafe", 3, "Mediano", "Deslactosada", 94.00)
pedido_3 = Te_tissana(3, "Te", 2, "chicho", "sin leche", 76.00, "Frio", "Chocolate")

pedido_total = [pedido_1, pedido_2, pedido_3]

for pedidos in pedido_total:
    Pedido_Cafeteria.mostar_pedido()
    pedido_total[pedidos].calcular_precio

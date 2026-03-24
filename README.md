# Cafeteria
#Proyecto cafeteria
# Fábrica de Cafés - Herencia y Polimorfismo

print("Programa realizado por")
print("Bruno Macías Guerrero - 039901")
print("Salvador Flores Cazares - 39883")
print("Alonso Soto Barrera  - 39982")

class Pedido_Cafeteria(): #Se crea la clase principal de todos los adimentos en la cafeteria
#estan presentes los atributos solicitados en la rubrica
# Todos los métodos y atributos aquí son heredados por las clases hijas, las cuales seran el frappe, te tissa, mocha moka
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio):
        self.id_pedido = id_pedido
        self.tipo = tipo
        self.tamano = tamano
        self.azucar = azucar
        self.leche = leche
        self.precio = precio
        
    def mostrar_pedido(self):
     # Imprime todos los detalles del pedido de forma legible.
        # Este método es heredado por todas las clases hijas
        # y se ejecuta igual para cualquier tipo de bebida.
        print(f"""Detalles del pedido:
ID: {self.id_pedido}
Tipo: {self.tipo}
Tamaño: {self.tamano}
Azúcar: {self.azucar}
Leche: {self.leche}
Precio base: {self.precio}""")
        
    def calcular_precio(self):
     # Método base: aplica únicamente el 16% de IVA al precio base.
        # Las clases hijas SOBREESCRIBEN este método
        iva = self.precio * 0.16
        return self.precio + iva

#funcion: precio por tamaño
#da el precio base acorde al tamaño del envase
def precio_por_tamano(tamano): #Poner parametros para la variable de tamano
    tamano = tamano.lower()
    if tamano == "chico":
        return 50 #precio de chico
    elif tamano == "mediano":
        return 65 #precio de mediano
    elif tamano == "grande":
        return 80 #precio de grande
    else:
        return 50 #en caso de no seleccionar una opcion mencionada automaticamente se toma como chico

#aqui se encuentra las clases hijas, la herencia
#cada clase hija agrega su propio atributo extra y se sobreescribe
#clase diseñada por: BRUNO MACIAS GUERRRERO
class Frappe(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, aditivo_extra): #Aditivos a agregar a la bebida
        super().__init__(id_pedido, "Frappe", tamano, azucar, leche, precio)
        self.aditivo_extra = aditivo_extra
        
    def calcular_precio(self):
        if self.aditivo_extra.lower() == "si":
            extra = 20
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16
        return subtotal + iva

#clase diseñada por SALVADOR FLORES CAZARES 
class Te_tissana(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, temperatura, hielo): #Aditivos a agregar a la bebida
        super().__init__(id_pedido, "Te", tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.hielo = hielo
        
    def calcular_precio(self):
        if self.hielo:
            extra = 10
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16
        return subtotal + iva

#clase diseñada por ALONSO SOTO BARRERA 
#la herencia se encuentra presente en donde el mocha moka hereda todos los atributos de la clase base de Pedido_Cafeteria
#algunso atributos extras son la temepratura y el aditivo
#el polimorfismo se encuentra al momento de calcular_precio suma $20 si el aditivo es chocolate o crema batida.
class Mocha_moka(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, temperatura, aditivo): #Aditivos a agregar a la bebida
    #se llama al constructor de la clase base con tipo fijo mocha
        super().__init__(id_pedido, "Mocha", tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.aditivo = aditivo
        
    def calcular_precio(self):
        if self.aditivo.lower() == "chocolate" or self.aditivo.lower() == "crema batida":
            extra = 20
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16 #declarar la variable del impuesto como el subtotal de la suma de los cafes por el .16
        return subtotal + iva


#se solicita el nombre del cliente al inicio, este bucle permite realizar multiples pedidos, cada pedido crear una #instancia de la clase correspondiente
#Al final se recorre la lista mostrando todos los pedidos
#almacenamiento de pedidos: se crea una lista fija para 100 espacios
pedidos_usuario = [None] * 100
indice = 0
contador_id = 1 

while True: #Mostrar menu de los tipos de bebidas en la cafeteria
    print("\n--- MENÚ ---") 
    print("1. Frappe") #Opcion de 1ra bebida
    print("2. Té") #Opcion de 2da bebida
    print("3. Mocha") #Opcion de 3er bebida
    print("4. Salir") #Opcion para salir del codigo y mostrar resumen y cuenta final

    opcion = int(input("Elige una opción: "))

    if opcion == 4:
        break #opcion para quebrar el codigo y mostrar cuenta final

    tamano = input("Tamaño (Chico/Mediano/Grande): ")
    precio_base = precio_por_tamano(tamano) #anadir precio dependiendo el tamano seleccionado

    azucar = int(input("Cantidad de azúcar: ")) #ingresar cantidad de azucar requerida por el usuario
    leche = input("Tipo de leche: ") #ingresar tipo de leche requerida por el usuario

    if opcion == 1:
        aditivo_extra = input("¿Deseas aditivo extra? (si/no): ")
        pedido = Frappe(contador_id, tamano, azucar, leche, precio_base, aditivo_extra) #aditivos default para la bebida

    elif opcion == 2:
        temperatura = input("Caliente o Frío: ") #ingresar temperatura para la bebida
        hielo = input("¿Deseas hielo? (si/no): ") #Pregunta si el usuario requiere hielo
        if hielo.lower() == "si":
            hielo = True
        else:
            hielo = False

        pedido = Te_tissana(contador_id, tamano, azucar, leche, precio_base, temperatura, hielo) #aditivos default para la bebida

    elif opcion == 3:
        temperatura = input("Caliente o Frío: ") #ingresar temperatura para la bebida
        aditivo = input("Chocolate / crema batida / ninguno: ") #aditivos extra para la bebida
        pedido = Mocha_moka(contador_id, tamano, azucar, leche, precio_base, temperatura, aditivo) #aditivos default para la bebida

    else: #Opcion invalida en caso de meter alguna opcion no mencionada en el programa
        print("Opción inválida")
        continue

#guarda el pedido en la lista y avanza los contadores
    pedidos_usuario[indice] = pedido
    indice = indice + 1
    contador_id = contador_id + 1


#resumen final de los pedidos realizandos, mostrandose al polimorfismo en accion 
# Todos los objetos responden a los mismos métodos
# (mostrar_pedido y calcular_precio) pero cada uno
# ejecuta su propia versión según su clase — esto es
print("\n--- PEDIDOS REALIZADOS ---") #Se imprimen los pedidos realizados totales
precio_final = 0

for cont in range(indice):
    print("-------------------")
    pedidos_usuario[cont].mostrar_pedido()
    total = pedidos_usuario[cont].calcular_precio()
    print(f"Precio final: ${total:.2f}")
    
    precio_final = precio_final + total

print(f"\nEl total a pagar es: ${precio_final:.2f}") #Imprimir precio final de la cuenta

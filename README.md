import P as p

calendario = []
clientes = []
salas = []
cupo = []
clientes.clear()
salas.clear()
turnos = []


def mostrar_menu(nombre, opciones):  # incorporamos el parámetro para mostrar el nombre del menú
    print('\033[1m',f'{nombre.center(50,"=",)}\n')
    for clave in sorted(opciones):
        print(f' {clave}) {opciones[clave][0]}')

def leer_opcion(opciones):
    while (a := input('Opción a elegir:')) not in opciones:
        print('Opción incorrecta, vuelva a intentarlo.')
    return a


def ejecutar_opcion(opcion, opciones):
    opciones[opcion][1]()

def generar_menu(nombre, opciones, opcion_salida):  # incorporamos el parámetro para mostrar el nombre del menú
    opcion = None
    while opcion != opcion_salida:
        mostrar_menu(nombre, opciones)
        opcion = leer_opcion(opciones)
        ejecutar_opcion(opcion, opciones)
        print()


def menu_principal():
    opciones = {
        '1': ('REGISTRAR RESERVACION DE SALA', submenu_reservar),
        '2': ('EDITAR NOMBRE DE EVENTO DE RESERVACION YA HECHA', submenu_editar_nom),
        '3': ('CONSULTAR LAS RESERVACIONES EXISTENTES PARA UNA FECHA ESPECIFICA', submenu_consultar_res),
        '4': ('REGISTRAR A UN NUEVO CLIENTE', submenu_cliente),
        '5': ('REGISTRAR UNA SALA', submenu_sala),
        '6': ('SALIR\n', salir)
    }

    generar_menu('Menú principal', opciones, '6')  #indicamos el nombre del menú

def submenu_cliente():
    opciones = {
        'a': ('Inserta el Nombre del cliente', nombre_cliente),
        'b': ('Volver al menú principal\n', salir1)
    }

    generar_menu('Registro del cliente', opciones, 'b')  # indicamos el nombre del submenú


def submenu_sala():
    opciones = {
        'a': ('Capturar el nombre y cupo de una sala', captura_sala),
        'b': ('Mostrar salas', mostrar_salas),
        'c': ('Volver al menú principal\n', salir1)
    }

    generar_menu('Registro de sala', opciones, 'c')  # indicamos el nombre del submenú
    
def submenu_reservar():
    opciones = {
        'a': ('Salas disponibles',salas_disponibles),
        'b': ('Reservar sala', reservar_sala),
        'c': ('Volver al menú principal\n', salir1)
    }

    generar_menu('Reservacion de sala', opciones, 'c')  # indicamos el nombre del submenú

# A partir de aquí creamos las funciones que ejecutan las acciones de los menús
def salas_disponibles():
    t = len(salas)
    if t > 0:
        for s1 in salas:
            print('\t'"ID Sala: ",s1.id,'\t'"Sala Registrada: ",s1.nombre,'\t'"Cupo de la sala: ",s1.cupo,"personas")
    else:
        print("-------------------------------------------")
        print("No hay salas disponibles")
        print("-------------------------------------------")
        
def reservar_sala(p_lista, p_id):
    for c in p_lista:
        if(c.id == p_id):
            result = c
            break
        else:
            result = None
    return result
        
        
def submenu_reservacion():
    print('')
    
def submenu_editar_nom():
    print('')
    
def submenu_consultar_res(): 
    print('')

def clave_cliente():
    print('')

def nombre_cliente():
    print("-------------------------------------------")
    print('Has elegido la opción nombre del cliente')
    print("-------------------------------------------")
    c = input("Ingresa el nombre del cliente: ")
    c1=p.Cliente(c)
    clientes.append(c1)
    print('\n'"Clave de cliente: ",c1.id,'\n'"Nombre del cliente: ",c1.nombre)
    
def clave_sala():
    print('')


def captura_sala():
    print("-------------------------------------------")
    print('Has elegido la opción capturar sala')
    print("-------------------------------------------")
    s=input("Ingresa el nombre de una sala: ") 
    cu =input("Captura el cupo de la sala: ")
    s1=p.Sala(s,cu)
    salas.append(s1)
    print('\n'"ID Sala: ",s1.id,'\n'"Sala Registrada: ",s1.nombre,'\n'"Cupo de la sala: ",s1.cupo,"personas")
    
def mostrar_salas():
    t = len(salas)
    if t > 0:
        for s1 in salas:
            print('\t'"ID Sala: ",s1.id,'\t'"Sala Registrada: ",s1.nombre,'\t'"Cupo de la sala: ",s1.cupo,"personas")
    else:
        print("-------------------------------------------")
        print("No hay salas disponibles")
        print("-------------------------------------------")
        
def salir1():
    print()

def salir():
    print('Saliendo')

if __name__ == '__main__':
    menu_principal() # iniciamos el programa mostrando el menú principal
    


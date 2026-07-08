#examen formato B
def mostrar_menu():
    print("\n========== MENÚ PRINCIPAL ==========")
    print("1. Cupos por género")
    print("2. Búsqueda de películas por rango de precio")
    print("3. Actualizar precio de película")
    print("4. Agregar película")
    print("5. Eliminar película")
    print("6. Salir")
    print("=====================================")

def leer_entero(mensaje):
    while True:
        try:
            return int(input(mensaje))
        except ValueError:
            print("Debe ingresar valores enteros")

# Base de datos inicial simulada según el ejemplo
peliculas = {
    "P101": {"titulo": "Luz de Otoño", "genero": "drama", "precio": 5000, "cupos": 10},
    "P103": {"titulo": "Planeta Agua", "genero": "documental", "precio": 6000, "cupos": 5},
    "P104": {"titulo": "Risa Total", "genero": "comedia", "precio": 7500, "cupos": 15},
}

while True:
    mostrar_menu()
    opcion = input("Ingrese opción: ")

    if opcion == "1":
        genero_buscar = input("Ingrese género a consultar: ").strip().lower()
        total_cupos = 0
        for p in peliculas.values():
            if p["genero"].lower() == genero_buscar:
                total_cupos += p["cupos"]
        print(f"El total de cupos disponibles es: {total_cupos}")

    elif opcion == "2":
        min_precio = leer_entero("Ingrese precio mínimo: ")
        max_precio = leer_entero("Ingrese precio máximo: ")
        
        encontradas = []
        for codigo, datos in peliculas.items():
            if min_precio <= datos["precio"] <= max_precio:
                encontradas.append(f"{datos['titulo']}--{codigo}")
        
        print(f"Las películas encontradas son: {encontradas}")

    elif opcion == "3":
        while True:
            codigo = input("Ingrese código de película: ").strip()
            if codigo in peliculas:
                nuevo_precio = leer_entero("Ingrese nuevo precio: ")
                peliculas[codigo]["precio"] = nuevo_precio
                print("Precio actualizado con éxito.")
            else:
                print("El código no existe")
            
            resp = input("¿Desea actualizar otro precio (s/n)?: ").strip().lower()
            if resp != 's':
                break

    elif opcion == "4":
        codigo = input("Ingrese código de película: ").strip()
        titulo = input("Ingrese título: ")
        genero = input("Ingrese género: ")
        duracion = leer_entero("Ingrese duración (minutos): ")
        clasificacion = input("Ingrese clasificación: ")
        idioma = input("Ingrese idioma: ")
        es_3d = input("¿Es 3D? (s/n): ")
        precio = leer_entero("Ingrese precio: ")
        cupos = leer_entero("Ingrese cupos: ")
        
        peliculas[codigo] = {
            "titulo": titulo,
            "genero": genero,
            "duracion": duracion,
            "clasificacion": clasificacion,
            "idioma": idioma,
            "es_3d": es_3d,
            "precio": precio,
            "cupos": cupos
        }
        print("Película agregada")

    elif opcion == "5":
        codigo = input("Ingrese código de película a eliminar: ").strip()
        if codigo in peliculas:
            del peliculas[codigo]
            print("Película eliminada correctamente.")
        else:
            print("El código no existe.")

    elif opcion == "6":
        print("Programa finalizado.")
        break
    else:
        print("Opción no válida. Intente nuevamente.")

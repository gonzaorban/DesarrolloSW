'''
Defina las clases (nombre, superclase, atributos y métodos) para implementar una solución orientada a objetos para el 
del siguiente problema:

Existen servidores de noticias los cuales se encargan de concentrar las noticias que provienen de las diferentes agencias. 
Las noticias poseen un titulo, una clasificación (por ejemplo, deportes, sociales, policiales, etc.) y un cuerpo, 
este ultimo pueden contener texto, imágenes o video así como también combinaciones de estos tipos de información. 
Los usuarios pueden realizar búsquedas de noticias en estos servidores, por ejemplo que el titulo sea igual a una frase, 
que la categoría sea “deportes”, que en el cuerpo de la noticia aparezca una palabra dada, que el cuerpo contenga una lista de palabras, 
que el documento no tenga mas de 200 palabras, o cualquier combinación de las anteriores formas.

Asimismo el servidor provee un servicio de suscripciones mediante el cual un usuario establece sus preferencias, 
y cuando una nueva noticia llegue al servidor, si la misma cumple con las preferencias del usuario, esta le será remitida al mismo. 
De esta manera un usuario puede establecer que le interesan todas las noticias que sean de deportes y que hablen de De Paul, cuando 
una noticia que hable de De Paul y sea en el ámbito deportivo, la misma le será remitida a este usuario. Por el contrario si la noticia 
habla de De Paul pero es del ámbito chimentero, la misma no le será remitida al usuario.
'''

import copy

class Noticias:
    # Constructor (se ejecuta al crear un objeto)
    def __init__(self, titulo, clasificacion, cuerpo):
        self.titulo = titulo
        self.clasificacion = clasificacion # hay una sola categoria
        self.cuerpo = cuerpo # objeto cuerpo

class Cuerpo:
    def __init__(self, texto=None, imagen=None, video=None):
        self.texto = texto
        self.imagen = imagen
        self.video = video
        if texto is not None:
            self.longitud = len(texto)

class Usuarios:
    def __init__(self, nombre, edad, email, constraseña, suscripcion, preferencias):
        self.nombre = nombre
        self.edad = edad
        self.email = email
        self.contraseña = constraseña
        self.suscripcion = suscripcion #Booleano
        if self.suscripcion:
            self.preferencias = preferencias
        self.recomendaciones = []

class Preferencias:
    def __init__(self, categorias=None, palabras=None):
        self.categoriasP = categorias or [] # Si no se pasan valores, por defecto se usan listas vacías gracias al truco or [].
        self.palabrasP = palabras or [] 

class Sistema:
    def __init__(self):
        self.lista_usuarios = []
        self.lista_noticias = []
    
    def agregar_usuario(self, usuario):
        self.lista_usuarios.append(usuario)
    
    def agregar_noticia(self, noticia):
        self.lista_noticias.append(noticia)
        # Recomendar noticia a usuarios suscriptos
        for usuario in self.lista_usuarios:
            if usuario.suscripcion and self.cumple_preferencias(noticia, usuario.preferencias):
                usuario.recomendaciones.append(noticia)
    
    def cumple_preferencias(self, noticia, preferencias):
        #Las preferencias no estan vacias y la clasificacion de la noticia no esta en las preferencias
        if preferencias.categoriasP and noticia.clasificacion not in preferencias.categoriasP:
            return False
        
        # Las preferencias no estan vacias y el cuerpo de la noticia no tiene texto o no todas las palabras estan en el texto
        if preferencias.palabrasP and (not noticia.cuerpo.texto or not all(p in noticia.cuerpo.texto for p in preferencias.palabrasP)):
            return False
        
        return True
    
    def busquedaFrase(self, frase, lista):
        salida = []
        for noticia in lista:
            if noticia.titulo == frase:
                salida.append(noticia)
        
        return salida

    def busquedaCategoria(self, categoria, lista):
        salida = []
        for noticia in lista:
            if noticia.clasificacion == categoria:
                salida.append(noticia)
        
        return salida

    def busquedaPalabras(self, listaPalabras, lista):
        salida = []
        for noticia in lista:
            if noticia.cuerpo.texto is not None:
                if all(palabra in noticia.cuerpo.texto for palabra in listaPalabras):
                    salida.append(noticia)
        
        return salida

    def busquedaMaximo(self, maximo, lista):
        salida = []
        for noticia in lista:
            if noticia.cuerpo.longitud <= maximo:
                salida.append(noticia)
        
        return salida


    def busqueda(self, frase = None, categoria = None, listaPalabra = None, maximoPalabras = None):            
        
        salida = copy.deepcopy(salida)
        
        if frase != None:
            salida = self.busquedaFrase(frase, salida)
        
        if categoria != None:
            salida = self.busquedaCategoria(categoria, salida)
        
        if listaPalabra != None:
            salida = self.busquedaPalabras(listaPalabra, salida)
        
        if maximoPalabras != None:
            salida = self.busquedaMaximo(maximoPalabras, salida)
        
        return(salida)

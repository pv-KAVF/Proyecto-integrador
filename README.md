codigo login en punto de venta 
ctk.set_appearance_mode("dark")
class SistemaPOSApp(ctk.CTk):
""" Clase principal que controla las ventanas del sistema
"""
def __init__(self):
super().__init__()
self.title("Sistema POS - Tiendas 3B")
self.geometry("1024x768")
self.configure(fg_color="#cc0000") # Fondo corporativo
# Contenedor padre donde se apilarán todas las
 
pantallas
 
self.contenedor = ctk.CTkFrame(self,
 
fg_color="transparent")
 
self.contenedor.pack(fill="both", expand=True)
self.contenedor.grid_rowconfigure(0, weight=1)
self.contenedor.grid_columnconfigure(0, weight=1)
# Diccionario para almacenar los frames de las
 
pantallas
 
self.pantallas = {}
# Inicializamos todas las pantallas y las guardamos en
 
el diccionario
 
for Pantalla en (PantallaLogin, PantallaCaja):
frame = Pantalla(padre=self.contenedor,
 
controlador=self)
 
self.pantallas[Pantalla] = frame
# Se colocan todas en la misma posición (celda
 
0,0)
 
frame.grid(row=0, column=0, sticky="nsew")
# Mostramos la pantalla inicial
self.mostrar_pantalla(PantallaLogin)
def mostrar_pantalla(self, clase_pantalla):
 
""" Eleva el frame solicitado al frente de la vista
 
"""
 
frame = self.pantallas[clase_pantalla]
frame.tkraise()
 
class PantallaLogin(ctk.CTkFrame):
""" Módulo de inicio de sesión """
def __init__(self, padre, controlador):
# Hereda del Frame pero con fondo oscuro para el login
super().__init__(padre, fg_color="#1e1e1e",
 
corner_radius=0)
 
self.controlador = controlador
# --- UI DEL LOGIN ---
# Contenedor central simulando un modal
marco_central = ctk.CTkFrame(self, width=450,
height=500, fg_color="#2b2b2b", corner_radius=15)
marco_central.place(relx=0.5, rely=0.5,
 
anchor="center")
 
titulo = ctk.CTkLabel(marco_central, text="INGRESO DE
 
TURNO", font=("Arial", 22, "bold"))
titulo.place(x=40, y=40)
self.entrada_usuario = ctk.CTkEntry(marco_central,
 
width=370, height=45, placeholder_text="Usuario")
self.entrada_usuario.place(x=40, y=120)
self.entrada_pass = ctk.CTkEntry(marco_central,
width=370, height=45, placeholder_text="••••••", show="*")
 
self.entrada_pass.place(x=40, y=190)
boton_entrar = ctk.CTkButton(marco_central,
 
text="INICIAR TURNO", width=370, height=50,
 
fg_color="#cc0000",
 
hover_color="#990000",
command=self.validar_credenciales)
boton_entrar.place(x=40, y=280)
 
def validar_credenciales(self):
usuario = self.entrada_usuario.get()
password = self.entrada_pass.get()
# AQUI SE HARÁ EL SELECT A MYSQL
# Simulación temporal:
if usuario != "" and password != "":
# Si es correcto, cambiamos a la pantalla de caja
self.controlador.mostrar_pantalla(PantallaCaja)
self.entrada_usuario.delete(0, 'end')
self.entrada_pass.delete(0, 'end')
else:
messagebox.showerror("Error", "Campos obligatorios
 
vacíos")
class PantallaCaja(ctk.CTkFrame):
""" Módulo principal de cobro (CRUD básico) """
def __init__(self, padre, controlador):
super().__init__(padre, fg_color="#ffffff") # Fondo
 
blanco para la caja
 
self.controlador = controlador
# --- UI DE LA CAJA ---
header = ctk.CTkFrame(self, height=80,
 
fg_color="#1e1e1e", corner_radius=0)
header.pack(fill="x", side="top")
titulo = ctk.CTkLabel(header, text="TIENDAS 3B - CAJA
REGISTRADORA", text_color="white", font=("Arial", 20, "bold"))
 
titulo.pack(side="left", padx=20, pady=25)
boton_salir = ctk.CTkButton(header, text="Cerrar
 
Turno", fg_color="#cc0000",
 
command=lambda:
self.controlador.mostrar_pantalla(PantallaLogin))
boton_salir.pack(side="right", padx=20, pady=25)
# Aquí irá el listado de productos y los botones del
 
CRUD...
 
label_temporal = ctk.CTkLabel(self, text="Aquí va el
módulo CRUD de ventas y productos", text_color="black")
 
label_temporal.pack(pady=100)
 
# Arranque de la aplicación
if __name__ == "__main__":
app = SistemaPOSApp()
app.mainloop()



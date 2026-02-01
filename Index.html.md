<!DOCTYPE html>  
<html lang="es">  
<head>  
<meta charset="UTF-8">  
<title>Rivelo</title>  
<style>  
body{  
font-family:Arial, sans-serif;  
margin:0;  
background:linear-gradient(135deg,#1e3c72,#2a5298);  
color:#333  
}  
header{  
background:#000;  
color:#fff;  
padding:20px;  
text-align:center;  
font-size:28px;  
letter-spacing:2px  
}  
.container{max-width:1000px;margin:auto;padding:20px}  
.card{  
background:#fff;  
border-radius:10px;  
padding:15px;  
margin:15px 0;  
box-shadow:0 5px 15px rgba(0,0,0,0.2);  
position:relative  
}  
.card img{max-width:100%;border-radius:8px}  
h3{color:#fff}  
.admin, #login{  
background:#ffffff;  
padding:15px;  
border-radius:10px;  
margin-bottom:20px  
}  
input,textarea,select{  
width:100%;  
padding:10px;  
margin:6px 0;  
border-radius:6px;  
border:1px solid #ccc  
}  
button{  
padding:10px;  
border:none;  
border-radius:6px;  
cursor:pointer;  
font-weight:bold  
}  
.btn-dark{background:#000;color:#fff}  
.delete-btn{  
position:absolute;  
top:10px;  
right:10px;  
background:red;  
color:#fff;  
padding:5px 8px;  
border-radius:5px;  
font-size:12px;  
cursor:pointer  
}  
.whatsapp-btn{  
text-align:center;  
margin:30px 0  
}  
.whatsapp-btn a{  
background:#25D366;  
color:#fff;  
padding:12px 25px;  
border-radius:8px;  
text-decoration:none;  
font-weight:bold;  
font-size:18px  
}  
.info{  
font-size:14px;  
color:#555  
}  
</style>  
</head>  
<body>  
  
<header>RIVELO</header>  
  
<div class="container">  
  
<div id="login">  
<h3>🔐 Panel privado Rivelo</h3>  
<input type="password" id="pass" placeholder="Contraseña">  
<button class="btn-dark" onclick="entrar()">Entrar</button>  
</div>  
  
<div class="admin" id="adminPanel" style="display:none;">  
<h3>➕ Añadir producto</h3>  
<input type="text" id="titulo" placeholder="Título">  
<textarea id="descripcion" placeholder="Descripción"></textarea>  
<input type="number" id="precio" placeholder="Precio €">  
<input type="text" id="imagen" placeholder="URL de imagen">  
<select id="estado">  
<option>Nuevo</option>  
<option>Usado</option>  
</select>  
<input type="text" id="ubicacion" placeholder="Ubicación">  
<button class="btn-dark" onclick="agregarProducto()">Guardar producto</button>  
</div>  
  
<h3>🛍️ Productos disponibles</h3>  
<div id="productos"></div>  
  
<div class="whatsapp-btn">  
<a href="https://wa.me/34610387701" target="_blank">Hablar por WhatsApp</a>  
</div>  
  
</div>  
  
<script>  
let productos = JSON.parse(localStorage.getItem('riveloProductos')) || [];  
  
function guardar(){  
localStorage.setItem('riveloProductos', JSON.stringify(productos));  
}  
  
function mostrarProductos(){  
let div=document.getElementById('productos');  
div.innerHTML="";  
productos.forEach((p,i)=>{  
div.innerHTML+=`  
<div class="card">  
<button class="delete-btn" onclick="eliminar(${i})">X</button>  
<h2>${p.titulo}</h2>  
<img src="${p.imagen}">  
<p>${p.descripcion}</p>  
<p class="info"><strong>Precio:</strong> ${p.precio} €</p>  
<p class="info"><strong>Estado:</strong> ${p.estado}</p>  
<p class="info"><strong>Ubicación:</strong> ${p.ubicacion}</p>  
</div>`;  
});  
}  
  
function entrar(){  
if(pass.value==="rivelo123"){  
adminPanel.style.display="block";  
alert("Bienvenido Rivelo 😎");  
}else{  
alert("Contraseña incorrecta");  
}  
}  
  
function agregarProducto(){  
productos.unshift({  
titulo:titulo.value,  
descripcion:descripcion.value,  
precio:precio.value,  
imagen:imagen.value,  
estado:estado.value,  
ubicacion:ubicacion.value  
});  
guardar();  
mostrarProductos();  
}  
  
function eliminar(i){  
productos.splice(i,1);  
guardar();  
mostrarProductos();  
}  
  
mostrarProductos();  
</script>  
  
</body>  
</html>  

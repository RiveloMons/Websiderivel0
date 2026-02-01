<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Rivelo Proveedores</title>
<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  background:linear-gradient(120deg,#0f2027,#203a43,#2c5364);
  color:#fff;
  overflow-x:hidden;
}
header{
  text-align:center;
  padding:25px;
  font-size:34px;
  font-weight:bold;
  letter-spacing:3px;
  background:#000;
}
.container{max-width:1100px;margin:auto;padding:20px}
.welcome{
  background:#ffffff;
  color:#000;
  padding:20px;
  border-radius:12px;
  text-align:center;
  margin-bottom:25px;
  animation:fadeIn 1s ease-in-out;
}
.section h2{
  border-left:6px solid #25D366;
  padding-left:10px;
}
.card{
  background:#fff;
  color:#000;
  border-radius:12px;
  padding:15px;
  margin:15px 0;
  box-shadow:0 8px 20px rgba(0,0,0,0.3);
  transition:0.3s;
}
.card:hover{transform:scale(1.03)}
.price{font-weight:bold;margin:8px 0}
button{
  padding:10px 15px;
  border:none;
  border-radius:6px;
  cursor:pointer;
  font-weight:bold;
  background:#000;
  color:#fff;
}
.vip{
  border:3px solid gold;
}
#adminLogin{
  text-align:center;
  margin:20px 0;
}
#adminPanel{
  display:none;
  background:#fff;
  color:#000;
  padding:20px;
  border-radius:12px;
  margin-bottom:30px;
}
input,textarea{
  width:100%;
  padding:8px;
  margin:6px 0;
}
@keyframes fadeIn{
  from{opacity:0;transform:translateY(20px)}
  to{opacity:1;transform:translateY(0)}
}
</style>
</head>
<body>

<header>RIVELO</header>
<div class="container">

<div class="welcome">
Bienvenido a Rivelo, la fuente privada de proveedores reales. Compra tu pack y recibe los contactos automáticamente en tu correo.
</div>

<!-- 🔐 LOGIN ADMIN -->
<div id="adminLogin">
  <input type="password" id="pass" placeholder="Contraseña administrador">
  <button onclick="login()">Entrar al panel</button>
</div>

<!-- 🛠 PANEL ADMIN -->
<div id="adminPanel">
  <h3>Editar Packs</h3>
  <textarea id="dataEdit" rows="10"></textarea>
  <button onclick="guardarCambios()">Guardar cambios</button>
</div>

<!-- 📦 SECCIONES -->
<div id="contenido"></div>

</div>

<script>
const PASSWORD="Rivelo#9274_PROveedores!";

// Datos editables
let packs = JSON.parse(localStorage.getItem("riveloPacks")) || [
{cat:"🇪🇸 Español",nombre:"Perfumes Español",precio:"19,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Perfumes 1 y 2",precio:"19,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Relojes y G-Shock",precio:"15,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Tecnología / iPhone / AirPods",precio:"30€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Zapatillas",precio:"15,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Ropa",precio:"15,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Fútbol",precio:"19,99€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Lujo / LV",precio:"25€",numeros:""},
{cat:"🇨🇳 Chinos",nombre:"Vapers",precio:"15,20€",numeros:""},
{cat:"⭐ VIP",nombre:"Todos los proveedores",precio:"150€",numeros:""}
];

function mostrar(){
let div=document.getElementById("contenido");
div.innerHTML="";
packs.forEach(p=>{
div.innerHTML+=`
<div class="card ${p.cat.includes('VIP')?'vip':''}">
<h3>${p.cat} - ${p.nombre}</h3>
<p class="price">Precio: ${p.precio}</p>
<button onclick="comprar('${p.nombre}')">Comprar</button>
</div>`;
});
}

function comprar(nombre){
alert("Aquí luego conectas el botón al enlace de Payhip del pack: "+nombre);
}

function login(){
if(pass.value===PASSWORD){
adminPanel.style.display="block";
dataEdit.value=JSON.stringify(packs,null,2);
}else{
alert("Contraseña incorrecta");
}
}

function guardarCambios(){
packs=JSON.parse(dataEdit.value);
localStorage.setItem("riveloPacks",JSON.stringify(packs));
mostrar();
alert("Cambios guardados");
}

mostrar();
</script>

</body>
</html>

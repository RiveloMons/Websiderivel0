<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Rivelo Proveedores</title>
<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
  color:#fff;
}
header{
  text-align:center;
  padding:30px;
  font-size:36px;
  font-weight:bold;
  letter-spacing:3px;
  background:#000;
}
.container{
  max-width:1200px;
  margin:auto;
  padding:20px;
}
.welcome{
  background:#ffffff;
  color:#000;
  padding:25px;
  border-radius:15px;
  text-align:center;
  margin-bottom:30px;
  animation:fadeIn 1s ease-in-out;
  font-size:18px;
  font-weight:bold;
}
#adminLogin{
  text-align:center;
  margin:20px 0;
}
#adminPanel{
  display:none;
  background:#fff;
  color:#000;
  padding:25px;
  border-radius:15px;
  margin-bottom:30px;
}
input, textarea{
  width:100%;
  padding:10px;
  margin:8px 0;
  border-radius:8px;
  border:1px solid #ccc;
  font-size:16px;
}
button{
  padding:15px 25px;
  border:none;
  border-radius:12px;
  cursor:pointer;
  font-weight:bold;
  font-size:18px;
  transition:0.3s;
}
button:hover{
  transform:scale(1.05);
}
#contenido{
  display:grid;
  grid-template-columns: repeat(auto-fit,minmax(300px,1fr));
  gap:20px;
}
.card{
  background: linear-gradient(135deg,#ffffff,#f0f0f0);
  color:#000;
  border-radius:20px;
  padding:20px;
  box-shadow:0 10px 25px rgba(0,0,0,0.3);
  text-align:center;
  transition:0.3s;
}
.card:hover{
  transform:scale(1.05);
  box-shadow:0 15px 30px rgba(0,0,0,0.4);
}
h2{
  margin-bottom:15px;
  color:#25D366;
}
p{
  margin:6px 0;
  font-size:16px;
}
.price{
  font-weight:bold;
  margin:10px 0;
  font-size:18px;
  color:#111;
}
.vip{
  border:4px solid gold;
}
@keyframes fadeIn{
  from{opacity:0;transform:translateY(20px);}
  to{opacity:1;transform:translateY(0);}
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
  <textarea id="dataEdit" rows="15"></textarea>
  <button onclick="guardarCambios()">Guardar cambios</button>
</div>

<!-- 📦 SECCIONES -->
<div id="contenido"></div>

</div>

<script>
const PASSWORD="Rivelo#9274_PROveedores!";

// Datos de proveedores
let packs = JSON.parse(localStorage.getItem("riveloPacks")) || [
{cat:"Chinos", nombre:"VAPERS", precio:"15,20€", numeros:"+86 138 7003 0606"},
{cat:"Chinos", nombre:"Pulseras LV", precio:"15,20€", numeros:"+86 159 8010 0656"},
{cat:"Chinos", nombre:"Accesorios de lujo", precio:"25€", numeros:"+86 178 9101 7227"},
{cat:"Chinos", nombre:"Botas de fútbol", precio:"19,99€", numeros:"+86 177 2083 5685, +86 135 3538 6151, +86 183 1215 9936, +86 157 6835 9931, +86 151 6048 4398, +86 153 0597 2112, +86 193 5944 0554, +86 181 5975 3025, +86 136 1601 7756, +86 130 5569 1894, +86 132 0594 3370"},
{cat:"Chinos", nombre:"Zapatillas", precio:"15,99€", numeros:"+86 195 7767 7246, +86 133 3845 1248, +86 131 6486 5952, +86 158 9208 5764, +86 153 0609 8139, +86 159 8034 8547, +86 137 9908 8613"},
{cat:"Chinos", nombre:"Tecnología", precio:"30€", numeros:"+86 183 0385 0813, +86 158 1870 9179, +86 180 3810 0841, +86 158 1865 0060, +86 186 8836 1378"},
{cat:"Chinos", nombre:"iPhones 1:1 y AirPods", precio:"30€", numeros:"+86 185 1194 9009"},
{cat:"Chinos", nombre:"Relojes", precio:"15,99€", numeros:"+852 5580 5301, +86 157 6690 3977"},
{cat:"Chinos", nombre:"Perfumes", precio:"19,99€", numeros:"+86 187 2951 4095, +86 188 2367 5993"},
{cat:"Español", nombre:"PERFUMES ESPAÑOL", precio:"19,99€", numeros:"+34 600 43 85 76"},
{cat:"Chinos", nombre:"Tecnología y perfumes", precio:"19,99€", numeros:"+86 183 0385 0813"},
{cat:"VIP", nombre:"Todos los proveedores", precio:"150€", numeros:"Todos los números"}
];

function mostrar(){
  let div=document.getElementById("contenido");
  div.innerHTML="";
  packs.forEach(p=>{
    div.innerHTML+=`
      <div class="card ${p.cat.includes('VIP')?'vip':''}">
        <h2>${p.cat} - ${p.nombre}</h2>
        <p class="price">Precio: ${p.precio}</p>
        <p>${p.numeros}</p>
        <button onclick="comprar('${p.nombre}')">Comprar</button>
      </div>
    `;
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

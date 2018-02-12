# Manipulación de elementos del escaparate virtual con DOM
### Generar campo de tarjeta de credito mediante DOM
Primero obtenemos el valor del campo direccion, despues creamos el input de la tarjeta de credito y lo añadimos con appendChild al formulario del HTML, despues si el campo de direccion no esta vacio, mostramos el input de la tarjeta, si esta vacio no lo mostramos y borramos el input de la tarjeta.
```
function muestraCampo(){
   
    var direccion= document.getElementById("direccion").value;/*
    var contenedor= document.getElementById("Campotarjeta");
    var inputTarjeta=document.createElement('INPUT');
    inputTarjeta.type='TEXT';
    inputTarjeta.id='tarjeta';
    contenedor.appendChild(inputTarjeta);*/
    
    if(direccion!=""){
        
     document.getElementById("Campotarjeta").style.display='block';
    }else{
        contenedor.removeChild(contenedor.childNodes[0]);
        document.getElementById("Campotarjeta").style.display='none';
    }
    

}
```
### Generar desplegable de paises con DOM
Primero creamos un array de paises y mediante un bucle for creamos el elemento opcion y le añadimos los atributos value, que serán los paises del array y por ultimo los añadimos al HTML con appendChild.

```
function campoPaises(){
    var state = new Array("Afghanistan", "Albania", "Algeria", "Andorra", "Angola", "Antarctica", "Antigua and Barbuda",
    "Argentina", "Armenia", "Australia", "Austria", "Azerbaijan", "Bahamas", "Bahrain", "Bangladesh", "Barbados",
    "Belarus", "Belgium", "Belize", "Benin", "Bermuda", "Bhutan", "Bolivia", "Bosnia and Herzegovina", "Botswana",
    "Brazil", "Brunei", "Bulgaria", "Burkina Faso", "Burma", "Burundi", "Cambodia", "Cameroon", "Canada", "Cape Verde",
    "Central African Republic", "Chad", "Chile", "China", "Colombia", "Comoros", "Congo, Democratic Republic",
    "Congo, Republic of the", "Costa Rica", "Cote d'Ivoire", "Croatia", "Cuba", "Cyprus", "Czech Republic", "Denmark",
    "Djibouti", "Dominica", "Dominican Republic", "East Timor", "Ecuador", "Egypt", "El Salvador", "Equatorial Guinea",
    "Eritrea", "Estonia", "Ethiopia", "Fiji", "Finland", "France", "Gabon", "Gambia", "Georgia", "Germany", "Ghana",
    "Greece", "Greenland", "Grenada", "Guatemala", "Guinea", "Guinea-Bissau", "Guyana", "Haiti", "Honduras", "Hong Kong",
    "Hungary", "Iceland", "India", "Indonesia", "Iran", "Iraq", "Ireland", "Israel", "Italy", "Jamaica", "Japan",
    "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Korea, North", "Korea, South", "Kuwait", "Kyrgyzstan", "Laos", "Latvia",
    "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein", "Lithuania", "Luxembourg", "Macedonia", "Madagascar",
    "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", "Mauritania", "Mauritius", "Mexico", "Micronesia",
    "Moldova", "Mongolia", "Morocco", "Monaco", "Mozambique", "Namibia", "Nauru", "Nepal", "Netherlands", "New Zealand",
    "Nicaragua", "Niger", "Nigeria", "Norway", "Oman", "Pakistan", "Panama", "Papua New Guinea", "Paraguay", "Peru",
    "Philippines", "Poland", "Portugal", "Qatar", "Romania", "Russia", "Rwanda", "Samoa", "San Marino", " Sao Tome",
    "Saudi Arabia", "Senegal", "Serbia and Montenegro", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia",
    "Solomon Islands", "Somalia", "South Africa", "Spain", "Sri Lanka", "Sudan", "Suriname", "Swaziland", "Sweden",
    "Switzerland", "Syria", "Taiwan", "Tajikistan", "Tanzania", "Thailand", "Togo", "Tonga", "Trinidad and Tobago",
    "Tunisia", "Turkey", "Turkmenistan", "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States",
    "Uruguay", "Uzbekistan", "Vanuatu", "Venezuela", "Vietnam", "Yemen", "Zambia", "Zimbabwe");
    var paises= document.getElementById("pais"),option;
    
    for(var hi=0; hi<state.length; hi++){
         option= document.createElement("option");
        option.setAttribute("value", state[hi]);
        option.innerHTML=state[hi];
        paises.appendChild(option);
    }
}
```
### Creacion de comentarios con DOM
Primero, creamos una funcion que nos indique si el usuario esta o no logueado, cuando el susario no este logueado, solo mostrará los comentarios que haya mientras que si esta logueado además de mostrar los comentarios, generará una caja de texto para que pueda enviar un comentario.
```
if(obtenerCookie("logueado")=="true"){
    generaCajaComentarios();
            
}
generaComentarios();
```
Despues, creamos unos comentarios con DOM para mostrar estes o no logueado, para ello creamos la funcion 'generaComentarios' y lo añadimos al div que los va a contener con appendChild.
```
function generaComentarios(){
    var comentarios = document.getElementById("cajaComentarios");
    var parrafo = document.createElement('p');
    var parrafo2 = document.createElement('p');
    var parrafo3 = document.createElement('p');
    var texto = document.createTextNode('Paco: muy bueno!');
    var texto2 = document.createTextNode('Pepe: riquisimo!');
    var texto3 = document.createTextNode('Lola: genial!');
    parrafo.appendChild(texto);
    parrafo2.appendChild(texto2);
    parrafo3.appendChild(texto3);
    comentarios.appendChild(parrafo);
    comentarios.appendChild(parrafo2);
    comentarios.appendChild(parrafo3);

}
```
Después llamamos a la funcion encargada de crear la caja de comentarios en funcion si el usuario esta logueado.
* Primero creamos el formulario mediante DOM y le añadimos un identificador y el metodo post
* despues generamos con DOM el input donde el usuario dejará su comentario, le añadimos un identificador y hacemos que el input sea tipo texto
* Por ultimo creamos el boton de envio mediante DOM y le añadimos estilos.
Una vez creados todos los elementos mediante appendChild se los añadimos al contenedor de los comentarios.
Por ultimo, añadimos un evento listener que en primer lugar llame a la funcion 'muestraComentario' que explicaremos más adelante. También llamaremos al icono de los comentarios  $("i.fa.fa-comment") y haremos en primer lugar que el icono cambie de color y en segundo lugar aumentaremos el comentario en 1 cada vez que se añada un comentario nuevo.
```
function generaCajaComentarios(){
    var comentarios=document.getElementById("cajaComentarios");
        
        var formulario=document.createElement('FORM');
        formulario.name='formularioComentarios';
        formulario.id='formularioComentarios';
        formulario.method='POST';
        
        var miInput=document.createElement('INPUT');
        miInput.type='TEXT';
        miInput.id='comentario';
        miInput.name='comentario';
        
        //boton de envio:
        var enviar = document.createElement("button");
        var t = document.createTextNode("Enviar comentario");
        //añadimos estilos al boton
        enviar.setAttribute("type", "submit");
        enviar.setAttribute("id", "enviarComentario");
        enviar.style.backgroundColor="#ff80bf";
        enviar.style.color="white";
        
        enviar.appendChild(t); 
        comentarios.appendChild(formulario);
        formulario.appendChild(miInput);
        formulario.appendChild(enviar);
        
        document.getElementById("enviarComentario").addEventListener('click', function(e){ 
            muestraComentario();
            //sumamos 1 cada vez que el susuario genera un comentario
            var contador= $("i.fa.fa-comment").html();
            contador=parseInt(contador);
            contador++;
            $("i.fa.fa-comment").text(contador);
            $("i.fa.fa-comment").css("color", "grey");

            e.preventDefault();
        });
        
}
```
Con la funcion 'muestraComentario' primero obtenemos el nombre del usuario logueado y lo amacenamos en la variable nombre, despues almacenamos en la variable com el comentario que ha introducido el usuario, creamos un parrafo nuevo (```<p>```) al que le añadimos un textNode con el nombre del usuario y su comentario.
por ultimo añadimos el comentario al contenedor de comentarios y mediante 'insertBefore' hacemos que el ultimo comentario que se añada sea el primero en mostrarse.

```
function muestraComentario(){
    var nombre= obtenerCookie("name");
    var com= document.getElementById("comentario").value;
    var comentarios = document.getElementById("cajaComentarios");
    var parrafo = document.createElement('p');
    var texto = document.createTextNode(nombre+": "+com);
    var usuario = document.createTextNode(nombre);
    parrafo.appendChild(texto);
    comentarios.insertBefore(parrafo, comentarios.childNodes[1]); 
    
}
```
Por ultimo creamos una funcion que despliegue los comentarios o los oculte cuando hagamos click en el icono comentarios. 
```
function muestramelo()
{
	var vista=document.getElementById("cajaComentarios").style.display;
	if(vista=='none'){
		vista='block';
	}else{
		vista='none';
    }

	document.getElementById("cajaComentarios").style.display = vista;
}
```

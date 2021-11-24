# blockchain_js

# Contenido
Dentro del desarrollo de componente se crearon diferentes clases y métodos los cuales se realiza una creacion de blockchain con javascript

para replicar este proyecto es nesesario contar con nodejs y git 

se crea una carpeta local donde se iniciara el proyecto:
desde la raiz del proyecto ejecutamos los siguientes comandos
#nodjs
para instalar jod js solo basta cin ir a esta pagina y descargar para el so que se este usando:
https://nodejs.org/es/download/ 

Para crear el proyecto vamos a iniciar una carpeta que contendra el proyecto y desde esa raiz se ejecutaran los siguientes pasos:

# Inicializamos el control de versiones
```bash
$ git init
$ git remote add origin url repocitorio en git
```
# Inicializamos el proyecto con NPM 
Esto creará un fichero llamado package.json que contendrá toda la información del proyecto.
l parámetro -y de npm init omite el asistente interactivo, creando el package.json con los valores por defecto directamente y sin preguntarnos. Si prefieres utilizar el asistente, omite ese parámetro.
```bash
$ npm init -y
```
luego usaremos el comando para instalar la libreria de js que nos permitira trabajar con las cadenas de bloques 
```bash
npm install crypto-js --save
```
### Archivo main.js

crearemos un archivo llamado menin y lo dejamos con la extencion .js en este archivo escribiremos el codigo para la creacion de bloques

### Clase Block

En esta clase se reliza la creacion de un bloque usando una libreria de javascript (crypto-js) la cual se instaciara con la el nombre de sha256:

```bash
 const SHA256 = require(['crypto-js/sha256']);
 class Block{
	constructor(index, data, previusHash=''){
		this.index = index;
		this.date = new Date();
		this.data = data;
		this.previusHash = previusHash;
		this.hash = this.createHash();
	}

	createHash(){
		return SHA256(this.index + this.data + this.date).toString();
	}
}
```

### Clase BlockChain
esta clase se encarga de ejecutar las diferentes metodos para añadir bloques 
```bash
class BlockChain{
	constructor(genesis){
		this.chain = [this.createFirsBlock(genesis)];
	}
	createFirsBlock(genesis){
		return new Block(0,genesis);
	}
	getLastBlock(){
		return this.chain[this.chain.length-1];
	}
	addBlock(data){
		let prevBlock = this.getLastBlock();
		let block = new Block(prevBlock.index+1,data,prevBlock.hash);
		this.chain.push(block);
	}
}
```

### como agregar un bloque desde el codigo
dentro de el mismo archivo main.js agregamos la sigientes lineas: inicializaremos un objeto de la clase BlockChain y agregamos parametros 
```bash
# inicializaremos un objeto de la clase BlockChain y agregamos parametros 
let mainCoin = new BlockChain('info genesis');
# agregamos un bloque
mainCoin.addBlock('primer cadena');
# agregamos un segundo bloque
mainCoin.addBlock('segunda cadena');
# imprimimos lo que nos debuelbe el objeto
console.log(JSON.stringify(mainCoin.chain,null,2));
```

### agregando cadenas bloques
desde la rais del proyecto ejecutamos el comando:
```bash
node main.js
```
para el ejemplo debe devolver un json con esta estructura indicando que ya creo los bloques 
```bash
[
  {
    "index": 0,
    "date": "2021-11-24T20:43:32.650Z",
    "data": "info genesis",
    "previusHash": "",
    "hash": "c0c3652399d5449f9ff8190d90768c34999038be80cdbec54e1a41fab3f8cd10"
  },
  {
    "index": 1,
    "date": "2021-11-24T20:43:32.653Z",
    "data": "primer cadena",
    "previusHash": "c0c3652399d5449f9ff8190d90768c34999038be80cdbec54e1a41fab3f8cd10",
    "hash": "2cbc6febe3fb585b0ad696679358f061244f25158faa74dd68e1ba0ecb178674"
  },
  {
    "index": 2,
    "date": "2021-11-24T20:43:32.653Z",
    "data": "segunda cadena",
    "previusHash": "2cbc6febe3fb585b0ad696679358f061244f25158faa74dd68e1ba0ecb178674",
    "hash": "cd3124be7491f57c7470af6dfabb67203a98a7a059808758d7c1f7516ab31581"
  }
]
```


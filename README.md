# blockchain_js

# Contenido
Dentro del desarrollo de componente se crearon diferentes clases y métodos los cuales se realiza una creacion de blockchain con javascript

para replicar este proyecto es nesesario contar con nodejs y git 

se crea una carpeta local donde se iniciara el proyecto:
desde la raiz del proyecto ejecutamos los siguientes comandos

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


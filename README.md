# blockchain_js

# Contenido
Dentro del desarrollo de componente se crearon diferentes clases y métodos los cuales se realiza una creacion de blockchain con javascript
### Clase Block

En esta clase se reliza la creacion de un bloque usando una libreria de javascript (sha256):

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


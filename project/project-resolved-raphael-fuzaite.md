# MongoDb - Projeto Final
**Autor:** Raphael Fuzaite
**Data:**

## Para qual sistema você usaria o MongoDB (diferente desse)?

```
Sistema de controle financeiro, e-commerce, rastreamento de encomendas, etc.
```

## Qual a modelagem da sua coleção de `users`?

```
var auth = {
	"username"	: "",
	"email"		: "",
	"password"	: "",
	"lastAccess": "",
	"online"	: "",
	"disabled"	: "",
	"hashToken"	: ""
};

var settings = {
	"avatarPath"	: "",
	"backgroundPath": ""
};

var users = {
	"name"			: "",
	"bio"			: "",
	"dataRegister"	: "",
	"settings"		: settings,
	"auth"			: auth,
	"typeMember"	: []
};

```

## Qual a modelagem da sua coleção de `projects`?

```
var file = {
	"_id"	: "",
	"path"	: "",
	"weight": "",
	"name"	: ""
};

var notification = {
	"userId": "",
	"notify": "",	
};

var comment = {
	"_id"			: "",
	"text"			: "",
	"dateComment"	: "",
	"files"			: [file],
	"notifications" : [notification]
};

var activity = {
	"_id"			: "",
	"name"			: "",
	"description"	: "",
	"dateBegin"		: "",
	"dateDream"		: "",
	"dateEnd"		: "",
	"realocate"		: "",
	"expired"		: "",
	"tags"			: [],
	"historic"		: [],
	"notifications"	: [notification],
	"comments"		: [comment]
};

var goal = {
	"_id"			: "",
	"name"			: "",
	"description"	: "",
	"dateBegin"		: "",
	"dateDream"		: "",
	"dateEnd"		: "",
	"realocate"		: "",
	"expired"		: "",
	"tags"			: [],
	"historic"		: [],
	"activities"	: [activity]
};

var user = {
	"_id"		: "",
	"name"		: "",
	"typeMember": []
};

var projects = {
	"_id"				: "",
	"name"				: "",
	"description"		: "",
	"dateBegin"			: "",
	"dateDream"			: "",
	"dateEnd"			: "",
	"visible"			: "",
	"realocate"			: "",
	"expired"			: "",
	"visualizableMod"	: "",
	"users"				: [user],
	"tags"				: [],	
	"notifications"		: [notification],
	"goals"				: [goal]
};

for ( i = 1; i <= 10; i++ ) {
	var random  = Math.floor(Math.random() * (6 - 1)) + 1;	
	var typeMember = ["admin", "dev", "design", "architecture", "devops", "manager"];
	var type = [];
	if(Math.floor(Math.random() * (2 - 0)) + 0) {
		type.push(typeMember[0]);
	}
	type.push(typeMember[random]);
	
	var auth = {
		"username"	: 'user000'+i,
		"email"		: 'user000'+i+'@rfuzaite.com',
		"password"	: '123@456',
		"lastAccess": new Date().toISOString(),
		"online"	: true,
		"disabled"	: false,
		"hashToken"	: btoa('user000'+i+'@rfuzaite.com||123@456')
	};
	
	var settings = {
		"avatarPath"	: 'C:/000'+i+'/avatar.png',
		"backgroundPath": 'C:/000'+i+'/bg.png'
	};
	
	var user = {
		"name"			: 'Name000'+i,
		"bio"			: 'Bio Name000'+i,
		"dataRegister"	: new Date().toISOString(),
		"settings"		: settings,
		"auth"			: auth,
		"typeMember"	: type
	};
	 
	console.log(JSON.stringify(user));
}

```

## Create - cadastro

```
- Cadastre 10 usuários diferentes.

- Cadastre 5 projetos diferentes.
	+ cada um com 5 membros, sempre diferentes dentro dos projetos;
	+ cada um com pelo menos 3 tags diferentes;
		* escolha 1 tag onde deva ficar em 2 projetos;
		* escolha 1 tag onde deva ficar em 3 projetos;
	+ cada projeto com pelo menos 1 goal;
		* cada goal com pelo menos 3 tags;
		* cada goal com pelo menos 2 atividades, deixe 1 projeto sem.
		
	> db.users.count()
	10
	> db.projects.count()
	5
	>		

```

## Retrieve - busca

```
- Liste as informações dos membros de 1 projeto específico que deve ser buscado pelo seu nome de forma a não ligar para maiúsculas e minúsculas.

	> db.projects.find({name: /PRO0001/i},{_id:0, users: 1}).forEach(function(item){ 
		var cur = db.users.find({_id:{$in:item.users}}); 
		while(cur.hasNext()) {
			printjson(cur.next());
		}; 
	});

- Liste todos os projetos com a tag que você escolheu para os 3 projetos em comum.

	> var tag = ['angular'];
	> db.projects.find({ tags:{ $in:tag } });

- Liste apenas os nomes de todas as atividades para todos os projetos.

	> db.projects.find({},{_id: 0, "goals.activities.name": 1});

- Liste todos os projetos que não possuam uma tag.

	> db.projects.find({tags:{$size:0}});
	
- Liste todos os usuários que não fazem parte do primeiro projeto cadastrado.

	> var project = db.projects.findOne();
	> var cur = db.users.find({_id:{$nin:project.users}});
	> while(cur.hasNext()){
		printjson(cur.next());
	  };

```
## Update - alteração

```
- Adicione para todos os projetos o campo views: 0.

	> var query = {};
	> var mod = {$set:{view:0}};
	> var options = {upsert: true, multi: true};
	> db.projects.update(query, mod, options);

- Adicione 1 tag diferente para cada projeto.

	> var query = { name: /PRO0001/i };
	> var mod = { $push: { tags: 'iot' } };
	> var options = {upsert: true};
	> db.projects.update(query, mod, options);
	
	> var query = { name: /PRO0002/i };
	> var mod = { $pushAll: { tags: ['iot', 'wcf'] } };
	> var options = {upsert: true};
	> db.projects.update(query, mod, options);
	
	...

- Adicione 2 membros diferentes para cada projeto.

	> var id = [];
	> var query = { name: /PRO0001/i };
	> var project = db.projects.find(query);
	> var cur = db.users.find({_id:{$nin:project.users}},{_id: 1}).limit(2);
	> while(cur.hasNext()){ id.push(cur.next()._id); };
	> var mod = { $pushAll: { users: id } };
	> var options = {upsert: true};
	> db.projects.update(query, mod, options);
	
	...

- Adicione 1 comentário em cada atividade, deixe apenas 1 projeto sem.

	> var query = {};
	> var mod = {$set:{view:0}};
	> var options = {upsert: true, multi: true};
	> db.projects.update(query, mod, options);

- Adicione 1 projeto inteiro com UPSERT.

	> var query = {};
	> var mod = {$set:{view:0}};
	> var options = {upsert: true, multi: true};
	> db.projects.update(query, mod, options);

```

## Delete - remoção

```
- Apague todos os projetos que não possuam tags.
- Apague todos os projetos que não possuam comentários nas atividades.
- Apague todos os projetos que não possuam atividades.
- Escolha 2 usuário e apague todos os projetos em que os 2 fazem parte.
- Apague todos os projetos que possuam uma determinada tag em goal.

```

## Gerenciamento de Usuário


```
- Crie um usuário com permissões APENAS de Leitura.
- Crie um usuário com permissões de Escrita e Leitura.
- Adicionar o papel grantRolesToUser e revokeRole para o usuário com Escrita e Leitura.
- Remover o papel grantRolesToUser para o usuário com Escrita e Leitura.
- Listar todos os usuários com seus papéis e ações.

```

## Sharding

```
- 1 Router
- 1 Config Server
- 3 Shardings

```

## Replica

```

- 3 Replicas

```
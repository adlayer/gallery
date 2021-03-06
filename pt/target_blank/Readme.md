# Target_blank

## O atributo
Durante muitos anos o atributo "target" e o valor "_blank" foram conhecidos como o par perfeito para que um link fosse aberto em uma nova janela.

Com o passar dos anos a evolução do html, dos múltiplos dispositivos acessando websites, discussões sobre  acessibilidade e usabilidade levaram a criação dos "padrões web".

Os evangelizadores dos padrões web levantaram a bandeira do "desenvolvimento em camadas" que consiste em separar a estrutura de um website em conteúdo, apresentação e comportamento.

A prática de dividir o desenvolvimento em camadas se mostrou eficaz e produtiva, motivando algumas alterações no futuro da web. Uma delas foi remover da especificação do Xhtml 1.0 o atributo "target". Por entender que a camada responsável pelo tratamento de onde e como um link será aberto pertence ao comportamento (normalmente implementado com javascript na web).

Mais tarde discussões sobre a usabilidade também foram levantadas contra o comportamento de abrir um link por padrão em uma nova aba ou janela, pois desse modo o website remove do usuário o direito de escolha e inválida a opção de abrir em uma nova aba presente na maioria dos navegadores.

Não se sabe com certeza qual o futuro dessa especificação mas muitos tem optado por identificar visualmente quais links serão abertos em outro contexto quando esse comportamento é indispensável.

O suporte ao target continua funcionando em muitos navegadores e foi readicionado na especificação do HTML 5, mas por causa de tantas controversas em torno dessa funcionalidade e por concordar que o target blank é um recurso intrusivo tanto na semântica, sintaxe e usabilidade de um site, decidimos por não inserir esse comportamento por padrão nos links gerados pelo nosso SDK.

Mas, entendemos que esse recurso pode ser extremamente necessário em alguns casos de uso. 
Ao invés de transforma-lo em uma configuração na interface e aumentar a complexidade optamos por ajudar você a implementar esse comportamento via javascript com poucas linhas de código. 

## Como implementar
### ATENÇÃO: todos os scripts abaixo deve ser executados depois que o html for carregado

### jQuery
```javascript
	jQuery('.adlayer_space a').click(function(e){
		e.preventDefault();
		window.open(	jQuery(this).attr('href'));
		return false;
	});
```
### Prototype
```javascript
	$('.adlayer_space a').observe('click', function(event){
		var element = event.element();
		window.open(element.readAttribute('href'));
		return false;
	});
```

### Dojo
```javascript
	dojo.query(".adlayer_space a").onclick(function(e){
		dojo.stopEvent( e );
		window.open(this.href);
		return false;
	});
```

### Native DOM
`document.getElementByClassName` pode não funcionar em Browsers antigos.

```javascript
	var spaces = document.getElementsByClassName('adlayer_space');
	for(var i = 0; i < spaces.length; i++){
   	var space = spaces[i];
    	var spaceChilds = space.childNodes;
  		for(var j = 0; j < spaceChilds.length; spaceChilds++){
			var element = spaceChilds[i];
			if(element.nodeName === 'A'){
				element.onclick = function(){
					window.open(element.href);
					return false;
				}
			}
		}
	}
```

# Bugs
Se você encontrar qualquer bug em alguma sugestão ou conhece uma maneira melhor de fazer isso informe-nos no [tópico](https://github.com/adlayer/gallery/issues/1) da implementação.

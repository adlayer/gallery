# Target_blank

## O atributo
Durante muitos anos o atributo "target" e o valor "_blank" foram conhecidos como o par perfeito para que um link fosse aberto em uma nova janela.

Com passar dos anos a evolução do html, dos múltiplos dispositivos acessando websites, discussões sobre sobre acessibilidade e usabilidade levaram a criação dos "padrões web".
Os evangelizadores dos padrões web levantaram a bandeira do "desenvolvimento em camadas" que consiste em separar a estrutura de um website em conteúdo, apresentação e comportamento.

A prática de dividir o desenvolvimento em camadas se mostrou eficaz e produtivo e motivou algumas alterações no futuro web. Entre elas remover da especificação do xhtml 1.0 o atributo "target", por entender que a camada responsável pelo tratamento de onde e como um link será aberto pertence a camada de comportamento (normalmente implementado com javascript na web).

Mais tarde discussões sobre a usabilidade também foram levantadas contra o comportamento de abrir um link por padrão em uma nova aba ou janela, pois desse modo o website remove do usuário o direito de escolha e invalida a opção de abrir em uma nova aba presente na maioria do navegadores.

Não se sabe com concerteza qual o futuro dessa especificação mas muitos tem optado por identificar visualmente quais links se serão abertos em outro contexto quando esse comportamento é indispensável.

O suporte ao target continua funcionando em muitos navegadores e foi readicionado na especificação do HTML 5, mas por causa de tantas controversas em torno dessa funcionalidade e por concordar que o target blank é um recurso intrusivo tanto na semantica, sintaxe e usabilidade de um site, decidimos por não inserir esse comportamento por padrão nos links gerados pelo nosso sdk.

Mas entendemos que esse recurso pode ser extremamente necessário em alguns casos de uso e ao invés transforma-lo em uma configuração na interface e aumentar a complexidade optamos por ajudar você a implementar esse comportamento via javascript com poucas linhas de código. 

## Como implementar

### jQuery
	jQuery('.adlayer_space a').click(function(e){
		e.preventDefault();
		window.open(	jQuery(this).attr('href'));
		return false;
	});

### Prototype
	$('.adlayer_space a').observe('click', function(event){
		var element = event.element();
		window.open(element.readAttribute('href'));
		return false;
	});

### Dojo
	dojo.query(".adlayer_space a").onclick(function(){
		window.open(this.href);
		return false;
	});
---
published: true
---
# ACTIVITY: O QUE É, COMO É INICIADA E CICLO DE VIDA BÁSICO

Se você está começando agora no desenvolvimento de aplicativos na plataforma Android e quer se dar bem, é importante conhecer e dominar um dos componentes mais importantes e utilizados no mundo do robozinho verde. Estamos falando da Activity (ou Atividade) e neste primeiro post da série vamos conhecer um pouco mais sobre o funcionamento e ciclo de vida do componente. Bora lá?

## O QUE É UMA ACTIVITY?

É literalmente uma tela na aplicação, responsável por definir e exibir um layout com componentes de interface de usuário (views), como botões, textos e imagens, por exemplo, e controlar os eventos recebidos. Entendido?

Se sim, neste post vou usar Tela ou Telas no lugar de Activity ou Activities, para facilitar a compreensão. Ok?

## COMO CRIAR UMA ACTIVITY?

Na maioria das vezes, quando queremos criar uma Activity utilizamos o Android Studio, que configura tudo para nós. Por padrão a ferramenta já faz alguns trabalhos, como:

- Definir um nome padrão da tela (MainActivity);
- Vincular o layout XML com a Activity;
- Marcar a Activity como a principal do projeto;
- Registrar a Activity no AndroidManifest.

Isso tudo é ótimo para ganharmos produtividade (afinal, é para isso que serve uma IDE inteligente) e focar apenas nas regras de negócio do nosso aplicativo, mas para quem está iniciando é sempre bom entender como tudo funciona por trás dos panos, se quisermos ser profissionais melhores e independentes de ferramentas. Certo? Então vamos lá:

## COMO UMA ACTIVITY É CRIADA

Antes de mais nada, uma Activity é uma classe Java comum como qualquer outra que você cria nos seus projetos. Porém, o que a torna uma classe especial e com “super poderes” é a super classe Activity do pacote do Framework Android (android.app.Activity) ou qualquer subclasse dela.

Para criar uma Activity do zero basta clicar com o botão direito no pacote do seu projeto principal, apontar para New e em seguida clicar em Java Class. Na janela que abrir, defina o nome e a super classe para sua Activity, assim:

![Activity1.png]({{site.baseurl}}/_posts/Activity1.png)

Dica: Uma coisa interessante é que o sufixo Activity depois do nome da tela não torna a sua classe uma Activity com “super poderes”, como mencionado anteriormente. O que a torna de fato uma Activity do Android é a super classe que a sua classe tem que herdar: android.app.Activity. O sufixo Activity na frente do nome é utilizado por questões de convenção, por isso é bom que você siga esse padrão.

A primeira coisa que precisamos fazer após criar e transformar nossa classe em uma Activity do Android é defini-la no AndroidManifest, especificamente dentro da tag <application></application>.

![Activity2-768x425.png]({{site.baseurl}}/_posts/Activity2-768x425.png)

O próximo passo é criar o layout XML e vinculá-lo à nossa WelcomeActivity. Para isso, primeiro localizamos a pasta layout, que está dentro da pasta res, que por sua vez se encontra dentro do pacote main. É aqui que criamos e definimos todos os layouts de todas as Activities do nosso projeto. Vamos criar o arquivo activity_welcome.xml clicando com o botão direito sobre a pasta res, apontar para New e clicar em Layout resource file. Na janela que abrir defina o nome do arquivo como activity_welcome, o Root element como LinearLayout e clique no botão Ok.

![Activity3.png]({{site.baseurl}}/_posts/Activity3.png)

Dica: também por questões de convenção definimos o nome do arquivo com o prefixo activity_ para dizer que este layout será vinculado a uma Activity. Outra coisa importante é que os nomes de recursos devem ser lowercase, conter somente caracteres a-z, números 0-9 ou underscores. O nome activityWelcome não é um nome válido para o recurso de layout da nossa Activity.

Antes de vincularmos nossa WelcomeActivity ao layout XML que acabamos de criar, vamos entender como uma Activity é instanciada pelo sistema.

## CICLO DE VIDA DE UMA ACTIVITY

Para entendermos como o Android cria e destrói uma Activity no sistema precisamos conhecer o conceito de Ciclo de Vida de uma Activity. Existem sete métodos de chamada de retorno (callbacks), definidos pelo Android, que são chamados pelo sistema em diversos momentos da vida de uma aplicação.

Um exemplo é quando ocorrem mudanças de estado devido à orientação da tela, idioma do aparelho ou quando o sistema recebe uma mensagem (Intent) com uma solicitação para mostrar uma Activity nova para o usuário. Os callbacks são os métodos dentro dos retângulos no diagrama abaixo:

![218650c4-352d-432c-996c-6516820d6862.png]({{site.baseurl}}/_posts/218650c4-352d-432c-996c-6516820d6862.png)
Fonte: https://developer.android.com/reference/android/app/Activity.html#ActivityLifecycle

onCreate(): chamado quando a Activity é criada pela primeira vez. Toda a configuração inicial é feita aqui, inclusive a vinculação do nosso layout XML à Activity para definir a interface do usuário.

onStart(): chamado logo após o onCreate(), quando a Activity está se tornando visível para o usuário.

onResume: chamado logo após onStart() e quando a Activity está no topo da pilha, completamente visível para o usuário e pronta para receber interações.

onDestroy(): último método chamado antes de o Android destruir completamente a Activity, seja porque o usuário apertou o botão voltar em uma tela ou porque o Android necessita de recursos memória e decide matar a Activity ou ainda porque o método finish() foi chamado explicitamente no código.

Como podemos verificar acima, é no método onCreate que temos que vincular nosso layout XML à nossa WelcomeActivity. O que precisamos entender agora é quando o método onCreate da Activity é chamado, ou seja, como o Android sabe o momento certo de criar nossa WelcomeActivity, lembrando que só temos ela no projeto. Para isso precisamos voltar ao nosso AndroidManifest e declarar um tipo de Intent especial, chamado intent-filter, que é uma forma de customizar como uma Activity é iniciada:

![Activity5-768x504.png]({{site.baseurl}}/_posts/Activity5-768x504.png)

Basicamente o que essa intent-filter faz é definir uma categoria e uma ação. A tag category diz ao Android que a WelcomeActivity pertence à categoria LAUNCHER e significa que um ícone de inicialização estará disponível na lista de aplicativos que o usuário possui instalada. A tag action do tipo MAIN diz ao Android que a WelcomeActivity pode ser iniciada de forma isolada e que ela será o ponto de entrada do aplicativo.

Agora falta apenas uma coisa. Já sabemos que o Android é responsável por instanciar uma Activity quando o usuário abre um determinado aplicativo (outras formas de inicialização de Activity veremos depois). Dessa forma, quando o usuário abrir nosso aplicativo uma mensagem será enviada ao sistema, que por sua vez vai localizar, instanciar e chamar primeiramente o método onCreate da nossa WelcomeActivity de forma transparente. É neste momento que vinculamos o nosso layout XML à nossa Activity:

![Activity6-768x411.png]({{site.baseurl}}/_posts/Activity6-768x411.png)

Tudo pronto! Temos um aplicativo funcional, que criamos com o mínimo de ajuda da IDE, entendendo todo o processo de criação de Activity e o seu ciclo de vida básico. Para aprender mais sobre Activity e seu ciclo de vida completo com mais detalhes, [dá uma olhada na documentação](https://developer.android.com/reference/android/app/Activity).

Em breve voltamos para falar sobre como lidar com mudanças de configuração para salvar o estado atual da Activity e oferecer uma experiência agradável ao usuário. Até lá!

Artigo postado no Blog da Concrete:
https://concrete.com.br/2018/05/18/activity-o-que-e-como-e-iniciada-e-ciclo-de-vida-basico/

Valeu!

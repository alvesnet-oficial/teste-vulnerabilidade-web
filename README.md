# Como testar a vulnerablidade de um site wordpress:

fonte: https://www.ti-enxame.com/pt/security/wordpress-4.7.1-rest-api-ainda-expondo-usuarios/961954884/

Dados sensiveis exposto:

https://dominios.x.x/wp-json/wp/v2/users

Resolução:

Use este trecho de código para esconder a lista de usuários e dar 404 como resultado, enquanto o resto das chamadas de api continuarão funcionando como estavam.

Acessar o arquivo 'functions.php' no Wordpress e adicinar o seguinte codigo:

add_filter( 'rest_endpoints', function( $endpoints ){
    if ( isset( $endpoints['/wp/v2/users'] ) ) {
        unset( $endpoints['/wp/v2/users'] );
    }
    if ( isset( $endpoints['/wp/v2/users/(?P<id>[\d]+)'] ) ) {
        unset( $endpoints['/wp/v2/users/(?P<id>[\d]+)'] );
    }
    return $endpoints;
});


# Como testar vulnerabilidade do servidor web:

Descobrir possivel versão do servidor web e senha de usuarios:

https://dominio.x.x//wp-content/plugins/wp-with-spritz/wp.spritz.content.filter.php?url=/../../../..//etc/passwd
    
# Como blindar o wordpress contra invasões:
    
https://pt.semrush.com/blog/como-blindar-o-seu-wordpress-contra-invasoes-evitando-perder-posicoes-no-google-passo-a-passo/




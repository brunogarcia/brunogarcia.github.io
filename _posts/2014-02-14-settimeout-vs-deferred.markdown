--- 
layout: post 
title: setTimeout() vs $.Deferred() 
date: '2014-02-14T20:02:00+01:00'
tumblr\_url: http://blog.garciaechegaray.com/post/76650860789/settimeout-vs-deferred
---

Este el típico problema en el cual utilizaba un setTimeout(). Estaba
obligado a esperar que se ejecutara la linea superior para poder hacer
uso del nodo DOM (en este caso “lightbox\_content\_user”).

> $(“\#wrap\_all”).prepend(\<?php echo json\_encode(\$lightbox) ?\>));
>
> setTimeout(function(){
>
>  $(“.lightbox\_content\_user”).css(‘width’, container\_width - 80);
> },
>
> 500);

Ahora estoy comenzando a utilizar un objeto jQuery llamado
[Deferred](https://api.jquery.com/category/deferred-object/).
Básicamente hace lo mismo, pero de forma mas limpia. Y así evitamos la
famosa [Callback Pyramid of
Doom](http://www.reddit.com/r/javascript/comments/1atmht/how_we_killed_the_callback_pyramid_of_doom/).

> var dfd = \$.Deferred();
>
> dfd.done(\$(“\#wrap\_all”).prepend(\<?php echo
> json\_encode(\$lightbox) ?\>);
>
> dfd.resolve(\$(“.lightbox\_content\_user”).css(‘width’,
> container\_width - 80));


<!-- Este .md fue generado a partir del .Rmd homónimo. Edítese el .Rmd -->
Personas suscritas a la organización
====================================

Paquetes
--------

``` r
library(httr)
library(rstudioapi)
```

Usuario/Contrasena
------------------

``` r
usr <- askForPassword('Usuario')
pwd <- askForPassword('Password')
```

Descargar listas
----------------

``` r
col <- GET("https://api.github.com/orgs/biogeografia-201902/outside_collaborators", authenticate(usr, pwd))
mie <- GET("https://api.github.com/orgs/biogeografia-201902/members", authenticate(usr, pwd))
```

Convertir a contenido
---------------------

``` r
col_js <- content(col)
mie_js <- content(mie)
```

Convertir a data frame
----------------------

``` r
col_df <- jsonlite::fromJSON(jsonlite::toJSON(col_js))
mie_df <- jsonlite::fromJSON(jsonlite::toJSON(mie_js))
```

Exportar
========

``` r
usrgh <- unlist(c(col_df$login, mie_df$login))
write(usrgh, 'suscripciones_github.txt')
```

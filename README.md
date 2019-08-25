
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
usrgh <- sort(unlist(c(col_df$login, mie_df$login)))
cat(
  'En fecha/hora: ',
  date(),
  ', aparecían como registradas', '\n',
  'las siguientes cuentas como miembros/as o colaboradores externos/as: ', '\n',
  paste(usrgh, collapse = '\n'),
  sep = ''
)
```

    ## En fecha/hora: Sun Aug 25 17:39:44 2019, aparecían como registradas
    ## las siguientes cuentas como miembros/as o colaboradores externos/as: 
    ## AbigailCP
    ## BidelkisCastillo
    ## dahianagb07
    ## enrique193
    ## Erasbel05
    ## geofis
    ## hoyodepelempito
    ## jimenezsosa
    ## Jorge-Mutonen
    ## Mangoland
    ## maritzafg
    ## merali-rosario
    ## ramosramos1886
    ## sanchez26
    ## victorcabsid
    ## yanderlin

``` r
write(usrgh, 'suscripciones_github.txt')
```

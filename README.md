
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
usrgh <- sort(unlist(c(paste(col_df$login, '(C)'), paste(mie_df$login, '(M)'))))
cat(
  'En fecha/hora: ',
  date(),
  ', aparecían como registradas', '\n',
  'las siguientes cuentas como miembros/as o colaboradores externos/as: ', '\n',
  paste(usrgh, collapse = '\n'),
  sep = ''
)
```

    ## En fecha/hora: Thu Sep 12 11:41:27 2019, aparecían como registradas
    ## las siguientes cuentas como miembros/as o colaboradores externos/as: 
    ## AbigailCP (M)
    ## BidelkisCastillo (M)
    ## dahianagb07 (M)
    ## emdilone (M)
    ## enrique193 (M)
    ## Erasbel05 (C)
    ## geofis (M)
    ## hoyodepelempito (M)
    ## jimenezsosa (M)
    ## Jorge-Mutonen (M)
    ## JuanJoseGH06 (M)
    ## Mangoland (M)
    ## maritzafg (M)
    ## merali-rosario (C)
    ## ramosramos1886 (M)
    ## sanchez26 (M)
    ## victorcabsid (M)
    ## yanderlin (M)

``` r
write(usrgh, 'suscripciones_github.txt')
```

Actividad (12/09/19)
====================

``` r
usrghact <- c("AbigailCP", "BidelkisCastillo", "dahianagb07",
               "emdilone", "enrique193", "jimenezsosa",
               "Jorge-Mutonen", "JuanJoseGH06",
               "Mangoland", "maritzafg", "yanderlin")
usrghact
```

    ##  [1] "AbigailCP"        "BidelkisCastillo" "dahianagb07"     
    ##  [4] "emdilone"         "enrique193"       "jimenezsosa"     
    ##  [7] "Jorge-Mutonen"    "JuanJoseGH06"     "Mangoland"       
    ## [10] "maritzafg"        "yanderlin"

``` r
write(usrghact, 'suscripciones_github_actividad.txt')
```
